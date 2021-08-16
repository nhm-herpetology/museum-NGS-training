# Computer Laboratory 1
>You will need a Unix Command Terminal or PuTTY interface to complete this lab
## The FASTQ format, your new best friend

<details>
  <summary>Click to expand content!</summary>

>NGS files can be rather large and most phylogenetics and populations genetics software packages import Illumina data as FASTQ files. The individual sequences in a FASTQ file are called 'reads'. There can be millions of reads in a single FASTQ file. 

Each DNA sequence in a FASTQ file looks like this: 
```
@M01811:34:000000000-ACGFH:1:1101:10492:1210 1:N:0:15
ACTTGTATTAAGACTAATGTTCATTATTACCCCAACTTCTTTTGAAGCTGGCAAAATTTCAAAAATTATAACACACTCAGAAACTATTTTAATTGCAAAGATGGTTCTGAGAGGCTGCCTTAAATGCAGAGATCTAGCTATCTTTCTTTCTCCCCTCTCTAGGGATTCTTCAGAAGGAGTCAGCAGAACAATGCCTCATATTCCTGCCCAAGGCAGAGAAACTGTTTAATTGACAGAACCAACAGAAATCGCTGCCAACACTGCCGTCTGCAGAAGTGTCTTGCCCTAGGAATGTCTCGAGATGG
+
CCCCCGGGFGGFGGGGGGGCFGGGGGGGGGGGGGGGGGGGGGGDGFGGGGGGGGGGGFGGCFGFGE<EAFGGGGGDFFGFG<FGGFFFGGGGGFFGGGGGGGGFAFFCFGGGGDCGGGGCDFFGGGFC,FFGAF9FFGGGGGGGGGGGGGFGG?FFGGGGGGGGGGGGFGGFFEGF@>EFGGGGGGFGGGGGDG?;DDEFGGGGFGG,@FGFFGG>FGGFGGFG?DGGGFGGFGGGGGGGGFFFFFCFFFDFFFFFFFFFFFFFFFFFFD6@;CFFF=CEEFEFF303,()1;;EECF4)62=A3
```  
The first line provides information from the sequencer (flow cell), the second the inferred DNA sequence, the third a standard +, and the fourth the Phred quality score (Q score). 

Phred Quality Score | Probability of Incorrect Base Call  | Base Call Accuracy
------------ | -------------  | -------------
10 | 1 in 10 | 90%
20 | 1 in 100  | 99%
30 | 1 in 1,000  | 99.9%
40 | 1 in 10,000  | 99.99%
50 | 1 in 100,000  | 99.999%
  
  

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

 1. Download and install the SRA Toolkit from NCBI/Github:
>For Ubuntu (e.g. Franklin@NHM). For other operating systems, visit: [SRA toolkit](https://github.com/ncbi/sra-tools/wiki)    
```
wget http://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/current/sratoolkit.current-ubuntu64.tar.gz  
```
```
tar -xf sratoolkit.current-ubuntu64.tar.gz
```
```
rm sratoolkit.current-ubuntu64.tar.gz
```  
```
cd sratoolkit.current-ubuntu64
```
```
cd bin
```
```
./vdb-config --interactive
```
This will open the SRA configuration. Use the Configuration Guide [here](https://github.com/ncbi/sra-tools/wiki/03.-Quick-Toolkit-Configuration). Then test with the following command:
```
./fastq-dump --stdout -X 2 SRR390728
```
You should see this output:
```
Read 2 spots for SRR390728
Written 2 spots for SRR390728
@SRR390728.1 1 length=72
CATTCTTCACGTAGTTCTCGAGCCTTGGTTTTCAGCGATGGAGAATGACTTTGACAAGCTGAGAGAAGNTNC
+SRR390728.1 1 length=72
;;;;;;;;;;;;;;;;;;;;;;;;;;;9;;665142;;;;;;;;;;;;;;;;;;;;;;;;;;;;;96&&&&(
@SRR390728.2 2 length=72
AAGTAGGTCTCGTCTGTGTTTTCTACGAGCTTGTGTTCCAGCTGACCCACTCCCTGGGTGGGGGGACTGGGT
+SRR390728.2 2 length=72
;;;;;;;;;;;;;;;;;4;;;;3;393.1+4&&5&&;;;;;;;;;;;;;;;;;;;;;<9;<;;;;;464262
```  
  
  2. Download some data using the SRA toolkit. As an example we will use Illumina MiSeq data from an individual of *Cylindrophis* *ruffus* used in Streicher & Wiens [2016](https://www.sciencedirect.com/science/article/abs/pii/S1055790316300495?via%3Dihub):

```
./fasterq-dump SRR3284185
```
  
You shoud see the following output: 
  
```
spots read:     115,128
reads read:     230,256
reads written:  230,256
```
>Read 1 (SRR3284185_1.fastq) and Read 2 (SRR3284185_2.fastq) data are now in your working directory.

</details>


## Preparing FASTQ files for downstream analyses

<details>
  <summary>Click to expand content!</summary>

>There are several things we want to do to a FASTQ file before we analyse it including removing bad quality bases and the adapter contamination we discussed in lecture.     

 1. We want to figure out what kind of Q-scores we are dealing with. Older Illumina machines used a system called phred-64 scoring whereas newer Illumina (and other sequencing platforms) use phred-33 scoring. Let's start by downloading and installing FastQC: 
  
```
wget https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.9.zip
```
```
unzip fastqc_v0.11.9.zip
```  
```  
rm fastqc_v0.11.9.zip
``` 
```
cd FastQC 
```  
```
chmod 755 fastqc
``` 

 2. Let's use the MiSeq files from *Cylindrophis* *ruffus* we downloaded from the SRA as example data. First, let's navigate to the SRA toolkit ```bin``` directory. Then determine the $PATH:
  
```
pwd  
```  
Your directory structure will differ from mine based on your user name. On Franklin, mine is: 
```
/home/jefs/NGS_course/sratoolkit.2.11.0-ubuntu64/bin  
```
```  
mv SRR3284185_1.fastq /home/jefs/NGS_course/FastQC
```
```  
mv SRR3284185_2.fastq /home/jefs/NGS_course/FastQC
```    
Now that both of the FASTQ files have been moved. Let's navigate to the FastQC directory. Once in the FastQC directory, run the following command:
```
./fastqc SRR3284185_1.fastq SRR3284185_2.fastq  
```  
This will produce several output files. If not working locally, you can use WinSCP to access the HTML output. There are also copies in the [Example Files](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Computer_Lab/Example_Files) directory. The FastQC summaries let us see that quality decreases (as expected) near the end of the sequences: around 185 bp in Read 1 and 135 bp in Read 2. They also reveal that adapter contamination is present in >10% of the sequences near the end of the sequence. We want to remove low quality bases and adapter contamination and we can do both of those things using [Illumiprocessor](https://github.com/faircloth-lab/illumiprocessor) 
  
 3. To use Illumiprocessor, a congiguration file is needed. The configuration file looks like this:

```
[adapters]
i7:AGATCGGAAGAGCACACGTCTGAACTCCAGTCAC*ATCTCGTATGCCGTCTTCTGCTTG
i5:AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGTAGATCTCGGTGGTCGCCGTATCATT

[tag sequences]  
INDEX-01:ATCACG

  
[tag map]
1_S1:INDEX-01

  
[names]
1_Cylindrophis_ruffus_FMNH_258674
  
```
The different sections of the configuration file are (1) the adapter section which identifies the universal adapter sequences (in our case these are i5 and i7 Illumina TruSeq adapters), (2) the tag sequences are the unique barcodes for each sample, (3) the tag map is used to name output files, and (4) the name of the sample that we want to be used in downstream analyses. 
  
</details>

**Helpful Links** 
>[bcl2fastq](https://emea.support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html) | [SRA toolkit](https://github.com/ncbi/sra-tools/wiki) | 
[FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) | [fastx tools](http://hannonlab.cshl.edu/fastx_toolkit/) | [illumiprocessor](https://illumiprocessor.readthedocs.io/en/latest/)
