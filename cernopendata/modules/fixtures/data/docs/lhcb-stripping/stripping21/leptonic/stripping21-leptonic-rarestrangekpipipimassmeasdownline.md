[[stripping21 lines]](./stripping21-index)

# StrippingRareStrangeKPiPiPiMassMeasDownLine

## Properties:

|                |                                                   |
|----------------|---------------------------------------------------|
| OutputLocation | Phys/RareStrangeKPiPiPiMassMeasDownLine/Particles |
| Postscale      | 1.0000000                                         |
| HLT            | None                                              |
| Prescale       | 1.0000000                                         |
| L0DU           | None                                              |
| ODIN           | None                                              |

## Filter sequence:

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SelFilterPhys_StdNoPIDsDownPions_Particles

|      |                                                                                                      |
|------|------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdNoPIDsDownPions](./stripping21-commonparticles-stdnopidsdownpions)/Particles')\>0 |

CombineParticles/RareStrangeKPiPiPiMassMeasDownLine

|                  |                                                                                                                                                                            |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/[StdNoPIDsDownPions](./stripping21-commonparticles-stdnopidsdownpions)' ]                                                                                        |
| DaughtersCuts    | { '' : 'ALL' , 'pi+' : '(TRCHI2DOF\<5) & (TRGHOSTPROB \< 0.3) & (MIPCHI2DV(PRIMARY)\>4.0)' , 'pi-' : '(TRCHI2DOF\<5) & (TRGHOSTPROB \< 0.3) & (MIPCHI2DV(PRIMARY)\>4.0)' } |
| CombinationCut   | (ADAMASS('K+') \< 100.0 \*MeV) & (AMAXDOCA('')\< 9999.0 \*mm)                                                                                                              |
| MotherCut        | (PT\> 250.0) & (ADMASS('K+') \< 100.0 \*MeV) & (BPVDIRA \> 0.999)& (VFASPF(VCHI2) \< 20.0) & (BPVVDCHI2 \> 64.0) & (BPVVDZ \> 900.0\*mm) & (BPVVDZ \< 2200.0\*mm)          |
| DecayDescriptor  | [K+ -\> pi+ pi+ pi-]cc                                                                                                                                                   |
| DecayDescriptors | [ '[K+ -\> pi+ pi+ pi-]cc' ]                                                                                                                                           |
| Output           | Phys/RareStrangeKPiPiPiMassMeasDownLine/Particles                                                                                                                          |

AddRelatedInfo/RelatedInfo1_RareStrangeKPiPiPiMassMeasDownLine

|                 |                                                                |
|-----------------|----------------------------------------------------------------|
| Inputs          | [ 'Phys/RareStrangeKPiPiPiMassMeasDownLine' ]                |
| DecayDescriptor | None                                                           |
| Output          | Phys/RelatedInfo1_RareStrangeKPiPiPiMassMeasDownLine/Particles |

AddRelatedInfo/RelatedInfo2_RareStrangeKPiPiPiMassMeasDownLine

|                 |                                                                |
|-----------------|----------------------------------------------------------------|
| Inputs          | [ 'Phys/RareStrangeKPiPiPiMassMeasDownLine' ]                |
| DecayDescriptor | None                                                           |
| Output          | Phys/RelatedInfo2_RareStrangeKPiPiPiMassMeasDownLine/Particles |

AddRelatedInfo/RelatedInfo3_RareStrangeKPiPiPiMassMeasDownLine

|                 |                                                                |
|-----------------|----------------------------------------------------------------|
| Inputs          | [ 'Phys/RareStrangeKPiPiPiMassMeasDownLine' ]                |
| DecayDescriptor | None                                                           |
| Output          | Phys/RelatedInfo3_RareStrangeKPiPiPiMassMeasDownLine/Particles |
