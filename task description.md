## 🔢 Task description

Your task is to create an AI Friend with the following tasks:

1. Use a language model as the main part of the dialogue engine. You can tune
   the 2B+ model in collab/kaggle on the dataset of your choice or take some
   open-source solutions. You can use Large Language Models by API, but the used
   prompts need deep explanation on why it’s used. Conversational Targets are
   written below, optimize for them during your work Requirements: 1. For
   finetuning, use adaptors to reduce the size of the trained model weight 2.
   Save the notebook/code with the preparation 3. Please describe in the
   notebook or in the separate markdown file, why you used the specific
   pre-trained model and the procedure to prepare it for the tasks.
2. Conversational Targets:

   1. Perform Ice-Breaker with the user
      1. Describe the best way to interact with the bot
      2. Try to make an emotional connection with the user, so the user feels
         some warm emotions from the beginning
   2. During the conversation, bot should become more and more close and flirty
      with the person

      Keep the following schedule in mind:

      1. 1-10 messages are intro
      2. 10-30 messages are the next
      3. 30+ messages — close relationships

3. Create a simple automatic evaluation pipeline for the quality of the
   conversations

!! **IMPORTANT !!** Every task is necessary, but paying attention to the last
task is more important. The evaluation pipeline must be included, as it provides
proof that your system performs well. A system with a well-written evaluation
pipeline, even without a fine-tuned model, is better than a large neural network
trained solely on dialogues.

!! **IMPORTANT !!**

## 📦 Requirements

**You are free to brainstorm and decide what is the best solution to implement**

1. Provide some useful UI (Telegram bot or some terminal input will work)
2. The solution should be containerized
3. You should use an open-source language model or LLM by API
4. You can use any data available on the web

You must provide a GitHub repo that includes:

- a `README.md` file that contains a **detailed description of the approach and
  the story of your experiments**
- A description of how to start the container and chat with the bot
- Code in `python` that was used to train the model and preprocess the data
- `requirements.txt` or `environment.yml` that includes all requirements to
  reproduce the results
- Adaptors weights for the finetuned model, if you have one

## 📈 Evaluation

We will measure the following things:

- solution integrity & focus on the user experience
- the quality of your training pipeline
- the quality of answers that your model provides (subjectively)
- the quality of the user journey
  - How Ice-Braker goes
  - How the emotional connection improves
- code quality
- ideas and code for the evaluation pipeline
- analysis of possible solutions to the problem, quality metrics, and your ideas
  to improve the approach

## 💫 Solution

- We expect a fully working baseline with a few important things from your
  experience
- If you don't have time to do all the steps, do the ones you think are the most
  important for the quality of the conversation. We estimate the time for the
  task as 12 h
