# This project is the work of :
## **Nathan Girard**, **Clémentine Lévy-Fidel**, **Camil Hamdane**, **Nathan Fiorellino**

<!-- TABLE OF CONTENTS -->
## Table of Contents

* [We start with Data and Questions !?](#We_start_with_Data_and_Questions_!?)
  * [Research questions and hypothesis](#Research_questions_and_hypothesis)
  * [Data](#Data)
   * [Quotebank](#Quotebank)
   * [Hatebase](#Hatebase)
   * [CSIS database (Washington Post subset)](#CSIS_database_(Washington_Post_subset))
* [We throw the data around](#We_throw_the_data_around)
  * [First Filtering](#First_Filtering)
  * [Second Filtering](#Second_Filtering)
  * [Sentiment Analysis](#Sentiment_Analysis)
  * [Parquet](#Parquet)
* [We stare at the data until it reveals its all secrets](#We_stare_at_the_data_until_it_reveals_all_its_secrets)
* [Built With](#built-with)
* [Bibliography](#bibliography)


![image](ALT_RIGHT.jpg)

_Figure 1: Alt-Right Rally_

## We start with Data and Questions !?

With communication on social media and online board becoming ubiquitous, some schools of thoughts that were traditionnally absent from traditional media, have found a new home online. In spite of the necessity of such a space for the foundation of a democracy, internet is also hosting harmful content and ideas. With the recent COVID-19 pandemic, we have spent a lot more time online during which we saw a lot more conspiracy theories and fake news surrounding the sanitary crisis. The theories and ideas that spread on the internet often overlap with right-wing extremism and alt-right beliefs, which saw a net rise over this period **[5](#bibliography)**. We believe this rise of alt-right ideas is correlated with the important rise of hate speech online during the pandemic, which stands at a 38% increase of instances of or discussions about hate speech on the internet from March 2020 to the summer of 2021 **[6](#bibliography)**. Before moving on, let us backtrack a little and define the vocabulary of interest:

> The Cambridge dictionary defines **hate speech** as a public speech that expresses hate or encourages violence towards a person or group based on something such as race, religion, sex, or sexual orientation.
>
> It defines alt-right by people with extreme conservative views, including extreme views about race, who reject ordinary politics and use the internet to spread their opinions.

The peace and prosperity that we encountered in developped countries of the North in the last century has led many nations in a path of constant technological progress and economic growth. This prosperity however might be threatened by global issues that not only jeopardize the economy, but also the future of humanity. The recent COVID-19 pandemic has shown once more how the current socio-economic system ubiquitous in most occidental democracies has potentially fatal flaws that we need to address before it is crushed under its own weight.

While most people agree about the uncertainty of the next hundred years, we still have yet to agree on a solution. Some of which are more oriented towards a progressive society, while others prefer a more conservative approach. While multiple point of view rely on economic and environmental claims to base their theories on, some others are based on hate and fear of the difference, hate and fear of the change we might need to forge a more inclusive society. In order to better tackle the issues we face, we need to understand how these ideologies are gaining more traction inside the public debate, to observe how they might shape the minds of citizens.

We have talked a lot about the rise of hate speech on the internet and in public discussions, but in order to take home some conclusions about the consequences on the real-world politics, we also have to analyze a factor that shapes more than others the political landscape of our society: the Press. While people spread more hate speech, it is critical to assess how the media relays that information and in which proportion,  Moreover, we will also investigate if this rise of hate speech in the media could be correlated with real-world events and attacks linked with alt-right extremists motivated by the same ideas we can find in some flagged quotes. Both a rise of hate speech discussion in the press and a rise in far-right extremist attacks are a factor and a symptom of the rise of hatred in the public debate, which we desperately need to address.
We are interested today about the rise of far-right extremism speech **between 2016 and 2020**, observed through a dataset of quotes from the press, highlighting the evolution of opinions and ideas that shape the past, present, and the future of our society.

### Research questions and hypothesis

Is far-right extremism speech on the rise since 2016 ? How accurately can we identify a trend with the Quotebank dataset, when put in perspective with right-wing extremist terrorist attacks ? Can we highlight some news outlets and persnnalities that spread hate speech more than other, and if so, is it consistent over the years ? Is it also consistent with their political opinions ?
Our team is composed of strong believers of equality and justice for all, especially in the early twentieth century where climate change and inequalities brought by excessive consumption threaten the stability of our society. We believe that right-wing extremism and hate speech is not helping us solving these issues as it is on the rise. We state as our initial null hypothesis that hate speech is staying constant in the public debate, and is not on the rise.

### Data
#### Quotebank
[Quotebank](https://zenodo.org/record/4277311#.YYqEUGXPxb8), an open corpus of 178 million quotations attributed to the speakers who uttered them, extracted from 162 million English news articles published between 2008 and 2020. To narrow down our study, we will focus on the time period between 2016 and 2020, an interval where major political events shaped the way far-right extremism is spreading in the media, while limiting the size of the dataset.

#### Hatebase
[Hatebase](https://hatebase.org/) is a dataset summarizing more than 3800 unique words in 98 different languages, that are documented in online discussions and real-world occurences, with a constant monitoring for a total of more than 800,000 sightings in different regions of the world and internet. In order to better distinguish hate speech from the rest, we needed a dictionnary of hateful words that tends to be less biased than a homemade one for its collaborative nature.

#### CSIS database (Washington Post subset)
In order to build our timeline, we plan on using the Washington Post study of the CSIS database **[[1]](#bibliography)** that lists major right-wing extremist incidents that happened between 1994 and 2021. This will allow us to study the correlation between the rise of these attacks and the normalization of hate speech in the media.


<!-- Process -->
## We throw the data around

![image](Figure.png)

_Figure 2: Pipeline of our data_

Our pipeline is designed in 3 majors steps. We first [extract](#data-extraction-and-exploration) the corresponding datasets unprocessed for data exploration. A preliminary analysis of the data has led us to the [preprocessing](#preprocessing) rules we established to only keep relevent data for our study.
The actual study is divided in multiple approaches. The first of which is a quantitative study of the number of occurences of certain expressions to better build a timeline, putting it in perspective with major political events that shaped the far-right speech spread (Donald Trump presidency, the Charlottesville terrorist attack...).
For our second approach, we are interested in looking at a more qualitative approach, where we actually look at the content of each quote. Using Natural Language Processing (NLP) techniques, some related papers built datasets and models able to predict the hatefulness of a sentence **[[2]](#bibliography)**. This would allow us to get a way to include context for the determination of the "hatefulness" of a quote, not only relying on keywords.
Another approach would be to check if our model can build a profile on a news outlet, or a personnality. This profile could show the evolution of their opinions over the years, which could infirm our initial hypothesis on the rise and normalization of hate speech.

### First Filtering
With an initial analysis, we identified several interesting values for the dataset, orienting our choices for the preprocessing step.

We studied the distribution of the number of occurences per quotes in the dataset, and we can see that most of the quotes are cited once. Our analysis is focused on the spread of hate ideology among the population, thus highly cited in the media, which show a trend in the public debate. A quote with only one occurence cannot be considered as crucial in the public debate. Moreover, we observed that some quotes with 1 occurence can be attributed to errors.

Moreover, as the Quobert algorithm sometimes struggles associating a unique speaker to a quote, we chose to remove the quotes with a low (<60%) probability of being associated with a speaker, and we also chose to remove quotes that are linked to multiple QIDs, so that our dataset is only composed of usable, reliable quotes.

### Second Filtering

As we are interested in quotes containing hate speech, we apply a second filtering on the whole corpus of quotes, by extracting the **quotes containing a hateful keyword** 




### Sentiment Analysis

*Pretrained Model*:
Lexical detection methods tend to have low precision because they classify all messages containing particular terms as hate speech and previous work using supervised learning has failed to distinguish between the two categories. We chose to use a pretrained model suited for hate speech detection called [Perspective API](https://www.perspectiveapi.com/). In particular, we will use the “Severe toxicity” metric as it is the most precise for our task [7].

### Parquet

## We stare at the data until it reveals **all** its secrets

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
5. Patriotism, Pandemic, and Precarity: How the Alt-Right and White Nationalist Movement Used the Pandemic [link](https://ecommons.udayton.edu/human_rights/2021/schedule/28/)
6. Ditch the label and Brandwatch - Uncovered: Online Hate speech in the Covid era. [link](https://www.brandwatch.com/reports/online-hate-speech/view/)
7. Zannettou, Savvas, Mai Elsherief, Elizabeth Belding, Shirin Nilizadeh, et Gianluca Stringhini. « Measuring and Characterizing Hate Speech on News Websites ». In 12th ACM Conference on Web Science, 125‑34. Southampton United Kingdom: ACM, 2020.

