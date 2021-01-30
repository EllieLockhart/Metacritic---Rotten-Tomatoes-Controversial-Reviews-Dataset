# Metacritic & Rotten Tomatoes Controversial Reviews Dataset
 A dataset of both controversial and non-controversial video game and film reviews, created with the intention of studying "review bombing" algorithmically.

 ## Version
 Currently on Version 2 (January 30, 2021): added is_english column as final column to all review CSVs, identifying as a boolean if the review is in English; included the code used to determine this in the ./notebooks directory on GitHub release, with additional notes and cautions included.

 I recommend cloning this archive directly at this time, as of January 30, 2021 there are significant flaws in the official release for tlj_reviews.csv (but not significantly for any other flaws) related to language detection, but these have been patched in recent commits.

### Context

Companies who produce mass media often seek to set metrics for performance, like any employer, which determine whether projects are successful and whether the product should be continued - as well as whether those involve in its production should be rewarded. In the field of video games, this has led to the controversial practice of [tying salary bonuses for developers to user and critic reactions](https://arstechnica.com/gaming/2012/03/why-linking-developer-bonuses-to-metacritic-scores-should-come-to-an-end/) to the product - usually as quantified by the website Metacritic. While the link between RottenTomatoes - the equivalent of Metacritic for film - and anyone's bottom line [is somewhat less clear](https://www.theringer.com/movies/2020/9/4/21422568/rotten-tomatoes-effective-on-box-office), it *is* clear that in recent years, these two websites - Metacritic for video games and RottenTomatoes for movies - have become ideological grounds for battle in the case of high profile games and movies.

Most recently in the summer of 2020, the Playstation 4-exclusive video game *The Last of Us Part II*, produced by Sony and Naughty Dog, transformed its Metacritic user review page into what can only be described after some study as a battlefield of obscenity and hatred. This instance of "review bombing" echoed what happened for Disney blockbusters *Captain Marvel* and, previously, *Star Wars: Episode VIII: The Last Jedi*. In all three cases, users diverged from largely positive (at least initial) critical reactions to launch full-on assaults with the intention of lowering the scores of the products, possibly to alter the behavior of the developers/filmmakers in the future.

In all three of these case studies, a massive amount of reviews were generated - far more than titles that received a great deal of attention but were not subject to "review bombing." (Subsequently, I will provide examples of this disparity.) If companies are going to use publicly posted user reviews as a method of judging whether a title is a success, and certainly if these reviews factor into employee pay, understanding how to identify "review bomb" reviews which may not even originate with potential or real customers is crucial. In all three cases I cite of review bombing, e-celebrities on YouTube and anonymous users on grey-web sites played a role in driving people to post reviews. While my initial survey of these reviews does not indicate that actual automation played a significant role in review bombing, it's quite likely false accounts were used to create multiple reviews, and that people in general were more motivated to post reviews than they were for other blockbuster titles. Thus, comparing these flashpoint films and games with less controversial ones could provide the opportunity to create an algorithmic way to determine the likelihood of a given review of an entertainment product having been influenced by a targeted campaign of the sort that applied in the case of *The Last of Us Part II*, *The Last Jedi*, and *Captain Marvel*.

### Content

Over a period of three months (11/20-01/21), significantly after the release of the principal controversial titles contained within, I utilized Python scripting to obtain and render into a consistent schema user scores (rounded to the nearest integer in the case of RottenTomatoes; exact in the case of Metacritic), date of posting, and textual content (the review itself) of both highly contentious titles subjected to review bombing (*The Last Jedi*, *Captain Marvel*, *The Last of Us Part II*) as well as "control" examples illustrating the vast difference in *number of reviews* as well as content between even very successful or visible titles (for instance, *Logan* [2017] in film to contrast with *Captain Marvel*). In all, the following titles are included, from the following user review pages, with .csv files labeled accordingingly:

**Review Bombing Targets**
- Captain Marvel - RottenTomatoes
- The Last of Us Part II - Metacritic
- Star Wars: The Last Jedi - RottenTomatoes

**Playstation 4 Exclusive Games Not Known to Be Significantly Subject to Review Bombing**
- Dark Souls (remake)
- Days Gone
- Final Fantasy VII Remake
- Ghost of Tsushima*
- God of War (2018)
- Gravity Rush 2
- Horizon: Zero Dawn
- Killzone: Shadow Fall
- The Order: 1886
- Red Dead Redemption 2 [not Playstation 4 exclusive; included due to thematic similarities with *The Last of Us Part II*)
- Resident Evil 7
- Sekiro: Shadows Die Twice
- Marvel's Spider-Man (PS4)
- Until Dawn
- Yakuza 0

**Control Films (all RottenTomatoes)**
- Logan (2017)
- Inception (2010)

CSV files contain the following columns, in sequence: r_id (unique review identifier from the larger SQL table from which these CSVs were created), of_title (title or abbreviation for the title in question, will be the same for all entries in a given CSV), r_date (review creation date in format YYYY-MM-DD), score (0-10 for games from Metacritic, 1-5 for Rotten Tomatoes films, always integer), review (text of the review), is_english (boolean, reflecting the language as determined through probabalistic algorithm, introduced in version 2 of this dataset published January 30, 2021).

* While *Ghost of Tsushima* was not review bombed, it was the first title released as a PS4 exclusive boxed title after *The Last of Us Part II* and my initial investigation has found that the controversy about the former bled directly into the latter, with users wishing to further undermine *The Last of Us Part II* stating their positive reviews of *Ghost* were motivated by antagonism towards *Last of Us* and making extensive references to *Last of Us* characters in their reviews of *Tsushima*.

**This data contains profanity and hateful speech**. I have not censored it or changed the content in any way other than that which is required to prepare it for machine analysis.

**ALSO NOTE**: individuals can leave scores with no text; no record of these reviews is kept in this dataset, but in the case of Metacritic these are counted by Metacritic in the summation of how many reviews exist. Thus, if you check the original source pages you will see far more reviews listed than are contained in this dataset. (A small number of reviews also contained text with special character usage that I was unable to successfully integrate into the dataset or to filter out; these have been omitted. The amount of such data is not significant given the size of the overall dataset, and moreover only affected a few sets of reviews (specifically, *The Last Jedi* and *Inception*.

### Acknowledgements

These reviews are the work of thousands of other people; my contribution is simply to assemble them in a form which can be analyzed.


### Inspiration

I think the most interesting questions to answer with this data are:

- to what extent can we identify reviews, whether positive or negative, that are genuine?
- in service of that question, can unsupervised clustering provide ways to determine groupings of reviews that can then be used to tran a model to find motivated-campaign reviews?
- to what extent, if any, is gender/race/sexuality/etc. bias more common in targets of review bombing than in "control" examples?

Mirrored from https://www.kaggle.com/ellielockhart/metacritic-rotten-tomatoes-controversial-reviews

Thousands of Metacritic & RottenTomatoes users contributed to this dataset, and I do not claim copyright over any part of their text contribution - only the arrangement and data transposition thereof.

This data was collected using Python scripting, JSON creation and parsing, and intermediary processing in a Neo4j Enterprise database (for video game reviews only) from HTML files retrieved from the user review pages for the respective films and Playstation-4 exclusive video games whose user reactions are being researched. In the case of films, all data was initially saved, including superfluous data such as user names and whether the users were "super reviewers" or verified. In the case of video game reviews from Metacritic, only relevant information was saved. This information was then parsed into JSON, with the RottenTomatoes data anonymized (user data was never collected for Metacritic data) and uploaded *via* further scripting to a PostgreSQL instance, where it was ordered, control characters removed, and cleaned (although not yet pre-prepared for NLP processing.) The data is for research purposes exclusively and is copyright its original owners; it should not be redistributed for any purpose beyond NLP analysis. The CC license only applies to the extent permitted by law, to the modifications and transmutations I have made, and does not assert any ownership over rights to the review text. The datasets are complete collections of all reviews of the titles in question as of the time the extractions were done (November or December of 2020 for Metacritic and January of 2021 for RottenTomatoes), excluding a limited number of entries which could not be successfully parsed due to unusual characters. They have not been edited in any way (beyond escaping control characters and duplicate entries) and include content in various languages. They also contain profanity and hate speech, which may be relevant to data analysis conducted on them. Any censorship or removal of content was done by RottenTomatoes or Metacritic or by the original authors.

## Contents of GitHub Repository
This GitHub repository contains both the dataset (in directory ./csv) and some scripts (Python/iPython/Jupyter) used to asseumble it (in directory ./notebooks). Many/most of these scripts require the installation of third-party Python libraries, and having a PostgreSQL database containing similar data. They are unlikely to be useful, but are provided in the hopes of demonstrating the provenance of the data.

### ./csv
- each CSV file is a movie or video game's corpus of reviews.

### ./notebooks
- ./notebooks/mark_language.ipynb: uses a fairly reliable language detection algorithm to determine which reviews are likely in English and mark the is_english column in a PostgreSQL database