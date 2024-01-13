[[stripping21r1p2 lines]](./stripping21r1p2-index)

# StrippingB2SSB2KstSSElectronDetLine

## Properties:

|                |                                           |
|----------------|-------------------------------------------|
| OutputLocation | Phys/B2SSB2KstSSElectronDetLine/Particles |
| Postscale      | 1.0000000                                 |
| HLT1           | None                                      |
| HLT2           | None                                      |
| Prescale       | 1.0000000                                 |
| L0DU           | None                                      |
| ODIN           | None                                      |

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

LoKi::VoidFilter/SELECT:Phys/StdLooseKstar2Kpi

|      |                                     |
|------|-------------------------------------|
| Code | 0StdLooseKstar2Kpi/Particles',True) |

FilterDesktop/KstarsForB2SS

|                 |                                                                                                                                                                                                                                                                            |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code            | ( PT \> 1250\*MeV)& ( MIPCHI2DV(PRIMARY)\> 55)& (PT \> 2000\*MeV )& (M \< ( 892\*MeV + 130\*MeV ) )& (M \> ( 892\*MeV - 130\*MeV ) )& (VFASPF(VCHI2/VDOF) \< 2.5 )& ( CHILD( MIPCHI2DV(PRIMARY), 1) \> 55 ) & ( CHILD( MIPCHI2DV(PRIMARY), 2) \> 55 ) & (BPVVDCHI2 \> 50 ) |
| Inputs          | [ 'Phys/[StdLooseKstar2Kpi](./stripping21r1p2-commonparticles-stdloosekstar2kpi)' ]                                                                                                                                                                                      |
| DecayDescriptor | None                                                                                                                                                                                                                                                                       |
| Output          | Phys/KstarsForB2SS/Particles                                                                                                                                                                                                                                               |

LoKi::VoidFilter/SELECT:Phys/StdAllLooseElectrons

|      |                                        |
|------|----------------------------------------|
| Code | 0StdAllLooseElectrons/Particles',True) |

FilterDesktop/ElectronsForB2SS

|                 |                                                                                             |
|-----------------|---------------------------------------------------------------------------------------------|
| Code            | ( PT \> 25\*MeV)& ( MIPCHI2DV(PRIMARY)\> 15)                                                |
| Inputs          | [ 'Phys/[StdAllLooseElectrons](./stripping21r1p2-commonparticles-stdalllooseelectrons)' ] |
| DecayDescriptor | None                                                                                        |
| Output          | Phys/ElectronsForB2SS/Particles                                                             |

CombineParticles/DetachedElectronPairForB2SS

|                  |                                                                  |
|------------------|------------------------------------------------------------------|
| Inputs           | [ 'Phys/ElectronsForB2SS' ]                                    |
| DaughtersCuts    | { '' : 'ALL' , 'e+' : 'ALL' , 'e-' : 'ALL' }                     |
| CombinationCut   | (AMAXDOCA('')\<0.5\*mm) &(ASUM(PT)\>50\*MeV)                     |
| MotherCut        | (VFASPF(VCHI2/VDOF)\< 16)& (BPVVDCHI2 \> 15)& (BPVIPCHI2()\> 10) |
| DecayDescriptor  | KS0 -\> e+ e-                                                    |
| DecayDescriptors | [ 'KS0 -\> e+ e-' ]                                            |
| Output           | Phys/DetachedElectronPairForB2SS/Particles                       |

CombineParticles/B2SSB2KstSSElectronDetLine

|                  |                                                                                       |
|------------------|---------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/DetachedElectronPairForB2SS' , 'Phys/KstarsForB2SS' ]                       |
| DaughtersCuts    | { '' : 'ALL' , 'K\*(892)0' : 'ALL' , 'K\*(892)~0' : 'ALL' , 'KS0' : 'ALL' }           |
| CombinationCut   | (ASUM(PT)\>3500\*MeV) & (AM\>4600\*MeV) & (AM\<6000\*MeV) & ( abs(MS1-MS2)\<60\*MeV ) |
| MotherCut        | (VFASPF(VCHI2/VDOF)\< 5)& (BPVDIRA \> 0.0)& (BPVVDCHI2\> 50)& (BPVIPCHI2()\< 15)      |
| DecayDescriptor  | [B0 -\> K\*(892)0 KS0 KS0]cc                                                        |
| DecayDescriptors | [ '[B0 -\> K\*(892)0 KS0 KS0]cc' ]                                                |
| Output           | Phys/B2SSB2KstSSElectronDetLine/Particles                                             |
