
# Pre-1923 book production and circulation statistics

## A transcription

Summary information about the book industries of the nineteenth and early twentieth centuries is not particularly easy to find. The national book histories (the *History of the Book in America*, the *Cambridge History of the Book in Britain*) often contain partial tables, but these tables have a frustrating way of being illustrative rather than comprehensive. There is, so far as I can tell, no reference that collects basic facts. Yet these industries did gather their own statistics for their trade journals, and these journals in turn are now readily accessible in big digital libraries.

I have often wanted such statistics, both in my teaching and my research. Here is a start on making them available.

# US title production from *Publishers' Weekly*

The file `pw-us-titles.csv` contains statistics on title production by US publishers as given in the the annual tabulations in *Publishers' Weekly*, which appear in the last January issue. My particular source has been the scans of the odd-numbered volumes from the University of Michigan found in HathiTrust (Hathi holds two copies of each volume of *PW*, but the scans of the volumes from Harvard are consistently worse in quality, often missing pages or distorted. The Michican scans are imperfect too, but less so).

I was interested in fiction publishing, and so I have started by transcribing the yearly numbers for fiction. As a baseline I have also transcribed the overall totals for title production.

The transcription is in a CSV format, with one row for each table cell. The columns are

- `source`: the HathiTrust ID of the scanned volume I have used. Prefix `https://babel.hathitrust.org/shcgi/pt?id=` to obtain a URL.
- `year`: the year of publication in question.
- `category`: what kinds of titles are counted. These vary over time in *PW*.
- `count`: the number of titles recorded by *PW*. In principle these correspond to tallies of titles appearing in *PW*'s *Weekly Record* feature in each issue.
- `note`: I have tried to include a few notes on conditions affecting the statistics.
- `issue`: the issue of *PW* from which the number is transcribed. May either be a sequential number or a volume and issue combination, depending on which appears in the running head of the magazine.
- `page`: page number for ditto. *PW* numbering, not PDF file numbering.

I think it is best to consider these statistics as a representation of a *classifying practice* rather than an objective measurement. First, *Publishers Weekly* enacts a division between "Juvenile" and "Fiction"; this division was problematic enough that the British *Publishers Circular* gave up on it in 1896. Second, the judgments about novelty and the distinction between a "new title" and a "new edition" are continually being subject to revision, as the yearly comments on the tables in *PW* attest. Finally, many new publications are not counted either because *PW* does not receive them, or *PW* does not seek out information about them, or *PW* does not consider them worth counting. I am still unsure about when and to what degree dime novels, for example, are counted. Thus, Street & Smith's paperback series are listed when *PW* introduces a separate listing of series in its Annual Summary Number for 1901 (the separate listing is discontinued in 1906, but Street & Smith's titles continue to be included). I do not find entries for S&S's dime novels before 1900 in *PW*'s Weekly Records, though I have not made an exhaustive search.

The new title counts might be described as an index of the relatively more legitimate publishers' collective investment in new material. What is lacking is (1) some index of their re-investment in old material through reprinting and (2) some index of the degree to which less legitimate publishers follow the same patterns.


# Pull requests

I would very much welcome additions to this data---as well as corrections. If you wish to transcribe more of the tables represented here only in excerpt, I would welcome the contribution. When you make a pull request, please

1. adhere to the format used here
2. ensure your commit message gives your full name

If for some reason you cannot follow the format, please explain why.

I will keep a running list of contributors in this file so that any users of this material will credit it properly.

# More to come

I plan to make a similar transcription of the *Publishers' Circular* figures for the UK available.

# Contributors

Andrew Goldstone (2016)