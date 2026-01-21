![Prinzbench](assets/prinzbench.png)
# prinzbench
prinzbench is a private benchmark that ranks LLMs based on their ability to conduct legal research and analysis ("legal reasoning") and locate obscure publicly available information online ("needle-in-the-haystack search").

The current leaderboard is set forth immediately below, followed by notes on methodology, grading, model access and specific models' performance.

<!-- LEADERBOARD_START -->
Last updated on January 20, 2026
![Chart-01.20.26](/assets/chart-01-19-26.png)

| Model                       | prinzbench (full) score (x/99) | Legal Research Sub-Score (x/75) | Search Sub-Score (x/24) |
| --------------------------- | -----------------------------: | ------------------------------: | ----------------------: |
| gpt-5.2-thinking (extended) |                             52 |                              41 |                      11 |
| gemini-3-flash              |                             36 |                              29 |                       7 |
| gemini-3-pro                |                             35 |                              29 |                       6 |
| grok-4.1-thinking           |                             25 |                              19 |                       6 |
| grok-4                      |                             23 |                              16 |                       7 |
| kimi-k2-thinking            |                             22 |                              18 |                       4 |
| sonnet-4.5                  |                             20 |                              20 |                       0 |
| opus-4.5                    |                             14 |                              14 |                       0 |

<!-- LEADERBOARD_END -->
## Purpose
Why this benchmark was created:
1. There has recently been much interest in benchmarks that measure LLMs' ability to perform economically valuable work.  The subject of *prinzbench* - legal research - is economically valuable work.
2. Many existing LLM benchmarks focus on subjects like math and coding, and there has recently been a sharp increase in LLMs' performance on these benchmarks.  However, some skeptics have declared that existing LLMs are great at math and coding only because the frontier labs overfit the models for these specific tasks, "hill-climbing the benchmarks" even as AI models' ability to help with other real-world tasks has remained limited.  *prinzbench* proves these skeptics wrong by showing that certain existing LLMs possess surprisingly strong ability to correctly research and analyze statutes, regulations and regulatory guidance in a particular niche area of U.S. law.[^1] 
## Methodology
*prinzbench* is intended to test AI models' ability to: (i) find legal authorities or factual information that are relevant to answering a legal research question; and (ii) properly analyze available legal authorities to reach the correct conclusion.  To that end, *prinzbench* comprises:
* 25 **Legal Research** questions, each of which presents the LLM with a fact pattern that must be correctly analyzed based on applicable U.S. laws
* 8 **Search** questions, each of which asks the LLM to find an obscure piece of information that is publicly available online

All 33 questions were drafted by the author, and have never been - nor will they ever be - shared with any other person.  

The **Legal Research** questions all relate to a particular niche area of U.S. law in which the author is an expert.  To answer these questions correctly, the LLM is required to locate the relevant statutes, regulations and/or regulatory guidance - all of which are publicly available online.  The answer to each Legal Research question can be found by examining only a few applicable legal authorities; there is never any need for the LLM to trawl through hundreds of cases and juxtapose their holdings in order to arrive at the correct response.  Certain Legal Research questions also require the LLM to locate obscure publicly available factual information to reach the correct conclusion.  

The **Search** questions were added to *prinzbench* to strengthen the benchmark's ability to test LLMs for "needle-in-the-haystack" search capabilities.  These questions are not necessarily related to the practice of law.  

All questions included in *prinzbench* are considered by the author to be very difficult: generally of the kind that, in the author's judgment, an average junior associate practicing in the relevant area of the law would likely not be able answer correctly if provided no research direction beyond the prompt provided to the LLM.  In compiling *prinzbench*, the author endeavored to include therein only truly challenging questions, and each candidate question was tested on an ad-hoc basis with various LLMs before a decision was made regarding its inclusion in the benchmark.  Well over 100 candidate questions were rejected through this process, as the LLMs - frustratingly for the author - had found them "too easy".

To arrive at each model's *prinzbench* (full) score, the model was asked each of the 33 questions exactly three (3) times.  Each response was graded at pass@1.  The maximum *prinzbench* (full) score is 99 points (*i.e.,* 33 questions * 3).  

In addition to each model's *prinzbench* (full) score, the leaderboard also presents each model's Legal Research sub-score (maximum 75 points) and Search sub-score (maximum 24 points), for informational purposes.
## Grading
Each LLM's response to each question was personally graded by the author, unaided by AI.

Some technical details regarding grading:
* A response was judged to be correct if the correct legal conclusion was present anywhere within the model's response.  For example, suppose the correct answer to a particular question is: "You must aggregate the impact of not fewer than 1,000 different transactions of the same type in order to violate a law; because it's unlikely that there would ever be 1,000 such transactions within the specified time frame, it is almost certain that the law was not violated."  If this exact reasoning was included in the body of the model's response, but the model's concluding paragraph simply said that the law was not violated, the response was marked as correct.
* LLMs have a tendency to include extraneous information in their responses, which is not directly relevant to answering the question.  In grading LLMs' responses, all such extraneous information was ignored - regardless of whether it was factually accurate or legally correct.  In other words, the models were graded on their ability to answer the specific question, not on the accuracy of the entirety of the response.

## Model Performance Specifics; Model Access
### OpenAI
At the benchmark's creation in January 2026, **gpt-5.2-Thinking** achieved the highest score on *prinzbench* by a large margin (52/99, as compared to the next-best model's 36/99).  The model also achieved by far the best Legal Research and Search sub-scores (41/75 and 11/24, respectively).

The author found the Search sub-score achieved by **gpt-5.2-Thinking** to be surprisingly low, as the model, in several cases, failed to answer Search questions that gpt-5.x-Thinking models had correctly answered in the past.  The reason for this anecdotal degradation in performance is unclear.

**gpt-5.2-Thinking** took by far the longest amount of time to answer each *prinzbench* question.  In one instance, the model reasoned for >22 minutes in answering a particular Search question (its response, sadly, still wound up being incorrect).  It is possible that the impressive legal reasoning ability of **gpt-5.2-Thinking** as compared to that of the other tested models is driven at least partially by its significantly longer average thinking time.

The author is considering benchmarking **gpt-5.2-Pro** on *prinzbench.*  
#### Model Access:
**gpt-5.2-Thinking** was accessed from the author's personal ChatGPT's Plus account, with "Extended Thinking" turned on, in January 2026.  Each chat was a temporary chat in order to disable ChatGPT's Memory and custom instructions features.

### Google 
At the benchmark's creation in January 2026, **gemini-3-flash** and **gemini-3-pro** achieved the second and third place, respectively, on *prinzbench*, bested only by **gpt-5.2-Thinking**.  The two models' scores were nearly identical (36/99 and 35/99, respectively).  The models exhibited especially strong Legal Research capabilities, bested - again - only by **gpt-5.2-Thinking**, and far stronger than those of the tested Anthropic, xAI and Moonshot models.  
#### Model Access:
**gemini-3-flash** and **gemini-3-pro** were both accessed, in January 2026, via AI Studio, with the following settings: Temperature: 1; Thinking Level: High; Grounding with Google Search: On.

### Anthropic
At the benchmark's creation in January 2026, **opus-4.5** and **sonnet-4.5** achieved the worst two scores on *prinzbench* out of the eight total AI models tested.  **opus-4.5** was by far the worst-performing model on *prinzbench*, scoring just 14/99.  To the author's surprise, **sonnet-4.5** achieved a higher score on *prinzbench* than **opus-4.5** (20/99 vs. 14/99).  This difference is fairly significant, and, in the author's view, is likely explained by **sonnet-4.5** being the (slightly) better legal reasoner out of the two models - a counterintuitive result.  

As of January 2026, the Anthropic models' Achilles' heel is their Search ability.  Both **opus-4.5** and **sonnet-4.5** scored 0/25 on the Search sub-section of *prinzbench*.  Focusing only on the Legal Research sub-scores, a more nuanced picture emerges of **sonnet-4.5**'s legal reasoning ability, as the model actually achieves a slightly higher Legal Research sub-score than the tested xAI and Moonshot models (20/75, as compared to 19/75 for **grok-4.1-Thinking** and 18/75 for **kimi-K2-Thinking**).[^2]  
#### Model Access:
**opus-4.5** and **sonnet-4.5** were both accessed from the author's personal Claude Pro account, with "Extended Thinking" turned on, in January 2026.  Each chat was a temporary chat in order to disable Claude's Memory and custom instructions features.[^3]

### xAI
At the benchmark's creation in January 2026, **grok-4.1-Thinking** and **grok-4** achieved unspectacular scores on *prinzbench* of 25/99 and 23/99 respectively.  The models performed as well as the Google models on the Search sub-score (6/25 and 7/25, respectively - which were the same results as those achieved by **gemini-3-flash** and **gemini-3-pro**), but significantly underperformed the Google models on the Legal Research sub-score.
#### Model Access:
**grok-4.1-Thinking** and **grok-4** were both accessed from the author's personal SuperGrok account in January 2026.  Each chat was a temporary chat in order to disable Memory and custom instructions features.

### Moonshot AI
At the benchmark's creation in January 2026, **kimi-K2-Thinking** achieved an unspectacular score of 22/99 on *prinzbench*.  The model's performance was similar to the performance of the xAI models, although it slightly lagged them in the Search sub-score (4/25 vs. 7/25 and 6/25 for **grok-4** and **grok-4.1-Thinking**, respectively).
#### Model Access:
**kimi-K2-Thinking** was accessed via kimi.com (logged in) in January 2026.

[^1]: This particular niche area of U.S. law is not well-represented in existing LLMs' training data, as shown by the fairly poor *prinzbench* scores achieved by several frontier models, including Anthropic's Opus 4.5 and Sonnet 4.5, as well as models released by Moonshot and xAI.

[^2]: The author does not consider the difference among these three scores to be significant and views the Legal Research sub-scores achieved by these three models as roughly equivalent.

[^3]: Given the fact that Anthropic disabled the Ultrathink feature in Claude Code, the author saw no particular reason to attempt to test **opus-4.5** and **sonnet-4.5** in Claude Code.  The author's ad-hoc testing of **opus-4.5** in Claude Code on similar questions did not reveal any perceived difference between the model's performance in Claude Code and its performance in the Claude app.
