[[stripping21r0p1 lines]](./stripping21r0p1-index)

# StdLooseKsLL

**CombineParticles/StdLooseKsLL**

|                  |                                                                                       |
|------------------|---------------------------------------------------------------------------------------|
| Inputs           | ['Phys/[StdLoosePions](./stripping21r0p1-commonparticles-stdloosepions)/Particles'] |
| DaughtersCuts    | {'pi+': '(P \> 2.\*GeV) & (MIPCHI2DV(PRIMARY) \> 9.)'}                                |
| CombinationCut   | (ADAMASS('KS0') \< 50.\*MeV) & (ADOCACHI2CUT(25, ''))                                 |
| MotherCut        | (ADMASS('KS0') \< 35.\*MeV) & (VFASPF(VCHI2) \< 25.)                                  |
| DecayDescriptor  | KS0 -\> pi+ pi-                                                                       |
| DecayDescriptors | []                                                                                  |
| Output           | None                                                                                  |
