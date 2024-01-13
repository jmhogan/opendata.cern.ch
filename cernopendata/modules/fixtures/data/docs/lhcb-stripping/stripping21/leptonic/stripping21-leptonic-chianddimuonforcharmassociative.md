[[stripping21 lines]](./stripping21-index)

# StrippingChiAndDiMuonForCharmAssociative

## Properties:

|                |                                                |
|----------------|------------------------------------------------|
| OutputLocation | Phys/ChiAndDiMuonForCharmAssociative/Particles |
| Postscale      | 1.0000000                                      |
| HLT            | None                                           |
| Prescale       | 1.0000000                                      |
| L0DU           | None                                           |
| ODIN           | None                                           |

## Filter sequence:

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SelFilterPhys_StdAllLooseMuons_Particles

|      |                                                                                                  |
|------|--------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdAllLooseMuons](./stripping21-commonparticles-stdallloosemuons)/Particles')\>0 |

CombineParticles/SelDiMuonForCharmAssociative

|                  |                                                                                                                                                  |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/[StdAllLooseMuons](./stripping21-commonparticles-stdallloosemuons)' ]                                                                  |
| DaughtersCuts    | { '' : 'ALL' , 'mu+' : ' ISMUON & ( PT \> 650 \* MeV ) & ( TRCHI2DOF \< 5 ) ' , 'mu-' : ' ISMUON & ( PT \> 650 \* MeV ) & ( TRCHI2DOF \< 5 ) ' } |
| CombinationCut   | psi \| psi_prime \| ( 8 \* GeV \< AM )                                                                                                           |
| MotherCut        | chi2vx \< 20                                                                                                                                     |
| DecayDescriptor  | J/psi(1S) -\> mu+ mu-                                                                                                                            |
| DecayDescriptors | [ 'J/psi(1S) -\> mu+ mu-' ]                                                                                                                    |
| Output           | Phys/SelDiMuonForCharmAssociative/Particles                                                                                                      |

CombineParticles/SelDoubleDiMuonForCharmAssociative

|                  |                                                   |
|------------------|---------------------------------------------------|
| Inputs           | [ 'Phys/SelDiMuonForCharmAssociative' ]         |
| DaughtersCuts    | { '' : 'ALL' , 'J/psi(1S)' : 'ALL' }              |
| CombinationCut   | AALL                                              |
| MotherCut        | ALL                                               |
| DecayDescriptor  | chi_b2(1P) -\> J/psi(1S) J/psi(1S)                |
| DecayDescriptors | [ 'chi_b2(1P) -\> J/psi(1S) J/psi(1S)' ]        |
| Output           | Phys/SelDoubleDiMuonForCharmAssociative/Particles |

LoKi::VoidFilter/SelFilterPhys_StdLooseAllPhotons_Particles

|      |                                                                                                      |
|------|------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseAllPhotons](./stripping21-commonparticles-stdlooseallphotons)/Particles')\>0 |

CombineParticles/SelPreChiAndDiMuonForCharmAssociative

|                  |                                                                                                                                                                       |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/SelDiMuonForCharmAssociative' , 'Phys/SelDoubleDiMuonForCharmAssociative' , 'Phys/[StdLooseAllPhotons](./stripping21-commonparticles-stdlooseallphotons)' ] |
| DaughtersCuts    | { '' : 'ALL' , 'J/psi(1S)' : 'ALL' , 'gamma' : ' ( PT \> 400 \* MeV ) & ( CL \> 0.05 ) ' }                                                                            |
| CombinationCut   | ( AM13 - AM1 \< 1.05 \* GeV ) \| ( AM23 - AM2 \< 1.05 \* GeV )                                                                                                        |
| MotherCut        | ALL                                                                                                                                                                   |
| DecayDescriptor  | chi_b2(1P) -\> J/psi(1S) J/psi(1S) gamma                                                                                                                              |
| DecayDescriptors | [ 'chi_b2(1P) -\> J/psi(1S) J/psi(1S) gamma ' ]                                                                                                                     |
| Output           | Phys/SelPreChiAndDiMuonForCharmAssociative/Particles                                                                                                                  |

Pi0Veto::Tagger/ChiAndDiMuonForCharmAssociative

|                 |                                                    |
|-----------------|----------------------------------------------------|
| Code            | "gamma" == ID                                      |
| Inputs          | [ 'Phys/SelPreChiAndDiMuonForCharmAssociative' ] |
| DecayDescriptor | None                                               |
| Output          | Phys/ChiAndDiMuonForCharmAssociative/Particles     |
