[[stripping21 lines]](./stripping21-index)

# StdLooseDetachedTau3pi

**CombineParticles/StdLooseDetachedTau3pi**

|                  |                                                                                                                                                                                                                          |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | ['Phys/[StdLoosePions](./stripping21-commonparticles-stdloosepions)/Particles']                                                                                                                                        |
| DaughtersCuts    | {'pi+': '(PT\>150.\*MeV) & (MIPCHI2DV(PRIMARY) \> 4.0) & (TRCHI2DOF\<3) & (TRGHOSTPROB\<0.4) & (PIDK \< 8)', 'pi-': '(PT\>150.\*MeV) & (MIPCHI2DV(PRIMARY) \> 4.0) & (TRCHI2DOF\<3) & (TRGHOSTPROB\<0.4) & (PIDK \< 8)'} |
| CombinationCut   | ((AM\>400.\*MeV) & (AM\<3500.\*MeV)) & (ADOCAMAX('')\<0.15\*mm) & ((AM12\<1670.\*MeV) or (AM23\<1670.\*MeV)) & (ANUM(PT \< 300\*MeV) \<= 1) & (1\<ANUM( ('pi+'==ABSID) & (MIPCHI2DV(PRIMARY)\>5)))                       |
| MotherCut        | (M\>400.\*MeV) & (M \< 3500.\*MeV) & (BPVDIRA\>0.99) & (VFASPF(VCHI2) \< 25 )                                                                                                                                            |
| DecayDescriptor  | None                                                                                                                                                                                                                     |
| DecayDescriptors | ['[tau+ -\> pi+ pi- pi+]cc']                                                                                                                                                                                         |
| Output           | None                                                                                                                                                                                                                     |
