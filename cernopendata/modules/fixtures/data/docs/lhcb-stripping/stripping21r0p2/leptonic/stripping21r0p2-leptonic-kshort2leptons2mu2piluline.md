[[stripping21r0p2 lines]](./stripping21r0p2-index)

# StrippingKshort2Leptons2mu2piLULine

## Properties:

|                |                                           |
|----------------|-------------------------------------------|
| OutputLocation | Phys/Kshort2Leptons2mu2piLULine/Particles |
| Postscale      | 1.0000000                                 |
| HLT1           | None                                      |
| HLT2           | None                                      |
| Prescale       | 1.0000000                                 |
| L0DU           | None                                      |
| ODIN           | None                                      |

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

LoKi::VoidFilter/SELECT:Phys/StdAllLooseMuons

|      |                                    |
|------|------------------------------------|
| Code | 0StdAllLooseMuons/Particles',True) |

FilterDesktop/Kshort2LeptonsMuonsL

|                 |                                                                                     |
|-----------------|-------------------------------------------------------------------------------------|
| Code            | (PT \> 50.0) &(MIPCHI2DV(PRIMARY) \> 20) &(TRGHOSTPROB \< 0.5) &(PIDmu \> -5)       |
| Inputs          | [ 'Phys/[StdAllLooseMuons](./stripping21r0p2-commonparticles-stdallloosemuons)' ] |
| DecayDescriptor | None                                                                                |
| Output          | Phys/Kshort2LeptonsMuonsL/Particles                                                 |

LoKi::VoidFilter/SELECT:Phys/StdAllNoPIDsPions

|      |                                     |
|------|-------------------------------------|
| Code | 0StdAllNoPIDsPions/Particles',True) |

FilterDesktop/Kshort2LeptonsPionsL

|                 |                                                                                       |
|-----------------|---------------------------------------------------------------------------------------|
| Code            | (PT \> 100.0) &(MIPCHI2DV(PRIMARY) \> 16) &(TRGHOSTPROB \< 0.5) &(PIDK \< 5)          |
| Inputs          | [ 'Phys/[StdAllNoPIDsPions](./stripping21r0p2-commonparticles-stdallnopidspions)' ] |
| DecayDescriptor | None                                                                                  |
| Output          | Phys/Kshort2LeptonsPionsL/Particles                                                   |

LoKi::VoidFilter/SELECT:Phys/StdNoPIDsUpPions

|      |                                    |
|------|------------------------------------|
| Code | 0StdNoPIDsUpPions/Particles',True) |

FilterDesktop/Kshort2LeptonsPionsU

|                 |                                                                                     |
|-----------------|-------------------------------------------------------------------------------------|
| Code            | (PT \> 50) &(MIPCHI2DV(PRIMARY) \> 10) &(TRGHOSTPROB \< 0.35) &(PIDK \< -3.5)       |
| Inputs          | [ 'Phys/[StdNoPIDsUpPions](./stripping21r0p2-commonparticles-stdnopidsuppions)' ] |
| DecayDescriptor | None                                                                                |
| Output          | Phys/Kshort2LeptonsPionsU/Particles                                                 |

CombineParticles/Kshort2Leptons2mu2piLULine

|                  |                                                                                                                                                                                                                                      |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/Kshort2LeptonsMuonsL' , 'Phys/Kshort2LeptonsPionsL' , 'Phys/Kshort2LeptonsPionsU' ]                                                                                                                                        |
| DaughtersCuts    | { '' : 'ALL' , 'mu+' : 'ALL' , 'mu-' : 'ALL' , 'pi+' : 'ALL' , 'pi-' : 'ALL' }                                                                                                                                                       |
| CombinationCut   | (AM \< 800.0 \*MeV) & (AMAXDOCA('') \< 1.0 \*mm) & ( ( ANUM( ( TRTYPE == 3 ) & ( ABSID == 'mu+' ) ) == 2 ) ) & ( ( ANUM( ( TRTYPE == 3 ) & ( ABSID == 'pi+' ) ) == 1 ) ) & ( ( ANUM( ( TRTYPE == 4 ) & ( ABSID == 'pi-' ) ) == 1 ) ) |
| MotherCut        | ( M \< 800.0 \*MeV) &( MIPDV(PRIMARY) \< 5 \*mm) & ( BPVVDCHI2 \> 2500) & ( VFASPF(VCHI2/VDOF) \< 25)                                                                                                                                |
| DecayDescriptor  | KS0 -\> mu+ mu- pi+ pi-                                                                                                                                                                                                              |
| DecayDescriptors | [ 'KS0 -\> mu+ mu- pi+ pi-' ]                                                                                                                                                                                                      |
| Output           | Phys/Kshort2Leptons2mu2piLULine/Particles                                                                                                                                                                                            |
