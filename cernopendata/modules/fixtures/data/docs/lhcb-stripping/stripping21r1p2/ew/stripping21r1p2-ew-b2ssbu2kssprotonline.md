[[stripping21r1p2 lines]](./stripping21r1p2-index)

# StrippingB2SSBu2KSSProtonLine

## Properties:

|                |                                     |
|----------------|-------------------------------------|
| OutputLocation | Phys/B2SSBu2KSSProtonLine/Particles |
| Postscale      | 1.0000000                           |
| HLT1           | None                                |
| HLT2           | None                                |
| Prescale       | 1.0000000                           |
| L0DU           | None                                |
| ODIN           | None                                |

## Filter sequence:

LoKi::VoidFilter/StrippingGoodEventConditionEW

|      |                                                                                      |
|------|--------------------------------------------------------------------------------------|
| Code | ALG_EXECUTED('StrippingStreamEWBadEvent') & ~ALG_PASSED('StrippingStreamEWBadEvent') |

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SELECT:Phys/StdAllLooseKaons

|      |                                    |
|------|------------------------------------|
| Code | 0StdAllLooseKaons/Particles',True) |

FilterDesktop/KaonsForB2SS

|                 |                                                                                     |
|-----------------|-------------------------------------------------------------------------------------|
| Code            | (PIDK \> 0) &( PT \> 1250\*MeV)& ( MIPCHI2DV(PRIMARY)\> 55)                         |
| Inputs          | [ 'Phys/[StdAllLooseKaons](./stripping21r1p2-commonparticles-stdallloosekaons)' ] |
| DecayDescriptor | None                                                                                |
| Output          | Phys/KaonsForB2SS/Particles                                                         |

LoKi::VoidFilter/SELECT:Phys/StdAllLooseProtons

|      |                                      |
|------|--------------------------------------|
| Code | 0StdAllLooseProtons/Particles',True) |

FilterDesktop/ProtonsForB2SS

|                 |                                                                                         |
|-----------------|-----------------------------------------------------------------------------------------|
| Code            | (PIDp \> 3.5) &( PT \> 1250\*MeV)& ( MIPCHI2DV(PRIMARY)\> 55)                           |
| Inputs          | [ 'Phys/[StdAllLooseProtons](./stripping21r1p2-commonparticles-stdalllooseprotons)' ] |
| DecayDescriptor | None                                                                                    |
| Output          | Phys/ProtonsForB2SS/Particles                                                           |

DaVinci::N5BodyDecays/B2SSBu2KSSProtonLine

|                  |                                                                                                                                                                              |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/KaonsForB2SS' , 'Phys/ProtonsForB2SS' ]                                                                                                                            |
| DaughtersCuts    | { '' : 'ALL' , 'K+' : 'ALL' , 'K-' : 'ALL' , 'p+' : 'ALL' , 'p~-' : 'ALL' }                                                                                                  |
| CombinationCut   | (AM\>4600\*MeV) & (AM\<6000\*MeV) & (( (abs(MYAM12-MYAM34)\< 100\*MeV) \| (abs(MYAM13-MYAM24)\< 100\*MeV) \| (abs(MYAM14-MYAM23)\< 100\*MeV) ))& ((AMAXDOCA('')\< 0.3\*mm) ) |
| MotherCut        | (VFASPF(VCHI2/VDOF)\< 9)& (BPVDIRA \> 0)& (BPVVDCHI2\> 100)& (BPVIPCHI2()\< 15)                                                                                              |
| DecayDescriptor  | [B+ -\> p+ p~- p+ p~- K+]cc                                                                                                                                                |
| DecayDescriptors | [ '[B+ -\> p+ p~- p+ p~- K+]cc' ]                                                                                                                                        |
| Output           | Phys/B2SSBu2KSSProtonLine/Particles                                                                                                                                          |
