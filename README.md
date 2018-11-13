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




**Tool Descriptions**

**Sabre**

The tool Sabre is used to demultiplex barcoded reads. Sabre takes in FASTQ files and produces a set of demultiplexed FASTQ files. The Sabre tool can be used for both paired or single-end reads. Unfortunately, the CHMK Pipeline is only able to support data single-end reads.

**Cutadapt**


Cutadapt is a tools that allows the user to remove the adapter from their sequences. The CHMK Pipeline prompts the user to initialize an adapter sequence. However, if the user is unaware of what their adapter's sequence is they can use the default adapter. The default adapter sequence is:  AGATCGGAA.

**Mapping**


The CHMK Pipeline utilizes the Burrow-Wheeler Aligner (BWA) to map the trimmed files, output by Cutadapt onto the reference genome. If the user already has a set of trimmed FASTQ files, they are able to skip directly to this step in the pipeline. This can be done by answering "n" when asked if the user wants to run the default protocol. When asked, the user should enter "mapping" into the program.

**SAM to BAM Conversion**


The SAM to BAM conversion is done using SAMtools. This step is largely reformatting the data so that it can be used for variant calling in the final step of the CHMK Pipeline.

**Variant Calling**


The variant calling step uses VCFtools to find and report any variation in the genomic sequences. The files containing the output of the variant calling step are .vcf files. These files will show up in the directory created by the user at the beginning of the program.




The following tools must be installed on your system in order to successfully run this pipeline:

**Sabre**

(https://github.com/najoshi/sabre)



**Cutadapt**

To see if the command worked type 'cutadapt'

(https://cutadapt.readthedocs.io/en/stable/installation.html)



**BWA**

(http://bio-bwa.sourceforge.net/)

(https://github.com/lh3/bwa)

Li H. and Durbin R. (2010) Fast and accurate long-read alignment with Burrows-Wheeler Transform. Bioinformatics, Epub. [PMID: 20080505]



**SAMtools/BCFtools/HTSlib**

The necessary information to install SAMtools, BCFtools, and HTSlib is located at the link below.

(http://www.htslib.org/)



**VCFtools**

(http://vcftools.sourceforge.net/)

The Variant Call Format and VCFtools, Petr Danecek, Adam Auton, Goncalo Abecasis, Cornelis A. Albers, Eric Banks, Mark A. DePristo, Robert Handsaker, Gerton Lunter, Gabor Marth, Stephen T. Sherry, Gilean McVean, Richard Durbin and 1000 Genomes Project Analysis Group, Bioinformatics, 2011
