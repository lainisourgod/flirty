# ✨Flirty✨ chatbot

Have problems flirting with a real person? Train yourself using ✨Flirty✨!

## About the case

The idea is to create an empathetic chatbot that will hold fun, emotional
conversations with users while making relationships more close over time. Full
task description is provided in
[task description file](./task%20description.md).

There's not a single line of code in this repo 😅 and I will address why it is
the case later in the README. The other files in repo are
[the current best prompt](./prompts.md) and [the history](./HISTORY.md) behind
developing it.

### Ideal solution

Consists of following points

1. Definition of what a good conversation with our chatbot is.
2. Chatbot implementation.
3. Good evaluation pipeline that checks a new conversation against the criteria
   from `1`.

## What I've done

### Exploration

Firstly, I talked to Gleesa in ChaChat and different _girl_ characters on
character.ai to understand the current pain points and limitations of bots. In
short, experience was bad. I found that for user to even _try_ to go into close
relationships with bot:

- Bot should have a personality I can imagine talking to. It's not interesting
  to _lick_ or hug (as was proposed by the app) some generic bot that doesn't
  have any traits I can relate to.
- Bot shouldn't try to closen relationships too fast. I don't want to share my
  anxieties as a first info about me in the conversation. Also suggesting to hug
  after talking about some technical stuff may be repelling.
- Bot should provide a meaningful and engaging conversation, be empathetic, chat
  like a real person would.

If any of these requirements is missing, as a user, I close the chat in the
first 10 messages. In a sense, to become a good person to flirt to, chatbot
should first become a good person to befriend with. And so I decided to focus on
creating an emphatetic and fun person to talk to — ice-breaker + casual talk
parts, — leaving "close relationships" part aside.

### Solution posibillities

As a pragmatic engineer, I strive to achieve the required result by least means
and so I decided to explore how far we can get with available systems (ChatGPT),
with focus on user experience and given pain points. However, I explore what can
be done engineering side in [Future steps](#future-steps) section, for both
chatbot and evaluation pipeline implementations.

My solution process was iterative:

- Write some prompt. A mix of own ideas and best practices from the web.
- Talk to bot.
- Find good and bad parts in the conversation.
- Redefine the mental image of what should (and should _not_) a good chatbot UX
  consist of.
- Repeat the process until no further improvements in both conversation quality
  and evaluation criteria understanding.

And so it seemed unrational for me to build an automatized evaluation pipeline
right from the beginning because I don't know yet the criteria I need. I would
love to first get the golden conversation I love and then develop a formal
criteria from it.

And so my MVP includes the prompt with elaborate description, evaluation
criteria and next steps for both improving the prompt and creating a more
sophisticated system. It's not ideal and doesn't hold against my every
requirement, but in my opinion, it is quite better than many systems I found out
in the wild. You can check out example conversation
[here](https://chat.openai.com/share/57cbfe28-c24a-4d21-8c10-be034b3a4148).

### The prompt development

#### Qualities I tried to inject into the prompt

- stays in role, feels like real person
- fun, engaging, not boring
- empathetic, safe, emotional

The challenges while developing the prompt were of 2 sorts: what are these
qualities, and how to best inject them into the prompt.

#### Prompt parts

- Persona definition. I created Andy with goal of having fun experience in mind.
- Desirable traits. I tried to include all the pain points I found while
  chatting with chat bots ~~(and real people)~~ and address them in this part.
- Message examples and anti-examples. To make traits more clear (for both LLM
  and developer).
- Style guide. To make it talk like a real person would.
- Conversation goal. To accentuate what kind of experience our user may want.
- Conversation structure. Ice-breaker, casual talk, close relationships.

You can check out the current version of the prompt in the
[prompt file](./prompts.md).

## Future steps

There's a big room for heavy engineering in this task

### Chatbot

0. Improving LLM MVP.

   - Add more structure to the prompt. My current prompt is a bit of a mess
     (according to GPT-4 😅), that would be hard to follow even for human. I
     guess creating a more rigid structure would certainly help.
     - Persona → Traits → Style guide → Examples + Anti-examples → Goal →
       Converstaion structure
   - I explore ways to improve the current prompt in more detail in the Cons
     section of Andy v1 in the [HISTORY](./HISTORY.md) file.
   - Inject into system prompt and play with generation parameters (e.g.
     temperature). I mostly used default ChatGPT3.5 UI because it's free and was
     enough for my initial explorations of the problem.
   - Try GPT4/Claude2.
   - Also trying some open-source LLMs may be beneficial
     - How far we can get without special finetuning
     - What are pros and cons of models finetuned for dialogue

1. Collecting the dataset of good dialogues

   - Web
     - Reddit threads (not exactly dialogue, but the style of speech is what we
       would need)
     - Youtube transcripts of people talking
     - Telegram/Discord group chats (not exactly dialogue, but still close)
   - Hugging Face
     - [daily dialog](https://huggingface.co/datasets/daily_dialog) with normal
       dialogues (and even emotion/action labels)
   - Asking LLM to talk to other LLM
     - Alpaca-like self-instruct (I would start from
       [saiga roleplay](https://huggingface.co/datasets/IlyaGusev/gpt_roleplay_realm))
     - Scraping character.ai via LLM (for research purposes only 😉)
     - **using the prompt I created**. If it's good enugh, we can use it a
       starting point to generate quality dialogues. It can be easily adapted to
       also describe a user (another LLM talking to bot).

2. Finetuning open source models for conversation.

- Why
  - Better inject the style and behaviour into our model.
  - User (and we) may not like the idea of their data going to OpenAI.
  - It is more economically reasonable to host your own LLM.
  - We may overcome limitations of censoring from other authority.
- How
  - I would start from uncensored versions of LLAMA like
    [this one](https://huggingface.co/georgesung/llama2_7b_chat_uncensored) so
    that our chatbot won't be overly moralizing and not acting as "assistant".

3. Creating an agent system.

   - To
     - Track the stage of the conversation (ice-breaker, casual, close)
     - Emotion recognition
     - Decision making (e.g. whether to go closer)
   - How
     - Use LLMs with different prompts like here and adding some
       post-processing/guardrailing on top
       - https://github.com/sheng-kai-wang/DST4LLM
       - https://github.com/logspace-ai/langflow
     - Train different classification models (stage, emotion, decision) if
       vanilla LLM would fail as an agent

### Evaluation pipeline

Disclaimer: I included "Ask LLM to do this for you" a lot in my future steps for
evaluation pipeline, but I clearly understand that it's limited in many ways.
LLM is a good and relatively cheap data and label generator, so it can be a good
starting point for lots of tasks described. And then we can re-label data with
assessors as needed and train smaller, cheaper and better quality models for the
tasks.

- Persona: does it behave in role?

  - pattern matching for "ai language model" and
    [similar](https://huggingface.co/datasets/anon8231489123/ShareGPT_Vicuna_unfiltered)
  - Ask LLM
  - Train separate classifier

- Traits

  - Look for
    - Showing the desired trait (e.g. conversation is fun)
    - Not showing the desired trait (e.g. not telling stories about themselves)
    - Showing a not desired trait (e.g. over-obsessing with the user)
  - Track score per trait and also an aggregate one.

- Style guide: does it chat like real person would?

  - "Acting as assistant"
    - May check for examples
      [here](https://huggingface.co/datasets/anon8231489123/ShareGPT_Vicuna_unfiltered)
    - Train sentiment model for "духота"
  - Slang usage
  - Message length
  - Starts with capital letter
  - Ends every message with question

- Examples and Anti-examples: does any of this happen in a conversation?

  - Check against examples by

    - pattern matching
    - embedding similarity
    - paraphrasing
    - asking LLM whether the message contains
      - may be too costly for frequent re-evaluation and many examples
      - but may be required for some examples

  - We can iteratively collect library of these examples

    - Generate similar to those we already have
      - using [paraphrasers](https://huggingface.co/inkoziev/paraphraser)
      - asking LLM to generate similar, like in self-instruction.
    - Find similar in our database
      - in user messages
      - in collected data
      - in our generations

- Goal

  - Ask LLM whether goals are achieved during the conversation
  - Collect noisy indirect labels from users (e.g. from likes, in-chat action
    counts, time spent)

- Conversaion structure
  - Count messages to check at which stage we should be at the given message
  - Cut conversation at some message and ask LLM to label on which stage people
    are
  - Sometimes we can do keyword matching (e.g. "kiss" may mean we are at close
    relationships stage)
  - Train a separate model to check dialogue state

## How to use

I mostly tested the solution via default ChatGPT3.5 UI because it's free and was
enough for my initial explorations of the problem. You can also talk with Andy
using any chatbot UI implementation selecting both 3.5 and 4 versions like this
one (needs OpenAI API key).

```sh
docker run -e OPENAI_API_KEY=xxxxxxxx -p 3000:3000 ghcr.io/mckaywrigley/chatbot-ui:main
```
