# Molecular Laboratory 4
>The protocols we will follow are based on those of Peterson et al. ([2012](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0037135)). Minor modifications of the protocol correspond to this paper: Streicher et al. ([2014](https://onlinelibrary.wiley.com/doi/abs/10.1111/mec.12814)). 

## Experimental design and sample organization

<details>
  <summary>Click to expand protocol!</summary>

>ddRADseq makes use of dual indexEs (=barcodes), so we need to plan ahead for how we will process samples. The first barcode is added during the ligation step of the library construction, and the second is added during PCR amplification of the libraries. As such, we can use the same core set of adapters for a small number of individuals, and then use PCR-barcode to greatly increase the number of individuals that can be mulitplexed.  
  
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


</details>

## Restriction digestion of genomic DNA

<details>
  <summary>Click to expand protocol!</summary>

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

## ddRADseq library construction

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
