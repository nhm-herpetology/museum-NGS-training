# Molecular Laboratory 3
>In [Unit 2](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_02/Molecular_Lab) we learned how to construct shotgun genomic libraries for Illumina platforms. We will now use our shotgun libraries for the targeted sequence capture of UCEs. 

## Hybridization of RNA probes to UCEs

<details>
  <summary>Click to expand protocol!</summary>

**Materials**

* Illumina shotgun library
* MyBaits 5k Tetrapod kit (Arbor BioSciences)
* 1.5 mL microcentrifuge tubes
* 0.2 mL PCR tubes
* Thermal Cycler
* Heat Block or water bath
* Nuclease-free water
* Magnetic tube rack

**Protocol**
>This protocol is based on the Arbor BioSciences MyBaits v5 [manual](https://arborbiosci.com/wp-content/uploads/2021/03/myBaits_v5.01_Manual.pdf)
  
1. We should have recieved the following kit components from Arbor Biosciences: 
  
Reagent | Cap Colour  | Storage temperature
------------ | -------------  | -------------
Hyb N | Red | 4 C (Box 1)
Hyb S | Teal  | 4 C (Box 1)
Beads | Clear  | 4 C (Box 1)
Binding Buffer | NA  | 4 C (Box 1)
Wash Buffer | NA  | 4 C (Box 1)
Hyb D | Yellow | -20 C (Box 2)
Hyb R | Purple  | -20 C (Box 2)
Block C | Dark Green  | -20 C (Box 2)
Block O | Blue  | -20 C (Box 2)
Block X* | Orange  | -20 C (Box 2)  
Buffer E | Light Green  | -20 C (Box 2)
RNA Baits | White  | -80 C (Box 3)  
>The blocking oligos (Block X) will need to be matched to the TruSeq Illumina adapters we made in Unit 2

2. Select the appropriate bait hybridization temperature:
  
Temperature | Target sequence max. divergence 
------------ | -------------  
65 C | < 10% 
62 C | 10% - 15%  
60 C | 15% - 25%
>For the purpose of this protocol we will use 65 C because we expect the UCEs to be very similar across taxa
  
3. Make Master Mix #1, the **Hybrid Mix** in a 1.5 mL tube: 
  * 9.25 uL of Hyb N
  * 3.5 uL of Hyb D
  * 0.5 uL of Hyb S
  * 1.25 uL of Hyb R
  * 5.5 uL of RNA Baits
 
4. Incubate the **Hybrid Mix** at 60 C for 1 minute on a heat block, vortexing occasionally. Remove from the heat block and allow to sit at room temperature for 5 minutes. 

5. Transfer 18.5 uL of the **Hybrid Mix** to a PCR tube.

6. Make Master Mix #2, the **Block Mix** in a 1.5 mL tube:
  * 2.5 uL of Block O
  * 2.5 uL of Block C
  * 0.5 uL of Block X (Called 'Block A' for Illumina single index adapters)
            
 7. Mix the **Block Mix** by pipetting. Transfer 5 uL to a fresh PCR tube.
            
 8. Add 7 uL of the Illumina shotgun library from [Unit 2](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_02/Molecular_Lab) to the PCR tube with 5 uL of **Block Mix**. This mixture will now be referred to as the **LIB**.
 
 9. Program a thermal cycler with the following steps: (1) 95 C for 5 minutes, (2) 65 C for 5 minutes, and (3) 65 C for infinity (or 16-24 hours).
  
 10. Place the **LIB** samples into the thermal cycler and start the program listed above. Close the lid and allow Step 1 (95 C for 5 minutes) to complete. This will denature the libraries so that the blockers can hybridize before capture. 
  
 11. After Step 1, open the lid of the thermal cycler and place the **Hybrid Mix** PCR tube into the thermal cycler. Close the lid and allow Step 2 to (65 C for 5 minutes) complete. This will allow the blockers to hybridize to the library DNA and for the **Hybrid Mix** to heat up to the reaction temperature. 
 
 12. After Step 2, open the lid of the termal cycler and carefully transfer 18 uL of **Hybrid Mix** to the **LIB** tube. Gently mix by pipetting up and down 5 times. Seal the PCR tube conating the **Hybrid Mix** and the **LIB** and remove the used **Hybrid Mix** PCR tube. Close the lid and allow Step 3 to commence (65 C for 16-24 hours).
>Normally you would leave this step to run overnight.   
  
            
</details>

## Binding, washing and enrichment of capture libraries 

<details>
  <summary>Click to expand protocol!</summary>  
  
**Materials**

* Hybridized capture libraries from the previous step
* MyBaits 5k Tetrapod kit (Arbor BioSciences)
* 1.5 mL microcentrifuge tubes
* 0.2 mL PCR tubes
* 50 mL conical tube
* Thermal Cycler
* Heat Block or water bath
* Nuclease-free water
* Magnetic tube rack

**Protocol**
>This protocol is based on the Arbor BioSciences MyBaits v5 [manual](https://arborbiosci.com/wp-content/uploads/2021/03/myBaits_v5.01_Manual.pdf)
  
1. As a reminder, we should have recieved the following kit components from Arbor Biosciences: 
  
Reagent | Cap Colour  | Storage temperature
------------ | -------------  | -------------
Hyb N | Red | 4 C (Box 1)
Hyb S | Teal  | 4 C (Box 1)
Beads | Clear  | 4 C (Box 1)
Binding Buffer | NA  | 4 C (Box 1)
Wash Buffer | NA  | 4 C (Box 1)
Hyb D | Yellow | -20 C (Box 2)
Hyb R | Purple  | -20 C (Box 2)
Block C | Dark Green  | -20 C (Box 2)
Block O | Blue  | -20 C (Box 2)
Block X* | Orange  | -20 C (Box 2)  
Buffer E | Light Green  | -20 C (Box 2)
RNA Baits | White  | -80 C (Box 3)  
>The blocking oligos (Block X) will need to be matched to the TruSeq Illumina adapters we made in Unit 2

2. Select the appropriate wash temperature:
  
Temperature | Target sequence max. divergence 
------------ | -------------  
65 C | < 10% 
62 C | 10% - 15%  
60 C | 15% - 25%
>For the purpose of this UCE protocol we will use 65 C to match the hybridization reaction, so turn on and set a heat block to 65 C

3. Prepare the **Wash Buffer X** in a 50 mL conical (falcon) tube:
  * 400 uL Hyb S 
  * 10 mL Wash Buffer
  * 39.6 mL Nuclease-free Water
 >Once made this buffer can be stored at 4 C for 1 month. If you have a small number of captures, you can half the recipe to 200 uL Hyb S, 5 mL Wash Buffer, and 19.8 mL water. 

4. Transfer 500 uL of **Wash Buffer X** to three 1.5 mL tubes. Place all three tubes on the 65 C heat block. 
>The buffer needs to be warmed for the bead washing we will do later  
  
5. Prepare the **Beads** from the Arbor BioSciences kit by alliquoting 30 uL of **Beads** into a 1.5 mL tube.
 
6. Place the tube on a magnetic rack and allow the beads to separate for 2 minutes. Once separated, remove and discard the supernatant.
  
7. Add 200 uL of **Binding Buffer** to the beads. Remove from the magnetic rack and resuspend the beads by vortexing. Spin down and return to the magnetic rack. 

8. Allow the beads to separate for 2 minutes and then remove the supernatant. 

9. Add 200 uL of **Binding Buffer** to the beads. Remove from the magnetic rack and resuspend the beads by vortexing. Spin down and return to the magnetic rack. 

10. Allow the beads to separate for 2 minutes and then remove the supernatant.  

11. Add 200 uL of **Binding Buffer** to the beads. Remove from the magnetic rack and resuspend the beads by vortexing. Spin down and return to the magnetic rack. 

12. Allow the beads to separate for 2 minutes and then remove the supernatant.  
> You should have just washed the beads with **Binding Buffer** three times
  
13. Resuspend the beads in 70 uL of **Binding Buffer**.
  
14. Place the the **Beads** + **Binding Buffer** solution on teh heat block and hold at 65 C for 2 minutes.
  
15. Add the Hybridized capture library to the **Beads** + **Binding Buffer** solution while still on the heat block. 

16. Incubate the libraries + beads for 5 minutes at 65 C. Halfway through (2.5 minutes) remove, invert, then return the 1.5 mL tube so that the beads stay suspended. 
>The probe captured library fragments are now bound to the biotin beads. 
  
17. Remove the libraries + beads 1.5 mL tube from the heat block and place on the magnetic rack. Allow the beads to separate for 5 minutes. Once separated, remove and discard the supernatant.

18. Add 375 uL of warmed **Wash Buffer X** (tube #1) to the beads on the magnetic rack. Briefly vortex and centrifuge the solution. 
  
19. Place the 1.5 mL tube on the 65 C heat block for 5 minutes. Halfway through (2.5 minutes) remove, invert, then return the 1.5 mL tube so that the beads stay suspended.

20. Remove the libraries + beads 1.5 mL tube from the heat block and place on the magnetic rack. Allow the beads to separate for 5 minutes. Once separated, remove and discard the supernatant.

21. Add 375 uL of fresh warmed **Wash Buffer X** (tube #2) to the beads on the magnetic rack. Briefly vortex and centrifuge the solution. 
  
22. Place the 1.5 mL tube on the 65 C heat block for 5 minutes. Halfway through (2.5 minutes) remove, invert, then return the 1.5 mL tube so that the beads stay suspended.
 
23. Remove the libraries + beads 1.5 mL tube from the heat block and place on the magnetic rack. Allow the beads to separate for 5 minutes. Once separated, remove and discard the supernatant.

24. Add 375 uL of warmed **Wash Buffer X** (tube #3) to the beads on the magnetic rack. Briefly vortex and centrifuge the solution. 
  
25. Place the 1.5 mL tube on the 65 C heat block for 5 minutes. Halfway through (2.5 minutes) remove, invert, then return the 1.5 mL tube so that the beads stay suspended.
> You should have just washed the beads with **Wash Buffer X** three times   
  
26. After the last wash and pelleting, remove as much liquid as possible without disturbing the bead pellet. 
  
27. Add 30 uL **Buffer E** to the tube with the bead pellet (or 30 uL 10mM Tris).
  
28. Incubate the beads + **Buffer E** at 95 C for 5 min
  
29. Immediately pellet the beads using the magnet rack and collect the supernatant containing the enriched libraries (move it to a clean 0.2 mL PCR tube). 

 >We will now proceed to the final stage of targeted sequence capture, PCR enrichment.   

  </details>  

## PCR amplification of capture libraries 

<details>
  <summary>Click to expand protocol!</summary>  
  
**Materials**

* Enriched libraries from the previous step
* Q5 DNA polymerase (NEB)
* Illumina TruSeq primers (i5 and i7)
* 0.2 mL PCR tubes
* Thermal Cycler
* Serapure bead solution
* Nuclease-free water
* 10 mM Tris
* Magnetic tube rack

**Protocol**  
>There are two main approaches to amplifying capture libraries following the last module. First, the PCR can be done using the **Buffer E** + bead solution as template or alternatively, the PCR can be done after eluting the enriched libraries into solution. In this case we have already eluted the enriched libraries. 

1. You should have 30 uL of enriched library (in **Buffer E**) from the previous module. 
  
2. Mix the following together in a 1.5 mL tube:
  * 5 uL of nucleas-free water
  * 25 uL Q5 DNA polymerase
  * 2.5 uL TruSeq P5 (10 uM)
  * 2.5 uL TruSeq P7 (10 uM)
  * 15 uL **Buffer E** (= enriched library)
  
3. Program the following into a thermal cycler: 

Step | Temperature  | Time
------------ | -------------  | -------------
1 | 98 C | 2 minutes
2 | 98 C  | 20 seconds
3* | 60 C  | 30 seconds
4* | 72 C | 45 seconds
5* | 72 C  | 5 minutes
6 | 8 C| Infinity
>*Steps 3-5 should be repeated 12 times. 

4. Insert the PCR mixture into the thermal cycler and run the program. Once completed, remove from the thermal cycler and transfer to a 1.5 mL tube. 
  
5. Add 90 uL of Serapure solution to the post-PCR sample.  

6. After adding the Serapure beads incubate at room temperature for 5 mins.

7. Place 1.5 mL tube on magnet rack. Allow beads to seperate (~5 min)

8. Remove supernatant with a P1000 pipetter and discard. Remove any remaining supernatent with a P100 or P200 pipetter.

9. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 1)

10. Remove supernatent as in Step 10.

11. Add 500 uL of 70% ethanol and let stand for 1 min (Wash No. 2)
  
12. Remove supernatant as in Step 10.
  
13. Allow beads to sit until there is no residual ethanol on the sides of the tube. This usually takes about 2-3 mins. 

14. Add 20 uL 10mM Tris to dried beads and resuspend the beads  
  
15. Place back on the magnetic rack and allow to beads to separate. Transfer the supernatant to a clean tube - this is your final **PCR-amplified enriched capture library** 
  </details> 
  
## Quantification of capture library using Agilent TapeStation

<details>
  <summary>Click to expand protocol!</summary>

  >We will now find out if our UCE capture protocol has been successful using the Agilent TapeStation. 

**Materials**

* PCR-amplified enriched capture library 
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
  
</details>
