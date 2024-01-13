[[stripping21r1p2 lines]](./stripping21r1p2-index)

# StrippingB2KX2MuMuSSDarkBosonLine

## Properties:

|                |                                         |
|----------------|-----------------------------------------|
| OutputLocation | Phys/B2KX2MuMuSSDarkBosonLine/Particles |
| Postscale      | 1.0000000                               |
| HLT1           | None                                    |
| HLT2           | None                                    |
| Prescale       | 0.10000000                              |
| L0DU           | None                                    |
| ODIN           | None                                    |

## Filter sequence:

LoKi::VoidFilter/StrippingGoodEventConditionLeptonic

|      |                                                                                                  |
|------|--------------------------------------------------------------------------------------------------|
| Code | ALG_EXECUTED('StrippingStreamLeptonicBadEvent') & ~ALG_PASSED('StrippingStreamLeptonicBadEvent') |

LoKi::VoidFilter/StrippingB2KX2MuMuSSDarkBosonLineVOIDFilter

|      |                                                                |
|------|----------------------------------------------------------------|
| Code | (recSummaryTrack(LHCb.RecSummary.nLongTracks, TrLONG) \< 250 ) |

CheckPV/checkPVmin1

|        |     |
|--------|-----|
| MinPVs | 1   |
| MaxPVs | -1  |

LoKi::VoidFilter/SELECT:Phys/StdAllLooseMuons

|      |                                    |
|------|------------------------------------|
| Code | 0StdAllLooseMuons/Particles',True) |

FilterDesktop/MuXDarkBosonFilter

|                 |                                                                                                                                                                                 |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code            | (NINGENERATION( (ID=='gamma') & ((PT \< 500\*MeV) \| (CL \< 0.3)),1)==0) & (TRGHP\<0.3) & (PIDmu\>-5) & (TRCHI2DOF\<3) & (P\>0\*MeV) & (MIPCHI2DV(PRIMARY)\>9) & (PT\>100\*MeV) |
| Inputs          | [ 'Phys/[StdAllLooseMuons](./stripping21r1p2-commonparticles-stdallloosemuons)' ]                                                                                             |
| DecayDescriptor | None                                                                                                                                                                            |
| Output          | Phys/MuXDarkBosonFilter/Particles                                                                                                                                               |

CombineParticles/X2MuMuSSDarkBosonSel

|                  |                                                                                       |
|------------------|---------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/MuXDarkBosonFilter' ]                                                       |
| DaughtersCuts    | { '' : 'ALL' , 'mu+' : 'ALL' , 'mu-' : 'ALL' }                                        |
| CombinationCut   | (AM \< 5000\*MeV) & (APT \> 250\*MeV) & (ACUTDOCA(0.2\*mm,''))& (ADOCACHI2CUT(25,'')) |
| MotherCut        | (BPVDIRA \> 0) & (BPVVDCHI2\>25) & (VFASPF(VCHI2/VDOF)\<10)                           |
| DecayDescriptor  | None                                                                                  |
| DecayDescriptors | [ '[KS0 -\> mu+ mu+]cc' ]                                                         |
| Output           | Phys/X2MuMuSSDarkBosonSel/Particles                                                   |

LoKi::VoidFilter/SELECT:Phys/StdAllNoPIDsKaons

|      |                                     |
|------|-------------------------------------|
| Code | 0StdAllNoPIDsKaons/Particles',True) |

FilterDesktop/KBDarkBosonFilter

|                 |                                                                                                                                                                                       |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Code            | (NINGENERATION( (ID=='gamma') & ((PT \< 500\*MeV) \| (CL \< 0.3)),1)==0) & (PROBNNK\>0.1) & (TRGHP\<0.3) & (TRCHI2DOF\<3) & (P\>2000\*MeV) & (MIPCHI2DV(PRIMARY)\>9) & (PT\>250\*MeV) |
| Inputs          | [ 'Phys/[StdAllNoPIDsKaons](./stripping21r1p2-commonparticles-stdallnopidskaons)' ]                                                                                                 |
| DecayDescriptor | None                                                                                                                                                                                  |
| Output          | Phys/KBDarkBosonFilter/Particles                                                                                                                                                      |

CombineParticles/B2KX2MuMuSSDarkBosonLine

|                  |                                                                                                                                                                                                                        |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inputs           | [ 'Phys/KBDarkBosonFilter' , 'Phys/X2MuMuSSDarkBosonSel' ]                                                                                                                                                           |
| DaughtersCuts    | { '' : 'ALL' , 'K+' : 'ALL' , 'K-' : 'ALL' , 'KS0' : 'ALL' }                                                                                                                                                           |
| CombinationCut   | (AM\>4800\*MeV) & (AM\<5800\*MeV) & (ASUM(SUMTREE(PT,(ISBASIC \| (ID=='gamma')),0.0))\>0\*MeV)                                                                                                                         |
| MotherCut        | (PT\>800\*MeV) & (VFASPF(VCHI2/VDOF)\<15) & (BPVLTIME()\>0.2\*ps) & (BPVIPCHI2()\<10) & (BPVDIRA \> 0) & (NINGENERATION(ISBASIC & HASTRACK & (MIPCHI2DV(PRIMARY) \< 25),1)==0) & (MM \> 4800\*MeV) & (MM \< 5800\*MeV) |
| DecayDescriptor  | None                                                                                                                                                                                                                   |
| DecayDescriptors | [ '[B+ -\> K+ KS0]cc' ]                                                                                                                                                                                            |
| Output           | Phys/B2KX2MuMuSSDarkBosonLine/Particles                                                                                                                                                                                |

AddRelatedInfo/RelatedInfo1_B2KX2MuMuSSDarkBosonLine

|                 |                                                      |
|-----------------|------------------------------------------------------|
| Inputs          | [ 'Phys/B2KX2MuMuSSDarkBosonLine' ]                |
| DecayDescriptor | None                                                 |
| Output          | Phys/RelatedInfo1_B2KX2MuMuSSDarkBosonLine/Particles |

AddRelatedInfo/RelatedInfo2_B2KX2MuMuSSDarkBosonLine

|                 |                                                      |
|-----------------|------------------------------------------------------|
| Inputs          | [ 'Phys/B2KX2MuMuSSDarkBosonLine' ]                |
| DecayDescriptor | None                                                 |
| Output          | Phys/RelatedInfo2_B2KX2MuMuSSDarkBosonLine/Particles |

AddRelatedInfo/RelatedInfo3_B2KX2MuMuSSDarkBosonLine

|                 |                                                      |
|-----------------|------------------------------------------------------|
| Inputs          | [ 'Phys/B2KX2MuMuSSDarkBosonLine' ]                |
| DecayDescriptor | None                                                 |
| Output          | Phys/RelatedInfo3_B2KX2MuMuSSDarkBosonLine/Particles |

AddRelatedInfo/RelatedInfo4_B2KX2MuMuSSDarkBosonLine

|                 |                                                      |
|-----------------|------------------------------------------------------|
| Inputs          | [ 'Phys/B2KX2MuMuSSDarkBosonLine' ]                |
| DecayDescriptor | None                                                 |
| Output          | Phys/RelatedInfo4_B2KX2MuMuSSDarkBosonLine/Particles |

AddRelatedInfo/RelatedInfo5_B2KX2MuMuSSDarkBosonLine

|                 |                                                      |
|-----------------|------------------------------------------------------|
| Inputs          | [ 'Phys/B2KX2MuMuSSDarkBosonLine' ]                |
| DecayDescriptor | None                                                 |
| Output          | Phys/RelatedInfo5_B2KX2MuMuSSDarkBosonLine/Particles |

AddRelatedInfo/RelatedInfo6_B2KX2MuMuSSDarkBosonLine

|                 |                                                      |
|-----------------|------------------------------------------------------|
| Inputs          | [ 'Phys/B2KX2MuMuSSDarkBosonLine' ]                |
| DecayDescriptor | None                                                 |
| Output          | Phys/RelatedInfo6_B2KX2MuMuSSDarkBosonLine/Particles |
