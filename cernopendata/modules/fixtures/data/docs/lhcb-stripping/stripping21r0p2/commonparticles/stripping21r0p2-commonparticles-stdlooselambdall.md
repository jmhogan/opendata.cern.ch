[[stripping21r0p2 lines]](./stripping21r0p2-index)

# StdLooseLambdaLL

**CombineParticles/StdLooseLambdaLL**

|                  |                                                                                                                                                                              |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | ['Phys/[StdLoosePions](./stripping21r0p2-commonparticles-stdloosepions)/Particles', 'Phys/[StdLooseProtons](./stripping21r0p2-commonparticles-stdlooseprotons)/Particles'] |
| DaughtersCuts    | {'p+': '(P\>2\*GeV) & (MIPCHI2DV(PRIMARY)\>9)', 'pi+': '(P\>2\*GeV) & (MIPCHI2DV(PRIMARY)\>9)'}                                                                              |
| CombinationCut   | (ADAMASS('Lambda0')\<50\*MeV) & (ADOCACHI2CUT(30, ''))                                                                                                                       |
| MotherCut        | (ADMASS('Lambda0')\<35\*MeV) & (VFASPF(VCHI2)\<30)                                                                                                                           |
| DecayDescriptor  | [Lambda0 -\> p+ pi-]cc                                                                                                                                                     |
| DecayDescriptors | []                                                                                                                                                                         |
| Output           | None                                                                                                                                                                         |
