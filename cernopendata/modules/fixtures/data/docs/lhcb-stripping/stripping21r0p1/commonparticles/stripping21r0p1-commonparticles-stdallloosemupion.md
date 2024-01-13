[[stripping21r0p1 lines]](./stripping21r0p1-index)

# StdAllLooseMuPion

**CombineParticles/StdAllLooseMuPion**

|                  |                                                                                                                                                                                      |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | ['Phys/[StdAllLooseMuons](./stripping21r0p1-commonparticles-stdallloosemuons)/Particles', 'Phys/[StdAllLoosePions](./stripping21r0p1-commonparticles-stdallloosepions)/Particles'] |
| DaughtersCuts    | {'pi-': '(PT\>200\*MeV) & (MIPCHI2DV(PRIMARY)\>0.)', 'mu+': '(PT\>200\*MeV) & (MIPCHI2DV(PRIMARY)\>0.)'}                                                                             |
| CombinationCut   | (ADOCACHI2CUT(30,''))                                                                                                                                                                |
| MotherCut        | (VFASPF(VCHI2)\<25)                                                                                                                                                                  |
| DecayDescriptor  | rho(770)0 -\> mu+ pi-                                                                                                                                                                |
| DecayDescriptors | []                                                                                                                                                                                 |
| Output           | None                                                                                                                                                                                 |
