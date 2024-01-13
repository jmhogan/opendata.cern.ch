[[stripping21r0p1 lines]](./stripping21r0p1-index)

# StrippingB2LLXBDT_Lb2mumuPKLine

## Properties:

|                |                                       |
|----------------|---------------------------------------|
| OutputLocation | Phys/B2LLXBDT_Lb2mumuPKLine/Particles |
| Postscale      | 1.0000000                             |
| HLT1           | None                                  |
| HLT2           | None                                  |
| Prescale       | 1.0000000                             |
| L0DU           | None                                  |
| ODIN           | None                                  |

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

LoKi::VoidFilter/SelFilterPhys_StdLooseDiMuon_Particles

|      |                                                                                                       |
|------|-------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseDiMuon](./stripping21r0p1-commonparticles-stdloosedimuon)/Particles',True)\>0 |

FilterDesktop/B2LLXBDTSelDiMuon

|                 |                                                                                                                                                                                                                                          |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code            | (HASVERTEX) & (VFASPF(VCHI2)\<16) & (MM\<5.0\*GeV) & (INTREE( (ID=='mu+') & (PT\>200\*MeV) & (MIPCHI2DV(PRIMARY)\>1.) & (TRGHOSTPROB\<0.5) )) & (INTREE( (ID=='mu-') & (PT\>200\*MeV) & (MIPCHI2DV(PRIMARY)\>1.) & (TRGHOSTPROB\<0.5) )) |
| Inputs          | [ 'Phys/[StdLooseDiMuon](./stripping21r0p1-commonparticles-stdloosedimuon)' ]                                                                                                                                                          |
| DecayDescriptor | None                                                                                                                                                                                                                                     |
| Output          | Phys/B2LLXBDTSelDiMuon/Particles                                                                                                                                                                                                         |

LoKi::VoidFilter/SelFilterPhys_StdLooseANNProtons_Particles

|      |                                                                                                               |
|------|---------------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseANNProtons](./stripping21r0p1-commonparticles-stdlooseannprotons)/Particles',True)\>0 |

FilterDesktop/B2LLXBDTSelProtons

|                 |                                                                                         |
|-----------------|-----------------------------------------------------------------------------------------|
| Code            | (PROBNNp\> 0.05) & (PT\>300\*MeV) & (TRGHOSTPROB\<0.4)                                  |
| Inputs          | [ 'Phys/[StdLooseANNProtons](./stripping21r0p1-commonparticles-stdlooseannprotons)' ] |
| DecayDescriptor | None                                                                                    |
| Output          | Phys/B2LLXBDTSelProtons/Particles                                                       |

LoKi::VoidFilter/SelFilterPhys_StdLooseANNKaons_Particles

|      |                                                                                                           |
|------|-----------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseANNKaons](./stripping21r0p1-commonparticles-stdlooseannkaons)/Particles',True)\>0 |

FilterDesktop/B2LLXBDTSelKaons

|                 |                                                                                     |
|-----------------|-------------------------------------------------------------------------------------|
| Code            | (PROBNNk \> 0.1) & (PT\>300\*MeV) & (TRGHOSTPROB\<0.4)                              |
| Inputs          | [ 'Phys/[StdLooseANNKaons](./stripping21r0p1-commonparticles-stdlooseannkaons)' ] |
| DecayDescriptor | None                                                                                |
| Output          | Phys/B2LLXBDTSelKaons/Particles                                                     |

CombineParticles/B2LLXBDTSelLambdastar

|                  |                                                                             |
|------------------|-----------------------------------------------------------------------------|
| Inputs           | [ 'Phys/B2LLXBDTSelKaons' , 'Phys/B2LLXBDTSelProtons' ]                   |
| DaughtersCuts    | { '' : 'ALL' , 'K+' : 'ALL' , 'K-' : 'ALL' , 'p+' : 'ALL' , 'p~-' : 'ALL' } |
| CombinationCut   | (AM \< 5.6\*GeV)                                                            |
| MotherCut        | (VFASPF(VCHI2) \< 25.)                                                      |
| DecayDescriptor  | [Lambda(1520)0 -\> p+ K-]cc                                               |
| DecayDescriptors | [ '[Lambda(1520)0 -\> p+ K-]cc' ]                                       |
| Output           | Phys/B2LLXBDTSelLambdastar/Particles                                        |

CombineParticles/B2LLXBDTSelLb2mumuPK

|                  |                                                                                                                        |
|------------------|------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/B2LLXBDTSelDiMuon' , 'Phys/B2LLXBDTSelLambdastar' ]                                                          |
| DaughtersCuts    | { '' : 'ALL' , 'J/psi(1S)' : 'ALL' , 'Lambda(1520)0' : 'ALL' , 'Lambda(1520)~0' : 'ALL' }                              |
| CombinationCut   | (in_range(3.7\*GeV, AM, 7.1\*GeV))                                                                                     |
| MotherCut        | (in_range(4.0\*GeV, M, 6.8\*GeV)) & (VFASPF(VCHI2/VDOF) \< 25.) & (BPVDIRA\> 0.999) & (BPVDLS\>0) & (BPVIPCHI2()\<400) |
| DecayDescriptor  | [Lambda_b0 -\> J/psi(1S) Lambda(1520)0]cc                                                                            |
| DecayDescriptors | [ '[Lambda_b0 -\> J/psi(1S) Lambda(1520)0]cc' ]                                                                    |
| Output           | Phys/B2LLXBDTSelLb2mumuPK/Particles                                                                                    |

FilterDesktop/B2LLXBDT_Lb2mumuPKLine

|                 |                                                              |
|-----------------|--------------------------------------------------------------|
| Code            | VALUE('LoKi::Hybrid::DictValue/B2LLXBDTMvaLb2mumuPK')\>-0.11 |
| Inputs          | [ 'Phys/B2LLXBDTSelLb2mumuPK' ]                            |
| DecayDescriptor | None                                                         |
| Output          | Phys/B2LLXBDT_Lb2mumuPKLine/Particles                        |

AddRelatedInfo/RelatedInfo1_B2LLXBDT_Lb2mumuPKLine

|                 |                                                    |
|-----------------|----------------------------------------------------|
| Inputs          | [ 'Phys/B2LLXBDT_Lb2mumuPKLine' ]                |
| DecayDescriptor | None                                               |
| Output          | Phys/RelatedInfo1_B2LLXBDT_Lb2mumuPKLine/Particles |

AddRelatedInfo/RelatedInfo2_B2LLXBDT_Lb2mumuPKLine

|                 |                                                    |
|-----------------|----------------------------------------------------|
| Inputs          | [ 'Phys/B2LLXBDT_Lb2mumuPKLine' ]                |
| DecayDescriptor | None                                               |
| Output          | Phys/RelatedInfo2_B2LLXBDT_Lb2mumuPKLine/Particles |

AddRelatedInfo/RelatedInfo3_B2LLXBDT_Lb2mumuPKLine

|                 |                                                    |
|-----------------|----------------------------------------------------|
| Inputs          | [ 'Phys/B2LLXBDT_Lb2mumuPKLine' ]                |
| DecayDescriptor | None                                               |
| Output          | Phys/RelatedInfo3_B2LLXBDT_Lb2mumuPKLine/Particles |

AddRelatedInfo/RelatedInfo4_B2LLXBDT_Lb2mumuPKLine

|                 |                                                    |
|-----------------|----------------------------------------------------|
| Inputs          | [ 'Phys/B2LLXBDT_Lb2mumuPKLine' ]                |
| DecayDescriptor | None                                               |
| Output          | Phys/RelatedInfo4_B2LLXBDT_Lb2mumuPKLine/Particles |

AddRelatedInfo/RelatedInfo5_B2LLXBDT_Lb2mumuPKLine

|                 |                                                    |
|-----------------|----------------------------------------------------|
| Inputs          | [ 'Phys/B2LLXBDT_Lb2mumuPKLine' ]                |
| DecayDescriptor | None                                               |
| Output          | Phys/RelatedInfo5_B2LLXBDT_Lb2mumuPKLine/Particles |

AddRelatedInfo/RelatedInfo6_B2LLXBDT_Lb2mumuPKLine

|                 |                                                    |
|-----------------|----------------------------------------------------|
| Inputs          | [ 'Phys/B2LLXBDT_Lb2mumuPKLine' ]                |
| DecayDescriptor | None                                               |
| Output          | Phys/RelatedInfo6_B2LLXBDT_Lb2mumuPKLine/Particles |
