[[stripping21 lines]](./stripping21-index)

# StrippingRareStrangeSigmaPMuMuDownLine

## Properties:

|                |                                              |
|----------------|----------------------------------------------|
| OutputLocation | Phys/RareStrangeSigmaPMuMuDownLine/Particles |
| Postscale      | 1.0000000                                    |
| HLT            | None                                         |
| Prescale       | 1.0000000                                    |
| L0DU           | None                                         |
| ODIN           | None                                         |

## Filter sequence:

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SelFilterPhys_StdLooseDownMuons_Particles

|      |                                                                                                    |
|------|----------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseDownMuons](./stripping21-commonparticles-stdloosedownmuons)/Particles')\>0 |

LoKi::VoidFilter/SelFilterPhys_StdNoPIDsDownProtons_Particles

|      |                                                                                                          |
|------|----------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdNoPIDsDownProtons](./stripping21-commonparticles-stdnopidsdownprotons)/Particles')\>0 |

CombineParticles/RareStrangeSigmaPMuMuDownLine

|                  |                                                                                                                                                                                                                                                                                 |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/[StdLooseDownMuons](./stripping21-commonparticles-stdloosedownmuons)' , 'Phys/[StdNoPIDsDownProtons](./stripping21-commonparticles-stdnopidsdownprotons)' ]                                                                                                           |
| DaughtersCuts    | { '' : 'ALL' , 'mu+' : '(TRCHI2DOF\< 9.0) & (TRGHOSTPROB\<0.3) & (MIPCHI2DV(PRIMARY)\>9.0)' , 'mu-' : '(TRCHI2DOF\< 9.0) & (TRGHOSTPROB\<0.3) & (MIPCHI2DV(PRIMARY)\>9.0)' , 'p+' : '(TRCHI2DOF\<9.0) & (TRGHOSTPROB\<0.3)' , 'p~-' : '(TRCHI2DOF\<9.0) & (TRGHOSTPROB\<0.3)' } |
| CombinationCut   | (ADAMASS('Sigma+')\<500.0 \*MeV) & (AMAXDOCA('')\< 10.0 \*mm)                                                                                                                                                                                                                   |
| MotherCut        | (VFASPF(VCHI2/VDOF)\< 25.0) & (PT\> 0.0 \*MeV)& (ADMASS('Sigma+') \< 500.0 \*MeV )& (BPVDIRA \> 0.9) & (BPVIPCHI2()\< 25.0)& (BPVLTIME()\> 7.0 \* ps)                                                                                                                           |
| DecayDescriptor  | [Sigma+ -\> p+ mu+ mu-]cc                                                                                                                                                                                                                                                     |
| DecayDescriptors | [ '[Sigma+ -\> p+ mu+ mu-]cc' ]                                                                                                                                                                                                                                             |
| Output           | Phys/RareStrangeSigmaPMuMuDownLine/Particles                                                                                                                                                                                                                                    |

AddRelatedInfo/RelatedInfo1_RareStrangeSigmaPMuMuDownLine

|                 |                                                           |
|-----------------|-----------------------------------------------------------|
| Inputs          | [ 'Phys/RareStrangeSigmaPMuMuDownLine' ]                |
| DecayDescriptor | None                                                      |
| Output          | Phys/RelatedInfo1_RareStrangeSigmaPMuMuDownLine/Particles |

AddRelatedInfo/RelatedInfo2_RareStrangeSigmaPMuMuDownLine

|                 |                                                           |
|-----------------|-----------------------------------------------------------|
| Inputs          | [ 'Phys/RareStrangeSigmaPMuMuDownLine' ]                |
| DecayDescriptor | None                                                      |
| Output          | Phys/RelatedInfo2_RareStrangeSigmaPMuMuDownLine/Particles |

AddRelatedInfo/RelatedInfo3_RareStrangeSigmaPMuMuDownLine

|                 |                                                           |
|-----------------|-----------------------------------------------------------|
| Inputs          | [ 'Phys/RareStrangeSigmaPMuMuDownLine' ]                |
| DecayDescriptor | None                                                      |
| Output          | Phys/RelatedInfo3_RareStrangeSigmaPMuMuDownLine/Particles |
