# 4372 Assignment 4

**NLP Using Transformers**

Google Colab: https://colab.research.google.com/drive/12c7R5gu1Ir5imhe8XWmZU924GfqrwtFN?usp=sharing

Team: Elizaveta Makhonina & Avizeh Walji 
Net ID: dal445515 & anw230000

Assignment 4: 1 notebook does all four tasks on one Project Gutenberg book: text summarization, machine translation (English -> French), a question-answering chatbot, and text generation.

Dataset:
Book: The Human Machine by Arnold Bennett, Project Gutenberg eBook #12811
Loaded straight from the public URL inside the notebook: https://www.gutenberg.org/cache/epub/12811/pg12811.txt

How to run:
1. Open assignment4.ipynb in Google Colab.
2. Turn on a GPU: Runtime -> Change runtime type -> T4 GPU.
3. Runtime -> Run all. The first cell installs the libraries. All models download automatically from HuggingFace.
4. Total run time is about 15-25 minutes on a T4 GPU (it also works on CPU, just much slower).
4. The last cell prints every result as JSON. These are the numbers used in the report.
To talk to the chatbot, uncomment chat() in the chatbot cell and type questions (type quit to stop).

Libraries:

transformers, torch, sentencepiece, sacremoses, rouge_score, sacrebleu, scikit-learn, pandas, numpy, requests (torch, scikit-learn, pandas, numpy and requests are already in Colab).

Models used (all pre-trained from HuggingFace):

Task:                  Models:
Summarization	         facebook/bart-large-cnn, sshleifer/distilbart-cnn-12-6
Translation	           Helsinki-NLP/opus-mt-en-fr, t5-small, Helsinki-NLP/opus-mt-fr-en (back-translation)
Question answering	   distilbert-base-cased-distilled-squad, deepset/roberta-base-squad2 (+ TF-IDF retriever)
Text generation	       gpt2, distilgpt2 (also fine-tuned on the book), gpt2-medium (only to score generated text)

Assumptions:

No reference summaries or French translations of this book exist on Gutenberg, so we wrote 6 reference summaries and used translation (EN -> FR -> EN) for BLEU/ROUGE.
The 12 QA test questions and answers were written by us from the book text.
Chapter 16 is held out for perplexity and not used for fine-tuning.
Random seeds are fixed, but sampling results can still change a little between GPUs/library versions.
