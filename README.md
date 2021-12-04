# bio-rad_take_home
This repo contains a project for BIO-RAD.

Assignment: Multiplet sequencing datasets

Attached in the folder are two files
Count_matrix.csv
Peak_names_out.csv

In this dataset, human (hg19) and mount (mm10) cells were mixed together and a single cell sequencing experiment was run. The goal of this experiment was to determine how often droplets are loaded with more than one cell. Each barcode, or column, in the “count matrix” represents a droplet which was loaded with cells. Rows are genes identified by RNA sequencing. 

Questions:
1) Summarize this dataset. How many droplets can you identify that are loaded with more than one cell? Distinguish between Human/Human, Mouse/Human, or Mouse/Mouse multiplets.

2) Write an R script which takes the two files attached as arguments and returns summary plots as a pdf file and a csv report for the number of droplets with 1 or 2+ cells identified.

3) Provide proper documentation, consider common user errors and provide meaningful error messages in return.



## EDIT
The original count_matrix.csv takes up 2.7 GB and was too large for my computer to process. I had to subset the data into smaller chunks, filter out genes that show up in < 1% of droplets, then bind the subsets back together. I call this filtered matrix "count_tbl_filt.csv", which takes up 1.3 GB and can be processed with "bio-rad.Rmd" on my 16 GB Ram 2019 MacBook Air. To see how I performed the initial filtering, view the code chunks at the top part of "bio-rad.Rmd" that have been commented out. The PDF report "bio-rad_report.pdf" begins with "count_tbl_filt.csv" and does not show the initial filtering steps. You'll notice I immediately remove large objects, using rm(), that are no longer necessary for downstream analysis. That was necessary for me to execute the full script, but might be unnecessary on better machines. 

## INSTALL LIBRARIES
Before running script, install the following R libraries. 

- install.packages("tidyverse")
- install.packages("data.table")
- install.packages("here")
- install.packages("gridExtra")
- install.packages("gt")
- install.packages("ggtext")
- install.packages("ggdark")
- install.packages("rmarkdown")
- install.packages("utils") 

## COMMAND LINE
Clone this repo, and request the file "count_tbl_filt.csv" from me. Place "count_tbl_filt.csv" into the "data" folder. "bio-rad.Rmd" and "data" folder should be located in the same folder. 

Substituting in your path, enter the following code at the command line. 

Rscript -e "rmarkdown::render('{local_path}/bio-rad.Rmd', output_file='bio-rad_report.pdf')"

Example:

Rscript -e "rmarkdown::render('~/Documents/R/bio-rad_take_home/bio-rad.Rmd', output_file='bio-rad_report.pdf')"

As long as the .Rmd file is in the same folder as the "data" folder that contains the count data "count_tbl_filt.csv", the "bio-rad_report.pdf" will be produced and located next to the .Rmd file. Two summary tables, "count_tbl_summary.csv" and "droplet_content_summary.csv" will also be written into the "data" folder, keeping everything well organized.  
