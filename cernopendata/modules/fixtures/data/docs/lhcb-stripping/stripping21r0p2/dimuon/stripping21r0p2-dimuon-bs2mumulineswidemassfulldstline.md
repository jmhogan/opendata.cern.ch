[[stripping21r0p2 lines]](./stripping21r0p2-index)

# StrippingBs2MuMuLinesWideMassFullDSTLine

## Properties:

|                |                                                |
|----------------|------------------------------------------------|
| OutputLocation | Phys/Bs2MuMuLinesWideMassFullDSTLine/Particles |
| Postscale      | 1.0000000                                      |
| HLT1           | None                                           |
| HLT2           | None                                           |
| Prescale       | 1.0000000                                      |
| L0DU           | None                                           |
| ODIN           | None                                           |

## Filter sequence:

LoKi::VoidFilter/StrippingGoodEventConditionDimuon

|      |                                                                                              |
|------|----------------------------------------------------------------------------------------------|
| Code | ALG_EXECUTED('StrippingStreamDimuonBadEvent') & ~ALG_PASSED('StrippingStreamDimuonBadEvent') |

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SELECT:Phys/StdLooseMuons

|      |                                 |
|------|---------------------------------|
| Code | 0StdLooseMuons/Particles',True) |

CombineParticles/Bs2MuMuLinesWideMassFullDSTLine

|                  |                                                                                                                                                                              |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/[StdLooseMuons](./stripping21r0p2-commonparticles-stdloosemuons)' ]                                                                                                |
| DaughtersCuts    | { '' : 'ALL' , 'mu+' : '(MIPCHI2DV(PRIMARY)\> 9)&(TRCHI2DOF \< 4) & ( TRGHOSTPROB \< 0.4 )' , 'mu-' : '(MIPCHI2DV(PRIMARY)\> 9)&(TRCHI2DOF \< 4) & ( TRGHOSTPROB \< 0.4 )' } |
| CombinationCut   | (ADAMASS('B_s0')\<1200\*MeV)& (AMAXDOCA('')\<0.3\*mm)                                                                                                                        |
| MotherCut        | (VFASPF(VCHI2/VDOF)\<9) & (ADMASS('B_s0') \< 1200\*MeV )& (BPVDIRA \> 0) & (BPVVDCHI2\> 121)& (BPVIPCHI2()\< 25)                                                             |
| DecayDescriptor  | B_s0 -\> mu+ mu-                                                                                                                                                             |
| DecayDescriptors | [ 'B_s0 -\> mu+ mu-' ]                                                                                                                                                     |
| Output           | Phys/Bs2MuMuLinesWideMassFullDSTLine/Particles                                                                                                                               |

AddRelatedInfo/RelatedInfo1_Bs2MuMuLinesWideMassFullDSTLine

|                 |                                                             |
|-----------------|-------------------------------------------------------------|
| Inputs          | [ 'Phys/Bs2MuMuLinesWideMassFullDSTLine' ]                |
| DecayDescriptor | None                                                        |
| Output          | Phys/RelatedInfo1_Bs2MuMuLinesWideMassFullDSTLine/Particles |

AddRelatedInfo/RelatedInfo2_Bs2MuMuLinesWideMassFullDSTLine

|                 |                                                             |
|-----------------|-------------------------------------------------------------|
| Inputs          | [ 'Phys/Bs2MuMuLinesWideMassFullDSTLine' ]                |
| DecayDescriptor | None                                                        |
| Output          | Phys/RelatedInfo2_Bs2MuMuLinesWideMassFullDSTLine/Particles |

AddRelatedInfo/RelatedInfo3_Bs2MuMuLinesWideMassFullDSTLine

|                 |                                                             |
|-----------------|-------------------------------------------------------------|
| Inputs          | [ 'Phys/Bs2MuMuLinesWideMassFullDSTLine' ]                |
| DecayDescriptor | None                                                        |
| Output          | Phys/RelatedInfo3_Bs2MuMuLinesWideMassFullDSTLine/Particles |

AddRelatedInfo/RelatedInfo4_Bs2MuMuLinesWideMassFullDSTLine

|                 |                                                             |
|-----------------|-------------------------------------------------------------|
| Inputs          | [ 'Phys/Bs2MuMuLinesWideMassFullDSTLine' ]                |
| DecayDescriptor | None                                                        |
| Output          | Phys/RelatedInfo4_Bs2MuMuLinesWideMassFullDSTLine/Particles |

AddRelatedInfo/RelatedInfo5_Bs2MuMuLinesWideMassFullDSTLine

|                 |                                                             |
|-----------------|-------------------------------------------------------------|
| Inputs          | [ 'Phys/Bs2MuMuLinesWideMassFullDSTLine' ]                |
| DecayDescriptor | None                                                        |
| Output          | Phys/RelatedInfo5_Bs2MuMuLinesWideMassFullDSTLine/Particles |

AddRelatedInfo/RelatedInfo6_Bs2MuMuLinesWideMassFullDSTLine

|                 |                                                             |
|-----------------|-------------------------------------------------------------|
| Inputs          | [ 'Phys/Bs2MuMuLinesWideMassFullDSTLine' ]                |
| DecayDescriptor | None                                                        |
| Output          | Phys/RelatedInfo6_Bs2MuMuLinesWideMassFullDSTLine/Particles |

AddRelatedInfo/RelatedInfo7_Bs2MuMuLinesWideMassFullDSTLine

|                 |                                                             |
|-----------------|-------------------------------------------------------------|
| Inputs          | [ 'Phys/Bs2MuMuLinesWideMassFullDSTLine' ]                |
| DecayDescriptor | None                                                        |
| Output          | Phys/RelatedInfo7_Bs2MuMuLinesWideMassFullDSTLine/Particles |

AddRelatedInfo/RelatedInfo8_Bs2MuMuLinesWideMassFullDSTLine

|                 |                                                             |
|-----------------|-------------------------------------------------------------|
| Inputs          | [ 'Phys/Bs2MuMuLinesWideMassFullDSTLine' ]                |
| DecayDescriptor | None                                                        |
| Output          | Phys/RelatedInfo8_Bs2MuMuLinesWideMassFullDSTLine/Particles |

AddRelatedInfo/RelatedInfo9_Bs2MuMuLinesWideMassFullDSTLine

|                 |                                                             |
|-----------------|-------------------------------------------------------------|
| Inputs          | [ 'Phys/Bs2MuMuLinesWideMassFullDSTLine' ]                |
| DecayDescriptor | None                                                        |
| Output          | Phys/RelatedInfo9_Bs2MuMuLinesWideMassFullDSTLine/Particles |

AddRelatedInfo/RelatedInfo10_Bs2MuMuLinesWideMassFullDSTLine

|                 |                                                              |
|-----------------|--------------------------------------------------------------|
| Inputs          | [ 'Phys/Bs2MuMuLinesWideMassFullDSTLine' ]                 |
| DecayDescriptor | None                                                         |
| Output          | Phys/RelatedInfo10_Bs2MuMuLinesWideMassFullDSTLine/Particles |
