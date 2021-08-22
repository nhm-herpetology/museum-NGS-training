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
* PCR tubes
* Thermal cycler, water bath, or heat block  

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
</details>

## Shotgun Library Construction II (Ligation, Size-selection and PCR)

<details>
  <summary>Click to expand protocol!</summary>

>Magnetic Beads are valuable for extracting genomic DNA, removing small unwanted nucleic acids (e.g. primers, adapaters), and size selection. Modified from B. Faircloth and T. Glenn protocol (UCLA, 2011). Original protocol by Rohland and Reich [2012](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3337438/).

**Materials**

* T4 DNA Ligase
* Adapter Oligonuclotides
* NEB Phusion polymerase
* Illumina TruSeq primers
* Nuclease-free water
* Magnetic tube rack


**Protocol**
1. Using the a-tailed reactions from the last unit...
</details>

## Quantification using Agilent TapeStation

<details>
  <summary>Click to expand protocol!</summary>

  >Magnetic Beads are valuable for extracting genomic DNA, removing small unwanted nucleic acids (e.g. primers, adapaters), and size selection. Modified from B. Faircloth and T. Glenn protocol (UCLA, 2011). Original protocol by Rohland and Reich [2012](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3337438/).

**Materials**

* T4 DNA Ligase
* Adapter Oligonuclotides
* NEB Phusion polymerase
* Illumina TruSeq primers
* Nuclease-free water
* Magnetic tube rack


**Protocol**
1. Using the a-tailed reactions from the last unit...
</details>
