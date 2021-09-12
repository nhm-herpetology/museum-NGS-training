# Bioinformatics Laboratory 1
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
  
>Note: Depending on the FASTQ file, we will need to figure out what kind of Q-scores we are dealing with. Older Illumina machines used a system called phred-64 scoring whereas newer Illumina (and other sequencing platforms) use phred-33 scoring. Some downstream software packages auto-detect this, but others do not.   

</details>

## Retrieving FASTQ data directly from the Illumina sequencer

<details>
  <summary>Click to expand content!</summary>

>If you are retrieving sequence data directly from the NHM NextSeq or MiSeq, you will need to convert the Illumina Base Call data into the FASTQ format. This can be done using the Illumina program [bcl2fastq](https://emea.support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html).

1. To install bcl2fastq, we will need to use conda. To install conda on Franklin or Crop Diversity Cluster we just need to type:

```
install-conda
```  	
	
2. Next, let's download and install bcl2fastq using conda:
```
conda install -c dranew bcl2fastq  
```   
 
3. Let's check to see if the program installed successfully: 
```
bcl2fastq -h 
``` 
>This should initiate the help screen	
	
4. Illumina datasets can be very large, so for this lab we are going to work with an unpublished dataset of 10 shotgun-sequenced museum specimens (16 GB) which was generated on the NHM Illumina NextSeq 500. The input data we need to run bcl2fastq are:
	* Base call files (*.bcl.gz)
	* Statistics files (*.stats)
	* Filter files (*.filter)
	* Cluster location files (*.locs)
	* RunInfo.xml
	* Configuration files
	* Sample sheet (*.csv)	

5. We will need to make the file called ```SampleSheet.csv``` because it is a configuration file specific to the adapters and indexes we used. It is formatted like this: 
```
[Header]			
IEMFileVersion	4		
Investigator Name	JS		
Experiment Name	JS		
Date	02/04/2019		
Workflow	GenerateFASTQ		
Application	NextSeq FASTQ Only		
Assay	TruSeq LT		
Description	Museum_specimen_data		
Chemistry	Default		
			
[Reads]			
151			
151			
			
[Settings]			
Adapter	AGATCGGAAGAGCACACGTCTGAACTCCAGTCA		
AdapterRead2	AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGT		
			
[Data]			
Sample_ID	Sample_Name	I7_Index_ID	index
3	3	i3	TTAGGC
4	4	i4	TGACCA
5	5	i5	ACAGTG
6	6	i6	GCCAAT
8	8	i8	ACTTGA
10	10	i10	TAGCTT
12	12	i12	CTTGTA
15	15	i15	ATGTCA
24	24	i24	AGCAGG
27	27	i27	ATTGAG
  
```
>This configuration file will be used by the software to process the Base Call data and transform them into FASTQ data.

The contents of the post-sequencing NextSeq 500 run folder (input directory for bcl2fastq) should look something like this:
```
Config   Recipe                RTARead2Complete.txt     SampleSheet.csv
Data     RTAComplete.txt       RTARead3Complete.txt     Thumbnail_Images
Images   RTAConfiguration.xml  RunCompletionStatus.xml
InterOp  RTALogs               RunInfo.xml
Logs     RTARead1Complete.txt  RunParameters.xml
``` 
	
6. Navigate to the run folder. Now let's run the program:
```
bcl2fastq -o FASTQ_output_data --barcode-mismatches 1 --no-lane-splitting 
``` 	

7. Once the analysis is completed, navigate to the output directory ```FASTQ_output_data```. It should contain the following files: 
 ```
10_S6_R1_001.fastq.gz  27_S10_R1_001.fastq.gz  6_S4_R1_001.fastq.gz
10_S6_R2_001.fastq.gz  27_S10_R2_001.fastq.gz  6_S4_R2_001.fastq.gz
12_S7_R1_001.fastq.gz  3_S1_R1_001.fastq.gz    8_S5_R1_001.fastq.gz
12_S7_R2_001.fastq.gz  3_S1_R2_001.fastq.gz    8_S5_R2_001.fastq.gz
15_S8_R1_001.fastq.gz  4_S2_R1_001.fastq.gz    Reports
15_S8_R2_001.fastq.gz  4_S2_R2_001.fastq.gz    Stats
24_S9_R1_001.fastq.gz  5_S3_R1_001.fastq.gz    Undetermined_S0_R1_001.fastq.gz
24_S9_R2_001.fastq.gz  5_S3_R2_001.fastq.gz    Undetermined_S0_R2_001.fastq.gz
```
>These are demultiplexed FASTQ files that can now be used in downstream analyses. 	
	
</details>

## Retrieving FASTQ data from the Sequence Read Archive (SRA)

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

 1. Let's start by downloading and installing FastQC: 
  
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
/home/jefs/NGS_course/Unit_1/sratoolkit.2.11.0-ubuntu64/bin  
```
```  
mv SRR3284185_1.fastq /home/jefs/NGS_course/Unit_1/FastQC
```
```  
mv SRR3284185_2.fastq /home/jefs/NGS_course/Unit_1/FastQC
```    
Now that both of the FASTQ files have been moved. Let's navigate to the FastQC directory. Once in the FastQC directory, run the following command:
```
./fastqc SRR3284185_1.fastq SRR3284185_2.fastq  
```  
This will produce several output files. If not working locally, you can use WinSCP to access the HTML output. There are also copies in the [Example Files](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab/Example_Files) directory. The FastQC summaries let us see that quality decreases (as expected) near the end of the sequences: around 185 bp in Read 1 and 135 bp in Read 2. They also reveal that adapter contamination is present in >10% of the sequences near the end of the sequence. 

3. Let's copy the FASTQ files to a new directory for cleaning and processing:
```
cp SRR3284185_1.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```  
```
cp SRR3284185_2.fastq /home/jefs/NGS_course/Unit_1/Data/raw-fastq
```  
  
Now navigate to the 'Data/raw-fastq' directory. Let's prepare the files for cleaning by renaming them and compressing them: 
```
mv SRR3284185_1.fastq SRR3284185_S1_L001_R1_001.fastq
```  
```
mv SRR3284185_2.fastq SRR3284185_S1_L001_R2_001.fastq
``` 
```
gzip SRR3284185_S1_L001_R1_001.fastq
```  
```
gzip SRR3284185_S1_L001_R2_001.fastq
``` 
  
We want to remove low quality bases and adapter contamination and we can do both of those things using [Illumiprocessor](https://github.com/faircloth-lab/illumiprocessor) 
  
4. To use Illumiprocessor we need to install phyluce which requires miniconda for installation. We already installed conda for the previous module, but if you have skipped ahead, here is how you install conda on Franklin or Crop Diversity Cluster:

```
install-conda
```  

5. Install phyluce (instructions here for Linux version, other versions available [here](https://github.com/faircloth-lab/phyluce/releases)): 

```
wget https://raw.githubusercontent.com/faircloth-lab/phyluce/v1.7.1/distrib/phyluce-1.7.1-py36-Linux-conda.yml
``` 
```  
conda env create -n phyluce-1.7.1 --file phyluce-1.7.1-py36-Linux-conda.yml
```   
>Dependencies and Illumiprocessor are now installed
  
6. Activate phyluce
 ```  
  conda activate phyluce-1.7.1
 ``` 
7. To use Illumiprocessor, a configuration file is needed. The configuration file looks like this:

```
[adapters]
i7:AGATCGGAAGAGCACACGTCTGAACTCCAGTCAC*ATCTCGTATGCCGTCTTCTGCTTG
i5:AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGTAGATCTCGGTGGTCGCCGTATCATT

[tag sequences]  
INDEX-16:CCGTCCCG

  
[tag map]
SRR3284185_S1:INDEX-16

  
[names]
SRR3284185_S1:Cylindrophis_ruffus_FMNH_258674
  
```
The different sections of the configuration file are (1) the adapter section which identifies the universal adapter sequences (in our case these are i5 and i7 Illumina TruSeq adapters), (2) the tag sequences are the unique barcodes for each sample, (3) the tag map is used to name output files, and (4) the name of the sample that we want to be used in downstream analyses. 

8. To make the configuration text file let's use the command line: 
 
 ```  
  cat > illumiprocessor.conf
 ```   
 Now paste the configuration text (from Step 7) into your terminal and then press CTRL + SHIFT + D. 
 
9. We are now ready to run Illumiprocessor to trim low quality bases + remove adapter contamiantion: 
 ```   
illumiprocessor \
    --input raw-fastq/ \
    --output clean-fastq \
    --config illumiprocessor.conf \
    --cores 1  
 ```    

10. Now let's navigate to the cleaned read directory and examine the stats:
  
```  
cd clean-fastq
```  
```  
cd Cylindrophis_ruffus_FMNH_258674
```
```  
cd stats
```
When we look at the summary statistics file using the ```cat``` command, we should see something like the following output: 
  
```
TrimmomaticPE: Started with arguments:
 -phred33 /home/jefs/NGS_course/Data/clean-fastq/Cylindrophis_ruffus_FMNH_258674/raw-reads/Cylindrophis_ruffus_FMNH_258674-READ1.fastq.gz /home/jefs/NGS_course/Data/clean-fastq/Cylindrophis_ruffus_FMNH_258674/raw-reads/Cylindrophis_ruffus_FMNH_258674-READ2.fastq.gz /home/jefs/NGS_course/Data/clean-fastq/Cylindrophis_ruffus_FMNH_258674/split-adapter-quality-trimmed/Cylindrophis_ruffus_FMNH_258674-READ1.fastq.gz /home/jefs/NGS_course/Data/clean-fastq/Cylindrophis_ruffus_FMNH_258674/split-adapter-quality-trimmed/Cylindrophis_ruffus_FMNH_258674-READ1-single.fastq.gz /home/jefs/NGS_course/Data/clean-fastq/Cylindrophis_ruffus_FMNH_258674/split-adapter-quality-trimmed/Cylindrophis_ruffus_FMNH_258674-READ2.fastq.gz /home/jefs/NGS_course/Data/clean-fastq/Cylindrophis_ruffus_FMNH_258674/split-adapter-quality-trimmed/Cylindrophis_ruffus_FMNH_258674-READ2-single.fastq.gz ILLUMINACLIP:/home/jefs/NGS_course/Data/clean-fastq/Cylindrophis_ruffus_FMNH_258674/adapters.fasta:2:30:10 LEADING:5 TRAILING:15 SLIDINGWINDOW:4:15 MINLEN:40
Using Long Clipping Sequence: 'AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGTAGATCTCGGTGGTCGCCGTATCATT'
Using Long Clipping Sequence: 'AGATCGGAAGAGCACACGTCTGAACTCCAGTCACCCGTCCCGATCTCGTATGCCGTCTTCTGCTTG'
ILLUMINACLIP: Using 0 prefix pairs, 2 forward/reverse sequences, 0 forward only sequences, 0 reverse only sequences
Input Read Pairs: 115128 Both Surviving: 106854 (92.81%) Forward Only Surviving: 7653 (6.65%) Reverse Only Surviving: 334 (0.29%) Dropped: 287 (0.25%)
TrimmomaticPE: Completed successfully
```  

We can see that Illumiprocessor dropped about 8% of the read pairs. Let's now have a look at the cleaned output files:
```  
cd ..  
```
```
cd split-adapter-quality-trimmed  
```
There will be three sets of fastq.gz files present: 
```  
Cylindrophis_ruffus_FMNH_258674-READ1.fastq.gz
Cylindrophis_ruffus_FMNH_258674-READ2.fastq.gz
Cylindrophis_ruffus_FMNH_258674-READ-singleton.fastq.gz
```  

In addition to retaining paired-end reads, Illumiprocessor also keeps 'singleton' reads that can be used to maximize coverage for *de novo* assembly. 

11. Let's use FASTQC to see how the cleaned FASTQ.GZ files compare to the raw FASTQ files.   

```
cp Cylindrophis_ruffus_FMNH_258674-READ1.fastq.gz /home/jefs/NGS_course/Unit_1/FastQC
```  
```
cp Cylindrophis_ruffus_FMNH_258674-READ2.fastq.gz /home/jefs/NGS_course/Unit_1/FastQC
```    
Now navigate to your FASTQC directory. 
```
./fastqc Cylindrophis_ruffus_FMNH_258674-READ1.fastq.gz Cylindrophis_ruffus_FMNH_258674-READ2.fastq.gz  
```
This will produce output files as we saw in Step 2. There are also copies in the [Example Files](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_01/Bioinformatics_Lab/Example_Files) directory. You can see from the resulting HTML output that the cleaning has improved the quality and adapter content of the read sets. Much better!  

>The cleaned FASTQ.GZ files are now ready for use in a variety of downstream applications. We will learn how to use them for *de novo* assembly and read mapping in [Unit 2](https://github.com/nhm-herpetology/museum-NGS-training/tree/main/Unit_02/Bioinformatics_Lab).  
  
</details>

**Helpful Links** 
>[bcl2fastq](https://emea.support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html) | [SRA toolkit](https://github.com/ncbi/sra-tools/wiki) | 
[FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) | [illumiprocessor](https://illumiprocessor.readthedocs.io/en/latest/) | [WinSCP](https://winscp.net/eng/download.php) | [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) 
