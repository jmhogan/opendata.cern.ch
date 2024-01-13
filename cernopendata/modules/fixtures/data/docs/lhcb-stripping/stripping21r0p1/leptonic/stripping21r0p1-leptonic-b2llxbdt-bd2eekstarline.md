[[stripping21r0p1 lines]](./stripping21r0p1-index)

# StrippingB2LLXBDT_Bd2eeKstarLine

## Properties:

|                |                                        |
|----------------|----------------------------------------|
| OutputLocation | Phys/B2LLXBDT_Bd2eeKstarLine/Particles |
| Postscale      | 1.0000000                              |
| HLT1           | None                                   |
| HLT2           | None                                   |
| Prescale       | 1.0000000                              |
| L0DU           | None                                   |
| ODIN           | None                                   |

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

LoKi::VoidFilter/SelFilterPhys_StdDiElectronFromTracks_Particles

|      |                                                                                                                         |
|------|-------------------------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdDiElectronFromTracks](./stripping21r0p1-commonparticles-stddielectronfromtracks)/Particles',True)\>0 |

FilterDesktop/B2LLXBDTSelDiElectron

|                 |                                                                                                                                                                                                                                                                  |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code            | (HASVERTEX) & (VFASPF(VCHI2)\<16) & (MM\<5.0\*GeV) & (INTREE( (ID=='e+') & (PT\>200\*MeV) & (MIPCHI2DV(PRIMARY)\>1.) & (PIDe\>-2) & (TRGHOSTPROB\<0.5) )) & (INTREE( (ID=='e-') & (PT\>200\*MeV) & (MIPCHI2DV(PRIMARY)\>1.) & (PIDe\>-2) & (TRGHOSTPROB\<0.5) )) |
| Inputs          | [ 'Phys/[StdDiElectronFromTracks](./stripping21r0p1-commonparticles-stddielectronfromtracks)' ]                                                                                                                                                                |
| DecayDescriptor | None                                                                                                                                                                                                                                                             |
| Output          | Phys/B2LLXBDTSelDiElectron/Particles                                                                                                                                                                                                                             |

LoKi::VoidFilter/SelFilterPhys_StdVeryLooseDetachedKst2Kpi_Particles

|      |                                                                                                                                 |
|------|---------------------------------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdVeryLooseDetachedKst2Kpi](./stripping21r0p1-commonparticles-stdveryloosedetachedkst2kpi)/Particles',True)\>0 |

FilterDesktop/B2LLXBDTSelKstar

|                 |                                                                                                           |
|-----------------|-----------------------------------------------------------------------------------------------------------|
| Code            | (VFASPF(VCHI2/VDOF)\<16) & (ADMASS('K\*(892)0')\< 300\*MeV)                                               |
| Inputs          | [ 'Phys/[StdVeryLooseDetachedKst2Kpi](./stripping21r0p1-commonparticles-stdveryloosedetachedkst2kpi)' ] |
| DecayDescriptor | None                                                                                                      |
| Output          | Phys/B2LLXBDTSelKstar/Particles                                                                           |

CombineParticles/B2LLXBDTSelBd2eeKstar

|                  |                                                                                                                        |
|------------------|------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/B2LLXBDTSelDiElectron' , 'Phys/B2LLXBDTSelKstar' ]                                                           |
| DaughtersCuts    | { '' : 'ALL' , 'J/psi(1S)' : 'ALL' , 'K\*(892)0' : 'ALL' , 'K\*(892)~0' : 'ALL' }                                      |
| CombinationCut   | (in_range(3.7\*GeV, AM, 6.8\*GeV))                                                                                     |
| MotherCut        | (in_range(4.0\*GeV, M, 6.5\*GeV)) & (VFASPF(VCHI2/VDOF) \< 25.) & (BPVDIRA\> 0.999) & (BPVDLS\>0) & (BPVIPCHI2()\<400) |
| DecayDescriptor  | [B0 -\> J/psi(1S) K\*(892)0]cc                                                                                       |
| DecayDescriptors | [ '[B0 -\> J/psi(1S) K\*(892)0]cc' ]                                                                               |
| Output           | Phys/B2LLXBDTSelBd2eeKstar/Particles                                                                                   |

FilterDesktop/B2LLXBDT_Bd2eeKstarLine

|                 |                                                               |
|-----------------|---------------------------------------------------------------|
| Code            | VALUE('LoKi::Hybrid::DictValue/B2LLXBDTMvaBd2eeKstar')\>-0.05 |
| Inputs          | [ 'Phys/B2LLXBDTSelBd2eeKstar' ]                            |
| DecayDescriptor | None                                                          |
| Output          | Phys/B2LLXBDT_Bd2eeKstarLine/Particles                        |

AddRelatedInfo/RelatedInfo1_B2LLXBDT_Bd2eeKstarLine

|                 |                                                     |
|-----------------|-----------------------------------------------------|
| Inputs          | [ 'Phys/B2LLXBDT_Bd2eeKstarLine' ]                |
| DecayDescriptor | None                                                |
| Output          | Phys/RelatedInfo1_B2LLXBDT_Bd2eeKstarLine/Particles |

AddRelatedInfo/RelatedInfo2_B2LLXBDT_Bd2eeKstarLine

|                 |                                                     |
|-----------------|-----------------------------------------------------|
| Inputs          | [ 'Phys/B2LLXBDT_Bd2eeKstarLine' ]                |
| DecayDescriptor | None                                                |
| Output          | Phys/RelatedInfo2_B2LLXBDT_Bd2eeKstarLine/Particles |

AddRelatedInfo/RelatedInfo3_B2LLXBDT_Bd2eeKstarLine

|                 |                                                     |
|-----------------|-----------------------------------------------------|
| Inputs          | [ 'Phys/B2LLXBDT_Bd2eeKstarLine' ]                |
| DecayDescriptor | None                                                |
| Output          | Phys/RelatedInfo3_B2LLXBDT_Bd2eeKstarLine/Particles |

AddRelatedInfo/RelatedInfo4_B2LLXBDT_Bd2eeKstarLine

|                 |                                                     |
|-----------------|-----------------------------------------------------|
| Inputs          | [ 'Phys/B2LLXBDT_Bd2eeKstarLine' ]                |
| DecayDescriptor | None                                                |
| Output          | Phys/RelatedInfo4_B2LLXBDT_Bd2eeKstarLine/Particles |

AddRelatedInfo/RelatedInfo5_B2LLXBDT_Bd2eeKstarLine

|                 |                                                     |
|-----------------|-----------------------------------------------------|
| Inputs          | [ 'Phys/B2LLXBDT_Bd2eeKstarLine' ]                |
| DecayDescriptor | None                                                |
| Output          | Phys/RelatedInfo5_B2LLXBDT_Bd2eeKstarLine/Particles |

AddRelatedInfo/RelatedInfo6_B2LLXBDT_Bd2eeKstarLine

|                 |                                                     |
|-----------------|-----------------------------------------------------|
| Inputs          | [ 'Phys/B2LLXBDT_Bd2eeKstarLine' ]                |
| DecayDescriptor | None                                                |
| Output          | Phys/RelatedInfo6_B2LLXBDT_Bd2eeKstarLine/Particles |
