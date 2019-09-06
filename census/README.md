# Book production figures from the Census of Manufactures

A formal census of manufactures in the US was first conducted in 1905 and at irregular intervals thereafter. I have been able to locate scans of the census volumes relevant to the publishing industries up through 1940, which give data for the years 1909, 1914, 1919, 1921, 1923, 1925, 1927, 1929, 1931, 1933, 1935, 1937, and 1939. The files included here transcribe the census tabulations of book production by classes for these years.

Each file is a TSV with four columns, `year`, `format` (i.e. books, pamphlets, or both), category (or "Class" as the census calls it), and `copies` (the number). The `copies` column has groups of three digits separated by commas (as they are in the originals); this made transcription much easier. The files are named for the years covered. Sources for each file (URLs and other locating information) are listed in [sources.csv](sources.csv).

I have retained the category names used in the censuses as they vary over time. The heading "Aggregate," which is the total of all books and pamphlets, I place in the `format` column, leaving `category` blank. "Books, total" and "Pamphlets, total" I transcribe by putting the format in `format` and "total" in the `category` column. For 1939 the "Bibles and testaments" category is subdivided into four. For ease of analysis I have lowercased all the `format` entries. I left the case as I found it in `category`, so care is needed in constructing time series from the data.

The 1935 census revises the figures for 1929, 1931, and 1933, so I have transcribed the figures for those years from the 1935 census. I only noticed this after transcribing the 1929 and 1931 figures from the 1931 census, so I have kept the other file on the off chance it is of interest somehow; it is in an `unrevised` subdirectory.

All the data can be loaded in R with

```r
library("tidyverse")
book_prod <- list.files(pattern="*.tsv") %>%
    map(read_tsv) %>%
    bind_rows()
```

