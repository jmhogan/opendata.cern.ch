[[stripping21r1 lines]](./stripping21r1-index)

# StrippingLowMultCEP_D2KmPipPip_D2KmPipPip_line

## Properties:

|                |                                                        |
|----------------|--------------------------------------------------------|
| OutputLocation | Phys/LowMultCEP_D2KmPipPip_D2KmPipPip_line/Particles   |
| Postscale      | 1.0000000                                              |
| HLT            | HLT_PASS_RE('Hlt2LowMult(D.\*\|C.\*\|Hadron)Decision') |
| Prescale       | 1.0000000                                              |
| L0DU           | None                                                   |
| ODIN           | None                                                   |

## Filter sequence:

LoKi::VoidFilter/StrippingLowMultCEP_D2KmPipPip_D2KmPipPip_lineVOIDFilter

|      |                                                                                                                                                                     |
|------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code | (recSummaryTrack(LHCb.RecSummary.nLongTracks, TrLONG) \> 1) & (recSummaryTrack(LHCb.RecSummary.nBackTracks, TrBACKWARD) \< 1) & (CONTAINS ('Rec/Track/Best') \< 12) |

CheckPV/checkPVmin0

|        |     |
|--------|-----|
| MinPVs | 0   |
| MaxPVs | -1  |

LoKi::VoidFilter/SelFilterPhys_StdAllNoPIDsKaons_Particles

|      |                                                                                                      |
|------|------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdAllNoPIDsKaons](./stripping21r1-commonparticles-stdallnopidskaons)/Particles')\>0 |

FilterDesktop/KaonsForLowMult

|                 |                                                                                     |
|-----------------|-------------------------------------------------------------------------------------|
| Code            | (PT \> 100.0) & (P \> 5000.0) & (TRCHI2DOF \< 3.0) & (PIDK \> 0.0)                  |
| Inputs          | [ 'Phys/[StdAllNoPIDsKaons](./stripping21r1-commonparticles-stdallnopidskaons)' ] |
| DecayDescriptor | None                                                                                |
| Output          | Phys/KaonsForLowMult/Particles                                                      |

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

CombineParticles/selD2pKmPipPip

|                  |                                                                                                          |
|------------------|----------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/KaonsForLowMult' , 'Phys/PionsForLowMult' ]                                                    |
| DaughtersCuts    | { '' : 'ALL' , 'K+' : 'ALL' , 'K-' : 'ALL' , 'pi+' : 'ALL' , 'pi-' : 'ALL' }                             |
| CombinationCut   | (APT \> 0.0) & (ADAMASS('D+') \< 80.0) & (ADOCAMAX('LoKi::DistanceCalculator') \< 0.5) & (AP \> 10000.0) |
| MotherCut        | (VFASPF(VCHI2PDOF) \< 15.0)                                                                              |
| DecayDescriptor  | None                                                                                                     |
| DecayDescriptors | [ 'D+ -\> K- pi+ pi+' ]                                                                                |
| Output           | Phys/selD2pKmPipPip/Particles                                                                            |

CombineParticles/selDm2KpPimPim

|                  |                                                                                                          |
|------------------|----------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/KaonsForLowMult' , 'Phys/PionsForLowMult' ]                                                    |
| DaughtersCuts    | { '' : 'ALL' , 'K+' : 'ALL' , 'K-' : 'ALL' , 'pi+' : 'ALL' , 'pi-' : 'ALL' }                             |
| CombinationCut   | (APT \> 0.0) & (ADAMASS('D+') \< 80.0) & (ADOCAMAX('LoKi::DistanceCalculator') \< 0.5) & (AP \> 10000.0) |
| MotherCut        | (VFASPF(VCHI2PDOF) \< 15.0)                                                                              |
| DecayDescriptor  | None                                                                                                     |
| DecayDescriptors | [ 'D- -\> K+ pi- pi-' ]                                                                                |
| Output           | Phys/selDm2KpPimPim/Particles                                                                            |

CombineParticles/LowMultCEP_D2KmPipPip_D2KmPipPip_line

|                  |                                                      |
|------------------|------------------------------------------------------|
| Inputs           | [ 'Phys/selD2pKmPipPip' , 'Phys/selDm2KpPimPim' ]  |
| DaughtersCuts    | { '' : 'ALL' , 'D+' : 'ALL' , 'D-' : 'ALL' }         |
| CombinationCut   | AALL                                                 |
| MotherCut        | ALL                                                  |
| DecayDescriptor  | None                                                 |
| DecayDescriptors | [ 'psi(3770) -\> D+ D-' ]                          |
| Output           | Phys/LowMultCEP_D2KmPipPip_D2KmPipPip_line/Particles |
