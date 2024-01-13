[[stripping21r1 lines]](./stripping21r1-index)

# StrippingBetaSPsi2SMuMu_Bs2Psi2SPhiMuMuDetachedLine

## Properties:

|                |                                                           |
|----------------|-----------------------------------------------------------|
| OutputLocation | Phys/BetaSPsi2SMuMu_Bs2Psi2SPhiMuMuDetachedLine/Particles |
| Postscale      | 1.0000000                                                 |
| HLT            | None                                                      |
| Prescale       | 1.0000000                                                 |
| L0DU           | None                                                      |
| ODIN           | None                                                      |

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

LoKi::VoidFilter/SelFilterPhys_StdLoosePhi2KK_Particles

|      |                                                                                                |
|------|------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLoosePhi2KK](./stripping21r1-commonparticles-stdloosephi2kk)/Particles')\>0 |

FilterDesktop/BetaSPsi2SMuMu_PhiForPsi2SToMuMu

|                 |                                                                                                                                                        |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code            | (ADMASS('phi(1020)') \< 20) & (PT \> 1000 \*MeV) & (VFASPF(VCHI2) \< 25) & (MAXTREE('K+'==ABSID, TRCHI2DOF) \< 5) & (MINTREE('K+'==ABSID, PIDK) \> -2) |
| Inputs          | [ 'Phys/[StdLoosePhi2KK](./stripping21r1-commonparticles-stdloosephi2kk)' ]                                                                          |
| DecayDescriptor | None                                                                                                                                                   |
| Output          | Phys/BetaSPsi2SMuMu_PhiForPsi2SToMuMu/Particles                                                                                                        |

CombineParticles/BetaSPsi2SMuMu_Bs2Psi2SPhiMuMuDetachedLine

|                  |                                                                                   |
|------------------|-----------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/BetaSPsi2SMuMu_PhiForPsi2SToMuMu' , 'Phys/BetaSPsi2SMuMu_Psi2SToMuMu' ] |
| DaughtersCuts    | { '' : 'ALL' , 'phi(1020)' : 'ALL' , 'psi(2S)' : 'ALL' }                          |
| CombinationCut   | in_range(5000,AM,5650)                                                            |
| MotherCut        | in_range(5150,M,5550) & (VFASPF(VCHI2PDOF)\<20)& (BPVLTIME()\> 0.2\*ps)           |
| DecayDescriptor  | B_s0 -\> psi(2S) phi(1020)                                                        |
| DecayDescriptors | [ 'B_s0 -\> psi(2S) phi(1020)' ]                                                |
| Output           | Phys/BetaSPsi2SMuMu_Bs2Psi2SPhiMuMuDetachedLine/Particles                         |
