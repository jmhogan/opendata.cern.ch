[[stripping21r1p2 lines]](./stripping21r1p2-index)

# StdLooseDetachedTau3piNonPhys

**CombineParticles/StdLooseDetachedTau3piNonPhys**

|                  |                                                                                                                                                      |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | ['Phys/[StdLoosePions](./stripping21r1p2-commonparticles-stdloosepions)/Particles']                                                                |
| DaughtersCuts    | {'pi+': '(PT\>150.\*MeV) & (MIPCHI2DV(PRIMARY) \> 4.0) & (TRCHI2DOF\<4) & (TRGHOSTPROB\<0.4) & (PIDK \< 8)'}                                         |
| CombinationCut   | ((AM\>400.\*MeV) & (AM\<3500.\*MeV)) & (ADOCAMAX('')\<0.15\*mm) & ((AM12\<1670.\*MeV) or (AM23\<1670.\*MeV)) & (ANUM(PT \< 300\*MeV) \<= 1) & (15))) |
| MotherCut        | (M\>400.\*MeV) & (M \< 3500.\*MeV) & (BPVDIRA\>0.99) & (VFASPF(VCHI2) \< 25 )                                                                        |
| DecayDescriptor  | None                                                                                                                                                 |
| DecayDescriptors | ['[tau+ -\> pi+ pi+ pi+]cc']                                                                                                                     |
| Output           | None                                                                                                                                                 |
