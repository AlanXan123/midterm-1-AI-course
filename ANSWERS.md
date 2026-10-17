# Midterm 1: answers

GitHub username: alanxan123 
Session code: ember-92
Fingerprint: 1dbf234f

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration

I used gpt to help me calculate the numbers, understand the questions, and write my answers in simple english. I used google colab to generate my personal data. 
Gpt also helped me compare the results and explain my decisions.

(About half a page: which assistants or tools you used and for what. If you used none, say so.)

## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
| A | 0.5000 | 0.6333 | 0.7333 | 0.5861 |
| B | 0.1667 | 0.3333 | 0.6167 | 0.3114 |

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 | 0.6333 | 0.5068 | 0.7438 |
| A, k=5 | 0.7333 | 0.6099 | 0.8287 |
| B, k=3 | 0.3333 | 0.2273 | 0.4594 |
| B, k=5 | 0.6167 | 0.4902 | 0.7291 |

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 | 31519.20 |
| A, k=5 | 41275.32 |
| B, k=3 | 21612.29 |
| B, k=5 | 24763.81 |

### 1d. Decision (at most 150 words)

Chosen candidate: B, k=5
I choose B with k=5 because it costs 24,763.81$ per year. The bank's budget is 28,100$, so this option is good.
Option A gives better results, but it is too expensive.
B with k=5 finds the correct information in 61.67% of questions. The 95% Wilson interval is from 49.02% to 72.91%.
Results for each language:
EN: 11/20 = 55%
RU: 13/20 = 65%
KK: 13/20 = 65%
B with k=3 is cheaper, but it finds fewer correct answers (33.33%).
I think that B with k=5 is the best choice because it gives better results than B with k=3 and stays within the budget.
(Decision, using your intervals and the budget. Give the recall of your choice for EN, RU and KK separately.)

### 1e. Next measurement (at most 60 words)
I would test B with k=5 using more real questions in english, russian, and kazakh.
I would check how often it finds the right information and gives correct answers.
This would help us see which language needs improvement before using the system in the bank.
## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H | 0.9056 | KK, clean | 0.8000 | 0.6269 | 0.9050 | 28506.50 |
| L | 0.8333 | KK, degraded | 0.7667 | 0.5907 | 0.8821 | 7200.00 |

Personal-data pages per year sent abroad under H: 562100

### 2b. Memo (at most 300 words)
To: Head of Operations
Subject: Choosing the best pipeline
I recommend Pipeline L for the bank.
Pipeline H has 90.56% accuracy, while pipeline L has 83.33%. H gives better overall results, but both have problems with kazakh documents.
H has its worst result on KK clean scans (80%), with a 95% Wilson interval of 62.69% to 90.50%. 
L has its worst result on KK degraded scans (76.67%), with an interval of 59.07% to 88.21%.
The intervals overlap, so we cant be sure which is better for these groups.
Pipeline H sends documents abroad. We need to check where the scans go, who stores them, and how long they are kept.
Every year, 562100 pages with personal data would leave Kazakhstan.
Pipeline L uses a bank server in Kazakhstan. The bank can control where scans are stored, who can see them, and when they are deleted.

We must check that these rules are followed. Kazakhstan's personal data law No. 94-V covers the ИИН. A company's promise about safety is not enough.
For safety, the bank should encrypt files, limit access, keep access logs, check deletion dates, and have employees review wrong answers. 
These checks should be tested regularly. H costs $28,506.50 per year, while L costs $7,200.

I choose L because its cheaper and gives the bank more control over personal data.
The main risk is lower accuracy, especially for kazakh documents. We should test it more before using it fully.
## Part 3: Explain your own numbers

### Q1

Number: 1.69
Why (at most 40 words): kazakh uses 2.13 times more bytes than english, but 3.61 times more tokens.
This means the higher cost comes not only from encoding, but also from the tokenizer, which uses more tokens for kazakh.

### Q2

Number: 447
Why (at most 40 words): yhe answer sentence starts at token 447. The model can still read it because it is within the 512 token limit. 
Some text at the end is cut off, but there is no error message.

### Q3

Number: 49.9%
Why (at most 40 words): top-p keeps the most likely tokens until their total probability reaches 90%. 
It removes the other tokens. Lowering temperature makes the top tokens more likely but does not remove them.

### Q4

Number: 24
Why (at most 40 words): the public leaderboard prefers Model X because it has 72 correct answers, while Y has 66. 
This teaches models to guess instead of saying "I don't know", even when they are not sure.

### Q5

Number: 4.85
Why (at most 40 words): this model has 4.85 times more tokens per parameter than Chinchilla and thats why its over-trained by this rule. 
Chinchilla showed that large models like GPT-3 were under trained and needed more training tokens.
