# BINF-6410-Pipeline
Group Project
BINF 6410
University of Guelph
13 November 2018
Karuna,Muskan,Christina,Hamed

The CHMK Pipeline is designed to find variation in genomic sequence data. In order to do this, CHMK Pipeline takes in a FASTQ file, aligns it to a reference genome, and produces list of BAM files containing all the variation for each sequence of interest. 

The CHMK Pipeline has many options for the user. If you do not chose the default settings when running the pipeline, you may start and stop at any given point along the pipeline. For example: you may already have SAM files. In this case you can tell the program that you would like to start at the SAM to BAM option. This will allow you to convert your files and the go on to variant calling. 

Additionally, the CHMK Pipeline give you the option to use both single or paired end reads. It is important to note that the default settings only consider single-end reads. In order to work with paired-end reads one must answer "n" to the option of running the default procedure. The program will then ask if you want to use paired-end reads further along in the options.














We used the following tool to compose our Pipeline:

Sabre
https://github.com/najoshi/sabre

Cutadapt
sudo apt-get install python3.6
sudo apt-get install python3-pip
sudo pip3 install cutadapt
To see if the command worked type 'cutadapt'
https://cutadapt.readthedocs.io/en/stable/installation.html

BWA
http://bio-bwa.sourceforge.net/
https://github.com/lh3/bwa
Li H. and Durbin R. (2010) Fast and accurate long-read alignment with Burrows-Wheeler Transform. Bioinformatics, Epub. [PMID: 20080505]


SAMtools/BCFtools/HTSlib
The necessary information to install SAMtools, BCFtools, and HTSlib is located at the link below.
http://www.htslib.org/download/

VCF
http://vcftools.sourceforge.net/
The Variant Call Format and VCFtools, Petr Danecek, Adam Auton, Goncalo Abecasis, Cornelis A. Albers, Eric Banks, Mark A. DePristo, Robert Handsaker, Gerton Lunter, Gabor Marth, Stephen T. Sherry, Gilean McVean, Richard Durbin and 1000 Genomes Project Analysis Group, Bioinformatics, 2011
