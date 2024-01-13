[[stripping21r1 lines]](./stripping21r1-index)

# StrippingKshort2MuMuMuMu_DownLine

## Properties:

|                |                                         |
|----------------|-----------------------------------------|
| OutputLocation | Phys/Kshort2MuMuMuMu_DownLine/Particles |
| Postscale      | 1.0000000                               |
| HLT            | None                                    |
| Prescale       | 1.0000000                               |
| L0DU           | None                                    |
| ODIN           | None                                    |

## Filter sequence:

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SelFilterPhys_StdLooseDownMuons_Particles

|      |                                                                                                      |
|------|------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseDownMuons](./stripping21r1-commonparticles-stdloosedownmuons)/Particles')\>0 |

FilterDesktop/DownMuonsForKshort2MuMuMuMu

|                 |                                                                                                                |
|-----------------|----------------------------------------------------------------------------------------------------------------|
| Code            | (TRCHI2DOF \< 5) & (P \> 3000.0 \*MeV) & (PT \> 300\* MeV) & (PIDmu-PIDpi \> -1) & (MIPCHI2DV(PRIMARY) \> 4.0) |
| Inputs          | [ 'Phys/[StdLooseDownMuons](./stripping21r1-commonparticles-stdloosedownmuons)' ]                            |
| DecayDescriptor | None                                                                                                           |
| Output          | Phys/DownMuonsForKshort2MuMuMuMu/Particles                                                                     |

CombineParticles/Kshort2MuMuMuMu_DownLine

|                  |                                                                                                                                                           |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/DownMuonsForKshort2MuMuMuMu' ]                                                                                                                  |
| DaughtersCuts    | { '' : 'ALL' , 'mu+' : 'ALL' , 'mu-' : 'ALL' }                                                                                                            |
| CombinationCut   | (AMAXDOCA('')\<0.2) & (AM13 \< 260.0 \*MeV) &(AM24 \< 260.0 \*MeV) &(AM34 \< 260.0 \*MeV) &(AM \< 550.0 \*MeV) & (AHASCHILD( (MIPCHI2DV(PRIMARY)\>15) ) ) |
| MotherCut        | (VFASPF(VCHI2/VDOF) \< 8) & (PT \> 2500.0 \*MeV) &(M \< 540.0 \*MeV) &(BPVVDCHI2\>9) & (BPVIPCHI2()\< 20) & (BPVDIRA \> 0.9999)                           |
| DecayDescriptor  | KS0 -\> mu+ mu+ mu- mu-                                                                                                                                   |
| DecayDescriptors | [ 'KS0 -\> mu+ mu+ mu- mu-' ]                                                                                                                           |
| Output           | Phys/Kshort2MuMuMuMu_DownLine/Particles                                                                                                                   |
