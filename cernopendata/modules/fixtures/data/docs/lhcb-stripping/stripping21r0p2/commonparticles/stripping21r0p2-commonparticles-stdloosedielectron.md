[[stripping21r0p2 lines]](./stripping21r0p2-index)

# StdLooseDiElectron

**CombineParticles/StdLooseDiElectron**

|                  |                                                                                                     |
|------------------|-----------------------------------------------------------------------------------------------------|
| Inputs           | ['Phys/[StdAllLooseElectrons](./stripping21r0p2-commonparticles-stdalllooseelectrons)/Particles'] |
| DaughtersCuts    | {'e+': '(PT\>500\*MeV)'}                                                                            |
| CombinationCut   | (AM\>30\*MeV) & (ADOCACHI2CUT(30,''))                                                               |
| MotherCut        | (VFASPF(VCHI2)\<25)                                                                                 |
| DecayDescriptor  | J/psi(1S) -\> e+ e-                                                                                 |
| DecayDescriptors | []                                                                                                |
| Output           | None                                                                                                |
