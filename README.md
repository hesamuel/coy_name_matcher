<img src="./assets/sorting.gif" align="center" width="40%" margin="0" ></img> 

# COMPANY NAME MATCHER
One of the challenges with querying company names from different databases is the discrepancy in the way entity names are spelt. For example, company “ABC” is shown as “ABC” in the Bloomberg system, but “AB C” in another data source. We need to make sure they actually refer to the same company.

I have decided to tackle this problem in two stages.

## STAGE 1:  ACCURATE REGISTERED BUSINESS ENTITY NAMES
A quick search of "SINGTEL" revealed more than 30 different business entities registered in Singapore -- with some devastatingly similar names like "SINGTEL AUSTRALIA HOLDING PTE LTD" and "SINGTEL AUSTRALIA INVESTMENT LTD.". A logical first step is to access the Accounting and Corporate Regulatory Authority's(ACRA) API to cross-check the names in our dataset. We can confirm with a high degree of accuracy if there are perfect matches. We will access the API via [data.gov.sg](https://data.gov.sg/dataset/entities-with-unique-entity-number).


## STAGE 2: INTERNAL MATCHING
For non-perfect matches, we will then create a function to check similarity scores within the data set. We will be using Levenshtein distance as our metric for measuring the difference between company names. Levenshtein distance between two words can be explained as the the minimum number of single-character edits (insertions, deletions or substitutions) required to change one word into the other.

## Directory

```
|__ code
|   |__ 01_Name_Match.ipynb  
|__ data
|   |__ name_match.csv
|__ assets
|   |__ (various_images_used_for_presentation)
|__ README.md
```


## CONCLUSION/LIMITATIONS
**Spelling-Errors?** - We got lucky that our test examples did not have severe typos. As an improvement, we could possibly add in a third stage to account for some non-matches. One of the first steps in stage 3 could be searching ACRA, but having a less stringent matching criteria. For all remaining non-matches, we might need to end up manually sorting the data.

**Singapore-only** - One of the limitations of our methods here is that ACRA only accounts for Singapore-registered companies. To improve our approaches, we might want to consider a more global database of companies.
