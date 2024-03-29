# Molecular Laboratory 4
>The protocols we will follow for ddRADseq are based on those of Peterson et al. ([2012](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0037135)). Minor modifications of the protocol correspond to this paper: Streicher et al. ([2014](https://onlinelibrary.wiley.com/doi/abs/10.1111/mec.12814)). 

## Experimental design and sample organization

<details>
  <summary>Click to expand protocol!</summary>

>ddRADseq makes use of dual indexes (=barcodes), so we need to plan ahead for how we will process samples. The first barcode is added during the ligation step of the library construction, and the second is added during PCR amplification of the libraries. As such, we can use the same core set of adapters for a small number of individuals, and then use PCR-barcode to greatly increase the number of individuals that can be mulitplexed.  
  
**Materials**

* List of samples to be included in the final pooled RADseq library
* Spreadsheet software


**Protocol**
1. Here is an example from Streicher et al. ([2014](https://onlinelibrary.wiley.com/doi/abs/10.1111/mec.12814)) for how we set up the barcode design. We had 10 unique ddRADseq adapter barcodes and multiple PCR-barcodes. We wanted to include 50 different anurans in the study, so we organised things into five sets of 10, each with a unique PCR barcode.   

Library Pool 1:
  
Sample ID | Adapter Index/Barcode | PCR Index/Barcode
------------ | -------------  | -------------
JAC 23544 | Index 1 (ACTAGG) | Index 1 (ATCACG)
JAC 23564 | Index 2 (GACCAA) | Index 1 (ATCACG)
JAC 29189 | Index 3 (TGTTGG)  | Index 1 (ATCACG)
JAC 23344 | Index 4 (CGAAAC)  | Index 1 (ATCACG)
JAC 23345 | Index 5 (AGCATT) | Index 1 (ATCACG)  
JAC 23346 | Index 6 (CATCTC) | Index 1 (ATCACG)  
JAC 23347 | Index 7 (GTCTAT) | Index 1 (ATCACG)   
JRM 4651 |Index 8 (TGGGAT) | Index 1 (ATCACG)
JHM 1 | Index 9 (TCTGCT) | Index 1 (ATCACG)  
JAC 28298 | Index 10 (AACGGT)  | Index 1 (ATCACG)   
 
Library Pool 2:  

Sample ID | Adapter Index/Barcode | PCR Index/Barcode
------------ | -------------  | -------------
JAC 30108 | Index 1 (ACTAGG) | Index 2 (CGATGT)
JAC 30105 | Index 2 (GACCAA) | Index 2 (CGATGT)
JWS 253 | Index 3 (TGTTGG)  | Index 2 (CGATGT)
JWS 277 | Index 4 (CGAAAC)  | Index 2 (CGATGT)
JWS 292 | Index 5 (AGCATT) | Index 2 (CGATGT) 
JWS 295 | Index 6 (CATCTC) | Index 2 (CGATGT)  
JWS 284 | Index 7 (GTCTAT) | Index 2 (CGATGT)   
JWS 296 |Index 8 (TGGGAT) | Index 2 (CGATGT)
JWS 294 | Index 9 (TCTGCT) | Index 2 (CGATGT)  
JMM 151 | Index 10 (AACGGT)  | Index 2 (CGATGT)   
  
Library Pool 3:  
  
Sample ID | Adapter Index/Barcode | PCR Index/Barcode
------------ | -------------  | -------------
JMM 152 | Index 1 (ACTAGG) | Index 3 (TTAGGC)
TJD 770 | Index 2 (GACCAA) | Index 3 (TTAGGC)
TJD 777 | Index 3 (TGTTGG)  | Index 3 (TTAGGC)
TJD 830 | Index 4 (CGAAAC)  | Index 3 (TTAGGC)
TJD 847 | Index 5 (AGCATT) | Index 3 (TTAGGC)
TJD 877 | Index 6 (CATCTC) | Index 3 (TTAGGC)  
BF 36 | Index 7 (GTCTAT) | Index 3 (TTAGGC))   
BF 58 |Index 8 (TGGGAT) | Index 3 (TTAGGC))
BF 45 | Index 9 (TCTGCT) | Index 3 (TTAGGC)  
BF 53 | Index 10 (AACGGT)  | Index 3 (TTAGGC)     
  
Library Pool 4:  

Sample ID | Adapter Index/Barcode | PCR Index/Barcode
------------ | -------------  | -------------
BF 55 | Index 1 (ACTAGG) | Index 4 (TGACCA)
BF 81 | Index 2 (GACCAA) | Index 4 (TGACCA)
BF 82 | Index 3 (TGTTGG)  | Index 4 (TGACCA)
BF 86 | Index 4 (CGAAAC)  | Index 4 (TGACCA)
BF 88 | Index 5 (AGCATT) | Index 4 (TGACCA)
BF Kitt Peak | Index 6 (CATCTC) | Index 4 (TGACCA) 
MF 3806 | Index 7 (GTCTAT) | Index 4 (TGACCA)  
MF 3811 |Index 8 (TGGGAT) | Index 4 (TGACCA)
MF 4226 | Index 9 (TCTGCT) | Index 4 (TGACCA)  
MF 4395 | Index 10 (AACGGT)  | Index 4 (TGACCA)    
  
Library Pool 5:
  
Sample ID | Adapter Index/Barcode | PCR Index/Barcode
------------ | -------------  | -------------
MF 4398 | Index 1 (ACTAGG) | Index 5 (ACAGTG)
MF 5085 | Index 2 (GACCAA) | Index 5 (ACAGTG)
MF 6101 | Index 3 (TGTTGG)  | Index 5 (ACAGTG)
MF 6115 | Index 4 (CGAAAC)  | Index 5 (ACAGTG)
MF 6203 | Index 5 (AGCATT) | Index 5 (ACAGTG)
MF 6205 | Index 6 (CATCTC) | Index 5 (ACAGTG)
MVZ 226838 | Index 7 (GTCTAT) | Index 5 (ACAGTG) 
MVZ 226839 |Index 8 (TGGGAT) | Index 5 (ACAGTG)
JAC 30517 | Index 9 (TCTGCT) | Index 5 (ACAGTG)  
ENS 9494 | Index 10 (AACGGT)  | Index 5 (ACAGTG)   

2. This allowed us to ultimately pool together all 50 samples and then bioinformatically sort the data once it was returned from the Illumina.  

</details>

## Quantification of double-stranded DNA (dsDNA)  

<details>
  <summary>Click to expand protocol!</summary>

>Here we will quantify DNA extracts using a fluorometer. This is important because only double-stranded DNAs will be used in the NGS library preparations. 

**Materials**
  
* Extracted DNA from ten samples  
* Qubit HS dsDNA reagent kit
  * HS Buffer
  * Fluorecent Dye
  * HS Standard 1
  * HS Standard 2
* Qubit fluorometer
* Crystal-clear Axygen microcentrifuge tubes

**Protocol**  
>This protocol is written for use with 1 uL of DNA extract. For samples that are likely to have very little dsDNA, it can be modified so that more template is used. 

1. First we need to make a Master Mix from the Qubit reagents. For each sample (+ the two size standards) we need to combine 1 uL of Dye with 199 uL of buffer. 
>In our case this means we add 12 uL of dye with 2370 uL of buffer

2. Add 190 uL of Master Mix to two Axygen tubes (these will be used for the Size Standard DNA).

3. Add 10 uL of HS Standard 1 to the first Axygen tube.
  
4. Add 10 uL of HS Standard 2 to the second Axygen tube. 
  
5. Add 199 uL of Master Mix to ten Axygen tubes (these will be used for the sample DNA).
  
6. To each of the ten sample tubes, add 1 uL of your DNA extract from each sample. 
>At this point, you should have seven tubes, each with 200 uL of liquid in them (two size standards and ten samples). 

7. Vortex each of the tubes and then spin down using a lab bench mini-centrifuge. Allow to sit at room temperature for 5 mins. 
  
8. Turn on the Qubit fluorometer. Select the appropriate assay kit from the home menu. 
  
9. Follow the instructions for inserting the size standards. 
  
10. Once calibrated, conduct a reading on each of the DNA extract samples and note the concentrations (in ng/uL) 
>Note: In order to get the concentrations in ng/uL format, you may need to modify the units on the Qubit fluorometer. 
  
11. These concentrations will be used to determine how many uL of DNA extract we use for the start of our library preparation protocol in the next module. 

12. Discard the used Axygen tubes at the end of the laboratory session. 
  
</details>

## Determining size and quality of DNA extractions with gel electrophoresis

<details>
  <summary>Click to expand protocol!</summary>

**Materials**
  
* Agarose
* 1X TAE Buffer
* Scale
* Microwave
* Electrophoresis rig with power source
* DNA Ladder (for testing beads)
* Gel loading dye
* Gel stain (e.g. SYBR safe)
* Parafilm

  
**Protocol**
  
1. Prepare a 1% TAE gel for electrophoresis. At the NHM, we can use a small gel casting frame which will require:
      * 0.75 g Agarose
      * 75 mL 1X TAE Buffer
      * 4 uL of SYBR safe or Gel Red DNA stain

2. Mix the Agarose and TAE Buffer in a glass flask. Microwave the flask until the the Agarose goes into solution (Don't let the flask boil over!)
  
3. Use hot pads to remove the flask from the microwave and allow to cool on the lab bench until you can safely touch the glass. Add the SYBR safe stain to the flask using a pipetter. Mix gently by hand.  

4. Carefully pour the solution into the casting tray and allow to solidify (usually ~20-30 mins)
>This will create the gel needed to view the DNA extractions

5. Mix 2 uL of loading dye with 5 uL of DNA extraction on a piece of parafilm.  
  
6. In the first well of the gel, oad 4 uL of pre-mixed ladder. Then load the 7 uL of DNA extraction + loading dye into your gel (which should now be placed in the Electrophoresis Rig) and run using the Power Source.   
  
>If the DNA extractions are high weight we should single bands above the largest ladder fragment, however, some shearing (=smear) is fine and we can still process with the ddRADseq protocol.   


</details>

## Restriction digestion of genomic DNA

<details>
  <summary>Click to expand protocol!</summary>

**Materials**

* Cut-smart buffer (NEB)
* SbFI-HF (NEB)
* Msp-I (NEB)
* Extracted DNA from samples 
* Nuclease-free water
* Magnetic tube rack


**Protocol**
  
1. Using fresh DNA extractions, we are now going to prepare the DNA for ddRADseq library construction. First, we need to prepare 200 ng from the example DNA extractions and then adjust the volumes with water so that all samples have 50 uL for the fragmentation step. I use a spreadsheet with four columns, similar to the method introduced in [Unit 2](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_02/Molecular_Lab), to do this: 
  
Sample ID | Qubit concentration (ng/uL)  | uL needed for 200 ng | uL of water to add
------------ | -------------  | ------------- | -------------
Sample 1 | 10.0 | 20.0  | 30.0
Sample 2 | 18.5  | 10.8 | 39.2
Sample 3 | 33.2  | 6.0 | 44.0
Sample 4 | 80.0  | 2.5  | 47.5  
 
> The third column is 200 divided by the second column value and the fourth column is 50 minus the third column value
  
 2. For each digestion combine the following in 0.2 mL PCR tubes: 
  * 6 uL NEB Buffer 4
  * 0.2 uL SbFI-HF enzyme
  * 1 uL MspI enzyme
  * 2.8 uL nuclease-free water
  * 50 uL of DNA extraction + nuclease-free water (200 ng of extracted dsDNA)
  
 3. Vortex and spin down the tubes. Now place the samples at 37 C for 6 hours.
 > The restriction digestion of your genomic DNA is now taking place.
  
</details>

## ddRADseq library construction

<details>
  <summary>Click to expand protocol!</summary>

>This protocol is based on the Peterson et al. [2012](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0037135) protocol. You can download a copy of the protovol [here](https://ndownloader.figstatic.com/files/327801). 

**Materials**

* T4 DNA Ligase
* Adapter Oligonuclotides
* NEB Phusion polymerase
* Illumina TruSeq primers
* Nuclease-free water
* Magnetic tube rack
* 1.5 mL tubes
* 0.2 mL PCR tubes
* 50 mL conical tube  

**Protocol**
1. We will be making our own adapters for this protocol and we need to make our own annealing buffer to combine our custom oligonucleotides in. THe recipe for the Annealing Buffer stock (10X) is:
   * 100 mM Tris, pH 8
   * 500 mM NaCl
   * 10 mM EDTA
>We can get these concentrations if we add 5 mL of 1M Tris, 5 mL of 5M NaCl, 1 mL of 0.5M EDTA, and 39 mL of sterile water. This will total to 50 mL which can be mixed in 50 mL conical tube. 
  
2. After we have made our Annealing Buffer, we will need to rehydrate the oligos as they come from Sigma Aldrich. There will be a sheet with the amount of nuclease-free water to add to each tube to get 100 uM concetrations. Each adapter is comprised of a set of oligos that look like this: 
  
P1.1_ACTAGG_1  
```
ACACTCTTTCCCTACACGACGCTCTTCCGATCTNNNNNNNNACTAGGTGC*A
```
P1.2_ACTAGG_1  
```
CCTAGTNNNNNNNNAGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGT  
``` 
MspI_P2.1
```
GTGACTGGAGTTCAGACGTGTGCTCTTCCGATCT
```  
MspI_P2.2    
```
CGAGATCGGAAGAGCGAGAACAA
```  
>P1 oligos are for the SbfI cutsites and P2 oligos are for the MspI cutsites. We will need to rehydrate the oligos after they arrive from the manufacturer which should result in 100 uM stock solutions for each oligonucleotide.    
  
3. Assuming 100 uM stock oligo concentrations, in 1.5 mL microcentrifuge tubes combine the following for each adapter: 
    * 20 uL PX.1
    * 20 uL PX.2
    * 5 uL 10X Annealing Buffer
    * 5 uL nuclease-free water
  
4. Vortex and spin down the tubes. Now place them on a heat block at 97.1 C for 2 minutes and 30 seconds (150 seconds total). 
  
5. Turn off the heat block and allow to cool to room temperature. 
>Alternatively, the adapter annealing can be performed in a thermocyler by incubating at 97.5 C for 2.5 minutes, then cooling at a rate of not greater than 3 C per minute until the solution reaches a temperature of 21°C after which the annealed adapters should be held at 4 C.
  
6. While we are waiting for the adapters to cool, we can clean our restriction digested DNA from the previous module using Serapure beads. We will use a 1.8 X concetration of beads to sample, so we need to add 108 uL of Serapure solution to the 60 uL of restriction digests. Transfer the restriction digest from PCR tubes to 1.5 mL microcentrifuge tubes. 
  
7. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)

8. Remove supernatent with a P1000 pipetter and discard. Remove any remaining supernatent with a P100 or P200 pipetter.

9. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 1)

10. Remove supernatent as in Step 13.

11. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 2)
  
12. Remove supernatent as in Step 13.
  
13. Allow beads to sit until there is no residual ethanol on the sides of the tube. This usually takes about 2-3 mins. 

14. Add 31 uL 10 mM Tris to dried beads and resuspend the beads in solution by removing the tube from the magnet rack. This may require gently flicking the tube to get the beads back into solution. You may then need to centrifuge the tube to return the beads to the solution to the bottom of the tube. 

15. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)
>The purified fragmented DNA is now in the supernatent.
  
16. We will now ligate adapters using the T4 DNA Ligase. For each reaction mix the following: 
    * 30 uL purified digestion
    * 2 uL of P1 adater (0.02 uM)
    * 2 uL of P2 adapter (5.92 uM)
    * 4 uL Ligation Buffer (NEB)
    * 1 uL T4 LIgase
    * 1 uL of water
 >You will need to make the appropriate adapter concentrations according to the molarity calculator from Peterson et al. (2012). In the case of SbfI and Msp sites + squamate genomes, we can do this with the following recipe: First, add 29.6 uL of 40 uM P2 adapters to 170.4 uL 1X annealing buffer... **this is your 5.92 uM working P2 dilution**. Second, make a three step dilution series for P1: (1) 1:10 dilution adding 1 uL of 40 uM P1 adapters to 9 uL of 1X annealing buffer (making a 4 uM dilution), (2) add 1 uL of 4 uM P1 adapters to 9 uL of 1X annealing buffer (making a 0.4 uM dilution), and (3) add 10 uL of 0.4 uM P1 adapters to 190 uL of 1X annealing buffer... **this is your 0.02 uM working P1 dilution**.  
  
 17. Run in a thermal cycler at 16 C for 35 min followed by 10 min at 65C (to inactivate the ligase enzyme).
  >Samples are now ligated and can be pooled prior to size selection. 
 
18. Pool all ten samples together in a single 1.5 mL tube. This should result in a total volume of ~400 uL.
  
19. Add 720 uL of Serapure bead solution to the pooled sample and mix. 
  
20. After adding the Serapure beads incubate at room temperature for 5 mins.

21. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)

22. Remove supernatent with a P1000 pipetter and discard. Remove any remaining supernatent with a P100 or P200 pipetter.

23. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 1)

24. Remove supernatent as in Step 13.

25. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 2)
  
26. Remove supernatent as in Step 13.
  
27. Allow beads to sit until there is no residual ethanol on the sides of the tube. This usually takes about 2-3 mins. 

28. Add 31 uL 10 mM Tris to dried beads and resuspend the beads in solution by removing the tube from the magnet rack. This may require gently flicking the tube to get the beads back into solution. You may then need to centrifuge the tube to return the beads to the solution to the bottom of the tube. 

29. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)
>The purified pooled, ligated sample is now ready for size selection.

30. Transfer 30 uL of ligated sample into a clean 1.5 mL tube.
  
31. Assemble (1) sample (~30 uL), (2) Blue Pippin cartridge, and (3) Blue Pippin size standard. Take them to the Blue Pippin. 
  
32. Mix 10 uL of Blue Pippin size standad with the 30 uL cleaned, pooled ligations. 
  
33. Turn on Blue Pippin and let software load. Select the 2% internal standard template and enter sample names accordingly. 
  
33. Follow the steps for cartridge preparation and device calibration listed in the Blue Pippin [manual](https://web.uri.edu/gsc/files/BluePippin-Operations-Manual-v58-CD81.pdf)

34. Set the machine to size select between 438 and 538 base pairs in size. 
  
35. Allow the Blue Pippin to run, this should take ~1.5 hours. 
  
36. Remove the ~40 uL of size-selected sample from the Blue Pippin Cartridge Sample Well(s) and place in a clean 1.5 mL tube. 
  
37. Prepare a PCR Master Mix with the following recipe: 
    * 6 uL PCR-grade water (96 uL for 16 rxn Master Mix)
    * 1 uL 10 uM PCR 1 universal primer (16 uL for 16 rxn Master Mix)
    * 1 uL 10 uM PCR 2 indexed primer (16 uL for 16 rxn Master Mix)
    * 10 uL Q5 PCR Master Mix (160 uL for 16 rxn Master Mix)

ddRADseq primer sequences are (5' to 3'): 
  
```
Primer 1: AAT GAT ACG GCG ACC ACC GAG ATC TAC ACT CTT TCC CTA CAC GAC G

Primer 2 (indexed): CAA GCA GAA GAC GGC ATA CGA GAT CGT GAT GTG ACT GGA GTT CAG ACG TGT GC
```
  
38. Aliquot 18 uL of the master mix into 16 clean PCR tubes and then add 2.5 uL of Blue Pippin size-selected sample to 15 of the tubes. Add any leftover size-selected sample to the 15th tube. The 16th PCR tube will be our negative control.

39. Mix and spin down the samples, then run using the 'Ilumina-PCR' program on the thermal cycler.
>The cycling profile is 98 C for 30 seconds, followed by 12 cycles of 98 C for 10 seconds, 65 C for 30 seconds and 72 C for 45 seconds, ending with 72 C for 5 minutes and holding at 4-10 C.   
  
40. Once completed, pool all of the PCRs into a single 1.5 mL tube (except the negative control). Add 540 uL of SearPure bead solution to the 1.5 mL tube. This is a ~1.8X concentration of beads to PCR product. 

41. After adding the Serapure beads incubate at room temperature for 5 mins.

42. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)

43. Remove supernatent with a P1000 pipetter and discard. Remove any remaining supernatent with a P100 or P200 pipetter.

44. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 1)

45. Remove supernatent as in Step 13.

46. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 2)
  
47. Remove supernatent as in Step 13.
  
48. Allow beads to sit until there is no residual ethanol on the sides of the tube. This usually takes about 2-3 mins. 

49. Add 16 uL 10 mM Tris to dried beads and resuspend the beads in solution by removing the tube from the magnet rack. This may require gently flicking the tube to get the beads back into solution. You may then need to centrifuge the tube to return the beads to the solution to the bottom of the tube. 

50. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)
>The cleaned, enriched Illumina library is now ready for quantification.

51. Transfer 15 uL of the shotgun ddRADseq pool into a clean 1.5 mL tube.
  
52. Repeat for as many samples as you want to mulitplex in sets of ten using a unique PCR index/barcode for each set.   
  
</details>

## Quantification of ddRADseq libraries using Agilent TapeStation

<details>
  <summary>Click to expand protocol!</summary>

  >We will now find out if each of the enrichment on each of our ten sample pools was successful using the Agilent TapeStation. 

**Materials**

* PCR-enriched RADseq libraries
* Agilent TapeStation
* Agilent D1000 Tape cartridge
* Agilent D1000 Sample Buffer
* Agilent D1000 Ladder
* TapeStation vortex (IKA)
* TapeStation loading tubes
* TapeStation pippette tips and pippetter

**Protocol**
>This is taken (more or less) directly from the Agilent TapeStation D1000 [protocol](https://www.agilent.com/cs/library/usermanuals/public/ScreenTape_D1000_QG.pdf)  
  
1. Turn on TapeStation System and connected computer. 

2. Launch the TapeStation Controller Software (icon on desktop)
  
3. Load D1000 ScreenTape into device and loading tips
  
4. Allow reagents (Buffer and Ladder) to sit at room temperature for 30 minutes prior to use. 
  
5. Vortex Buffer and spin down before use. 
  
6. Mix 3 uL Buffer with 1 uL Ladder in a clean TapeStation tube. 
  
7. Mix 3 uL Buffer with 1 uL enriched capture Library
  
8. Spin ladder and sample down in a mini-centrifuge. 
  
9. Vortex using IKA vortexer at 2000 rpm for 1 minute. 
  
10. Again, spin ladder and sample down in a mini-centrifuge.
  
11. Load samples into the TapeStation instrument.
  
12. Select the required samples on the TapeStation Controller. 
  
13. Click 'Start' and specify a filename with which to save results. 
  
14. If there is evidence that all of the sub-libraries have worked, proceed to step 15. 
  
15. We will now pool the sub-libraries to make your final ddRADseq libray for sequencing. 
  
</details>
