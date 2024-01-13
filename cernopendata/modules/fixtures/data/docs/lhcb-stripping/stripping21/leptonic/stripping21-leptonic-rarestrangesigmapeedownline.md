[[stripping21 lines]](./stripping21-index)

# StrippingRareStrangeSigmaPEEDownLine

## Properties:

|                |                                            |
|----------------|--------------------------------------------|
| OutputLocation | Phys/RareStrangeSigmaPEEDownLine/Particles |
| Postscale      | 1.0000000                                  |
| HLT            | None                                       |
| Prescale       | 0.10000000                                 |
| L0DU           | None                                       |
| ODIN           | None                                       |

## Filter sequence:

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SelFilterPhys_StdNoPIDsDownElectrons_Particles

|      |                                                      |
|------|------------------------------------------------------|
| Code | CONTAINS('Phys/StdNoPIDsDownElectrons/Particles')\>0 |

LoKi::VoidFilter/SelFilterPhys_StdNoPIDsDownProtons_Particles

|      |                                                                                                          |
|------|----------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdNoPIDsDownProtons](./stripping21-commonparticles-stdnopidsdownprotons)/Particles')\>0 |

CombineParticles/RareStrangeSigmaPEEDownLine

|                  |                                                                                                                                                                                                                                                                               |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/StdNoPIDsDownElectrons' , 'Phys/[StdNoPIDsDownProtons](./stripping21-commonparticles-stdnopidsdownprotons)' ]                                                                                                                                                       |
| DaughtersCuts    | { '' : 'ALL' , 'e+' : '(TRCHI2DOF\<9.0) & (TRGHOSTPROB\<0.3) & (MIPCHI2DV(PRIMARY)\>4.0)' , 'e-' : '(TRCHI2DOF\<9.0) & (TRGHOSTPROB\<0.3) & (MIPCHI2DV(PRIMARY)\>4.0)' , 'p+' : '(TRCHI2DOF\<9.0) & (TRGHOSTPROB\<0.3) ' , 'p~-' : '(TRCHI2DOF\<9.0) & (TRGHOSTPROB\<0.3) ' } |
| CombinationCut   | (ADAMASS('Sigma+')\<100.0 \*MeV) & (AMAXDOCA('')\< 10.0 \*mm)                                                                                                                                                                                                                 |
| MotherCut        | (VFASPF(VCHI2/VDOF)\< 25.0) & (PT\> 0.0 \*MeV)& (ADMASS('Sigma+') \< 100.0 \*MeV )& (BPVDIRA \> 0.9) & (BPVIPCHI2()\< 25.0)& (BPVLTIME()\> 7.0 \* ps)                                                                                                                         |
| DecayDescriptor  | [Sigma+ -\> p+ e+ e-]cc                                                                                                                                                                                                                                                     |
| DecayDescriptors | [ '[Sigma+ -\> p+ e+ e-]cc' ]                                                                                                                                                                                                                                             |
| Output           | Phys/RareStrangeSigmaPEEDownLine/Particles                                                                                                                                                                                                                                    |

AddRelatedInfo/RelatedInfo1_RareStrangeSigmaPEEDownLine

|                 |                                                         |
|-----------------|---------------------------------------------------------|
| Inputs          | [ 'Phys/RareStrangeSigmaPEEDownLine' ]                |
| DecayDescriptor | None                                                    |
| Output          | Phys/RelatedInfo1_RareStrangeSigmaPEEDownLine/Particles |

AddRelatedInfo/RelatedInfo2_RareStrangeSigmaPEEDownLine

|                 |                                                         |
|-----------------|---------------------------------------------------------|
| Inputs          | [ 'Phys/RareStrangeSigmaPEEDownLine' ]                |
| DecayDescriptor | None                                                    |
| Output          | Phys/RelatedInfo2_RareStrangeSigmaPEEDownLine/Particles |

AddRelatedInfo/RelatedInfo3_RareStrangeSigmaPEEDownLine

|                 |                                                         |
|-----------------|---------------------------------------------------------|
| Inputs          | [ 'Phys/RareStrangeSigmaPEEDownLine' ]                |
| DecayDescriptor | None                                                    |
| Output          | Phys/RelatedInfo3_RareStrangeSigmaPEEDownLine/Particles |
