[[stripping21r1 lines]](./stripping21r1-index)

# StrippingLowMultCEP_ChiC2KKKKWS_line

## Properties:

|                |                                                        |
|----------------|--------------------------------------------------------|
| OutputLocation | Phys/LowMultCEP_ChiC2KKKKWS_line/Particles             |
| Postscale      | 1.0000000                                              |
| HLT            | HLT_PASS_RE('Hlt2LowMult(D.\*\|C.\*\|Hadron)Decision') |
| Prescale       | 0.10000000                                             |
| L0DU           | None                                                   |
| ODIN           | None                                                   |

## Filter sequence:

LoKi::VoidFilter/StrippingLowMultCEP_ChiC2KKKKWS_lineVOIDFilter

|      |                                                                                                                                                                    |
|------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code | (recSummaryTrack(LHCb.RecSummary.nLongTracks, TrLONG) \> 1) & (recSummaryTrack(LHCb.RecSummary.nBackTracks, TrBACKWARD) \< 1) & (CONTAINS ('Rec/Track/Best') \< 8) |

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

CombineParticles/LowMultCEP_ChiC2KKKKWS_line

|                  |                                                                                                                                    |
|------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/KaonsForLowMult' ]                                                                                                       |
| DaughtersCuts    | { '' : 'ALL' , 'K+' : 'ALL' , 'K-' : 'ALL' }                                                                                       |
| CombinationCut   | (APT \> 0.0) & (APT \< 5000.0) & (AM \> 2850.0) & (AM \< 4500.0) & (ADOCAMAX('LoKi::DistanceCalculator') \< 0.7) & (AP \> 10000.0) |
| MotherCut        | (VFASPF(VCHI2PDOF) \< 15.0)                                                                                                        |
| DecayDescriptor  | None                                                                                                                               |
| DecayDescriptors | [ '[chi_c1(1P) -\> K+ K+ K+ K+]cc' , '[chi_c1(1P) -\> K+ K+ K+ K-]cc' ]                                                      |
| Output           | Phys/LowMultCEP_ChiC2KKKKWS_line/Particles                                                                                         |
