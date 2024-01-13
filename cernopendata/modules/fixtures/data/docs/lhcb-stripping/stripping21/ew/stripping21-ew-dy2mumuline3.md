[[stripping21 lines]](./stripping21-index)

# StrippingDY2MuMuLine3

## Properties:

|                |                             |
|----------------|-----------------------------|
| OutputLocation | Phys/DY2MuMuLine3/Particles |
| Postscale      | 1.0000000                   |
| HLT            | None                        |
| Prescale       | 1.0000000                   |
| L0DU           | None                        |
| ODIN           | None                        |

## Filter sequence:

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SelFilterPhys_StdAllLooseMuons_Particles

|      |                                                                                                  |
|------|--------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdAllLooseMuons](./stripping21-commonparticles-stdallloosemuons)/Particles')\>0 |

CombineParticles/DY2MuMuLine3

|                  |                                                                                                                                              |
|------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/[StdAllLooseMuons](./stripping21-commonparticles-stdallloosemuons)' ]                                                              |
| DaughtersCuts    | { '' : 'ALL' , 'mu+' : '(P\>10.0\*GeV) & (PT\>3.0\*GeV) & (TRPCHI2\>0.001)' , 'mu-' : '(P\>10.0\*GeV) & (PT\>3.0\*GeV) & (TRPCHI2\>0.001)' } |
| CombinationCut   | ATRUE                                                                                                                                        |
| MotherCut        | (MM\>10.0\*GeV) & (MM\<20.0\*GeV)                                                                                                            |
| DecayDescriptor  | Z0 -\> mu+ mu-                                                                                                                               |
| DecayDescriptors | [ 'Z0 -\> mu+ mu-' ]                                                                                                                       |
| Output           | Phys/DY2MuMuLine3/Particles                                                                                                                  |
