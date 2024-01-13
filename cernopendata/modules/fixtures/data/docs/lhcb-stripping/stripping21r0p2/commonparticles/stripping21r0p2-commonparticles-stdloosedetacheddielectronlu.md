[[stripping21r0p2 lines]](./stripping21r0p2-index)

# StdLooseDetachedDiElectronLU

**CombineParticles/StdLooseDetachedDiElectronLU**

|                  |                                                                                                                                                                                                      |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | ['Phys/[StdAllLooseElectrons](./stripping21r0p2-commonparticles-stdalllooseelectrons)/Particles', 'Phys/[StdNoPIDsUpElectrons](./stripping21r0p2-commonparticles-stdnopidsupelectrons)/Particles'] |
| DaughtersCuts    | {'e+': '(PT\>250\*MeV) & (MIPCHI2DV(PRIMARY) \> 4)'}                                                                                                                                                 |
| CombinationCut   | (AM\>30\*MeV) & (ADOCACHI2CUT(30,''))                                                                                                                                                                |
| MotherCut        | (VFASPF(VCHI2)\<25)                                                                                                                                                                                  |
| DecayDescriptor  | J/psi(1S) -\> e+ e-                                                                                                                                                                                  |
| DecayDescriptors | []                                                                                                                                                                                                 |
| Output           | None                                                                                                                                                                                                 |
