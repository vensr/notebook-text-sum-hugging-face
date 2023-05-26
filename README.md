## What is this post about?

As more and more long form content burgeons on the internet, it is becoming increasingly time-consuming for someone like a researcher or any readers to filter out the content they want. Summaries or paraphrase synopsis help readers quickly go through the highlights of a huge amount of textual content and save enough time to study the relevant documents.

In the example today, we will discuss about one such model which will summarize the textual content so that the reader can just get an extract of the whole document.

## Using Pre-Trained Models

HuggingFace Transformer models provide an easy to use implementation of some of the best performing models in natural language processing. 

Transformer models are the current state-of-the-art (SOTA) in several NLP tasks such as text classification, text generation, text summarization, and question answering.

As of now if you check on [hugging face models for summarization](https://huggingface.co/models?pipeline_tag=summarization), there are around 1,123 models.

Today I would talk about using one of these models from Meta [BART](https://huggingface.co/facebook/bart-large-cnn) pre-trained on English language, and fine-tuned on CNN Daily Mail that can be used for for text summarization in english language.

## Text Summarization Task

The notebook is available at the [github url](https://github.com/vensr/notebook-text-sum-hugging-face) for reference.

Before we start the text summarization task, ensure that the following python libraries are installed.

```bash
# packages required for creating the pipeline and loading pre-trained models
pip install transformers datasets -q
```

Import the required libraries

```python
from transformers import pipeline
```

The text summarization task using hugging face pipeline is a 2 step process.

* Load the pre-trained model and create a hugging face pipeline
```python
summarizer = pipeline("summarization", model="facebook/bart-large-cnn")````
```

* Summarize the text
```python
ARTICLE = """ Chennai Super Kings captain MS Dhoni might get banned from playing the Indian Premier League (IPL) 2023 final. Dhoni was once fined for a code of conduct due to a slow rate, but now he can be banned from playing the final at the Narendra Modi Stadium on May 28, Sunday.
During the GT vs CSK Qualifier 1 clash, Dhoni argued with the umpires which caused a four-minute delay. 
The wily Mahendra Singh Dhoni on Tuesday not only guided Chennai Super Kings to yet another IPL final but his clever act of gamesmanship by eating valuable minutes allowed his lethal weapon Matheesha Pathirana to bowl the 16th over against Gujarat Titans in the first IPL qualifier.
CSK pipped the defending champions Gujarat Titans by 15 runs on their home ground, MA Chidambaram Stadium, to qualify for a record-extending 10th final as the four-time winners finally managed a win over the IPL 2022 winners in four matches.
The incident took place when CSK bowler Matheesha Pathirana, who returned 4-0-37-2 while accounting for the dangerous Vijay Shankar and Mohammed Shami, was not allowed to bowl his second spell at the death.
Pathirana had left the field in the second half of the chase of treating an undisclosed niggle. As per the IPL playing conditions, any player who leaves the field for more than eight minutes must be on the field for a similar amount of time after returning, after which he is allowed to bowl.
But when Pathirana returned he was asked by Dhoni to bowl the 16th over with Gujarat Titans needing another 71 to win from 30 balls, having crawled to 102 for six.
As per ESPN Cricinfo, Dhoni then had a conversation with umpire Chris Gaffaney. The commentary, meanwhile, informed that the Sri Lankan was out for nine minutes and the discussion on the field pertained to whether Pathirana could bowl or not.
The report also stated that Dhoni was informed by match officials that Pathirana would have to wait for some more time before he could bowl. Dhoni then said that he understood the fact but he had no option but ask Pathirana to bowl. 
All these discussions took a total of 4 minutes after which Pathirana was allowed to bowl with an acceptable time of eight minutes being over. While Pathirana didn't get a wicket in that over, he did get a wicket in his very next over.
"""
print(summarizer(ARTICLE, max_length=200, min_length=30, do_sample=False))
````

Note that you can control the maximum length and minimum length of the summary.

You should see the output that is something like this

<b>"Chennai Super Kings beat Gujarat Titans by 15 runs in IPL 2023 qualifier. But captain Mahendra Singh Dhoni has been banned from playing. Dhoni argued with umpires over whether he could bowl the 16th over."</b>

That is all, you can also expose this as an API service and create a great interface and use them in your projects.

## References

* [Hugging Face Text Summarization Models](https://huggingface.co/models?pipeline_tag=summarization)

* [Hugging Face Text Summarization Task](https://huggingface.co/tasks/summarization)

* [BART Model Details](https://huggingface.co/facebook/bart-large-cnn)

* [Hugging Face Docs](https://huggingface.co/docs)

{{< chat minilab-huggingface-text-summarization >}}
