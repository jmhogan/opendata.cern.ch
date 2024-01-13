[[stripping21r1p2 lines]](./stripping21r1p2-index)

# StdLooseDplus2KKPi

**CombineParticles/StdLooseDplus2KKPi**

|                  |                                                                                                                                                                          |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | ['Phys/[StdLooseKaons](./stripping21r1p2-commonparticles-stdloosekaons)/Particles', 'Phys/[StdLoosePions](./stripping21r1p2-commonparticles-stdloosepions)/Particles'] |
| DaughtersCuts    | {'K+': '(P \> 2\*GeV)', 'pi+': '(P \> 2\*GeV)'}                                                                                                                          |
| CombinationCut   | ((AM\>1760.\*MeV) & (AM\<2080.\*MeV) & ((APT\>1.\*GeV) \| (ASUM(PT)\>1.\*GeV)) & (ADOCAMAX('')\<0.5\*mm))                                                                |
| MotherCut        | ((VFASPF(VCHI2) \< 30 ) & (M\>1770.\*MeV) & (M \< 2070.\*MeV) & (BPVVDCHI2\>36) & (BPVDIRA\>0.98))                                                                       |
| DecayDescriptor  | [D+ -\> K- K+ pi+]cc                                                                                                                                                   |
| DecayDescriptors | []                                                                                                                                                                     |
| Output           | None                                                                                                                                                                     |
