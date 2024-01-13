[[stripping21r1 lines]](./stripping21r1-index)

# StrippingBuToKX3872_BuToKX3872LooseLine

## Properties:

|                |                                               |
|----------------|-----------------------------------------------|
| OutputLocation | Phys/BuToKX3872_BuToKX3872LooseLine/Particles |
| Postscale      | 1.0000000                                     |
| HLT            | None                                          |
| Prescale       | 1.0000000                                     |
| L0DU           | None                                          |
| ODIN           | None                                          |

## Filter sequence:

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SelFilterPhys_StdLooseJpsi2MuMu_Particles

|      |                                                                                                      |
|------|------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseJpsi2MuMu](./stripping21r1-commonparticles-stdloosejpsi2mumu)/Particles')\>0 |

FilterDesktop/SelFilter_BuToKX3872Loose_JPsi

|                 |                                                                                                                                                                                           |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code            | (ADMASS('J/psi(1S)') \< 70.0 \* MeV) & (VFASPF(VCHI2/VDOF) \< 10.0) & (2 == NINTREE((ABSID=='mu-') & (TRCHI2DOF \< 4.0) & (MIPCHI2DV(PRIMARY) \> 2.0) & (PT \> 500.0 \* MeV) & (ISMUON))) |
| Inputs          | [ 'Phys/[StdLooseJpsi2MuMu](./stripping21r1-commonparticles-stdloosejpsi2mumu)' ]                                                                                                       |
| DecayDescriptor | None                                                                                                                                                                                      |
| Output          | Phys/SelFilter_BuToKX3872Loose_JPsi/Particles                                                                                                                                             |

LoKi::VoidFilter/SelFilterPhys_StdAllLoosePions_Particles

|      |                                                                                                    |
|------|----------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdAllLoosePions](./stripping21r1-commonparticles-stdallloosepions)/Particles')\>0 |

CombineParticles/SelBuild_BuToKX3872Loose_Rho

|                  |                                                                                                                                          |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/[StdAllLoosePions](./stripping21r1-commonparticles-stdallloosepions)' ]                                                        |
| DaughtersCuts    | { '' : 'ALL' , 'pi+' : '(TRCHI2DOF \< 4.0) & (MIPCHI2DV(PRIMARY) \> 6.0)' , 'pi-' : '(TRCHI2DOF \< 4.0) & (MIPCHI2DV(PRIMARY) \> 6.0)' } |
| CombinationCut   | ATRUE                                                                                                                                    |
| MotherCut        | ALL                                                                                                                                      |
| DecayDescriptor  | rho(770)0 -\> pi+ pi-                                                                                                                    |
| DecayDescriptors | [ 'rho(770)0 -\> pi+ pi-' ]                                                                                                            |
| Output           | Phys/SelBuild_BuToKX3872Loose_Rho/Particles                                                                                              |

CombineParticles/Sel_BuToKX3872_BuToKX3872Loose_X3872

|                  |                                                                                   |
|------------------|-----------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/SelBuild_BuToKX3872Loose_Rho' , 'Phys/SelFilter_BuToKX3872Loose_JPsi' ] |
| DaughtersCuts    | { '' : 'ALL' , 'J/psi(1S)' : 'ALL' , 'rho(770)0' : 'ALL' }                        |
| CombinationCut   | (ADAMASS('X_1(3872)') \< 220.0 \* MeV)                                            |
| MotherCut        | (ADMASS('X_1(3872)') \< 190.0 \* MeV) & (VFASPF(VCHI2/VDOF) \< 10.0)              |
| DecayDescriptor  | X_1(3872) -\> J/psi(1S) rho(770)0                                                 |
| DecayDescriptors | [ 'X_1(3872) -\> J/psi(1S) rho(770)0' ]                                         |
| Output           | Phys/Sel_BuToKX3872_BuToKX3872Loose_X3872/Particles                               |

LoKi::VoidFilter/SelFilterPhys_StdLooseKaons_Particles

|      |                                                                                              |
|------|----------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseKaons](./stripping21r1-commonparticles-stdloosekaons)/Particles')\>0 |

FilterDesktop/SelFilter_BuToKX3872Loose_Kaon

|                 |                                                                             |
|-----------------|-----------------------------------------------------------------------------|
| Code            | (TRCHI2DOF \< 4.0) & (PT \> 150.0 \* MeV) & (MIPCHI2DV(PRIMARY) \> 5.0)     |
| Inputs          | [ 'Phys/[StdLooseKaons](./stripping21r1-commonparticles-stdloosekaons)' ] |
| DecayDescriptor | None                                                                        |
| Output          | Phys/SelFilter_BuToKX3872Loose_Kaon/Particles                               |

CombineParticles/BuToKX3872_BuToKX3872LooseLine

|                  |                                                                                                                                 |
|------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/SelFilter_BuToKX3872Loose_Kaon' , 'Phys/Sel_BuToKX3872_BuToKX3872Loose_X3872' ]                                       |
| DaughtersCuts    | { '' : 'ALL' , 'K+' : 'ALL' , 'K-' : 'ALL' , 'X_1(3872)' : 'ALL' }                                                              |
| CombinationCut   | (ADAMASS('B+') \< 500.0 \* MeV)                                                                                                 |
| MotherCut        | (ADMASS('B+') \< 400.0 \* MeV) & (VFASPF(VCHI2/VDOF) \< 5.0) & (BPVIPCHI2() \< 20.0) & (BPVDIRA\> 0.9995) & (BPVVDCHI2 \> 30.0) |
| DecayDescriptor  | None                                                                                                                            |
| DecayDescriptors | [ 'B+ -\> X_1(3872) K+' , 'B- -\> X_1(3872) K-' ]                                                                             |
| Output           | Phys/BuToKX3872_BuToKX3872LooseLine/Particles                                                                                   |
