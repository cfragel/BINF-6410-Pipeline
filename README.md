# BINF-6410-Pipeline
```
Group Project
BINF 6410
University of Guelph
13 November 2018
Karuna,Muskan,Christina,Hamed
GitHub id : kvijayak, Muskan3195, cfragel, hzamankh
```


# CHMK Pipeline


The CHMK Pipeline is designed to find variation in genomic sequence data. In order to do this, CHMK Pipeline takes in a FASTQ file, aligns it to a reference genome, and produces list of BAM files containing all the variation for each sequence of interest. 

The CHMK Pipeline has many options for the user. If you do not chose the default settings when running the pipeline, you may start and stop at any given point along the pipeline. For example: you may already have SAM files. In this case you can tell the program that you would like to start at the SAM to BAM option. This will allow you to convert your files and then go on to variant calling. 

Before the analysis begins, the user can set the number of CPU and Threads that they would like to use. The user will be prompted by he program to enter their desired number. 

The user must also be aware of the path to their files. For example, when asked for the path to their reference genome the user should enter something along the lines of: "/home/Directory/filename"



**Tool Descriptions**

**Demultiplexing**

The tool Sabre is used to demultiplex barcoded reads. Sabre takes in FASTQ files and produces a set of demultiplexed FASTQ files. The Sabre tool can be used for both paired or single-end reads. The se option allows for sabre to be run using single-end reads while the pe option allows for the use of paired-end reads.

sabre se -f $DATA -b $BARCODE -u unk.fastq

```
se identifies that sabre is using single-end reads
-b identifies the barcode file
-u identfies the format of the output file
```


**Trimming**


Cutadapt is a tools that allows the user to remove the adapter from their sequences. The CHMK Pipeline prompts the user to initialize an adapter sequence. However, if the user is unaware of what their adapter's sequence is they can use the default adapter. The default adapter sequence is:  AGATCGGAA.

parallel -j $CPU cutadapt -a $ADAP -m 50 -o {}.fastq {}.fq ::: $(ls -1 *.fq | sed 's/.fq//')

In the above line of code

```
-j option indicates to not include deletions of skips. 
-a option is used for identifying the adapter sequence. 
-m options sets the maximum length that can be trimmed  -o sets the file type for the output.
```

**Mapping**


The CHMK Pipeline utilizes the Burrow-Wheeler Aligner (BWA) to map the trimmed files, output by Cutadapt onto the reference genome. If the user already has a set of trimmed FASTQ files, they are able to skip directly to this step in the pipeline. This can be done by answering "n" when asked if the user wants to run the default protocol. When asked, the user should enter "mapping" into the program.

parallel -j $CPU bwa mem -t $THR $REF {}.fastq ">" {}.sam ::: $(ls -1 *.fastq | sed 's/.fastq//')

```
-t option identifies the number of Thread
 mem causes the trailing '5 end the may occur at the adapter to be cut off
 ```


**SAM to BAM Conversion**


The SAM to BAM conversion is done using SAMtools. This step is largely reformatting the data so that it can be used for variant calling in the final step of the CHMK Pipeline.

parallel -j $CPU samtools view -b -S -h {}.sam ">" {}.temp.bam ::: $(ls -1 *.sam | sed 's/.sam//')

parallel -j $CPU samtools sort {}.temp.bam -o {}.sort.bam ::: $(ls -1 *.temp.bam | sed 's/.temp.bam//')

parallel -j $CPU samtools index {} ::: $(ls -1 *.sort.bam)

```
-b option changes the format the BAM
-h includes the header in the output file
-S is for identifying SAM files
```


**Variant Calling**


The variant calling step uses BCFtools to find and report any variation in the genomic sequences. The files containing the output of the variant calling step are .vcf files. These files will show up in the directory created by the user at the beginning of the program.


samtools mpileup -g -f $REF -b $PWD/bamlist > variants.bcf

```
-g and -f format the output file so that all bits are set as INT.
```


The following tools must be installed on your system in order to successfully run this pipeline:

**Sabre**

(https://github.com/najoshi/sabre)



**Cutadapt 1.18**

To see if the command worked type 'cutadapt'

(https://cutadapt.readthedocs.io/en/stable/installation.html)



**BWA 0.7.17**

(http://bio-bwa.sourceforge.net/)

(https://github.com/lh3/bwa)

Li H. and Durbin R. (2010) Fast and accurate long-read alignment with Burrows-Wheeler Transform. Bioinformatics, Epub. [PMID: 20080505]



**SAMtools 1.9/BCFtools 1.9/HTSlib 1.9**

The necessary information to install SAMtools, BCFtools, and HTSlib is located at the link below.

(http://www.htslib.org/)




