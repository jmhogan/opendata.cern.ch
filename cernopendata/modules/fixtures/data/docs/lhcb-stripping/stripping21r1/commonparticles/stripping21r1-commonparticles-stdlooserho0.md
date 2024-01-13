[[stripping21r1 lines]](./stripping21r1-index)

# StdLooseRho0

**CombineParticles/StdLooseRho0**

|                  |                                                                                     |
|------------------|-------------------------------------------------------------------------------------|
| Inputs           | ['Phys/[StdLoosePions](./stripping21r1-commonparticles-stdloosepions)/Particles'] |
| DaughtersCuts    | {}                                                                                  |
| CombinationCut   | (ADAMASS('rho(770)0')\<100\*MeV)& (ADOCACHI2CUT(15, ''))                            |
| MotherCut        | (BPVVDZ\>0) & (VFASPF(VCHI2)\<9) & (BPVDIRA\>0.95) & (BPVVDCHI2\>25)                |
| DecayDescriptor  | rho(770)0 -\> pi+ pi-                                                               |
| DecayDescriptors | []                                                                                |
| Output           | None                                                                                |
