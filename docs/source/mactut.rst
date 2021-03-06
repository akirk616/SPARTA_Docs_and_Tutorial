.. _mactut:

Mac OS X tutorial
=================

.. important:: There is a known issue introduced by Apple in the newer operating system (El Capitan) that does affect SPARTA. You will need to install the command line tools. To initiate that process, type 'gcc' into the terminal (without the quotes) and hit enter. From here it will ask you if you want to install the command line tools. Click 'Install' or 'Agree'. Close and re-open the terminal and proceed with the subsequent installation steps.

**Download the workflow**: `SPARTA for Mac <http://www.github.com/biobenkj/SPARTA_Mac/archive/master.zip>`_

#. :ref:`introduction`

#. :ref:`basic-terminal-commands`

#. :ref:`install-dependencies`

#. :ref:`initializing-sparta`

#. :ref:`analyzing-example-data`

#. :ref:`analyzing-your-data`

#. :ref:`identifying-potential-batch-effects`

#. :ref:`altering-workflow-execution-options`


.. _introduction:

Introduction
------------

Many bioinformatics software packages and workflows require the user to utilize them from
the command line or terminal. SPARTA is no different. The reason the command line interface
is utilized is that a great deal of power and flexibility can be gained without the use of
a graphical user interface (GUI). Further, a GUI can be difficult to implement across various
platforms. To find the command line interface/Terminal on Mac OS X, go to Finder -> Applications -> Utilities -> Terminal (might just be worth dragging it onto your dock).

.. image:: mactermnav.jpg
	:align: center
	:alt: Navigate to terminal on a Mac
	
Decompress the SPARTA_Mac-master.zip file by double-clicking on it. Now, drag and drop the
decompressed folder onto your desktop.

SPARTA expects either compressed (.gz) or uncompressed FASTQ files (.fq or .fastq) as input,
with a reference genome file in FASTA format and a genome feature file (.gtf) within the folder
that contains the input data. To see an example of appropriate input data, look inside the
ExampleData folder within the SPARTA_Mac-master folder.

To download a reference genome and genome feature file for your favorite bacteria, go to
the `Ensembl website <http://bacteria.ensembl.org/info/website/ftp/index.html>`_. The reference
genome and feature file are already present for the ExampleData.

.. _basic-terminal-commands:

Basic Terminal Commands
-----------------------

Let's have a look at some basic Terminal commands, we will cover the commands necessary to:

**1.** Move through folders

**2.** List the contents of a folder

**3.** Make new folders

**4.** Rename files/folders

**5.** Delete files/folders

.. csv-table::
   :header: " ", "Command", "What it does", "Examples"
   :widths: 2, 8, 10, 40

   "**1.**", "cd", "Change directory/folder", "cd ~ (this changes to your home directory); cd .. (this goes back one folder)"
   "**2.**", "ls", "List the contents of a folder", "ls"
   "**3.**", "mkdir", "Make a new directory/folder", "mkdir NewFolder (this will make a new folder called 'NewFolder' in your current directory)"
   "**4.**", "mv", "Rename or move a file from one name to another", "mv file1 file2 (this will rename/move file1 to file2)"  
   "**5.**", "rm", "Remove a file (add the -r flag to remove a folder)", "rm file1 (remove file1); rm -r folder1 (remove folder1)" 

**Command reference sheet**

.. image:: linuxcoms.jpg
	:align: center
	:alt: Linux/Unix command list
	
*Ref. sheet from: http://files.fosswire.com/2007/08/fwunixref.pdf*

.. _install-dependencies:

Install Dependencies
--------------------

The SPARTA workflow requires a few things in order to run: Python, Java, NumPy, and R.
If you already have these installed, great! If you don't, let's start by downloading the 
latest version of `Python 2 <https://www.python.org/downloads/release/python-2710/>`_
(see image below). You will want to download and install the red boxed version of Python 2.
Follow the prompts to install Python with the default values.

.. image:: pythonmacdownload.jpg
	:align: center
	:alt: Python download for Mac
	
Great! Let's check and see if Java is already installed on your system. Open up the terminal,
(if you don't remember how to do this, head back to the :ref:`introduction`) and type::
    
    java -version
	
If Java is already installed, it will produce some output that looks like this::
	
    java version "1.8.0_31"
    Java(TM) SE Runtime Environment (build 1.8.0_31-b13)
    Java HotSpot(TM) 64-Bit Server VM (build 25.31-b07, mixed mode) 
	
If the output does *not* look something like this, Java is likely not installed and two of
the tools require Java to function (Trimmomatic and FastQC). Let's download and install a 
suitable version of `Java <http://www.oracle.com/technetwork/java/javase/downloads/index.html>`_
(see image below). You will want to download and install the red boxed version of Java JRE.
You will also need to click on the button (red arrow) to accept the terms and conditions
of using Java JRE. Follow the prompts to install Java.

.. image:: javadownloadmac.jpg
	:align: center
	:height: 300 px
	:width: 500 px
	:alt: Java JRE download for Mac
	
.. image:: JREdownloadmac.jpg
	:align: center
	:height: 750 px
	:width: 950 px
	:alt: Java JRE download for Mac
	
To install NumPy, go back to or open the Terminal and type::
    
    sudo pip install numpy
	
This will prompt you for your password. Enter your password and hit Enter/Return. 

.. note:: As you type in your password, **no characters will appear** but you *are* entering characters.

Once you have entered your password and hit Enter/Return, NumPy will be downloaded and installed
on your system.

Finally, let's install R. Navigate to the SPARTA_Mac folder and go to the folder labeled 
"Install_R". Within this folder is an R installer. Double-click on the installer and follow
the prompts to install R.

.. note:: If you have OSX 10.9 (Mavericks) or higher, you will want to use version 3.2.3. If you have OSX 10.6 to 10.8, you want to use the version 3.2.1. To check which version you have, click on the Apple logo in the upper left hand corner of your screen and then click on "About This Mac". A window will appear telling you which version of OSX you have.

Congratulations! You've installed the necessary dependencies to run SPARTA!

.. _initializing-sparta:

Initializing SPARTA
-------------------

Once SPARTA is initialized, the workflow will seek to identify that all of the necessary
dependencies are met. If they are not satisfied, a message specific to what is not installed
will appear as output in the terminal window.

To initialize SPARTA, go to the Terminal and navigate to the SPARTA_Mac-master folder on your desktop by typing::

     cd ~/Desktop/SPARTA_Mac-master
     
To start the workflow, type::

     python SPARTA.py
     
This will start the software and check for dependencies.

.. _analyzing-example-data:

Analyzing Example Data
----------------------

SPARTA is distributed with some example data. Specifically, it is the first 100,000 reads
of each sample from `Baker et al. <http://onlinelibrary.wiley.com/doi/10.1111/mmi.12688/abstract>`_.

To begin the analysis, navigate into the SPARTA_Mac-master folder and drag and drop the folder
called "ExampleData" out onto the desktop.

If you haven't already, :ref:`initialize SPARTA <introduction>` from the Terminal.

If all the :ref:`dependencies <install-dependencies>` are met, SPARTA will pause and prompt
the user::

    Is the RNAseq data in a folder on the Desktop? (Y or N):
    
Type::

    Y
    
Hit Enter/Return

.. note:: SPARTA assumes the data is located in a folder on the desktop by default. It is easiest if all future analyses have the data in a folder (WITHOUT SPACES IN THE NAME) on the desktop.
 
Now it will prompt the user for the name of the folder::

    What is the name of the folder on the Desktop containing the RNAseq data?:
    
Type::
    
    ExampleData
    
This is the name of the folder on the desktop that contains the input example data.
Hit Enter/Return.
From here, the software will trim, QC, align, and count transcript abundance for each sample.
All output/analyses are put in a folder that SPARTA generates on the desktop called "RNAseq_Data".
Within this folder are separate folders for each SPARTA run that are denoted by the date (e.g. 2015-06-04).
Within these folders are four more folders that separate each step of the analysis and are
called: 1) QC, 2) Bowtie, 3) HTSeq, and 4) DEanalysis.

Once the trimming, QC, alignment, and counting are complete, SPARTA will again pause and prompt
the user for how many experimental conditions exist within the analysis.

The output at this point will look like this:

.. image:: conditionoutput.jpg
	:align: center
	:height: 300 px
	:width: 500 px
	:alt: Condition output
	
At the prompt that says::

    How many conditions are there?:
    
Type::

    4
    
Hit Enter/Return.
There are 4 experimental conditions that we are considering:

#. Glycerol pH 7.0
#. Glycerol pH 5.7
#. Pyruvate pH 7.0
#. Pyruvate pH 5.7

Each condition has 2 replicates. The next prompt will read::

    Enter the relevant file names, based on the names given in 'SPARTA has these files', with the replicates separated by a comma.
    As an example, please see the 'conditions_input_example.txt' in the DEanalysis folder.
    Once you have entered the file names, hit Enter/Return:
    
At this point, we need to edit a text file (conditions_input.txt) to tell SPARTA which file belongs to a given condition.
To do this:

#. Navigate to the SPARTA output folder called RNAseq_Data located on the desktop
#. Go to the current run folder (will be the last folder listed if sorted by name)
#. Go into the DEanalysis folder
#. Open the conditions_input.txt file in a text editor (NOT MICROSOFT WORD) such as TextEdit

The number of experimental conditions listed are based on the number entered at the prompt
asking "How many conditions are there?:". Thus, in our case, there are 4. The contents of
the file will look like::

    Reference_Condition_Files:
    Experimental_Condition_2_Files:
    Experimental_Condition_3_Files:
    Experimental_Condition_4_Files:
    
We now need to enter the file names of the replicates in each condition. These are comma-separated
file names that correspond to the output given by SPARTA (denoted with red bracket)

.. image:: conditionoutputhighlight.jpg
	:align: center
	:height: 300 px
	:width: 400 px
	:alt: Condition output highlighted
	
.. note:: The file names are case-sensitive and must be spelled *exactly* as listed in the output given by SPARTA

Thus, when all the file names are inputed, the conditions_input.txt file should look like this::

    Reference_Condition_Files: mapgly7a.sam, mapgly7b.sam
    Experimental_Condition_2_Files:mapgly5a.sam, mapgly5b.sam
    Experimental_Condition_3_Files:mappyr7a.sam, mappyr7b.sam
    Experimental_Condition_4_Files:mappyr5a.sam, mappyr5b.sam
	
Now, save the changes by going to File -> Save.
Go back to the terminal and hit Enter/Return. From here, the workflow will perform the differential
gene expression analysis through edgeR. If a batch effect may be present, the output will attempt to 
warn the user of the potential, unintended variable that *must* be accounted for before drawing
experimental conclusions.

All the differential gene expression output is located in the RNAseq_Data -> date of your current run -> DEanalysis
folder. The file output includes:

#. Differential gene expression tables
#. MDS plot (somewhat analogous to a principle component analysis plot) which will show whether your replicates group together and treatment groups separate based on the treatment
#. BCV plot (biological coefficient of variation) to look at gene level variation between samples

Congratulations! You've analyzed RNA-seq data from raw reads to differential gene expression!

.. _analyzing-your-data:

Analyzing Your Data
-------------------

If you haven't already, we recommend working through the :ref:`example data analysis <analyzing-example-data>`
first before attempting to work through your own data set to familiarize yourself with the
workflow.

As stated in the :ref:`introduction`, SPARTA expects either compressed (.gz) or uncompressed FASTQ files (.fq or .fastq) as input,
with a reference genome file in FASTA format and a genome feature file (.gtf) within the folder
that contains the input data on your desktop. To see an example of appropriate input data, look inside the
ExampleData folder within the SPARTA_Mac-master folder.

Now, to analyze your own data, follow the steps to :ref:`initialize SPARTA <initializing-sparta>`,
and start the analysis!

If you would like to tweak the analysis options for a given step/tool, have a look at the
:ref:`altering-workflow-execution-options`.

.. _identifying-potential-batch-effects:

Identifying Potential Batch Effects
-----------------------------------

Batch effects can be a source of variation in RNA-seq data that can confound biological conclusions. 
In fact, there have been documented cases of batch effects present in published studies that led
readers to be concerned for the validity of the results.

To quote a previously published paper in `Nature Reviews Genetics <http://www.nature.com/nrg/journal/v11/n10/full/nrg2825.html>`_,
"Batch effects are sub-groups of measurements that have qualitatively different behaviour across conditions and are unrelated
to the biological or scientific variables in a study. For example, batch effects may occur if a subset of experiments was run on 
Monday and another set on Tuesday, if two technicians were responsible for different subsets of the experiments or if two different 
lots of reagents, chips or instruments were used." 

Thus, it is paramount that one address batch effects within their data before drawing biological
conclusions from a specific RNA-seq experiment. To illustrate what a batch effect may look
like within the data, we will utilize several different plots.

This first plot comes from the `Nature Reviews Genetics <http://www.nature.com/nrg/journal/v11/n10/full/nrg2825.html>`_
paper where they examine Affymetrix data from a `published bladder cancer study <http://cancerres.aacrjournals.org/content/64/11/4040.long>`_. 
You can quickly see that panels C and D from Figure 1 show that samples from batch 1 (blue)
cluster together based on gene expression and samples from batch 2 (orange) cluster together.

.. image:: batchexample.jpg
	:align: center
	:height: 300 px
	:width: 500 px
	:alt: Batch effect example
	
Within RNA-seq data, using SPARTA and the MDS plot generated by edgeR, another example of
batch effects within a study comparing *Mycobacterium tuberculosis* treated with a compound, we can clearly
see that the mock-treated samples (DMSO) and compound-treated samples (ETZ) separate based on batch (A vs B)
instead of by treatment. Ideally, we would have the samples group together based on treatment
as opposed to batch.

.. image:: batcheffect.jpg
	:align: center
	:height: 300 px
	:width: 500 px
	:alt: Batch effect example in RNA-seq data
	
If a potential batch effect is detected in the data set, SPARTA will output a message into
the terminal that says::

    IMPORTANT! YOU MAY HAVE A BATCH EFFECT! PLEASE LOOK AT THE MDS PLOT!
    
If this occurs, have a look at the MDS plot in the RNAseq_Data folder -> date of current run -> DEanalysis folder -> MDSplot.png

From here, you will want to adjust your model to account for the batch effect. Within edgeR, this can be
accomplished through an additive linear model. The documentation for edgeR contains a tutorial on
how to deal with batch effects that can be found `here <http://bioconductor.org/packages/release/bioc/vignettes/edgeR/inst/doc/edgeRUsersGuide.pdf>`_.

Future implementations of SPARTA will include the ability to adjust for batch effects. 

.. _altering-workflow-execution-options:

Altering Workflow Execution Options
-----------------------------------

SPARTA is capable of allowing the user to alter the parameters associated with each analysis
step to be tailored to specific use cases. Below are the different parameters that can be altered
and their usage.

Options::

  Usage: python SPARTA.py [options]

	Simple Program for Automated reference-based bacterial RNA-seq Transcriptome
	Analysis (SPARTA)

  -h, --help            show this help message and exit
  --cleanup             Clean up the intermediate files to save space. Default
                        action is to retain the intermediate files.
  --verbose             Display more output for each step of the analysis.
  --noninteractive      Non-interactive mode. This is for running SPARTA
                        without any user input. Assumes data is on the
                        desktop. If this option is specified, you must fill
                        out the configuration file (ConfigFile.txt) with the
                        appropriate experimental conditions in the SPARTA
                        folder.
  --threads=THREADS     Define the number of threads that SPARTA should run
                        with. This will enable some speed-up on multi-
                        processor machines. As a generality, define the number
                        of threads as the same number of cores in your
                        computer. Default is 2.

  Trimmomatic options:
    The order the options will be run are: ILLUMINACLIP, LEADING,
    TRAILING, SLIDINGWINDOW, MINLEN

    --clip=ILLUMINACLIP
                        ILLUMINACLIP options. MiSeq & HiSeq usually
                        TruSeq3.fa; GAII usually TruSeq2.fa. Default is
                        ILLUMINACLIP:TruSeq3-SE.fa:2:30:10. Usage:
                        --clip=<adapterseqs>:<seed mismatches>:<palindrome
                        clip threshold>:<simple clip threshold>
    --lead=LEADING      Set the minimun quality required to keep a base.
                        Default is LEADING=3. Usage: --lead=<quality>
    --trail=TRAILING    Set the minimum quality required to keep a base.
                        Default is TRAILING=3. Usage: --trail=<quality>
    --slidewin=SLIDINGWINDOW
                        SLIDINGWINDOW options. Default is SLIDINGWINDOW:4:15.
                        Usage: --slidewin=<window_size>:<required_quality>
    --minlentrim=MINLENTRIM
                        Set the minimum read length to keep in base pairs.
                        Default is 36. Usage: --minlentrim=<readlength>

  Bowtie options:
    --mismatch=MISMATCH
                        Output alignments with at most a defined number of
                        mismatches. Usage: --mismatch=<integer_value>
    --otherbowtieoptions=OTHERBOWTIEOPTIONS
                        Bowtie has so many options that it is not worth
                        listing them here. Go to http://bowtie-
                        bio.sourceforge.net/manual.shtml#command-line for the
                        manual and all available options. Usage:
                        --otherbowtieoptions='all options inputed as a string
                        (note the quotes!)'

  HTSeq options:
    --stranded=STRANDED
                        Stranded options: yes, no, reverse. Default is
                        --stranded=reverse. Usage: --stranded=yes/no/reverse
    --order=ORDER       Order options: name, pos. Usage: --order=name/pos.
    --minqual=MINQUAL   Skip all reads with quality lower than the given
                        value. Default is --minqual=10. Usage:
                        --minqual=<value>
    --type=TYPE         The feature type (3rd column in GTF file) to be used.
                        Default is --type=exon (suitable for RNA-seq analysis)
    --idattr=IDATTR     Feature ID from the GTF file to identify counts in the
                        output table Default is --idattr=gene_id. Usage:
                        --idattr=<id attribute>
    --mode=MODE         Mode to handle reads overlapping more than one
                        feature. Default is --mode=union. Usage: --mode=union
                        /intersection-strict/intersection-nonempty
