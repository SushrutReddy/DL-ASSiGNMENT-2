# 🎤 GPT-2 Fine-Tuning on Drake Lyrics

This project fine-tunes OpenAI's GPT-2 model on lyrics from the artist **Drake**, enabling it to generate lyrics in a similar style based on any given prompt.

---

## 📌 Project Overview

The goal of this project is to explore Natural Language Generation (NLG) using **GPT-2**, a large-scale transformer-based language model. Instead of generating general English text or headlines, we customize the model to produce **music lyrics**, specifically those in the style of **Drake**.

This project demonstrates the process of:
- Collecting and processing a domain-specific dataset (Drake lyrics)
- Fine-tuning a pre-trained transformer model (GPT-2)
- Generating creative, stylistically consistent text

---

## 🔁 Project Workflow (Explanation)

### 1. **Dataset Collection**
We start by downloading a publicly available dataset of song lyrics from Kaggle:
- Dataset: [Poetry Lyrics Dataset](https://www.kaggle.com/datasets/paultimothymooney/poetry)
- We use only the `drake.txt` file which contains lyrics written by Drake.

### 2. **Preprocessing**
- The text is lightly preprocessed.
- The tokenizer splits text into tokens (word pieces), converts to IDs, and adds special tokens if necessary.
- No heavy cleaning is done to preserve the natural lyrical structure and rhymes.

### 3. **Model & Tokenizer Setup**
- We use the base GPT-2 model and tokenizer from Hugging Face.
- GPT-2 is a generative language model pre-trained on a large corpus of English text.
- We adjust the tokenizer's padding and ensure it aligns with GPT-2’s requirements.

### 4. **Training the Model**
- We fine-tune GPT-2 using Hugging Face’s `Trainer` API.
- The model learns to predict the next word in the sequence based on Drake's lyrics.
- Training is done for a few epochs to capture the lyrical style without overfitting.

### 5. **Saving the Fine-Tuned Model**
- After training, the model and tokenizer are saved locally.
- These can be reloaded anytime for further generation or continued training.

### 6. **Generating New Lyrics**
- We use Hugging Face’s `pipeline` to generate text from the fine-tuned model.
- You can give it a custom prompt like:
