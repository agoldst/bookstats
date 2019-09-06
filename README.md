
# Early-twentieth-century book production and circulation statistics

## A transcription

Summary information about the book industries of the nineteenth and early twentieth centuries is not particularly easy to find. The national book histories (the *History of the Book in America*, the *Cambridge History of the Book in Britain*) often contain partial tables, but these tables have a frustrating way of being illustrative rather than comprehensive. I have not found a ready reference that collects basic facts. Yet these industries did gather their own statistics for their trade journals, and these journals in turn are now readily accessible in big digital libraries.

I have often wanted such statistics, both in my teaching and my research. Here is a start on making them available. Since IANABH (I am not a book historian), this may duplicate work that has already been done in scholarship I am not aware of. If someone shows up to scold me about that, so much the better: I'll be able to use someone else's more polished work.

# US title production

## Fiction and total new titles, 1888–1921, from *Publishers' Weekly*

The file [pw-us-titles.csv](pw-us-titles.csv) contains statistics on title production by US publishers as given in the the annual tabulations in *Publishers' Weekly*, which appear in the last January issue. My particular source has been the scans of the odd-numbered volumes from the University of Michigan found in HathiTrust (Hathi holds at least two copies of each volume of *PW*, but the scans of the volumes from Harvard are consistently worse in quality, often missing pages or distorted. The Michigan scans are imperfect too, but less so).

I was interested in fiction publishing, and so I have started by transcribing the yearly numbers for fiction. As a baseline I have also transcribed the overall totals for title production.

The transcription is in a CSV format, with one row for each table cell. The columns are:

- `year`: the year of publication in question.

- `category`: either `fiction` or `total`, these being the two table rows I have transcribed here.

- `by_origin`: In most years the totals are subdivided in two ways, (1) into titles and editions and (2) by origin. This column reads `F` if the entry falls under the former, `T` if the latter. The division is not stable in the years I've transcribed. It is missing in 1898–99, introduced in 1890, dropped again in 1891–92, and reintroduced in 1893. In 1911 the divisions are slightly renamed. In 1920–21 the first subdivision adds `pamphlets`. Within any category, the total of (1) equals the total of (2).

- `subcategory`: what kinds of titles are counted. These are my own notations, not the exact words used in *PW*, which nonetheless vary interestingly. `titles` here means "new titles exclusive of new editions." Under the distinctions by origin, `US manufactured` refers to foreign-authored texts (by *PW*'s reckoning) manufactured in the U.S. `imported` initially refers to books printed from sheets imported from England (1893), then includes bound imports from England (1894) and later expands to include all foreign imports (1911).

- `count`: the number of titles recorded by *PW*. In principle these correspond to tallies of titles appearing in *PW*'s *Weekly Record* feature in each issue.

- `note`: I have included a few notes on conditions affecting the statistics, drawing on remarks made in the discussions that accompany the tables in *PW*.

- `issue`: the issue of *PW* from which the number is transcribed. May either be a sequential number or a volume and issue combination, depending on which appears in the running head of the magazine.

- `page`: page number for ditto. *PW* numbering, not PDF file numbering.

- `source`: the HathiTrust ID of the scanned volume I have used. Prefix `https://babel.hathitrust.org/shcgi/pt?id=` to obtain a URL.

In R, the file can be loaded with

```R
library("readr")
pw <- read_csv("pw-us-titles.csv", col_types=cols(issue=col_character()))
```

It is probably best to consider these statistics as a representation of a *classifying practice* rather than an objective measurement. First, *Publishers' Weekly* enacts a division between "Juvenile" and "Fiction"; this division was problematic enough that the British *Publishers' Circular* gave up on it in 1896. Second, the judgments about novelty and the distinction between a "new title" and a "new edition" are continually being subject to revision, as the yearly comments on the tables in *PW* attest. Finally, many new publications are not counted either because *PW* does not receive them, or *PW* does not seek out information about them, or *PW* does not consider them worth counting. I am still unsure about when and to what degree dime novels, for example, are counted. Thus, Street & Smith's paperback series are listed when *PW* introduces a separate listing of series in its Annual Summary Number for 1901 (the separate listing is discontinued in 1906, but Street & Smith's titles continue to be included). I do not find entries for S&S's dime novels before 1900 in *PW*'s Weekly Records, though I have not made an exhaustive search.

## US Book Titles by Category, 1880-1927

The file [ohara.csv](ohara.csv) transcribes a 1929 summary table compiled by Downing Palmer O'Hara from *PW*'s own yearly summaries--which goes to show, incidentally, that the present labor of retranscribing this data has been ongoing for at least 90 years. Sushil Sivaram and I have OCR'd a digital file of this table (as reprinted in *PW* itself) and corrected the figures (some errors may well remain). The citation for the source is

Downing Palmer O'Hara, "Book Titles Published by Classes in the United States, 1880-1927," _Publishers' Weekly_, January 19, 1929: 276-77; *Publishers Weekly Archive*, [pubweekly.napubcoonline.com](https://pubweekly.napubcoonline.com).

Each entry in the table is the *sum of new titles and new editions* in the category. The alignment of categories with the varying labels used over time by *PW* is O'Hara's.  

I have corrected what appear to be O'Hara's mistranscriptions (I have not consulted the MA thesis from which the table is taken) as follows:

1887, Sociology: 147] 143 [cf. table on <https://hdl.handle.net/2027/mdp.39015033509525?urlappend=%3Bseq=331> s.v. "Political and Social Science"]

1904, General Literature: 627] 697 [cf. table on <https://hdl.handle.net/2027/mdp.39015033468151?urlappend=%3Bseq=125> s.v. "Literature and Collected Works"]

The file format is CSV; I have preserved O'Hara's column headers, some of which have spaces in them. Missing entries are simply empty in the transcription. The file can be read in R with

```R
library("readr")
ohara <- read_csv("ohara.csv")
```

The correspondence with the fiction and all-title tallies in `pw-us-titles.csv` can be verified with

```R
library("tidyverse")

# verify fiction count
pw %>% filter(category == "fiction", !by_origin) %>%
    group_by(year) %>%
    summarize(count=sum(count)) %>%
    left_join(ohara %>% select(Year, Fiction), by=c(year="Year")) %>% summarize(all(count == Fiction))

# sum O'Hara's categories to get yearly totals of all titles and editions
ohara_totals <- ohara %>% gather(category, count, -Year) %>%
    replace_na(list(count=0)) %>%
    group_by(Year) %>%
    summarize(count=sum(count))

# verify that these totals correspond to PW's
pw %>% filter(category == "total", !by_origin) %>%
    group_by(year) %>%
    summarize(count=sum(count)) %>%
    left_join(ohara_totals %>% select(Year, count), by=c(year="Year")) %>%
    summarize(all(count.x == count.y))
```

(Making this check enabled me to fix a number of transcription errors.)

# US Book Production, 1905–1939

In the [census](census) folder are transcriptions of US Census of Manufactures data on the number of copies of books produced (by category). More detail can be found in the [README](census/README.md) file there .

# Pull requests

I would very much welcome additions to this data—as well as corrections. If you wish to transcribe more of the tables represented here only in excerpt, I would welcome the contribution. When you make a pull request, please

1. adhere to the format used here
2. ensure your commit message gives your full name and details your process.

If for some reason you cannot follow the format, please explain why. If you do not know how to make a [pull request](https://help.github.com/articles/using-pull-requests/), please get in touch. I can't undertake to merge in changes manually—visions of getting Excel spreadsheets over e-mail rise up before me—but I will try to help if I can.

I will keep a running list of contributors in this file so that any users of this material will credit it properly.

# More to come

I plan to make a similar transcription of the *Publishers' Circular* figures for the UK available. In the meantime, a printed reference for such figures is Simon Eliot, *Some Patterns and Trends in British Publishing, 1800–1919* (London: Bibliographical Society, 1994).

# Contributors

Andrew Goldstone (March 2016–present)

Sushil Sivaram (September 2019–present)
