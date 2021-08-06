# Computer Laboratory 1
>You will need a Unix Command Terminal or PuTTY interface to complete this lab
## The FASTQ format, your new best friend

<details>
  <summary>Click to expand content!</summary>

>NGS files can be rather large and are used by most phylogenetics and populations genetics software packages as FASTQ files.

Each DNA sequence in a FASTQ file is formatted like this: 
```
@M01811:34:000000000-ACGFH:1:1101:10492:1210 1:N:0:15
ACTTGTATTAAGACTAATGTTCATTATTACCCCAACTTCTTTTGAAGCTGGCAAAATTTCAAAAATTATAACACACTCAGAAACTATTTTAATTGCAAAGATGGTTCTGAGAGGCTGCCTTAAATGCAGAGATCTAGCTATCTTTCTTTCTCCCCTCTCTAGGGATTCTTCAGAAGGAGTCAGCAGAACAATGCCTCATATTCCTGCCCAAGGCAGAGAAACTGTTTAATTGACAGAACCAACAGAAATCGCTGCCAACACTGCCGTCTGCAGAAGTGTCTTGCCCTAGGAATGTCTCGAGATGG
+
CCCCCGGGFGGFGGGGGGGCFGGGGGGGGGGGGGGGGGGGGGGDGFGGGGGGGGGGGFGGCFGFGE<EAFGGGGGDFFGFG<FGGFFFGGGGGFFGGGGGGGGFAFFCFGGGGDCGGGGCDFFGGGFC,FFGAF9FFGGGGGGGGGGGGGFGG?FFGGGGGGGGGGGGFGGFFEGF@>EFGGGGGGFGGGGGDG?;DDEFGGGGFGG,@FGFFGG>FGGFGGFG?DGGGFGGFGGGGGGGGFFFFFCFFFDFFFFFFFFFFFFFFFFFFD6@;CFFF=CEEFEFF303,()1;;EECF4)62=A3
```  
The individual sequences in a FASTQ file are called 'reads'. There can be millions of reads in a single FASTQ file. The first line provides information from the sequencer, the second the inferred DNA sequence and the third the quality score (=PHRED). 

PHRED scoring is important, because not all Illumina calls are equally reliable. How can we... 
  

</details>

## Retrieving Illumina data directly from the sequencer

<details>
  <summary>Click to expand content!</summary>

>If you are getting sequence data back from the NHM NextSeq or MiSeq, you will need to use...
  
</details>

## Retrieving Illumina data from the Sequence Read Archive (SRA)

<details>
  <summary>Click to expand content!</summary>

>If you want to obtain previously published data, you will want to use the SRA toolkit from NCBI. 

 1. Download some data:

```
prefetch --type fastq SRR11180057
```

</details>


## Preparing FASTQ files for downstream analyses

<details>
  <summary>Click to expand content!</summary>

>There are several things we want to do to a FASTQ file before we analyse it including removing bad quality bases and the adapter contamination we discussed in lecture.   

 1. Using Illumiprocessor to remove adapter contamination is helpful when you have multiplexed samples. A congiguration file is needed. The configuration file looks like this:

```
[adapters]
i7:AGATCGGAAGAGCACACGTCTGAACTCCAGTCAC*ATCTCGTATGCCGTCTTCTGCTTG
i5:AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGTAGATCTCGGTGGTCGCCGTATCATT

[tag sequences]  
INDEX-01:ATCACG
INDEX-02:CGATGT
INDEX-03:TTAGGC
INDEX-04:TGACCA
  
[tag map]
1_S1:INDEX-01
2_S2:INDEX-02
3_S3:INDEX-03
4_S4:INDEX-04  
```
The adapter section identifies the universal adapter sequences, the tag sequences are the unique barcodes for each sample; the tag map is used to name output files. 
  
</details>

**Helpful Links** 
>[bcl2fastq](https://emea.support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html) | [SRA toolkit](https://github.com/ncbi/sra-tools/wiki) | 
[FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) | [fastx tools](http://hannonlab.cshl.edu/fastx_toolkit/) | [illumiprocessor](https://illumiprocessor.readthedocs.io/en/latest/)
