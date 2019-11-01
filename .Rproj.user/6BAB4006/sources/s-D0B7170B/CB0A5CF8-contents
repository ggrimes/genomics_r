# R Basics continued - factors and data frames

# Working with spreadsheets (tabular data)

#Importing tabular data into R

#There are several ways to import data into R. 
#For our purpose here, we will focus on using the tools every R installation comes with (so called “base” R) 
#to import a comma-delimited file containing the results of our variant calling workflow. 
#We will need to load the sheet using a function called read.csv().

?read.csv()

#Now, let’s read in the file combined_tidy_vcf.csv 
## read in a CSV file and save it as 'variants'
variants <- read.csv("rawdata/combined_tidy_vcf.csv")
#?View(variants)
View(variants)
# Summarizing and determining the structure of a data frame.
# A data frame is the standard way in R to store tabular data. 
# A data fame could also be thought of as a collection of vectors, all of which have the same length. 
# Using only two functions, we can learn a lot about out data frame 
# including some summary statistics as well as well as the “structure” of the data frame. 
# Let’s examine what each of these functions can tell us:
summary(variants)

#skim it
skimr::skim(variants)

#before we operate on the data, we also need to know a little more about the data frame structure 
#to do that we use the str() function:
str(variants)


# Introducing Factors
#Factors are the final major data structure we will introduce in our R genomics lessons. 
#Factors can be thought of as vectors which are specialized for categorical data.

## subset the "REF" column to a new object
REF <- variants$REF

# Let’s look at the first few items in our factor using head():
head(REF)
str(REF)


# Plotting

#One of the most common uses for factors will be when you plot categorical values. 
#For example, suppose we want to know how many of our variants had each possible nucleotide 
#(or nucleotide combination) in the reference genome? We could generate a plot:

plot(REF)
#extra forcats

plot(forcats::fct_lump(REF,n=4))


## Subsetting data frames
#Next, we are going to talk about how you can get specific values from data frames, 
#and where necessary, change the mode of a column of values.

#The subsetting notation is very similar to what we learned for vectors. The key differences include:

#Typically provide two values separated by commas: data.frame[row, column]

variants[1,1]
#In cases where you are taking a continuous range of numbers use a colon between the numbers (start:stop, inclusive)
variants[1:5,1:5]

#For a non continuous set of numbers, pass a vector using c()
variants[c(1,4,9),1:5]

#Index using the name of a column(s) by passing them as vectors using c()
variants[1:5,c("POS")]

#Finally, in all of the subsetting exercises above, we printed values to the screen. Y
#ou can create a new data frame object by assigning them to a new object name

# create a new data frame from variants obkect containing only observations from sample_id SRR2584863 
SRR2584863_variants <-variants[variants$sample_id=="SRR2584863",]

# check the dimension of the data frame ?dim()
dim(SRR2584863_variants)

## get a summary of the data frame ?summary()
summary(SRR2584863_variants)

#coercion
#StringsAsFactors = FALSE

#Data frame bonus material: math, sorting, renaming
#You can use functions like mean(), min(), max() on an individual column.
max(variants$DP)

#You can sort a data frame using the order() function:
sorted_by_DP <- variants[order(variants$DP), ]
head(sorted_by_DP$DP)

#You can rename columns: ?colnames
colnames(variants)[colnames(variants) == "sample_id"] <- "strain"

# check the column name (hint names are returned as a vector)
colnames(variants)


# Saving your data frame to a file
#?write.csv()
#?file.path()
write.csv(x = SRR2584863_variants, file = file.path("data","SRR2584863_variants.csv"))




# Key Points

# It is easy to import data into R from tabular formats including Excel. 
# However, you still need to check that R has imported and interpreted your data correctly

#There are best practices for organizing your data (keeping it tidy) and R is great for this
#Base R has many useful functions for manipulating your data, 
#but all of R’s capabilities are greatly enhanced by software packages developed by the community


# Swirl exercises data frames and factors