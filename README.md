
# COSMIC SigProfiler Tools for Single base substitution identification

This Brief description is for the researchers with minimal knowledge about Python 
but want to take advantage of the COSMIC SigProfiler tools to identify genetic signatures 
and create a representative decomposition chart to present.

I have made a Youtube video to help you with the process: 




## Acknowledgements

 - This description is based on the COSMIC SigProfiler tools developed by UCSD AlexandrovLab.
 Link: https://github.com/AlexandrovLab/SigProfilerExtractor
##  Primary Programming Tool
Python3

Recommendations: This tool is much simpler if run on Mac OS Terminal compared to Windows Command Prompt.
## Sample Input

In order for this tool to run smoothly, please strictly follow the format of this sample file. 
The Tool will be able to process VCF files but txt is always recommened for beginners due to its 
simplicity(if your original file is in CSV or excel format, you can use a free online converter to convert it to a txt file).

 ![ezgif com-gif-maker](https://user-images.githubusercontent.com/94341094/141750685-cfb173df-dbeb-4d7e-86b0-aa5b7d8e8c10.gif)

## Sample Output
![SBS1536_Decomposition_Plots-page-0](https://user-images.githubusercontent.com/94341094/141750105-08c56fde-0276-46b7-a3c3-ebb860b389b3.gif)



## How to Download the tool
Open Terminal on your Computer(This Tools does not need to be run on a IDE like pycharm)

You would need to use both the matrixGenerator and the Extractor to get the full results.
1. Make sure your python version is newer than python3.4 (if you are using a mac and never used terminal before, you will not have Python3 installed because the default version of the OS is Python2). 
The best way to check your python3 version would be using the command:

    python3
If this command does not show version information or shows a python3 version older than python3.4, then you will have to manually install python3 and add it to path. I know it sounds scary but trust me it is very easy. Here is a link that teaches you how to do that:
   https://www.youtube.com/watch?v=XF_rklW9XkU 

2.  install SigProfilerMatrixGenerator 
        
         pip install SigProfilerMatrixGenerator
3.  Install SigProfiler Extractor
        
        pip install SigProfilerExtractor

4.  install the desired reference genome. Here I am using GRCH37/hg19 (make sure you run these command one by one, not all together)
 
        python3

        from SigProfilerMatrixGenerator import install as genInstall

        genInstall.install('GRCh37')

Now you have both tools and the reference genome installed! You can proceed to using the tools to generate Matrix and Extractor results now!


## Using Matrix generator

in order for the extractor to work, you will need to generate a readable matrix. The steps here will help you accomplish that by using the SigProfiler Matrixgenerator tool. 

    python3

    from SigProfilerMatrixGenerator.scripts import SigProfilerMatrixGeneratorFunc as matGen

    matrices = matGen.SigProfilerMatrixGeneratorFunc("Alzheimers","GRCh37","/Users/shaoyizhang/Desktop/DNV2",exome=False, bed_file=None, chrom_based=False, plot=True, tsb_stat=False, seqInfo=True)

The third line is where most people start to get confused. "Alzheimers" is the name is have given to my results, "GRCh37" is the reference genome I am using, "/Users/shaoyizhang/Desktop/DNV2" is the path to my txt (you will have to create a folder on your desktop, in that folder you will create another folder and name it "input", and you will put the txt file in to the "input" folder. In my example DNV2 is the name of the first file I created, after that the tool will automatically look for your "input" file and the txt in it).

After you have successfully run the MatrixGenerator, you will be able to see an automatically generated "output" folder and a "log" folder. You can ignore the log file and go straight to the output file. In that file you will be able to see a plot file and a SBS file. If you found everything you need in the PLOT file then you will not need to use the extractor tool anymore. But if you want to get the extraction results and the decomposition file you will proceed to the next step.

## Using Extractor Tool

Before you proceed, please make sure you have already completed the step using Maxtrix Generator, because Extractor tool will only read data from the Maxtrix Generator.

      python3

      from SigProfilerExtractor import sigpro as sig

      sig.sigProfilerExtractor("matrix","Alzheimers","/Users/shaoyizhang/Desktop/DNV2/output/SBS/Alzheimers.SBS1536.all",reference_genome="GRCh37",minimum_signatures=1,maximum_signatures=10,nmf_replicates=100,cpu=-1)

Again, please run the three line separately. The first two lines you can copy and paste directly into your terminal. But for the third line, you would have to change the path and reference genome. In my example, the path included is where your matrix generator results are located. The fastest way to get the path to your matrix generator result is to go to the folder you created earlier - output - SBS. In there you will find multiple matrix generated files. You can pick one of them and drag them directly to a new terminal, the terminal will print the results immediately -  Then you can copy and paste the path to your code. 

The results will be generated in your user folder. You can go to "your disk" - Users - "yourname". In this folder you will be able to find a folder named "results". 

Congratulations! You will find all the decomposition plots and information files in the result folder!
## Reading the results

The COSMIC team at Alexandrov lab made a comprehensive tutorial on how to find and read the results. 
Youtube link: https://www.youtube.com/watch?v=BchtNeaQlv0
