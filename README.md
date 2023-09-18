# ✨Flirty✨ chat-bot

Have problems flirting with a real person? Train yourself using ✨Flirty✨!

## About the case

The idea is to create an empathetic chat-bot that will hold fun, emotional
conversations with users while making relationships more close over time. Full
task description is provided in
[task description file](./task%20description.md).

### Ideal solution

Consists of following points

1. Definition of what is a good conversation with our chat-bot.
2. Chat-bot implementation.
3. Good evaluation pipeline that checks a new conversation against the criteria
   from `1`.

## What I've done

### Exploration

Firstly, I talked to Gleesa in ChaChat and different _girl_ characters on
character.ai to understand the current pain points and limitations of bots. In
short, experience was bad. I found that for user to even _try_ to go into close
relationships with bot:

- bot should have a personality I can imagine talking to. it's not interesting
  to _lick_ or hug (as was proposed by the app) some generic bot that doesn't
  have any traits at the moment for me
- bot shouldn't try to close relationships too fast. I don't want to share my
  anxieties as a first info about me in the conversation
- bot should provide a meaningful and engaging conversation, be empathetic, chat
  like a real person would

If any of these requirements is missing, as a user, I close the chat in the
first 10 messages.

### Solution posibillities

As a pragmatic engineer, I strive to achieve the required result by least means
and so I decided to explore how far we can go with available systems (ChatGPT
3.5/4), with focus on user experience and given pain points. However, I explore
what can be done engineering side in [Future steps](#future-steps) section.

### My criteria

- stays in role, feels like real person
- fun, engaging, not boring
- empathetic, safe, emotional

## Future steps

There's a big room for heavy engineering the chat-bot part in this task:

- collecting the dataset of good dialogues
  - web
  - hugging face
  - asking LLM to talk to other LLM
    - alpaca-like self-instruct (like in saiga:
      https://huggingface.co/datasets/IlyaGusev/gpt_roleplay_realm)
    - scraping
- finetuning open source models for conversation
- creating an agent system to
  - track the stage of the conversation (ice-breaker, casual, close)
  - emotion recognition
  - decision making (e.g. whether to go closer)
- training different classification models (stage, emotion, decision) if vanilla
  LLM would fail as an agent

## How to start

```sh
docker run -e OPENAI_API_KEY=xxxxxxxx -p 3000:3000 ghcr.io/mckaywrigley/chatbot-ui:main
```
