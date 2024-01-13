[[stripping21r1 lines]](./stripping21r1-index)

# StrippingLFVB2hTauMuLine

## Properties:

|                |                                |
|----------------|--------------------------------|
| OutputLocation | Phys/LFVB2hTauMuLine/Particles |
| Postscale      | 1.0000000                      |
| HLT            | None                           |
| Prescale       | 1.0000000                      |
| L0DU           | None                           |
| ODIN           | None                           |

## Filter sequence:

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SelFilterPhys_StdLooseMuons_Particles

|      |                                                                                              |
|------|----------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseMuons](./stripping21r1-commonparticles-stdloosemuons)/Particles')\>0 |

LoKi::VoidFilter/SelFilterPhys_StdLooseDetachedTau3pi_Particles

|      |                                                                                                                |
|------|----------------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseDetachedTau3pi](./stripping21r1-commonparticles-stdloosedetachedtau3pi)/Particles')\>0 |

LoKi::VoidFilter/SelFilterPhys_StdNoPIDsPions_Particles

|      |                                                                                                |
|------|------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdNoPIDsPions](./stripping21r1-commonparticles-stdnopidspions)/Particles')\>0 |

LoKi::VoidFilter/SelFilterPhys_StdNoPIDsKaons_Particles

|      |                                                                                                |
|------|------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdNoPIDsKaons](./stripping21r1-commonparticles-stdnopidskaons)/Particles')\>0 |

LoKi::VoidFilter/SelFilterPhys_StdNoPIDsProtons_Particles

|      |                                                                                                    |
|------|----------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdNoPIDsProtons](./stripping21r1-commonparticles-stdnopidsprotons)/Particles')\>0 |

CombineParticles/LFVB2hTauMuLine

|                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/[StdLooseDetachedTau3pi](./stripping21r1-commonparticles-stdloosedetachedtau3pi)' , 'Phys/[StdLooseMuons](./stripping21r1-commonparticles-stdloosemuons)' , 'Phys/[StdNoPIDsKaons](./stripping21r1-commonparticles-stdnopidskaons)' , 'Phys/[StdNoPIDsPions](./stripping21r1-commonparticles-stdnopidspions)' , 'Phys/[StdNoPIDsProtons](./stripping21r1-commonparticles-stdnopidsprotons)' ]                                                                                                                                                                                                                                                                                         |
| DaughtersCuts    | { '' : 'ALL' , 'K+' : '(MIPCHI2DV(PRIMARY)\>36.)&(TRCHI2DOF\<3)&(PIDK\>5)& (TRGHOSTPROB\<0.3)' , 'K-' : '(MIPCHI2DV(PRIMARY)\>36.)&(TRCHI2DOF\<3)&(PIDK\>5)& (TRGHOSTPROB\<0.3)' , 'mu+' : '(MIPCHI2DV(PRIMARY)\>36.)&(TRCHI2DOF\<3)& (TRGHOSTPROB\<0.3)' , 'mu-' : '(MIPCHI2DV(PRIMARY)\>36.)&(TRCHI2DOF\<3)& (TRGHOSTPROB\<0.3)' , 'p+' : '(MIPCHI2DV(PRIMARY)\>36.)&(TRCHI2DOF\<3)&(PIDp\>5)& (TRGHOSTPROB\<0.3)' , 'pi+' : '(MIPCHI2DV(PRIMARY)\>36.)&(TRCHI2DOF\<3) & (TRGHOSTPROB\<0.3)' , 'pi-' : '(MIPCHI2DV(PRIMARY)\>36.)&(TRCHI2DOF\<3) & (TRGHOSTPROB\<0.3)' , 'p~-' : '(MIPCHI2DV(PRIMARY)\>36.)&(TRCHI2DOF\<3)&(PIDp\>5)& (TRGHOSTPROB\<0.3)' , 'tau+' : 'ALL' , 'tau-' : 'ALL' } |
| CombinationCut   | (ADAMASS('B+')\<400\*MeV)& (AMAXDOCA('')\<0.15\*mm)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| MotherCut        | (VFASPF(VCHI2/VDOF)\<9) & (BPVDIRA\>0.999)& (ADMASS('B_s0') \< 400\*MeV )& (BPVDIRA \> 0) & (BPVVDCHI2\> 225)& (BPVIPCHI2()\< 16)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| DecayDescriptor  | None                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| DecayDescriptors | [ '[B+ -\> K+ tau+ mu-]cc' , '[B+ -\> K- tau+ mu+]cc' , '[B+ -\> K+ tau- mu+]cc' , '[B+ -\> pi+ tau+ mu-]cc' , '[B+ -\> pi- tau+ mu+]cc' , '[B+ -\> pi+ tau- mu+]cc' , '[B+ -\> p+ tau+ mu-]cc' , '[B- -\> p+ tau- mu-]cc' , '[B+ -\> p+ tau- mu+]cc' ]                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Output           | Phys/LFVB2hTauMuLine/Particles                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
