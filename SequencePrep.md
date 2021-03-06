# Great Apes Sequence Prep  

Sequences will be extracted from NCBI using BLAST. 

The BioProject SRA data for the Great Apes project: https://www.ncbi.nlm.nih.gov/sra?linkname=bioproject_sra_all&from_uid=189439

Great Apes Project website: http://biologiaevolutiva.org/greatape/data.html

### BLAST conditions: 

What was the query sequence? 

Are we using other sequences as well? 

Blast version?  

Reference? 


Download all hits in fasta format. 

Download HIT table for information on start and end position of match with query sequence. 

This is saved independently for each run. There are multiple runs per individual. 


## Sequence alignments and choosing loci

The first thing we need to figure out is where we're making cut-offs for different loci. 

Look at the distribution of start and end points for all the data. 

I'm going to import all the data into R, and then draw a histogram of all the sequence start points. 

Open R in the folder with all the data. On my computer this is here: 

/Users/alexjvr/2018.postdoc/GorillaMSc_201807
```
R version 3.5.0

Dian.data <- read.csv("DianSRX243537.csv", header=T) # import the csv file into R. I've added a row with headers at the top of this HIT file. If this isn't there, you can say header=F. 

## let's first look at what the data looks like. For some of the sequences only a short fragment matched the query sequence
hist(Dian.data$alignmentLength) ## We probably want to exclude all the shorter reads. This represents quite a small amount of the data anyway. 

Dian.data1 <- Dian.data[Dian.data$alignmentLength > 89,]  ## this function subsets the original dataset and writes it to a new one. There are various was to do this. You can google for other options of you like. The comma at the end tells R to write all of the columns to the new file. 

summary(Dian.data1$alignmentLength) ## Check that the function has worked

hist(Dian.data1$StartQuery, breaks=20)  # hist is the function to draw a histogram. Breaks is a way of binning the data. The more breaks, the smaller the bins. Call the column you want to plot by referring to the data and then the specifying the column ($). 

# to save any graphs or tables to pdf you can do the following
pdf("Figurename.pdf") ## give the pdf a name. Remember the extension. You can write to a bunch of different formats using the same syntax: https://www.statmethods.net/interface/io.html

hist(Dian.data1$StartQuery, breaks=20) ## all the code for the figure. This is just some simple code, but often these can have a lot more lines of code. 

dev.off() ## signals the end of the pdf file, and that it should be written to file. It will be saved in the folder where you're working, unless you change the path. 
```

Google any questions. Usually the top hits will be helpful, particularly on [R-bloggers](https://www.r-bloggers.com/basics-of-histograms/) and [Stackoverflow](https://stackoverflow.com/questions/16931895/exact-number-of-bins-in-histogram-in-r). 

Similarly, you can google anything to do with github and coding in github markdown. You can't break anything, so don't be afraid to try things! 


If you want to add figures onto the github page, open an issue (see above). Just click on the issue tab (open in a new window). Start a new issue and name it e.g. greatApesFigures.md (remember the .md makes it a markdown file). 

Now upload the image you've saved (or taken a screenshot of). I usually label them. e.g. ## Figure 1 Distribution of read lengths.

Once that's uploaded, you can copy the link (http:....) and paste it here in the following format: 

```
![alt_txt][YourFigureName]

[YourFigureNamy]:http:....

```







