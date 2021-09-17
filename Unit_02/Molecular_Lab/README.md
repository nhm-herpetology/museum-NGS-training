# Molecular Laboratory 2

## Shotgun Library Construction I (Fragmentation, End-Repair, A-tailing)

<details>
  <summary>Click to expand protocol!</summary>

>Here we will start building an NGS library of genomic double-stranded DNA (dsDNA) for eight samples using starting amounts of 500 ng dsDNA and NEBNext Master Mixes. 

**Materials**

* NEBNext dsDNA Fragmentase kit (M0348S/L)
* Serapure magnetic bead solution (from Unit 1)
* Magnetic Bead Rack
* NEBNext End Repair Module (E6050)
* NEBNext dA-tailing Module (E6053)  
* 1.5 mL microcentrifuge tubes
* PCR-grade water
* Fresh 70% ethanol
* 10 mM Tris (DNA Storage Buffer from Unit 1)
* PCR tubes
* Thermal cycler, water bath, or heat block  

**Protocol**
  
1. Set a heat block or water bath to 37 C.
   
2. Using the DNA extractions from Unit 1, we are now going to prepare the DNA for library construction. First, we need to prepare 500 ng from the DNA isolates and then adjust the volumes with water so that all samples have 60 uL for the fragmentation step. I use a spreadsheet with four columns to do this: 
  
Sample ID | Qubit concentration (ng/uL)  | uL needed for 500 ng | uL of water to add
------------ | -------------  | ------------- | -------------
Sample 1 | 10.0 | 50.0  | 10.0
Sample 2 | 18.5  | 27.0 | 33.0
Sample 3 | 33.2  | 15.1 | 44.9
Sample 4 | 80.0  | 6.3  | 53.7

> The third column is the second column value divided by 500 and the fourth column is 60 minus the third column value

3. In 1.5 mL microcentrifuge tubes, prepare the following recipe for all eight samples: 
  * 4 uL Fragmentase Buffer
  * 2 uL Fragmentase
  * 60 uL extracted DNA

4. Place the 1.5 mL tubes in the 37 C heat block/water bath for 25 minutes. 
  
5. Remove Serapure magnetic bead solution from 4 C storage and agitate/vortex so that beads are suspended in the solution. It should look the same as when we made the beads in Unit 1. 
  
6. Remove the fragmented DNA samples from the 37 C incubation and add 126 uL of Serapure beads to each sample. This is a 1.8X concentration.   

7. After adding the Serapure beads incubate at room temperature for 5 mins.

8. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)

9. Remove supernatent with a P1000 pipetter and discard. Remove any remaining supernatent with a P100 or P200 pipetter.

10. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 1)

11. Remove supernatent as in Step 13.

12. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 2)
  
13. Remove supernatent as in Step 13.
  
14. Allow beads to sit until there is no residual ethanol on the sides of the tube. This usually takes about 2-3 mins. 

15. Add 31 uL 10 mM Tris to dried beads and resuspend the beads in solution by removing the tube from the magnet rack. This may require gently flicking the tube to get the beads back into solution. You may then need to centrifuge the tube to return the beads to the solution to the bottom of the tube. 

16. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)
>The purified fragmented DNA is now in the supernatent. 

17. Transfer 30 uL of fragmented DNA into clean PCR tubes. We will now begin the End-repair reactions. 
  
18. To each tube with 30 uL of fragmented DNA, add the following: 
  * 2.5 uL 10X End-repair Buffer
  * 1.25 uL End-repair enzyme
  * 6.25 uL PCR-grade water

19. Mix each reaction by pippeting gently up and down and then spin down in a mini-centrifuge.

20. Transfer the PCR tubes to a thermal cycler and run the 'End-repair' program which will keep the samples at 20 C for 30 minutes. 
  
21. Once complete, remove the PCR tubes from the thermal cylcer and transfer each sample (~40 uL) to new 1.5 mL tubes and add 72 uL of Serapure magnetic bead solution. This is a 1.8X concentration.
  
22. After adding the Serapure beads incubate at room temperature for 5 mins.

23. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)

24. Remove supernatent with a P1000 pipetter and discard. Remove any remaining supernatent with a P100 or P200 pipetter.

25. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 1)

26. Remove supernatent as in Step 13.

27. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 2)
  
28. Remove supernatent as in Step 13.
  
29. Allow beads to sit until there is no residual ethanol on the sides of the tube. This usually takes about 2-3 mins. 

30. Add 31 uL 10 mM Tris to dried beads and resuspend the beads in solution by removing the tube from the magnet rack. This may require gently flicking the tube to get the beads back into solution. You may then need to centrifuge the tube to return the beads to the solution to the bottom of the tube. 

31. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)
>The purified End-repaired DNA is now in the supernatent.   

32. Transfer 30 uL of fragmented DNA into clean PCR tubes. We will now begin the dA-tail reactions. 

33. To each tube with 30 uL of end-repaired DNA, add the following: 
  * 1.25 uL 10X dA-tailing Buffer
  * 0.75 uL Klenow fragment
  * 8 uL PCR-grade water 

34. Mix each reaction by pippeting gently up and down and then spin down in a mini-centrifuge.

35. Transfer the PCR tubes to a thermal cycler and run the 'A-tailing' program which will keep the samples at 37 C for 30 minutes. 
  
36. Once complete, remove the PCR tubes from the thermal cylcer and transfer each sample (~40 uL) to new 1.5 mL tubes and add 72 uL of Serapure magnetic bead solution. This is a 1.8X concentration.
  
37. After adding the Serapure beads incubate at room temperature for 5 mins.

38. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)

39. Remove supernatent with a P1000 pipetter and discard. Remove any remaining supernatent with a P100 or P200 pipetter.

40. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 1)

41. Remove supernatent as in Step 13.

42. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 2)
  
43. Remove supernatent as in Step 13.
  
44. Allow beads to sit until there is no residual ethanol on the sides of the tube. This usually takes about 2-3 mins. 

45. Add 26 uL 10 mM Tris to dried beads and resuspend the beads in solution by removing the tube from the magnet rack. This may require gently flicking the tube to get the beads back into solution. You may then need to centrifuge the tube to return the beads to the solution to the bottom of the tube. 

46. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)
>The purified dA-tailed DNA is now in the supernatent.
  
47. Transfer 25 uL of fragmented DNA into clean PCR tubes. These will be used for ligation in the next module. 
  
</details>

## Shotgun Library Construction II (Ligation, Size-selection and PCR)

<details>
  <summary>Click to expand protocol!</summary>

>Here we will finish building an NGS library of genomic double-stranded DNA (dsDNA) for the eight samples processed last time in the molecular lab. 

**Materials**

* 1.0M TRIS
* 5.0M NaCl 
* 0.5M EDTA
* Purified dA-tailed reactions
* Adapter Oligonucleotides (Indexed + Universal)
* NEBNext Quick Ligation Module (E6056)
* NEBNext Q5 HotStart HiFi PCR Master Mix (M0543)
* Illumina TruSeq primers
* Serapure magnetic bead solution
* Fresh 70% Ethanol
* Nuclease-free water
* Magnetic tube rack
* Blue Pippin (Sage Science)
* 2% Agarose cartridge w/ internal standard for Blue Pippin
* Thermal cycler
* 1.5 mL microcentrifuge tubes
* 50 mL conical (falcon) tube for the annealing buffer

**Protocol**

1. We will start by constructing our own adapters that will be used to barcode (=index) each of the eight dA-tailed reactions. First, we need to make the annealing buffer. In a 50 mL conical tube mix the following: 
  * 5 mL 1M TRIS
  * 5 mL 5M NaCl
  * 1 mL 0.5M EDTA
  * 39 mL nuclease-free water
>This is your annealing buffer

2. Turn a heat block to 95 C (if using a water bath use extra care as this is obviously quite hot)
  
3. In clean 1.5 mL tubes combine the following for as many indexes as you have:
  * 10 uL 100 uM Oligo 1 (Indexed)
  * 10 uL 100 uM Oligo 2 (Universal)
  * 5 uL Annealing Buffer
  * 25 uL nuclease-free water 
  >This should create 40 uM adapter working stocks

Illumina adapters look like this (5' to 3'): 
  
```
Indexed:    P*GATCGGAAGAGCACACGTCTGAACTCCAGTCACATCACGATCTCGTATGCCGTCTTCTGCTTG
Universal:  AATGATACGGCGACCACCGAGATCTACACTCTTTCCCTACACGACGCTCTTCCGATC*T    
```
  
4. Spin down and place the 1.5 mL adapter tubes on the 95 C heat block. Let sit at 95 C for 1 min and then turn off the heat block and allow it to return to room temperature over 30 to 45 minutes. 
>The goal here is to slowly decrease the heat (~1 C per minute) to allow the adapter oligos to anneal to one another.

5. Once back to room temperature, remove from the heat block (and if not using right away) store at -20 C.  
  
6. To make 1 uM concentrations for use in the ligation step below, combine the following in a clean 1.5 mL tube:
   * 2.5 uL of 40 uM annealed adapter solution
   * 97.5 ul nuclease-free water
  
7. To each tube with 25 uL of dA-tailed DNA, add the following: 
  * 2.5 uL 5X Ligation Buffer
  * 1.25 uL T4 DNA Ligase
  * 2.5 uL 1 uM Illumina adapter (made previously).  

I like to keep track of which barcodes were used on which samples as follows: 
  
Sample ID | Index  | Barcode ID 
------------ | -------------  | ------------- 
Sample 1 | 1  | ATCACG  
Sample 2 | 2  | CGATGT 
Sample 3 | 3  | TTAGGC 
Sample 4 | 4  | TGACCA  
  
8. Mix each reaction by pippeting gently up and down and then spin down in a mini-centrifuge.

9. Transfer the PCR tubes to a thermal cycler and run the 'Ligation' program which will keep the samples at 20 C for 15 minutes.  
>Following ligation, your samples will all be uniquely barcoded and can be separated bioinformatically, so it is safe to now combine them into a single pool. 
  
10. Pool all eight samples together in a single 1.5 mL tube. This should result in a total volume of ~240 uL.
  
11. Add 400 uL of Serapure bead solution to the pooled sample and mix. 
  
12. After adding the Serapure beads incubate at room temperature for 5 mins.

13. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)

14. Remove supernatent with a P1000 pipetter and discard. Remove any remaining supernatent with a P100 or P200 pipetter.

15. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 1)

16. Remove supernatent as in Step 13.

17. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 2)
  
18. Remove supernatent as in Step 13.
  
19. Allow beads to sit until there is no residual ethanol on the sides of the tube. This usually takes about 2-3 mins. 

20. Add 31 uL 10 mM Tris to dried beads and resuspend the beads in solution by removing the tube from the magnet rack. This may require gently flicking the tube to get the beads back into solution. You may then need to centrifuge the tube to return the beads to the solution to the bottom of the tube. 

21. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)
>The purified pooled, ligated sample is now ready for size selection.

22. Transfer 30 uL of ligated sample into a clean 1.5 mL tube.
  
23. Assemble (1) sample (~30 uL), (2) Blue Pippin cartridge, and (3) Blue Pippin size standard. Take them to the Blue Pippin. 
  
24. Mix 10 uL of Blue Pippin size standad with the 30 uL cleaned, pooled ligations. 
  
25. Turn on Blue Pippin and let software load. Select the 2% internal standard template and enter sample names accordingly. 
  
26. Follow the steps for cartridge preparation and device calibration listed in the Blue Pippin [manual](https://web.uri.edu/gsc/files/BluePippin-Operations-Manual-v58-CD81.pdf)

27. Set the machine to size select between 438 and 538 base pairs in size. 
  
28. Allow the Blue Pippin to run, this should take ~1.5 hours. 
  
29. Remove the size-selected sample from the Blue Pippin Cartridge Sample Well(s) and place in a clean 1.5 mL tube. 
  
30. Prepare a PCR Master Mix with the following recipe: 
    * 6 uL PCR-grade water (96 uL for 16 rxns)
    * 1 uL TruSeq primer 1 (16 uL for 16 rxns)
    * 1 uL TruSeq primer 2 (16 uL for 16 rxns)
    * 10 uL Q5 PCR Master Mix (160 uL for 16 rxns)

Illumina TruSeq pimer sequences are (5' to 3'): 
  
```
Primer 1: AAT GAT ACG GCG ACC ACC GAG A
Primer 2: CAA GCA GAA GAC GGC ATA CGA G
```
  
31. Alliquot 18 uL the master mix into 16 clean PCR tubes and then add 2 uL of Blue Pippin size-selected sample to 15 of the tubes. The 16th PCR tube will be our negative control.

32. Mix and spin down the samples, then run using the 'Ilumina-PCR' program on the thermal cycler. 
  
33. Once completed, pool all of the PCRs into a single 1.5 mL tube (except the negative control). Add 540 uL of SearPure bead solution to the 1.5 mL tube. This is a 1.8X concentration. 

34. After adding the Serapure beads incubate at room temperature for 5 mins.

35. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)

36. Remove supernatent with a P1000 pipetter and discard. Remove any remaining supernatent with a P100 or P200 pipetter.

37. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 1)

38. Remove supernatent as in Step 13.

39. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 2)
  
40. Remove supernatent as in Step 13.
  
41. Allow beads to sit until there is no residual ethanol on the sides of the tube. This usually takes about 2-3 mins. 

42. Add 16 uL 10 mM Tris to dried beads and resuspend the beads in solution by removing the tube from the magnet rack. This may require gently flicking the tube to get the beads back into solution. You may then need to centrifuge the tube to return the beads to the solution to the bottom of the tube. 

43. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)
>The cleaned, enriched Illumina library is now ready for quantification.

44. Transfer 15 uL of the shotgun Illumina library into a clean 1.5 mL tube.  
  
</details>

## Quantification of Illumina Libraries using Agilent TapeStation

<details>
  <summary>Click to expand protocol!</summary>

  >We will now find out if our Illumina library construction has been successful using the Agilent TapeStation. 

**Materials**

* Cleaned, pooled, size-selected and PCR-enriched Illumina library 
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
  
7. Mix 3 uL Buffer with 1 uL enriched Illumina Library
  
8. Spin ladder and sample down in a mini-centrifuge. 
  
9. Vortex using IKA vortexer at 2000 rpm for 1 minute. 
  
10. Again, spin ladder and sample down in a mini-centrifuge.
  
11. Load samples into the TapeStation instrument.
  
12. Select the required samples on the TapeStation Controller. 
  
13. Click 'Start' and specify a filename with which to save results. 
  
</details>
