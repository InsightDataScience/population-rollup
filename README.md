

## Table of Contents
1. [Problem](README.md#problem)
1. [Steps to submit your solution](README.md#steps-to-submit-your-solution)
1. [Input Dataset](README.md#input-dataset)
1. [Expected output](README.md#expected-output)
1. [Instructions](README.md#instructions)
1. [Tips on getting an interview](README.md#tips-on-getting-an-interview)
1. [Repo directory structure](README.md#repo-directory-structure)
1. [Testing your code](README.md#testing-your-code)
1. [Questions?](README.md#questions?)

## Problem
  
The federal Census produces a plethora of datasets on a variety of topics tabulated in a number of different ways. In particular, the Census is known for population counts, including down to census tracts, or relatively small areas that average 4,000 inhabitants. Data at that detailed level is useful, but sometimes it's also helpful to roll up some of the information.

**For this challenge, we want you to take the [2000 to 2010 Census Tract Population Change](https://www.census.gov/data/tables/time-series/dec/metro-micro/tract-change-00-10.html) dataset, perform a few calculations and then write out a new file with the summarized data.


## Steps to submit your solution

* To submit your entry, use the link you received in your coding challenge invite email
* Do NOT attach a file - we will not accept solutions with attached files
* Do NOT send your solution over an email - We are unable to accept coding challenges that way
* To see whether your code will pass at least one key test on our system (do this prior to submission), use this page: https://insight-cc-submission.com/test-my-repo-link and choose 'Population Roll-up' in the challenge dropdown

### Creating private repositories
To avoid plagiarism and wrongdoing, we request you submit a private repository of your code, and then invite us to collaborate prior to submitting your solution. Both GitHub and Bitbucket offer free private repositories at no extra cost.
* Create a private repository on GitHub or Bitbucket with the directory structure detailed [below](README.md#repo-directory-structure)
* Add "insight-cc-bot" (or cc@insightdataengineering.com on Bitbucket) as a collaborator in your project
  * [How to add collaborators on GitHub?](https://help.github.com/articles/inviting-collaborators-to-a-personal-repository/)
  * [How to add users and groups as collaborators in Bitbucket?](https://confluence.atlassian.com/bitbucket/grant-repository-access-to-users-and-groups-221449716.html)
* **We will NOT be grading submissions we do not have access to.**

### Submitting a link to your repository
* Provide a link to the specific repo for this project, not your general profile
* Exactly follow the directory structure [detailed](README.md#repo-directory-structure) in this Readme, especially providing a 'run.sh' shell script that executes your code
* Put any comments in the README file of your project repo

## Input dataset
For this challenge, when we grade your submission, an input file, `censustract-00-10.csv`, will be moved to the top-most `input` directory of your repository. Your code must read that input file, process it and write the results to an output file, `report.csv` that your code must place in the top-most `output` directory of your repository.

Below is a sample `censustract-00-10.csv` file: 
```
GEOID,ST10,COU10,TRACT10,AREAL10,AREAW10,CSA09,CBSA09,CBSA_T,MDIV09,CSI,COFLG,POP00,HU00,POP10,HU10,NPCHG,PPCHG,NHCHG,PHCHG
02130000100,02,130,000100,4835.518216,1793.906364,,28540,"Ketchikan, AK",,2,C,3801,1736,3484,1694,-317,-8.34,-42,-2.42
02130000200,02,130,000200,5.204047664,0.4525275793,,28540,"Ketchikan, AK",,2,C,4909,2156,4884,2179,-25,-0.51,23,1.07
02130000300,02,130,000300,2.771683112,0.4653222332,,28540,"Ketchikan, AK",,2,C,3054,1493,2841,1394,-213,-6.97,-99,-6.63
02130000400,02,130,000400,14.91968071,0.3246679135,,28540,"Ketchikan, AK",,2,C,2310,891,2268,899,-42,-1.82,8,0.90
48487950300,48,487,950300,933.9565129,6.998080686,,46900,"Vernon, TX",,2,C,2304,916,1849,892,-455,-19.75,-24,-2.62
48487950500,48,487,950500,13.21399173,0.01418539391,,46900,"Vernon, TX",,2,C,3172,1338,2955,1388,-217,-6.84,50,3.74
48487950600,48,487,950600,10.65575478,0,,46900,"Vernon, TX",,2,C,6022,2715,5994,2781,-28,-0.46,66,2.43
48487950700,48,487,950700,13.01780124,0.0371546123,,46900,"Vernon, TX",,2,C,3181,1409,2737,1257,-444,-13.96,-152,-10.79
```

Each line of the input file, except for the first-line header, represents population data for a census tract. Consult this [file layout document produced by the Census](https://www2.census.gov/programs-surveys/metro-micro/technical-documentation/file-layout/tract-change-00-10/censustract-00-10-layout.doc) for a description of each field.

The sample input file is taken from the data file at [2000 to 2010 Census Tract Population Change](https://www.census.gov/data/tables/time-series/dec/metro-micro/tract-change-00-10.html), which contains population counts for census tracts and how much they've changed over the decade. While census tracts are fairly small geographical areas inhabited by 1,200 to 8,000 people, they also can be grouped into larger Metropolitan and Micropolitan Statistical Areas called Core Based Statistical Areas. These core areas comprise a set of communities, often with a population center and shared economic and social ties. 

Metropolitan and Micropolitan statistical areas can span one or more counties and states. For instance, "New York-Northern New Jersey-Long Island, NY-NJ-PA" is a Metropolitan Statistical Area and Core Based Statistical Area that is centered around New York City, extends east through Long Island and west through northern New Jersey and parts of Pennsylvania.

For this challenge, we want to know for each Core Based Statistical Area, the 
* total number of census tracts, 
* total population in 2000, 
* total population in 2010 and 
* average population percent change for census tracts in this Core Based Statistical Area

Note that census tracts within a Core Based Statstical Area are not necessarily grouped together in the input file, and that there will be a small minority of census tracts that fall outside of any Core Based Statistical Area.

Finally, the Census provides the data in the form of an [Excel spreadsheet](http://www2.census.gov/programs-surveys/decennial/tables/time-series/tract-change-00-10/censustract-00-10.xlsx) but you can assume the input file we'll be using to test your code will be in the form of a comma-separated-value file (see [here](https://www2.census.gov/programs-surveys/metro-micro/technical-documentation/file-layout/tract-change-00-10/censustract-00-10-layout.doc) for more information on the data dictionary). If you are having difficulty converting the Excel spreadsheet into a CSV file, we've made the converted file available to you [here](https://drive.google.com/file/d/14O7dSplprnptDYkn1Jg4M1ojBIkVAsVP/view?usp=sharing).


## Expected output

After reading and processing the input file, your code should create an output file, `report.csv`, with as many lines as unique Core Based Statistical Areas found in the input file. If there are no core areas in the input file, your code should still create the `report.csv` file but it should contain no lines.

For every line that exists in the output file, the following fields should be written in this order:
* Core Based Statstical Area Code (i.e., CBSA09)
* Core Based Statistical Area Code Title (i.e., CBSA_T)
* total number of census tracts
* total population in the CBSA in 2000
* total population in the CBSA in 2010
* average population percent change for census tracts in this CBSA. Round to two decimal places using standard rounding conventions (i.e., Any percentage between 0.005% and 0.010%, inclusive, should round to 0.01% and anything less than 0.005% should round to 0.00%)

The lines in the output file should be sorted by Core Based Statstical Area Code (ascending)

Given the above `censustract-00-10.csv` input file, we'd expect an output file, `report.csv`, in the following format
```
28540,"Ketchikan, AK",4,14074,13477,-4.41
46900,"Vernon, TX",4,14679,13535,-10.25
```
Notice that Core Based Statistical Area Codes titles include a comma (`,`), so values for that field should be enclosed by double quotation marks (`"`). 

## Instructions
We designed this coding challenge to assess your coding skills, your understanding of computer science fundamentals and ability to program in a Linux environment. They are both prerequisites of becoming a data engineer. To solve this challenge you might pick a programing language of your choice (preferably Python, Scala, Java, or C/C++ because they are commonly used and will help us better assess you), but you are only allowed to use the default data structures that come with that programming language (you might use I/O libraries). For example, you can code in Python, but you should not use Pandas or any other external libraries (i.e., don't use Python modules that must be installed using 'pip').

The objective here is to see if you can implement the solution using basic data structure building blocks and software engineering best practices (by writing clean, modular, and well-tested code).

If you are chosen for an interview, you may be asked to think about ways this exercise could be expanded, such as identifying other, useful datasets that you could be joined with the data here and provide additional value.

## Tips on getting an interview
As a data engineer, it’s important that you write clean, well-documented code that scales for a large amount of data. For this reason, it’s important to ensure that your solution works well for a large number of records, rather than just for this example.

It's important to use software engineering best practices like unit tests, especially because data is not always clean and predictable.

Before submitting your solution you should summarize your approach and run instructions (if any) in your README.

You may write your solution in any mainstream programming language, such as C, C++, Go, Java, Python, Ruby, or Scala. Once completed, submit a link of your Github or Bitbucket repo with your source code.

In addition to the source code, the top-most directory of your repo must include the input and output directories, and a shell script named run.sh that compiles and runs the program(s) that implement(s) the required features.

See the figure below for the required structure of the top-most directory in your repo, or simply clone this repo.

## Repo directory structure
The top-level directory structure for your repo should look like the following: (So that we can grade your submission, replicate this directory structure at the top-most level of your project repository. Do not place the structure in a subdirectory)

    ├── README.md
    ├── run.sh
    ├── src
    │   └── population.py
    ├── input
    │   └── censustract-00-10.csv (your code should assume this input file exists but you do not need to check this file into your repository)
    ├── output
    |   └── report.csv (your code should produce this file but you do not need to check this file into your repository)
    ├── insight_testsuite
        └── tests
            └── test_1
            |   ├── input
            |   │   └── censustract-00-10.csv
            |   |__ output
            |   │   └── report.csv
            ├── your-own-test_1
                ├── input
                │   └── censustract-00-10.csv
                |── output
                    └── report.csv

**Don't fork this repo** and don't use this `README` instead of your own. The content of `src` does not need to be a single file called `population.py`, which is only an example. Instead, you should include your own source files and give them expressive names.

## Testing your code
As an engineer, you'll want to make sure you are thoroughly testing your code. Use the `insight_testsuite` directory to showcase the tests you conducted on your code. Under that directory, create a separate folder for each test. Each test directory should also have a separate `input` subdirectory containing the `censustract-00-10.csv` input file you want to test, and an `output` subdirectory containing the expected `report.csv` output for that test.

We've included one test (`test_1`), which contains the sample input and output files detailed in this Readme. To test your code, you can manually move each input test file into the top-level input directory, then run your program and compare the output with the expected output. Or you can write a script to do this automatically, but note we are not requiring you to write a test script.

We do ask that you test your code using the <a href="https://insight-cc-submission.com/test-my-repo-link">web page</a> mentioned earlier to ensure your code can run in the Linux environment that we will review your code. The test page will check to see if your code passes `test_1`. If there are errors or if the results don't match what is expected, you should debug your code's behavior by yourself. If you receive system errors that you do not believe are due to your code, you can email cc@insightdataengineering.com for help.

If your code must be compiled to run (e.g., javac, make), that compilation (as well as the execution) of your code must be specified in the `run.sh` script of your code repository. 

For Python programmers, you can use Python 2 or Python 3. If you use the former, specify `python` in your `run.sh` script, or if you use the later, specify `python3`, which defaults to Python 3.5.2. Other options that could be use are `python3.7` or `python3.8`.

## Questions?
Email us at cc@insightdataengineering.com
