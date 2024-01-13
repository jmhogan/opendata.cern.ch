[[stripping21 lines]](./stripping21-index)

# StrippingDY2eeLine4

## Properties:

|                |                           |
|----------------|---------------------------|
| OutputLocation | Phys/DY2eeLine4/Particles |
| Postscale      | 1.0000000                 |
| HLT            | None                      |
| Prescale       | 1.0000000                 |
| L0DU           | None                      |
| ODIN           | None                      |

## Filter sequence:

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SelFilterPhys_StdAllNoPIDsElectrons_Particles

|      |                                                                                                            |
|------|------------------------------------------------------------------------------------------------------------|
| Code | CONTAINS('Phys/[StdAllNoPIDsElectrons](./stripping21-commonparticles-stdallnopidselectrons)/Particles')\>0 |

CombineParticles/DY2eeLine4

|                  |                                                                                                                                                                                                                                                                                                                                                                                     |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/[StdAllNoPIDsElectrons](./stripping21-commonparticles-stdallnopidselectrons)' ]                                                                                                                                                                                                                                                                                           |
| DaughtersCuts    | { '' : 'ALL' , 'e+' : '(P\>10.0\*GeV) &((PT\>5.0\*GeV) & (PPINFO(LHCb.ProtoParticle.CaloPrsE,0)\>50.0) & (PPINFO(LHCb.ProtoParticle.CaloEcalE,0)\>P\*0.1) & (PPINFO(LHCb.ProtoParticle.CaloHcalE,99999)10.0\*GeV) &((PT\>5.0\*GeV) & (PPINFO(LHCb.ProtoParticle.CaloPrsE,0)\>50.0) & (PPINFO(LHCb.ProtoParticle.CaloEcalE,0)\>P\*0.1) & (PPINFO(LHCb.ProtoParticle.CaloHcalE,99999) |
| CombinationCut   | ATRUE                                                                                                                                                                                                                                                                                                                                                                               |
| MotherCut        | (MM\>20.0\*GeV) & (MM\<40.0\*GeV)                                                                                                                                                                                                                                                                                                                                                   |
| DecayDescriptor  | Z0 -\> e+ e-                                                                                                                                                                                                                                                                                                                                                                        |
| DecayDescriptors | [ 'Z0 -\> e+ e-' ]                                                                                                                                                                                                                                                                                                                                                                |
| Output           | Phys/DY2eeLine4/Particles                                                                                                                                                                                                                                                                                                                                                           |
