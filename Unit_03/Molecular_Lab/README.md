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
* 50 mL conical tube
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
  * 0.5 uL of Block X
            
 7. Mix the **Block Mix** by pipetting. Transfer 5 uL to a fresh PCR tube.
            
 8. Add 7 uL of the Illumina shotgun library from [Unit 2](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_02/Molecular_Lab) to the PCR tube with 5 uL of **Block Mix**. This mixture will now be referred to as the **LIB**.
 
 9. Program a thermal cycler with the following steps: (1) 95 C for 5 minutes, (2) 65 C for 5 minutes, and (3) 65 C for infinity (or 16-24 hours).
  
 10. Place the **LIB** samples into the thermal cycler and start the program listed above. Close the lid and allow Step 1 (95 C for 5 minutes) to complete. This will denature the libraries so that the blockers can hybridize before capture. 
  
 11. After Step 1, open the lid of the thermal cycler and place the **Hybrid Mix** PCR tube into the thermal cycler. Close the lid and allow Step 2 to (65 C for 5 minutes) complete. This will allow the blockers to hybridize to the library DNA and for the **Hybrid Mix** to heat up to the reaction temperature. 
 
 12. After Step 2, open the lid of the termal cycler and carefully transfer 18 uL of **Hybrid Mix** to the **LIB** tube. Gently mix by pipetting up and down 5 times. Seal the PCR tube conating the **Hybrid Mix** and the **LIB** and remove the used **Hybrid Mix** PCR tube. Close the lid and allow Step 3 to commence (65 C for 16-24 hours).
>Normally you would leave this step to run overnight.   
  
            
</details>

## Binding, washing and PCR enrichment of capture libraries 

<details>
  <summary>Click to expand protocol!</summary>  
 
1. Select the appropriate wash temperature:
  
Temperature | Target sequence max. divergence 
------------ | -------------  
65 C | < 10% 
62 C | 10% - 15%  
60 C | 15% - 25%
>For the purpose of this UCE protocol we will use 65 C to match the hybridization reaction

2. Prepare the **Wash Buffer** in a 50 mL conical (falcon) tube.   
    
  
</details>  
  
## Quantification of capture library using Agilent TapeStation

<details>
  <summary>Click to expand protocol!</summary>

  >We will now find out if our UCE capture protocol has been successful using the Agilent TapeStation. 

**Materials**

* 'Super-duper-solid-gold' capture library 
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
