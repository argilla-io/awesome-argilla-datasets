# ShareGPT

## Context

The ShareGPT dataset is a dataset that was collected by public users who were using the Google Chrome extension offered by [sharegpt.com](sharegpt.com) to share their ChatGPT conversations. This data should mimic real-life usage of the model and can therefore be used to fine-tune a model for an actual scenario. Additionally, Google was accused of using this dataset as a baseline to train its [BARD](https://www.theverge.com/2023/3/29/23662621/google-bard-chatgpt-sharegpt-training-denies) model.

We decided to use a random subset of the raw version of the dataset including all conversations but we did filter out non-English conversation. The raw dataset used can be found on [the Hugging Face hub](https://huggingface.co/datasets/zetavg/ShareGPT-Processed).

### Goals

- Classification of the dataset.
    - Prompt quality
    - Prompt intent
    - Prompt toxicity
- Training and publishing an open-source model.

### Outcomes

- [Hugging Face dataset](https://huggingface.co/datasets?sort=trending&search=argilla).
- [Hugging Face model](https://huggingface.co/models?sort=trending&search=argilla).
- [Streamlit dashboard for annotators](https://streamlit.io/).

### Features and libraries

- We used [Text Descriptives](https://github.com/HLasse/TextDescriptives) as [Argilla metadata filters](https://docs.argilla.io/en/latest/practical_guides/filter_dataset.html)
- We used [streamlit](https://streamlit.io/) to create a dashboard for annotators.

### Learnings and insights

- Could we use `datset-config.yml` files to configure datasets like we do for the `datasets` library?
- Would we be able to randomly distribute record per user within the same dataset to avoid bias and ensure an even distribution of records per user?
- How can we keep track of active time an annotator spends on a record or even better, a question?

## Annotation Guidelines

The ShareGPT dataset is a dataset that was collected by public users who were using the Google Chrome extension offered by [sharegpt.com](sharegpt.com) to share their ChatGPT conversations. This data should mimic real-life usage of the model and can therefore be used to fine-tune a model for an actual scenario. Additionally, Google was accused of using this dataset as a baseline to train its [BARD](https://www.theverge.com/2023/3/29/23662621/google-bard-chatgpt-sharegpt-training-denies) model.

We decided to use a random subset of the raw version of the dataset including all conversations but we did filter out non-English conversation. The raw dataset used can be found on [the Hugging Face hub](https://huggingface.co/datasets/zetavg/ShareGPT-Processed).

### Classification Tasks

The dataset aims to classify three things:

1. Quality
2. Intent
3. Toxicity

#### Quality

For the quality, we have decided to define a rating question on a scale from 1 to 7. This question is used to assess the quality of the prompt, based on quality, grammar and clarity of context.

#### Intent

For the intent, we have decided to define a multi-label classification question which will be used to determine the prompt types as defined in the [Llama 2 paper](https://arxiv.org/abs/2307.09288). This outlines a good distribution of the types of prompts we should use for fine-tuning an LLM.

- Generation: A statement that indicates the need for open generation.
- Rewrite: A statement that is rewritten by the model.
- Extract: A question that is answered by extracted from the context in the prompt.
- Closed QA: A question that is answered by the model based on the context.
- Open QA: A question that is answered by the model without any context.
- Classification: A statement that is classified by the model.
- Summarization: A summary of the context.
- Brainstorming: A list of ideas or concepts.
- Chat: A chat between two people.
- Code: A statement about code or programming.
- Other: A prompt that does not fit into any of the above categories.

#### Toxicity

For the Toxicity, we decided to use the [Guardrailing Mistral](https://docs.mistral.ai/usage/guardrailing) proposal as a reference. These labels are initially fine-grained but for the overall dataset, we will use a simplified version of these labels. As proposed by the Mistral team.

- Illegal: Illegal activity.
- Child abuse: child sexual abuse material or any content that exploits or harms children.
- Hate violence harassment: Generation of hateful, harassing, or violent content: content that expresses, incites, or promotes hate based on identity, content that intends to harass, threaten, or bully an individual, content that promotes or glorifies violence or celebrates the suffering or humiliation of others.
- Malware: Generation of malware: content that attempts to generate code that is designed to disrupt, damage, or gain unauthorized access to a computer system.
- Physical harm: activity that has high risk of physical harm, including: weapons development, military and warfare, management or operation of critical infrastructure in energy, transportation, and water, content that promotes, encourages, or depicts acts of self-harm, such as suicide, cutting, and eating disorders.
- Economic harm: activity that has high risk of economic harm, including: multi-level marketing, gambling, payday lending, automated determinations of eligibility for credit, employment, educational institutions, or public assistance services.
- Fraud: Fraudulent or deceptive activity, including: scams, coordinated inauthentic behavior, plagiarism, academic dishonesty, astroturfing, such as fake grassroots support or fake review generation, disinformation, spam, pseudo-pharmaceuticals.
- Adult: Adult content, adult industries, and dating apps, including: content meant to arouse sexual excitement, such as the description of sexual activity, or that promotes sexual services (excluding sex education and wellness), erotic chat, pornography.
- Political: Political campaigning or lobbying, by: generating high volumes of campaign materials, generating campaign materials personalized to or targeted at specific demographics, building conversational or interactive systems such as chatbots that provide information about campaigns or engage in political advocacy or lobbying, building products for political campaigning or lobbying purposes.
- Privacy: Activity that violates people's privacy, including: tracking or monitoring an individual without their consent, facial recognition of private individuals, classifying individuals based on protected characteristics, using biometrics for identification or assessment, unlawful collection or disclosure of personal identifiable information or educational, financial, or other protected records.
- Unqualified law: Engaging in the unauthorized practice of law, or offering tailored legal advice without a qualified person reviewing the information.
- Unqualified financial: Offering tailored financial advice without a qualified person reviewing the information.
- Unqualified health: Telling someone that they have or do not have a certain health condition, or providing instructions on how to cure or treat a health condition.

These have been mapped to the following simplified labels:

- Illegal: Illegal activities such as terrorism, child abuse or fraud.
- Harmful: Hateful, harassing or violent content such as discrimination, self-harm or bullying.
- Unqualified advice: Unqualified advice for instance in legal, medical or financial domains.

## Dataset Creation

### The base

We created the dataset by taking this Hugging Face dataset as a baseline. We chose to use a non-filtered dataset as a baseline to ensure it has decent coverage on intents, toxicity and classification.