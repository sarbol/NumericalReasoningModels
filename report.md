# Evaluating Programmatic Reasoning in LLMs with the ConFinQA Dataset

The **ConFinQA dataset** evaluates the performance and potential application of Language Models (LLMs) in the finance domain. The dataset contains questions that challenge models to:

- Retrieve relevant data,
- Perform numerical reasoning,
- Execute arithmetic operations to provide the correct answer.

Recent advancements in large pre-trained language models have made them excel in modeling language patterns, but they still struggle with tasks requiring **complex reasoning ability**.

This report investigates the performance of three large language models on the ConFinQA dataset:

- **GPT-4o**
- **03-mini**
- **Qwen2.5-14B**

These models have demonstrated impressive reasoning capabilities on standard benchmarks suggesting they might perform well on this task. On the MATH benchmark GPT-4o scored 75.9%, 03-mini scored 97.3% and Qwen2.5-14B scored 55.6%. Another important benchmark that test domain specific knowledge is the Open Financial LLM Leaderboard where GPT4-turbo have an Average Performance of 39.2% and Qwen2.5-7B 28.2%. GPT-4o and 03-mini models are currently not benchmarked on this leaderboard but they are successor to GPT4-turbo and are expected to have equivalent or better performance. Likewise Qwen2.5-14B is not benchmarked but a better performance is assumed.


## 📊 Dataset Structure
The data contains 3037 questions based on a financial report. Each question has 3 labeled answers

- A formatted answer
- A symbolic program
- The execution result of the program

Each question is grounded in a **financial report** with the following structure:

- `pre_text`
- `table`
- `post_text`

This serves as the **context** for answering the question.



## 🧠 Model Approach
A **zero-shot prompt** is issued to each model. This prompt:

1. Describes the **role** of the model.
2. Specifies the **task** to be performed.
3. Defines the **expected output**.

This task is focused on **numerical reasoning** — understanding a clear question, applying domain-specific knowledge, and performing high school-level mathematical operations.

### Why Zero-Shot?

- LLMs are trained on a **large corpus**, including financial texts.
- Few-shot prompts can **limit** model reasoning and induce copying behavior ([Zhiyu Chen et al]).
- Carefully selecting examples is impractical due to the **infinite question space**.

The prompt describes:

- Allowed operations
- Referencing mechanisms for intermediate steps
- Relevant constants
- Two output examples