# ADA - Project
Group: **The Data Collectivists**
Members : Nathan Girard, Clémentine Lévy-Fidel, Camil Hamdane, Nathan Fiorellino

<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Project](#about-the-project)
  * [Introduction](#Introduction)
  * [Data](#Data)
* [Methods](#methods)
  * [Data Extraction and Exploration](#data-extraction-and-exploration)
  * [Preprocessing](#preprocessing)
  * [Processing and Graphics](#processing-and-graphics)
* [Timeline](#timeline)
* [Built With](#built-with)
* [Bibliography](#bibliography)

<!-- ABOUT THE PROJECT -->
## About the Project

### Introduction

The peace and prosperity that we encountered in developped countries of the North in the last century has led many nations in a path of constant technological progress and economic growth. This prosperity however might be threatened by newfound global issues that not only jeopardize the economy, but also the future of humanity. The recent COVID-19 pandemic has shown once more how the current socio-economic system ubiquitous in most occidental democracies has potentially fatal flaws that we need to address before it is crushed under its own weight.

While most people agree about the uncertainty of the next hundred years, we still have yet to agree on a solution. Some of which are more oriented towards a progressive society, while others prefer a more conservative approach. While multiple point of view rely on economic and environmental claims to base their theories on, some others are based on hate and fear of the difference, hate and fear of the change we might need to forge a more inclusive society. In order to better tackle the issues we face, we need to understand how some ideologies are gaining more traction inside the public debate, to observe how they might shape the minds of citizens. In particular, far-right extremism has found a new echo in many Occidental societies, notably in the US **[[3]](#bibliography)**, partly made possible due to online forums. Forums like 4chan, 8kun etc have revealed to be a large alt-right ideology gathering **[[4]](#bibliography)**, useful to extract reccuring topics and vocabulary that suggest alt-right speech.

We are interested today about the rise of far-right extremism speech **between 2016 and 2020**, observed through a dataset of quotes from the press, highlighting the evolution of opinions and ideas that shape the past, present, and the future of our society.

### Research questions and hypothesis

Is far-right extremism speech on the rise since 2016 ? How accurately can we identify a trend with the Quotebank dataset, when put in perspective with right-wing extremist terrorist attacks ? Can we highlight some news outlets and personnalities that spread hate speech more than other, and if so, is it consistent over the years ? Is it also consistent with their political opinions ? 
Our team is composed of strong believers of equality and justice for all, especially in the early twentieth century where climate change and inequalities brought by excessive consumption threaten the stability of our society. We believe that right-wing extremism and hate speech is not helping us solving these issues as it is on the rise. We state as our initial null hypothesis that hate speech is staying constant in the public debate, and is not on the rise. 

### Data

[Quotebank](https://zenodo.org/record/4277311#.YYqEUGXPxb8), an open corpus of 178 million quotations attributed to the speakers who uttered them, extracted from 162 million English news articles published between 2008 and 2020. To narrow down our study, we will focus on the time period between 2016 and 2020, an interval where major political events shaped the way far-right extremism is spreading in the media, while limiting the size of the dataset. 
In order to build our timeline, we plan on using the Washington Post study of the CSIS database **[[1]](#bibliography)** that lists major right-wing extremist incidents that happened between 1994 and 2021. This will allow us to study the correlation between the rise of these attacks and the normalization of hate speech in the media.
Moreover, we will also need to define what is and how to discriminate hate speech.
For the hate speech dictionnary, we will rely on the [Hatebase](https://hatebase.org/) dataset, which is a multilingual corpus of words related to hate speech. 


<!-- METHODS -->
## Methods

Our pipeline is designed in 3 majors steps. We first [extract](#data-extraction-and-exploration) the corresponding datasets unprocessed for data exploration. A preliminary analysis of the data has led us to the [preprocessing](#preprocessing) rules we established to only keep relevent data for our study.
The actual study is divided in multiple approaches. The first of which is a quantitative study of the number of occurences of certain expressions to better build a timeline, putting it in perspective with major political events that shaped the far-right speech spread (Donald Trump presidency, the Charlottesville terrorist attack...).
For our second approach, we are interested in looking at a more qualitative approach, where we actually look at the content of each quote. Using Natural Language Processing (NLP) techniques, some related papers built datasets and models able to predict the hatefulness of a sentence **[[2]](#bibliography)**. This would allow us to get a way to include context for the determination of the "hatefulness" of a quote, not only relying on keywords.
Another approach would be to check if our model can build a profile on a news outlet, or a personnality. This profile could show the evolution of their opinions over the years, which could infirm our initial hypothesis on the rise and normalization of hate speech.


### Data Extraction and Exploration

With an initial analysis, we identified several interesting values for the dataset, orienting our choices for the preprocessing step.

![graph](img/graph.png) \\


_Figure 1: Distribution of the number of occurences per quotes in a sample of the 2020 Quotebank dataset_

We studied the distribution of the number of occurences per quotes in the dataset, and we can see that most of the quotes are cited once. Our analysis is focused on the spread of hate ideology among the population, thus highly cited in the media, which show a trend in the public debate. A quote with only one occurence cannot be considered as crucial in the public debate. Moreover, we observed that some quotes with 1 occurence can be attributed to errors.

Moreover, as the Quobert algorithm sometimes struggles associating a unique speaker to a quote, we chose to remove the quotes with a low (<60%) probability of being associated with a speaker, and we also chose to remove quotes that are linked to multiple QIDs, so that our dataset is only composed of usable, reliable quotes.

### Preprocessing

To clean the dataset, we 

* Removed quotes with low numOccurences (less than 10)
* Removed quotes with no QID
* Removed quotes with multiple QIDs

In the future we plan on:

* Removing news outlets relaying less than a certain number of quotes that do not contribute to reflecting global trends.


## Timeline

We propose the following timeline, on which we will divide the tasks equally.

- [x] **Step 1:** Find a research question exploiting [Quotebank](https://zenodo.org/record/4277311#.YYqEUGXPxb8) data (Milestone P1), 
- [x] **Step 2:** Extract data and implementation of the preprocessing pipeline (Milestone P2), 
- [x] **Step 3:** Finish the preprocessing steps and apply it to the entire selected dataset,
   - *17th of november*
- [ ] **Step 4:** Study the occurences of certain keywords with the Hatebase dataset (Quantitative approach), 
   - *24th of november*
- [ ] **Step 5:** Working model for the assessement of the hatefullness of a quotation. 
   - *First week of december*
- [ ] **Step 6:** Timeline of hate speech evolution with major right-wing extremism related events. 
   - *First week of december*
- [ ] **Step 6:** Graphics and visualization refining and final report. 
   - *second week of december*

## Built With

* [Python 3.7](https://www.python.org)
* [Quotebank](https://zenodo.org/record/4277311#.YYqEUGXPxb8)
* [Pandas](https://pandas.pydata.org)
* [Seaborn](https://seaborn.pydata.org)

## Bibliography

1. [Washington Post article](https://www.washingtonpost.com/investigations/interactive/2021/domestic-terrorism-data/) [Github repository](https://github.com/wpinvestigative/csis_domestic_terrorism)
2. Qian, J., Bethke, A., Liu, Y., Belding, E., & Wang, W. Y. (2019). A benchmark dataset for learning to intervene in online hate speech.
3. Stevenson, J. (2019). Right-wing extremism and the terrorist threat. Survival, 61(1), 233-244.
4. Baele, S. J., Brace, L., & Coan, T. G. (2021). Variations on a Theme? Comparing 4chan, 8kun, and Other chans’ Far-Right “/pol” Boards. Perspectives on Terrorism, 15(1), 65-80.
