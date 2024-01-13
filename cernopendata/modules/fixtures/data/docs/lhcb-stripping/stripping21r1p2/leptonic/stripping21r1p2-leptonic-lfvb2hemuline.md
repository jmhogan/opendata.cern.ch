[[stripping21r1p2 lines]](./stripping21r1p2-index)

# StrippingLFVB2heMuLine

## Properties:

|                |                              |
|----------------|------------------------------|
| OutputLocation | Phys/LFVB2heMuLine/Particles |
| Postscale      | 1.0000000                    |
| HLT1           | None                         |
| HLT2           | None                         |
| Prescale       | 1.0000000                    |
| L0DU           | None                         |
| ODIN           | None                         |

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

LoKi::VoidFilter/SELECT:Phys/StdLooseMuons

|      |                                 |
|------|---------------------------------|
| Code | 0StdLooseMuons/Particles',True) |

LoKi::VoidFilter/SELECT:Phys/StdLooseElectrons

|      |                                     |
|------|-------------------------------------|
| Code | 0StdLooseElectrons/Particles',True) |

LoKi::VoidFilter/SELECT:Phys/StdNoPIDsPions

|      |                                  |
|------|----------------------------------|
| Code | 0StdNoPIDsPions/Particles',True) |

LoKi::VoidFilter/SELECT:Phys/StdNoPIDsKaons

|      |                                  |
|------|----------------------------------|
| Code | 0StdNoPIDsKaons/Particles',True) |

LoKi::VoidFilter/SELECT:Phys/StdNoPIDsProtons

|      |                                    |
|------|------------------------------------|
| Code | 0StdNoPIDsProtons/Particles',True) |

CombineParticles/LFVB2heMuLine

|                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/[StdLooseElectrons](./stripping21r1p2-commonparticles-stdlooseelectrons)' , 'Phys/[StdLooseMuons](./stripping21r1p2-commonparticles-stdloosemuons)' , 'Phys/[StdNoPIDsKaons](./stripping21r1p2-commonparticles-stdnopidskaons)' , 'Phys/[StdNoPIDsPions](./stripping21r1p2-commonparticles-stdnopidspions)' , 'Phys/[StdNoPIDsProtons](./stripping21r1p2-commonparticles-stdnopidsprotons)' ]                                                                                                                                                                                                                                                                                                                                                                                                       |
| DaughtersCuts    | { '' : 'ALL' , 'K+' : '(MIPCHI2DV(PRIMARY)\>25.)&(TRCHI2DOF\<3)&(PIDK\>5) & (TRGHOSTPROB\<0.3)' , 'K-' : '(MIPCHI2DV(PRIMARY)\>25.)&(TRCHI2DOF\<3)&(PIDK\>5) & (TRGHOSTPROB\<0.3)' , 'e+' : '(MIPCHI2DV(PRIMARY)\>25.)&(TRCHI2DOF\<3) & (PIDe \> 2)' , 'e-' : '(MIPCHI2DV(PRIMARY)\>25.)&(TRCHI2DOF\<3) & (PIDe \> 2)' , 'mu+' : '(MIPCHI2DV(PRIMARY)\>25.)&(TRCHI2DOF\<3) & (TRGHOSTPROB\<0.3)' , 'mu-' : '(MIPCHI2DV(PRIMARY)\>25.)&(TRCHI2DOF\<3) & (TRGHOSTPROB\<0.3)' , 'p+' : '(MIPCHI2DV(PRIMARY)\>25.)&(TRCHI2DOF\<3)&(PIDp\>5) & (TRGHOSTPROB\<0.3)' , 'pi+' : '(MIPCHI2DV(PRIMARY)\>25.)&( TRCHI2DOF \< 3 )& (TRGHOSTPROB\<0.3)' , 'pi-' : '(MIPCHI2DV(PRIMARY)\>25.)&( TRCHI2DOF \< 3 )& (TRGHOSTPROB\<0.3)' , 'p~-' : '(MIPCHI2DV(PRIMARY)\>25.)&(TRCHI2DOF\<3)&(PIDp\>5) & (TRGHOSTPROB\<0.3)' } |
| CombinationCut   | (ADAMASS('B+')\<600\*MeV)& (AMAXDOCA('')\<0.3\*mm)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| MotherCut        | (VFASPF(VCHI2/VDOF)\<9) & (ADMASS('B_s0') \< 600\*MeV )& (BPVDIRA \> 0) & (BPVVDCHI2\> 225)& (BPVIPCHI2()\< 25)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| DecayDescriptor  | None                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| DecayDescriptors | [ '[B+ -\> K+ e+ mu-]cc' , '[B+ -\> K- e+ mu+]cc' , '[B+ -\> K+ e- mu+]cc' , '[B+ -\> pi+ e+ mu-]cc' , '[B+ -\> pi- e+ mu+]cc' , '[B+ -\> pi+ e- mu+]cc' , '[B+ -\> p+ e+ mu-]cc' , '[B- -\> p+ e- mu-]cc' , '[B+ -\> p+ e- mu+]cc' ]                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Output           | Phys/LFVB2heMuLine/Particles                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
