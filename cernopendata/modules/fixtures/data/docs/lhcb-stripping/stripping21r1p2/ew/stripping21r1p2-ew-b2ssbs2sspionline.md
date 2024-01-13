[[stripping21r1p2 lines]](./stripping21r1p2-index)

# StrippingB2SSBs2SSPionLine

## Properties:

|                |                                  |
|----------------|----------------------------------|
| OutputLocation | Phys/B2SSBs2SSPionLine/Particles |
| Postscale      | 1.0000000                        |
| HLT1           | None                             |
| HLT2           | None                             |
| Prescale       | 1.0000000                        |
| L0DU           | None                             |
| ODIN           | None                             |

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

LoKi::VoidFilter/SELECT:Phys/StdAllLoosePions

|      |                                    |
|------|------------------------------------|
| Code | 0StdAllLoosePions/Particles',True) |

FilterDesktop/PionsForB2SS

|                 |                                                                                     |
|-----------------|-------------------------------------------------------------------------------------|
| Code            | ( PT \> 1500\*MeV)& ( MIPCHI2DV(PRIMARY)\> 64)                                      |
| Inputs          | [ 'Phys/[StdAllLoosePions](./stripping21r1p2-commonparticles-stdallloosepions)' ] |
| DecayDescriptor | None                                                                                |
| Output          | Phys/PionsForB2SS/Particles                                                         |

DaVinci::N4BodyDecays/B2SSBs2SSPionLine

|                  |                                                                                                                                                                          |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/PionsForB2SS' ]                                                                                                                                                |
| DaughtersCuts    | { '' : 'ALL' , 'pi+' : 'ALL' , 'pi-' : 'ALL' }                                                                                                                           |
| CombinationCut   | (AM\>4900\*MeV) & (AM\<5800\*MeV) & (( (abs(MYAM12-MYAM34)\< 25\*MeV) \| (abs(MYAM13-MYAM24)\< 25\*MeV) \| (abs(MYAM14-MYAM23)\< 25\*MeV) ))& ((AMAXDOCA('')\< 0.2\*mm)) |
| MotherCut        | (VFASPF(VCHI2/VDOF)\< 3)& (BPVDIRA \> 0)& (BPVVDCHI2\> 125)& (BPVIPCHI2()\< 10)                                                                                          |
| DecayDescriptor  | B_s0 -\> pi+ pi- pi+ pi-                                                                                                                                                 |
| DecayDescriptors | [ 'B_s0 -\> pi+ pi- pi+ pi-' ]                                                                                                                                         |
| Output           | Phys/B2SSBs2SSPionLine/Particles                                                                                                                                         |
