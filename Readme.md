# Details #

Google code does not allow uploading files anymore.
we therefore made all our files and data and Matlab code available through through the following links:

eelhaik.aravindachakravartilab.org/files/MethylationPredictor\_Scripts.zip
eelhaik.aravindachakravartilab.org/files/MethylationPredictor\_Data.zip


## Instructions ##
After obtaining data for gene expression we were able to calculate for each rice gene the GC3, GE, CV etc.
the results of this analysis are in the file:rice4reg\_grad\_no\_header.txt.
This file contains for each rice gene, the average methylation obtained by bisulfite sequencing (this is what we try to predict), and 9 other measures,
most importantly for our work the gene expression CV in the 6th column.

Next, for each gene we used the sequence data to calculate the frequency of sixmers (6 base pairs in overlapping windows).
The results were summarized in a file such as: **sixmer\_num\_short.txt** that has the gene ID, sixmer ID, number of sixmers in gene, and gene code.
01301019 113243 1 429
01301019 113321 1 429

Such file will be very large, and you can find and example for such file in **\Sixmers\sixmer\_short\_num.txt**.
I found it easier to create for each gene a separate file with the number of each sixmer that exists in this gene (e.g., **\Sixmers\1301060.txt**) and then it has only 2 columns:
sixmer ID, number of sixmers in gene
111113	 1
111121	 1

Next, you will need to calculate the CV for each sixmer type.
The file Process6Mers\_multiple.m does that and outputs the file **rice4reg\_grad\_Results.txt** which has for each sixmer type (out of posible 4096), the mean methylation
(calculated from the data that we are trying to predict) and other properties, including the one of interest CV, which is in the 6th column.

Finally, all you have to do is for each gene of interest, load the file with the sixmer counts per gene (e.g., **1301040.txt**) and obtain the CV for each sixmer type (from **rice4reg\_grad\_Results.txt**)
and using our equations Eq. 3 and Eq. 4 - calculate the predicted methylation. This is done using **PredictMethylationLevels.m**.

## Database files ##
**rice4reg\_grad\_Results.txt** - for each sixmer, (sixmer _GC3	MEAN	STDEV	CV	GEN\_SIG	GCL	GCM	GCR	LENGTH	GRADLM	GRADMR)_

**rice4reg\_grad\_no\_header.txt and rice4reg\_grad\_header.txt**- for each rice gene it has (LOCUS\_ID	AVG\_MET	GC3	MEAN	STDEV	CV	GEN\_SIG	GCL	GCM	GCR	LENGTH	GRADLM	GRADMR)

**\Sixmers\sixmer\_num\_short.txt** - example of a file that lists the sixmers in each rice gene [locus\_ID, sixmer type, count per gene, gene ID].

**\Sixmers\other files** - same information as before, but 1 file per 1 gene so only 2 columns are included [type, count per gene](sixmer.md).

## Scripts ##
**Process6Mers\_multiple.m** - Reads the rice data and sixmers frequency in each gene. Produces **rice4reg\_grad\_Results.txt** with the mean attributes for each sixmer.

**PredictMethylationLevels.m** - Predicts methylation leveles.