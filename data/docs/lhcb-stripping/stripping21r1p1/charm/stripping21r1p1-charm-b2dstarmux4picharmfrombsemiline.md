[[stripping21r1p1 lines]](./stripping21r1p1-index)

# Strippingb2DstarMuX4PiCharmFromBSemiLine

## Properties:

|                |                                                                                   |
|----------------|-----------------------------------------------------------------------------------|
| OutputLocation | Phys/b2DstarMuX4PiCharmFromBSemiLine/Particles                                    |
| Postscale      | 1.0000000                                                                         |
| HLT1           | None                                                                              |
| HLT2           | HLT_PASS_RE('Hlt2.\*SingleMuon.\*Decision') \| HLT_PASS_RE('Hlt2Topo.\*Decision') |
| Prescale       | 1.0000000                                                                         |
| L0DU           | None                                                                              |
| ODIN           | None                                                                              |

## Filter sequence:

LoKi::VoidFilter/StrippingGoodEventConditionCharm

|      |                                                                                            |
|------|--------------------------------------------------------------------------------------------|
| Code | ALG_EXECUTED('StrippingStreamCharmBadEvent') & ~ALG_PASSED('StrippingStreamCharmBadEvent') |

LoKi::VoidFilter/Strippingb2DstarMuX4PiCharmFromBSemiLineVOIDFilter

|      |                                                                 |
|------|-----------------------------------------------------------------|
| Code | ( recSummaryTrack(LHCb.RecSummary.nLongTracks, TrLONG) \< 250 ) |

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SelFilterPhys_StdLooseMuons_Particles

|      |                                                                                                     |
|------|-----------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseMuons](./stripping21r1p1-commonparticles-stdloosemuons)/Particles',True)\>0 |

FilterDesktop/SelMuforCharmFromBSemi

|                 |                                                                                                                            |
|-----------------|----------------------------------------------------------------------------------------------------------------------------|
| Code            | (PT \> 800.0 \*MeV) & (P\> 3.0\*GeV)& (TRGHOSTPROB\< 0.5)& (TRCHI2DOF\< 4.0) & (MIPCHI2DV(PRIMARY)\> 4.0)& (PIDmu \> -0.0) |
| Inputs          | [ 'Phys/[StdLooseMuons](./stripping21r1p1-commonparticles-stdloosemuons)' ]                                              |
| DecayDescriptor | None                                                                                                                       |
| Output          | Phys/SelMuforCharmFromBSemi/Particles                                                                                      |

LoKi::VoidFilter/SelFilterPhys_StdLoosePions_Particles

|      |                                                                                                     |
|------|-----------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLoosePions](./stripping21r1p1-commonparticles-stdloosepions)/Particles',True)\>0 |

FilterDesktop/SelPiforCharmFromBSemi

|                 |                                                                                                                           |
|-----------------|---------------------------------------------------------------------------------------------------------------------------|
| Code            | (TRCHI2DOF \< 4.0) & (P\>2.0\*GeV) & (PT \> 250.0 \*MeV)& (TRGHOSTPROB\< 0.5)& (MIPCHI2DV(PRIMARY)\> 9.0) & (PIDK\< 10.0) |
| Inputs          | [ 'Phys/[StdLoosePions](./stripping21r1p1-commonparticles-stdloosepions)' ]                                             |
| DecayDescriptor | None                                                                                                                      |
| Output          | Phys/SelPiforCharmFromBSemi/Particles                                                                                     |

DaVinci::N4BodyDecays/Sel_D0_to_4Pi_forCharmFromBSemi

|                  |                                                                                                                                              |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/SelPiforCharmFromBSemi' ]                                                                                                          |
| DaughtersCuts    | { '' : 'ALL' , 'pi+' : 'ALL' , 'pi-' : 'ALL' }                                                                                               |
| CombinationCut   | (ADAMASS('D0') \< 42.0 \*MeV) &( (APT1+APT2+APT3+APT4) \> 1800.0 )&( ACHI2DOCA(1,4) \< 7 ) &( ACHI2DOCA(2,4) \< 7 ) &( ACHI2DOCA(3,4) \< 7 ) |
| MotherCut        | (ADMASS('D0') \< 40.0 \*MeV) &(VFASPF(VCHI2PDOF) \< 6.0)&(SUMTREE( PT, ISBASIC )\> 1800.0\*MeV)&(BPVVDCHI2 \> 100.0)&(BPVDIRA \> 0.99 )      |
| DecayDescriptor  | None                                                                                                                                         |
| DecayDescriptors | [ 'D0 -\> pi- pi+ pi- pi+' ]                                                                                                               |
| Output           | Phys/Sel_D0_to_4Pi_forCharmFromBSemi/Particles                                                                                               |

ConjugateNeutralPID/SelConjugateD0ForDstar_4PiForCharmFromBSemi

|                 |                                                            |
|-----------------|------------------------------------------------------------|
| Inputs          | [ 'Phys/Sel_D0_to_4Pi_forCharmFromBSemi' ]               |
| DecayDescriptor | None                                                       |
| Output          | Phys/SelConjugateD0ForDstar_4PiForCharmFromBSemi/Particles |

LoKi::VoidFilter/SelFilterPhys_StdAllLoosePions_Particles

|      |                                                                                                           |
|------|-----------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdAllLoosePions](./stripping21r1p1-commonparticles-stdallloosepions)/Particles',True)\>0 |

CombineParticles/SelDstar_4PiForCharmFromBSemi

|                  |                                                                                                                                                                                   |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/SelConjugateD0ForDstar_4PiForCharmFromBSemi' , 'Phys/Sel_D0_to_4Pi_forCharmFromBSemi' , 'Phys/[StdAllLoosePions](./stripping21r1p1-commonparticles-stdallloosepions)' ] |
| DaughtersCuts    | { '' : 'ALL' , 'D0' : 'ALL' , 'D~0' : 'ALL' , 'pi+' : '( PT \> 80.0 \*MeV )' , 'pi-' : '( PT \> 80.0 \*MeV )' }                                                                   |
| CombinationCut   | (AM - ACHILD(M,1) + 5 \> 0.0 \*MeV) & (AM - ACHILD(M,1) - 5 \< 170.0 \*MeV)                                                                                                       |
| MotherCut        | ((VFASPF(VCHI2/VDOF) \< 8.0 ) & (M - CHILD(M,1) \> 0.0 \*MeV) & (M - CHILD(M,1) \< 170.0 \*MeV))                                                                                  |
| DecayDescriptor  | [D\*(2010)+ -\> D0 pi+]cc                                                                                                                                                       |
| DecayDescriptors | [ '[D\*(2010)+ -\> D0 pi+]cc' ]                                                                                                                                               |
| Output           | Phys/SelDstar_4PiForCharmFromBSemi/Particles                                                                                                                                      |

CombineParticles/Selb2DstarMuX4PiCharmFromBSemi

|                  |                                                                                                                                                                                                |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/SelDstar_4PiForCharmFromBSemi' , 'Phys/SelMuforCharmFromBSemi' ]                                                                                                                     |
| DaughtersCuts    | { '' : 'ALL' , 'D\*(2010)+' : 'ALL' , 'D\*(2010)-' : 'ALL' , 'mu+' : 'ALL' , 'mu-' : 'ALL' }                                                                                                   |
| CombinationCut   | (AM\<6200\*MeV)                                                                                                                                                                                |
| MotherCut        | (MM\> 2500 \*MeV) & (MM\<6000 \*MeV) & (VFASPF(VCHI2/VDOF)\< 6.0) & (BPVDIRA\> 0.999) & (MINTREE(((ABSID=='D+') \| (ABSID=='D0') \| (ABSID=='Lambda_c+')) , VFASPF(VZ))-VFASPF(VZ) \> 0 \*mm ) |
| DecayDescriptor  | None                                                                                                                                                                                           |
| DecayDescriptors | [ '[B~0 -\> D\*(2010)+ mu-]cc' , '[B~0 -\> D\*(2010)+ mu+]cc' ]                                                                                                                          |
| Output           | Phys/Selb2DstarMuX4PiCharmFromBSemi/Particles                                                                                                                                                  |

TisTosParticleTagger/b2DstarMuX4PiCharmFromBSemiLine

|                 |                                                                                                                                       |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------|
| Inputs          | [ 'Phys/Selb2DstarMuX4PiCharmFromBSemi' ]                                                                                           |
| DecayDescriptor | None                                                                                                                                  |
| Output          | Phys/b2DstarMuX4PiCharmFromBSemiLine/Particles                                                                                        |
| TisTosSpecs     | { 'Hlt1.\*Track.\*Decision%TOS' : 0 , 'Hlt2.\*SingleMuon.\*Decision%TOS' : 0 , 'Hlt2Global%TIS' : 0 , 'Hlt2Topo.\*Decision%TOS' : 0 } |
