[[stripping21r1 lines]](./stripping21r1-index)

# StrippingBetaSPsi2SMuMu_Bd2Psi2SKstarMuMuDetachedLine

## Properties:

|                |                                                             |
|----------------|-------------------------------------------------------------|
| OutputLocation | Phys/BetaSPsi2SMuMu_Bd2Psi2SKstarMuMuDetachedLine/Particles |
| Postscale      | 1.0000000                                                   |
| HLT            | None                                                        |
| Prescale       | 1.0000000                                                   |
| L0DU           | None                                                        |
| ODIN           | None                                                        |

## Filter sequence:

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SelFilterPhys_StdAllLooseMuons_Particles

|      |                                                                                                    |
|------|----------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdAllLooseMuons](./stripping21r1-commonparticles-stdallloosemuons)/Particles')\>0 |

CombineParticles/BetaSPsi2SMuMu_Psi2SToMuMu

|                  |                                                                                   |
|------------------|-----------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/[StdAllLooseMuons](./stripping21r1-commonparticles-stdallloosemuons)' ] |
| DaughtersCuts    | { '' : 'ALL' , 'mu+' : 'PIDmu \> 0.0' , 'mu-' : 'PIDmu\>0.0' }                    |
| CombinationCut   | (ADAMASS('psi(2S)')\<60.0\*MeV) & (ADOCACHI2CUT( 30.0 ,''))                       |
| MotherCut        | (VFASPF(VCHI2/VDOF) \< 16) & (MFIT)                                               |
| DecayDescriptor  | psi(2S) -\> mu+ mu-                                                               |
| DecayDescriptors | [ 'psi(2S) -\> mu+ mu-' ]                                                       |
| Output           | Phys/BetaSPsi2SMuMu_Psi2SToMuMu/Particles                                         |

LoKi::VoidFilter/SelFilterPhys_StdLooseKstar2Kpi_Particles

|      |                                                                                                      |
|------|------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseKstar2Kpi](./stripping21r1-commonparticles-stdloosekstar2kpi)/Particles')\>0 |

FilterDesktop/BetaSPsi2SMuMu_KstarForPsi2SToMuMu

|                 |                                                                                                                                                                                                                              |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code            | (in_range(826,M,966)) & (PT \> 1200\*MeV) & (VFASPF(VCHI2) \< 16)& (MAXTREE('K+'==ABSID, TRCHI2DOF) \< 4 )& (MAXTREE('pi-'==ABSID, TRCHI2DOF) \< 4 )& (MINTREE('K+'==ABSID, PIDK) \> 0)& (MINTREE('pi-'==ABSID, PIDK) \< 10) |
| Inputs          | [ 'Phys/[StdLooseKstar2Kpi](./stripping21r1-commonparticles-stdloosekstar2kpi)' ]                                                                                                                                          |
| DecayDescriptor | None                                                                                                                                                                                                                         |
| Output          | Phys/BetaSPsi2SMuMu_KstarForPsi2SToMuMu/Particles                                                                                                                                                                            |

CombineParticles/BetaSPsi2SMuMu_Bd2Psi2SKstarMuMuDetachedLine

|                  |                                                                                     |
|------------------|-------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/BetaSPsi2SMuMu_KstarForPsi2SToMuMu' , 'Phys/BetaSPsi2SMuMu_Psi2SToMuMu' ] |
| DaughtersCuts    | { '' : 'ALL' , 'K\*(892)0' : 'ALL' , 'K\*(892)~0' : 'ALL' , 'psi(2S)' : 'ALL' }     |
| CombinationCut   | in_range(5000,AM,5650)                                                              |
| MotherCut        | in_range(5150,M,5550) & (VFASPF(VCHI2PDOF)\<20)& (BPVLTIME()\> 0.2\*ps)             |
| DecayDescriptor  | [B0 -\> psi(2S) K\*(892)0]cc                                                      |
| DecayDescriptors | [ '[B0 -\> psi(2S) K\*(892)0]cc' ]                                              |
| Output           | Phys/BetaSPsi2SMuMu_Bd2Psi2SKstarMuMuDetachedLine/Particles                         |
