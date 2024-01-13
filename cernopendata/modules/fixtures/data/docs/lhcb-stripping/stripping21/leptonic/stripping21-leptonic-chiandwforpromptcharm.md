[[stripping21 lines]](./stripping21-index)

# StrippingChiAndWForPromptCharm

## Properties:

|                |                                      |
|----------------|--------------------------------------|
| OutputLocation | Phys/ChiAndWForPromptCharm/Particles |
| Postscale      | 1.0000000                            |
| HLT            | None                                 |
| Prescale       | 1.0000000                            |
| L0DU           | None                                 |
| ODIN           | None                                 |

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

FilterDesktop/SelWForPromptCharm

|                 |                                                                                                 |
|-----------------|-------------------------------------------------------------------------------------------------|
| Code            | ( 'mu+'== ABSID ) & ( PT \> 15 \* GeV ) & ( -100 \* GeV \< ptCone ) & ( -100 \* GeV \< etCone ) |
| Inputs          | [ 'Phys/[StdAllLooseMuons](./stripping21-commonparticles-stdallloosemuons)' ]                 |
| DecayDescriptor | None                                                                                            |
| Output          | Phys/SelWForPromptCharm/Particles                                                               |

FilterDesktop/SelMuonForPromptCharm

|                 |                                                                                                             |
|-----------------|-------------------------------------------------------------------------------------------------------------|
| Code            | ISMUON & in_range ( 2 , ETA , 4.9 ) & ( PT \> 550 \* MeV ) & ( PIDmu - PIDpi \> 0 ) & ( CLONEDIST \> 5000 ) |
| Inputs          | [ 'Phys/[StdAllLooseMuons](./stripping21-commonparticles-stdallloosemuons)' ]                             |
| DecayDescriptor | None                                                                                                        |
| Output          | Phys/SelMuonForPromptCharm/Particles                                                                        |

CombineParticles/SelDiMuonForPromptCharm

|                  |                                                |
|------------------|------------------------------------------------|
| Inputs           | [ 'Phys/SelMuonForPromptCharm' ]             |
| DaughtersCuts    | { '' : 'ALL' , 'mu+' : 'ALL' , 'mu-' : 'ALL' } |
| CombinationCut   | psi \| psi_prime \| ( AM \> 8 \* GeV )         |
| MotherCut        | chi2vx \< 20                                   |
| DecayDescriptor  | J/psi(1S) -\> mu+ mu-                          |
| DecayDescriptors | [ 'J/psi(1S) -\> mu+ mu-' ]                  |
| Output           | Phys/SelDiMuonForPromptCharm/Particles         |

CombineParticles/SelDiMuonAndWForPromptCharm

|                  |                                                                      |
|------------------|----------------------------------------------------------------------|
| Inputs           | [ 'Phys/SelDiMuonForPromptCharm' , 'Phys/SelWForPromptCharm' ]     |
| DaughtersCuts    | { '' : 'ALL' , 'J/psi(1S)' : 'ALL' , 'mu+' : 'ALL' , 'mu-' : 'ALL' } |
| CombinationCut   | AALL                                                                 |
| MotherCut        | ALL                                                                  |
| DecayDescriptor  | None                                                                 |
| DecayDescriptors | [ ' [ chi_b0(2P) -\> J/psi(1S) mu+ ]cc ' ]                       |
| Output           | Phys/SelDiMuonAndWForPromptCharm/Particles                           |

LoKi::VoidFilter/SelFilterPhys_StdLooseAllPhotons_Particles

|      |                                                                                                      |
|------|------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdLooseAllPhotons](./stripping21-commonparticles-stdlooseallphotons)/Particles')\>0 |

DaVinci::N3BodyDecays/SelPreChiAndWForPromptCharm

|                  |                                                                                                                                                                                            |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/SelDiMuonAndWForPromptCharm' , 'Phys/SelDiMuonForPromptCharm' , 'Phys/SelWForPromptCharm' , 'Phys/[StdLooseAllPhotons](./stripping21-commonparticles-stdlooseallphotons)' ]      |
| DaughtersCuts    | { '' : 'ALL' , 'J/psi(1S)' : ' ( M \< 3.21 \* GeV ) \| in_range ( 8.5 \* GeV , M , 12.0 \* GeV ) ' , 'gamma' : ' ( PT \> 400 \* MeV ) & ( CL \> 0.05 ) ' , 'mu+' : 'ALL' , 'mu-' : 'ALL' } |
| CombinationCut   | AM13 - AM1 \< 1.01 \* GeV                                                                                                                                                                  |
| MotherCut        | ALL                                                                                                                                                                                        |
| DecayDescriptor  | [ chi_b1(2P) -\> J/psi(1S) mu+ gamma ]cc                                                                                                                                                 |
| DecayDescriptors | [ '[ chi_b1(2P) -\> J/psi(1S) mu+ gamma ]cc' ]                                                                                                                                         |
| Output           | Phys/SelPreChiAndWForPromptCharm/Particles                                                                                                                                                 |

Pi0Veto::Tagger/ChiAndWForPromptCharm

|                 |                                          |
|-----------------|------------------------------------------|
| Code            | "gamma" == ID                            |
| Inputs          | [ 'Phys/SelPreChiAndWForPromptCharm' ] |
| DecayDescriptor | None                                     |
| Output          | Phys/ChiAndWForPromptCharm/Particles     |
