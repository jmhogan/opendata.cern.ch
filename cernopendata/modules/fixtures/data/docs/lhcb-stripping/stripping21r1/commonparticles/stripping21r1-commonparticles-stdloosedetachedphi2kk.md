[[stripping21r1 lines]](./stripping21r1-index)

# StdLooseDetachedPhi2KK

**CombineParticles/StdLooseDetachedPhi2KK**

|                  |                                                                                     |
|------------------|-------------------------------------------------------------------------------------|
| Inputs           | ['Phys/[StdLooseKaons](./stripping21r1-commonparticles-stdloosekaons)/Particles'] |
| DaughtersCuts    | {'K+': '(MIPCHI2DV(PRIMARY) \> 4.)'}                                                |
| CombinationCut   | (AM \< 1100.\*MeV) & (ADOCACHI2CUT(30,''))                                          |
| MotherCut        | (VFASPF(VCHI2) \< 25.0)                                                             |
| DecayDescriptor  | phi(1020) -\> K+ K-                                                                 |
| DecayDescriptors | []                                                                                |
| Output           | None                                                                                |
