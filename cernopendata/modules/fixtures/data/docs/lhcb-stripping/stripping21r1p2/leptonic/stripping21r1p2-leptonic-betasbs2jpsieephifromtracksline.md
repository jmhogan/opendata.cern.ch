[[stripping21r1p2 lines]](./stripping21r1p2-index)

# StrippingBetaSBs2JpsieePhiFromTracksLine

## Properties:

|                |                                                |
|----------------|------------------------------------------------|
| OutputLocation | Phys/BetaSBs2JpsieePhiFromTracksLine/Particles |
| Postscale      | 1.0000000                                      |
| HLT1           | None                                           |
| HLT2           | None                                           |
| Prescale       | 1.0000000                                      |
| L0DU           | None                                           |
| ODIN           | None                                           |

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

LoKi::VoidFilter/SELECT:Phys/StdLoosePhi2KK

|      |                                  |
|------|----------------------------------|
| Code | 0StdLoosePhi2KK/Particles',True) |

FilterDesktop/SelPhi2KKForBetaSBs2JpsieePhiFromTracks

|                 |                                                                                                                                                                                         |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code            | (MM \> 995.0 \*MeV) & (MM \< 1045.0 \*MeV) & (PT \> 1000.0 \*MeV) & (MINTREE('K+'==ABSID,PIDK-PIDpi) \> -3.0 ) & (MAXTREE('K+'==ABSID,TRCHI2DOF) \< 3.0) & (VFASPF(VCHI2/VDOF) \< 15.0) |
| Inputs          | [ 'Phys/[StdLoosePhi2KK](./stripping21r1p2-commonparticles-stdloosephi2kk)' ]                                                                                                         |
| DecayDescriptor | None                                                                                                                                                                                    |
| Output          | Phys/SelPhi2KKForBetaSBs2JpsieePhiFromTracks/Particles                                                                                                                                  |

LoKi::VoidFilter/SELECT:Phys/StdDiElectronFromTracks

|      |                                           |
|------|-------------------------------------------|
| Code | 0StdDiElectronFromTracks/Particles',True) |

FilterDesktop/SelJpsi2eeForBetaSBs2JpsieePhiFromTracks

|                 |                                                                                                                                                                                                                                   |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code            | (MM \> 1800.0 \*MeV) & (MM \< 3600.0 \*MeV) & (PT \> 800.0 \*MeV) & (MINTREE('e+'==ABSID,PIDe-PIDpi) \> 0.0 ) & (MINTREE('e+'==ABSID,PT) \> 500.0 \*MeV) & (MAXTREE('e+'==ABSID,TRCHI2DOF) \< 3.0) & (VFASPF(VCHI2/VDOF) \< 15.0) |
| Inputs          | [ 'Phys/[StdDiElectronFromTracks](./stripping21r1p2-commonparticles-stddielectronfromtracks)' ]                                                                                                                                 |
| DecayDescriptor | None                                                                                                                                                                                                                              |
| Output          | Phys/SelJpsi2eeForBetaSBs2JpsieePhiFromTracks/Particles                                                                                                                                                                           |

CombineParticles/BetaSBs2JpsieePhiFromTracksLine

|                  |                                                                                                        |
|------------------|--------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/SelJpsi2eeForBetaSBs2JpsieePhiFromTracks' , 'Phys/SelPhi2KKForBetaSBs2JpsieePhiFromTracks' ] |
| DaughtersCuts    | { '' : 'ALL' , 'J/psi(1S)' : 'ALL' , 'phi(1020)' : 'ALL' }                                             |
| CombinationCut   | (AM \> 3900.0 \*MeV) & (AM \< 6000.0 \*MeV)                                                            |
| MotherCut        | (VFASPF(VCHI2/VDOF) \< 10.0) & (BPVLTIME()\>0.3\*ps)                                                   |
| DecayDescriptor  | B_s0 -\> J/psi(1S) phi(1020)                                                                           |
| DecayDescriptors | [ 'B_s0 -\> J/psi(1S) phi(1020)' ]                                                                   |
| Output           | Phys/BetaSBs2JpsieePhiFromTracksLine/Particles                                                         |
