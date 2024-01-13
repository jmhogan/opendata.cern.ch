[[stripping21r1 lines]](./stripping21r1-index)

# StrippingLowMultCEP_D2KsPiPiLL_D2KsPiPiDD_line

## Properties:

|                |                                                        |
|----------------|--------------------------------------------------------|
| OutputLocation | Phys/LowMultCEP_D2KsPiPiLL_D2KsPiPiDD_line/Particles   |
| Postscale      | 1.0000000                                              |
| HLT            | HLT_PASS_RE('Hlt2LowMult(D.\*\|C.\*\|Hadron)Decision') |
| Prescale       | 1.0000000                                              |
| L0DU           | None                                                   |
| ODIN           | None                                                   |

## Filter sequence:

LoKi::VoidFilter/StrippingLowMultCEP_D2KsPiPiLL_D2KsPiPiDD_lineVOIDFilter

|      |                                                                                                                                                                     |
|------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code | (recSummaryTrack(LHCb.RecSummary.nLongTracks, TrLONG) \> 1) & (recSummaryTrack(LHCb.RecSummary.nBackTracks, TrBACKWARD) \< 1) & (CONTAINS ('Rec/Track/Best') \< 12) |

CheckPV/checkPVmin0

|        |     |
|--------|-----|
| MinPVs | 0   |
| MaxPVs | -1  |

LoKi::VoidFilter/SelFilterPhys_StdAllNoPIDsPions_Particles

|      |                                                                                                      |
|------|------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdAllNoPIDsPions](./stripping21r1-commonparticles-stdallnopidspions)/Particles')\>0 |

FilterDesktop/PionsForLowMult

|                 |                                                                                     |
|-----------------|-------------------------------------------------------------------------------------|
| Code            | (PT \> 100.0) & (P \> 5000.0) & (TRCHI2DOF \< 3.0)                                  |
| Inputs          | [ 'Phys/[StdAllNoPIDsPions](./stripping21r1-commonparticles-stdallnopidspions)' ] |
| DecayDescriptor | None                                                                                |
| Output          | Phys/PionsForLowMult/Particles                                                      |

LoKi::VoidFilter/SelFilterPhys_StdLooseKsLL_Particles

|      |                                                                                            |
|------|--------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseKsLL](./stripping21r1-commonparticles-stdlooseksll)/Particles')\>0 |

FilterDesktop/KsLLForLowMult

|                 |                                                                           |
|-----------------|---------------------------------------------------------------------------|
| Code            | (ADMASS('KS0') \< 50.0)                                                   |
| Inputs          | [ 'Phys/[StdLooseKsLL](./stripping21r1-commonparticles-stdlooseksll)' ] |
| DecayDescriptor | None                                                                      |
| Output          | Phys/KsLLForLowMult/Particles                                             |

CombineParticles/selD2KsPiPiLL

|                  |                                                                                                          |
|------------------|----------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/KsLLForLowMult' , 'Phys/PionsForLowMult' ]                                                     |
| DaughtersCuts    | { '' : 'ALL' , 'KS0' : 'ALL' , 'pi+' : 'ALL' , 'pi-' : 'ALL' }                                           |
| CombinationCut   | (APT \> 0.0) & (ADAMASS('D0') \< 80.0) & (ADOCAMAX('LoKi::DistanceCalculator') \< 0.5) & (AP \> 10000.0) |
| MotherCut        | (VFASPF(VCHI2PDOF) \< 15.0)                                                                              |
| DecayDescriptor  | None                                                                                                     |
| DecayDescriptors | [ 'D0 -\> KS0 pi+ pi-' ]                                                                               |
| Output           | Phys/selD2KsPiPiLL/Particles                                                                             |

LoKi::VoidFilter/SelFilterPhys_StdLooseKsDD_Particles

|      |                                                                                            |
|------|--------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseKsDD](./stripping21r1-commonparticles-stdlooseksdd)/Particles')\>0 |

FilterDesktop/KsDDForLowMult

|                 |                                                                           |
|-----------------|---------------------------------------------------------------------------|
| Code            | (ADMASS('KS0') \< 50.0)                                                   |
| Inputs          | [ 'Phys/[StdLooseKsDD](./stripping21r1-commonparticles-stdlooseksdd)' ] |
| DecayDescriptor | None                                                                      |
| Output          | Phys/KsDDForLowMult/Particles                                             |

CombineParticles/selD2KsPiPiDD

|                  |                                                                                                          |
|------------------|----------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/KsDDForLowMult' , 'Phys/PionsForLowMult' ]                                                     |
| DaughtersCuts    | { '' : 'ALL' , 'KS0' : 'ALL' , 'pi+' : 'ALL' , 'pi-' : 'ALL' }                                           |
| CombinationCut   | (APT \> 0.0) & (ADAMASS('D0') \< 80.0) & (ADOCAMAX('LoKi::DistanceCalculator') \< 0.5) & (AP \> 10000.0) |
| MotherCut        | (VFASPF(VCHI2PDOF) \< 15.0)                                                                              |
| DecayDescriptor  | None                                                                                                     |
| DecayDescriptors | [ 'D0 -\> KS0 pi+ pi-' ]                                                                               |
| Output           | Phys/selD2KsPiPiDD/Particles                                                                             |

CombineParticles/LowMultCEP_D2KsPiPiLL_D2KsPiPiDD_line

|                  |                                                            |
|------------------|------------------------------------------------------------|
| Inputs           | [ 'Phys/selD2KsPiPiDD' , 'Phys/selD2KsPiPiLL' ]          |
| DaughtersCuts    | { '' : 'ALL' , 'D0' : 'ALL' , 'D~0' : 'ALL' }              |
| CombinationCut   | AALL                                                       |
| MotherCut        | ALL                                                        |
| DecayDescriptor  | None                                                       |
| DecayDescriptors | [ 'psi(3770) -\> D0 D~0' , '[psi(3770) -\> D0 D0]cc' ] |
| Output           | Phys/LowMultCEP_D2KsPiPiLL_D2KsPiPiDD_line/Particles       |
