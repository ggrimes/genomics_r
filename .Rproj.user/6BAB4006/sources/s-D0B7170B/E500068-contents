# Aggregating and Analyzing Data with dplyr

install.packages("dplyr") ## install
library("dplyr")          ## load

# Here we’re going to cover 6 of the most commonly used functions as well as using pipes (%>%) to combine them.
# 
# select()
# filter()
# group_by()
# summarize()
# mutate()


# Tibble
variants_tbl <- readr::read_csv("rawdata/combined_tidy_vcf.csv")
variants_tbl<-as_tibble(variants)


#Selecting columns and filtering rows
# select sample_id, REF, ALT, DP from varaints df
select(variants_tbl, sample_id, REF, ALT, DP)

#To select all columns except certain ones, put a “-“ in front of the variable to exclude it.
#select all but CHROM column
select(variants_tbl, -CHROM)

#dplyr also provides useful functions to select columns based on their names. For instance, ends_with()
# select columns that end with B
select(variants_tbl, ends_with("B")) %>% 


# To choose rows, we can use filter(). 
# For instance, to keep the rows for the sample_id SRR2584863:
filter(variants_tbl,sample_id=="SRR2584863")

#Note that this is equivalent to the base R code below, but is easier to read!
variants[variants_tbl$sample_id == "SRR2584863",]

#filter() will keep all the rows that match the conditions that are provided. 
#Here are a few examples:

## rows for which the reference genome has T or G 
filter(variants_tbl, REF %in% c("T", "G")) %>% 

## rows with QUAL values greater than or equal to 100
filter(variants_tbl, QUAL >= 100)

## rows that have TRUE in the column INDEL
filter


# Pipes

# %>% 

#

variants_tbl %>%
  filter(sample_id == "SRR2584863") %>%
  select(REF, ALT, DP)

#we want to create a new object with this smaller version of the data we can do so by assigning it a new name:
SRR2584863_variants <- variants_tbl %>%
  filter(sample_id == "SRR2584863") %>%
  select(REF, ALT, DP)

SRR2584863_variants

###########Exercise##################
#Starting with the variants dataframe, 
#use pipes to subset the data to include only observations from SRR2584863 sample, 
#where the filtered depth (DP) is at least 10. Retain only the columns REF, ALT, and POS.
###########Exercise##################


# Mutate

#We have a column titled “QUAL”. 
#This is a Phred-scaled confidence score that a polymorphism exists at this position given 
#the sequencing data. Lower QUAL scores indicate low probability of a polymorphism existing at that site.
#We can convert the confidence value QUAL to a probability value according to the formula:
  
#  Probability = 1- 10 ^ -(QUAL/10)

Let’s add a column (POLPROB) to our variants dataframe that shows the probability of a polymorphism at that site given the data. We’ll show only the first six rows of data.
#adding a column using dplyr

variants %>%
  mutate(POLPROB = 1 - (10 ^ -(QUAL/10)))

############Exercise##################
#There are a lot of columns in our dataset, so let’s just look at the sample_id, POS, QUAL, and POLPROB columns for now.
#Add a line to the above code to only show those columns.
#####################################







#Let’s create a new column, called “indel_size” that contains the size difference between the our sequences and the reference genome. 
#The function, nchar() returns the number of letters in a string.

variants %>%
  mutate(indel_size = nchar(ALT) - nchar(REF))


variants_indel <- variants_tbl %>%
  mutate(
    indel_size = nchar(ALT) - nchar(REF),
    mutation_type = case_when(
      indel_size > 0 ~ "insertion",
      indel_size < 0 ~ "deletion",
      indel_size == 0 ~ "point"
    ))


# Split-apply-combine data analysis and the summarize() function
#Many data analysis tasks can be approached using the “split-apply-combine” paradigm: 
# split the data into groups, apply some analysis to each group, and then combine the results. dplyr makes 
# this very easy through the use of the 
#group_by() function, which splits the data into groups. 
# When the data is grouped in this way summarize() can be used to collapse each group into a single-row summary. 
# summarize() 
#does this by applying an aggregating or summary function to each group.
# 
# For example, if we wanted to group by mutation_type and find the average size for the insertions and deletions:
variants_indel %>% 
  group_by(mutation_type) %>% 
  summarise(mean_size = mean(indel_size))

#So to view the lowest and highest filtered depth (DP) for each sample:
variants_indel %>%
  group_by(sample_id) %>%
  summarize(min(DP),max(DP))


It is often useful to calculate how many observations are present in each group. 
The function n() helps you do that:


  
    
  variants_indel %>%
  group_by(mutation_type) %>%
  summarize(
    n = n()
  )