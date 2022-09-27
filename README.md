# genomics_r

R Programming for biologist

# Setup on Noteable service

The R for genomics course will use University Noteable service for course work and it is vital that you check it works before attending the course.

<https://www.ed.ac.uk/information-services/learning-technology/noteable/accessing-noteable>

You will need to use the direct login account for the course. This uses your university username (uun) and password.

[https://noteable.edina.ac.uk/login](https://noteable.edina.ac.uk/launch/)

## From noteable

within R console

    #install.packages("xfun_0.16.tar.gz",repos=null)
    install.packages("xfun",repos="http://cran.rstudio.com")
    install.packages("swirl",repos="http://cran.rstudio.com")
    #swirl::install_course("R Programming")
    swirl::install_course("Getting and Cleaning Data")
    swirl::install_course("Exploratory_Data_Analysis")

## Download swirl package

<https://cran.r-project.org/src/contrib/swirl_2.4.5.tar.gz>

### Download course files

Download the three course files below

<https://github.com/swirldev/swirl_courseshttp://swirlstats.com/scn/Exploratory_Data_Analysis.swc> <http://swirlstats.com/scn/R_Programming.swc> <http://swirlstats.com/scn/Exploratory_Data_Analysis.swc>

Upload packages and swc files to noteable service.

Within RStudio run

    install.packages("swirl/swirl_2.4.5.tar.gz",repos=NULL)
    library("swirl")
    install_course(swc_path = "swirl/R_Programming.swc")
