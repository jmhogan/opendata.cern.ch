[[stripping21r1p2 lines]](./stripping21r1p2-index)

# StrippingKshort2Leptons2pi2eLLLine

## Properties:

|                |                                          |
|----------------|------------------------------------------|
| OutputLocation | Phys/Kshort2Leptons2pi2eLLLine/Particles |
| Postscale      | 1.0000000                                |
| HLT1           | None                                     |
| HLT2           | None                                     |
| Prescale       | 1.0000000                                |
| L0DU           | None                                     |
| ODIN           | None                                     |

## Filter sequence:

LoKi::VoidFilter/StrippingGoodEventConditionLeptonic

|      |                                                                                                  |
|------|--------------------------------------------------------------------------------------------------|
| Code | ALG_EXECUTED('StrippingStreamLeptonicBadEvent') & ~ALG_PASSED('StrippingStreamLeptonicBadEvent') |

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SELECT:Phys/StdAllNoPIDsPions

|      |                                     |
|------|-------------------------------------|
| Code | 0StdAllNoPIDsPions/Particles',True) |

FilterDesktop/Kshort2LeptonsPionsL

|                 |                                                                                       |
|-----------------|---------------------------------------------------------------------------------------|
| Code            | (PT \> 100.0) &(MIPCHI2DV(PRIMARY) \> 16) &(TRGHOSTPROB \< 0.5) &(PIDK \< 5)          |
| Inputs          | [ 'Phys/[StdAllNoPIDsPions](./stripping21r1p2-commonparticles-stdallnopidspions)' ] |
| DecayDescriptor | None                                                                                  |
| Output          | Phys/Kshort2LeptonsPionsL/Particles                                                   |

LoKi::VoidFilter/SELECT:Phys/StdDiElectronFromTracks

|      |                                           |
|------|-------------------------------------------|
| Code | 0StdDiElectronFromTracks/Particles',True) |

FilterDesktop/Kshort2LeptonsDiElectronsV

|                 |                                                                                                                                                           |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code            | (MINTREE(ABSID\<14,PT) \> 100.0) &(MINTREE(ABSID\<14,MIPCHI2DV(PRIMARY)) \> 16) &(MAXTREE(ABSID\<14,TRGHOSTPROB) \< 0.5) &(MINTREE(ABSID\<14,PIDe) \> -4) |
| Inputs          | [ 'Phys/[StdDiElectronFromTracks](./stripping21r1p2-commonparticles-stddielectronfromtracks)' ]                                                         |
| DecayDescriptor | None                                                                                                                                                      |
| Output          | Phys/Kshort2LeptonsDiElectronsV/Particles                                                                                                                 |

DaVinci::N3BodyDecays/Kshort2Leptons2pi2eLLLine

|                  |                                                                                                                        |
|------------------|------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/Kshort2LeptonsDiElectronsV' , 'Phys/Kshort2LeptonsPionsL' ]                                                  |
| DaughtersCuts    | { '' : 'ALL' , 'J/psi(1S)' : 'ALL' , 'pi+' : 'ALL' , 'pi-' : 'ALL' }                                                   |
| CombinationCut   | (AM \< 800.0 \*MeV) & (AMAXDOCA('') \< 1.0 \*mm)                                                                       |
| MotherCut        | (M \< 800.0 \*MeV) &(MIPDV(PRIMARY) \< 1 \*mm) & ((BPVVDSIGN\*M/P) \> 0.8953\*2.9979e-01) & (VFASPF(VCHI2/VDOF) \< 50) |
| DecayDescriptor  | KS0 -\> pi+ pi- J/psi(1S)                                                                                              |
| DecayDescriptors | [ 'KS0 -\> pi+ pi- J/psi(1S)' ]                                                                                      |
| Output           | Phys/Kshort2Leptons2pi2eLLLine/Particles                                                                               |
