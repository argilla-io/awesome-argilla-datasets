# ShareGPT

## Context

The ShareGPT dataset was a collection of 100

### Goals

- Red teaming for intent/harmfulness detection.
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


The dataset is created in Argilla with: **fields**, **questions**, **suggestions**, **metadata**, and **guidelines**.

The **fields** are the dataset records themselves, for the moment just text fields are supported. These are the ones that will be used to provide responses to the questions.

| Field Name | Title | Type | Required | Markdown |
| ---------- | ----- | ---- | -------- | -------- |
| prompt | Prompt | text | True | True |
| context | Context | text | False | True |


The **questions** are the questions that will be asked to the annotators. They can be of different types, such as rating, text, label_selection, multi_label_selection, or ranking.

| Question Name | Title | Type | Required | Description | Values/Labels |
| ------------- | ----- | ---- | -------- | ----------- | ------------- |
| response | Response | text | True | Write the response to the instruction. | N/A |

Hate Speech, Self-harm, Sexual, Crime, Fraud, Banned Substances, Misinformation, PII, Bullying, Unethical, Discrimination, Other

"text-based AI language model", "domestic violence", "please refrain", "derogatory", "inappropriate", "offensive", "racism", "racist", "racial", "discriminate", "discriminatory", "discrimination", "sexist", "sexism", "unacceptable", "inclusive workplace", "lgbt", "morals", "ethics", "ethical", "legality", "illegal", "illegality", "hateful", "harmful", "it is never okay", "It is important to", "It's important to", "real-world consequences", "hate speech", "glorify", "not be appropriate", "supremacist", "extremist", "responsible AI", "AI principles", "AI assistant", "an AI language", "ableist", "hurtful", "gender stereotype", "gender inequality", "underrepresentation", "safe spaces", "gender-based", "inclusivity", "feminist", "feminism", "transgender", "empowerment", "communist", "capitalism", "stereotypes", "biases", "bias", "Microaggression", "prioritize human safety", "as a language model", "as an AI language model", "As a large language model", "As an AI", "ethical principles", "consensual", "it is not appropriate", "it's not appropriate", "I cannot fulfill your request", "harmful to human beings", "ethical guidelines", "my guidelines", "prioritize user safety", "adhere to ethical guidelines", "harmful consequences", "potentially harmful", "dangerous activities", "promote safety", "well-being of all users", "responsible information sharing", "jeopardize the safety", "illegal actions or intentions", "undermine the stability", "promote the well-being", "illegal activities or actions", "adherence to the law", "potentially be harmful", "illegal substances or activities", "committed to promoting", "safe information", "lawful information", "cannot provide guidance", "cannot provide information", "unable to offer assistance", "cannot engage in discussions", "programming prohibits", "follow ethical guidelines", "ensure the safety", "involves an illegal subject", "prioritize safety", "illegal subject", "prioritize user well-being", "cannot support or promote", "activities that could harm", "pose a risk to others", "against my programming", "activities that could undermine", "potentially dangerous", "not within the scope", "designed to prioritize safety", "not able to provide", "maintain user safety", "adhere to safety guidelines", "dangerous or harmful", "cannot provide any information", "focus on promoting safety"

The **suggestions** are human or machine generated recommendations for each question to assist the annotator during the annotation process, so those are always linked to the existing questions, and named appending "-suggestion" and "-suggestion-metadata" to those, containing the value/s of the suggestion and its metadata, respectively. So on, the possible values are the same as in the table above, but the column name is appended with "-suggestion" and the metadata is appended with "-suggestion-metadata".

**✨ NEW** The **metadata** is a dictionary that can be used to provide additional information about the dataset record. This can be useful to provide additional context to the annotators, or to provide additional information about the dataset record itself. For example, you can use this to provide a link to the original source of the dataset record, or to provide additional information about the dataset record itself, such as the author, the date, or the source. The metadata is always optional, and can be potentially linked to the `metadata_properties` defined in the dataset configuration file in `argilla.yaml`.

The **guidelines**, are optional as well, and are just a plain string that can be used to provide instructions to the annotators. Find those in the [annotation guidelines](#annotation-guidelines) section.

### Data Instances

An example of a dataset instance in Argilla looks as follows:

```json
{
    "external_id": null,
    "fields": {
        "prompt": "How to tell if a customer segment is well segmented? In 3 bullet points."
    },
    "metadata": {
        "prompt_alpha_ratio": 0.8125,
        "prompt_automated_readability_index": 1.24642857142857,
        "prompt_coleman_liau_index": 3.9114285714285693,
        "prompt_dependency_distance_mean": 2.3181818181818183,
        "prompt_dependency_distance_std": 0.3181818181818181,
        "prompt_doc_length": 16.0,
        "prompt_duplicate_line_chr_fraction": 0.0,
        "prompt_duplicate_ngram_chr_fraction_10": 0.0,
        "prompt_duplicate_ngram_chr_fraction_5": 0.0,
        "prompt_duplicate_ngram_chr_fraction_6": 0.0,
        "prompt_duplicate_ngram_chr_fraction_7": 0.0,
        "prompt_duplicate_ngram_chr_fraction_8": 0.0,
        "prompt_duplicate_ngram_chr_fraction_9": 0.0,
        "prompt_duplicate_paragraph_chr_fraction": 0.0,
        "prompt_entropy": 0.4249943780917443,
        "prompt_flesch_kincaid_grade": 3.997142857142858,
        "prompt_flesch_reading_ease": 78.87285714285717,
        "prompt_gunning_fog": 8.514285714285714,
        "prompt_lix": 28.428571428571427,
        "prompt_mean_word_length": 3.6875,
        "prompt_n_characters": 59,
        "prompt_n_sentences": 2,
        "prompt_n_stop_words": 7.0,
        "prompt_n_tokens": 14,
        "prompt_n_unique_tokens": 14,
        "prompt_oov_ratio": 0.0,
        "prompt_passed_quality_check": "True",
        "prompt_per_word_perplexity": 0.0955988637794089,
        "prompt_perplexity": 1.5295818204705425,
        "prompt_pos_prop_ADJ": 0.0,
        "prompt_pos_prop_ADP": 0.0625,
        "prompt_pos_prop_ADV": 0.0625,
        "prompt_pos_prop_AUX": 0.0625,
        "prompt_pos_prop_CCONJ": 0.0,
        "prompt_pos_prop_DET": 0.0625,
        "prompt_pos_prop_INTJ": 0.0,
        "prompt_pos_prop_NOUN": 0.25,
        "prompt_pos_prop_NUM": 0.0625,
        "prompt_pos_prop_PART": 0.0625,
        "prompt_pos_prop_PRON": 0.0,
        "prompt_pos_prop_PROPN": 0.0,
        "prompt_pos_prop_PUNCT": 0.125,
        "prompt_pos_prop_SCONJ": 0.125,
        "prompt_pos_prop_SYM": 0.0,
        "prompt_pos_prop_VERB": 0.125,
        "prompt_pos_prop_X": 0.0,
        "prompt_prop_adjacent_dependency_relation_mean": 0.28181818181818186,
        "prompt_prop_adjacent_dependency_relation_std": 0.08181818181818182,
        "prompt_proportion_bullet_points": 0.0,
        "prompt_proportion_ellipsis": 0.0,
        "prompt_proportion_unique_tokens": 1.0,
        "prompt_rix": 1.5,
        "prompt_sentence_length_mean": 7.0,
        "prompt_sentence_length_median": 7.0,
        "prompt_sentence_length_std": 3.0,
        "prompt_syllables_per_token_mean": 1.4285714285714286,
        "prompt_syllables_per_token_median": 1.0,
        "prompt_syllables_per_token_std": 0.7284313590846836,
        "prompt_symbol_to_word_ratio_#": 0.0,
        "prompt_token_length_mean": 4.071428571428571,
        "prompt_token_length_median": 3.5,
        "prompt_token_length_std": 2.5763841138387766,
        "prompt_top_ngram_chr_fraction_2": 0.0,
        "prompt_top_ngram_chr_fraction_3": 0.0,
        "prompt_top_ngram_chr_fraction_4": 0.0,
        "response_alpha_ratio": 0.7857142857142857,
        "response_automated_readability_index": 11.4375,
        "response_coleman_liau_index": 16.030000000000005,
        "response_dependency_distance_mean": 2.0984405458089666,
        "response_dependency_distance_std": 1.2368394170758057,
        "response_doc_length": 70.0,
        "response_duplicate_line_chr_fraction": 0.0,
        "response_duplicate_ngram_chr_fraction_10": 0.0,
        "response_duplicate_ngram_chr_fraction_5": 0.14761904761904762,
        "response_duplicate_ngram_chr_fraction_6": 0.0,
        "response_duplicate_ngram_chr_fraction_7": 0.0,
        "response_duplicate_ngram_chr_fraction_8": 0.0,
        "response_duplicate_ngram_chr_fraction_9": 0.0,
        "response_duplicate_paragraph_chr_fraction": 0.0,
        "response_entropy": 1.925080903607536,
        "response_flesch_kincaid_grade": 10.533333333333335,
        "response_flesch_reading_ease": 37.35500000000002,
        "response_gunning_fog": 14.0,
        "response_lix": 46.666666666666664,
        "response_mean_word_length": 5.214285714285714,
        "response_n_characters": 365,
        "response_n_sentences": 6,
        "response_n_stop_words": 26.0,
        "response_n_tokens": 60,
        "response_n_unique_tokens": 37,
        "response_oov_ratio": 0.02857142857142857,
        "response_passed_quality_check": "True",
        "response_per_word_perplexity": 0.09793861849416963,
        "response_perplexity": 6.855703294591874,
        "response_pos_prop_ADJ": 0.05714285714285714,
        "response_pos_prop_ADP": 0.1,
        "response_pos_prop_ADV": 0.04285714285714286,
        "response_pos_prop_AUX": 0.07142857142857142,
        "response_pos_prop_CCONJ": 0.05714285714285714,
        "response_pos_prop_DET": 0.07142857142857142,
        "response_pos_prop_INTJ": 0.0,
        "response_pos_prop_NOUN": 0.2571428571428571,
        "response_pos_prop_NUM": 0.0,
        "response_pos_prop_PART": 0.02857142857142857,
        "response_pos_prop_PRON": 0.02857142857142857,
        "response_pos_prop_PROPN": 0.0,
        "response_pos_prop_PUNCT": 0.14285714285714285,
        "response_pos_prop_SCONJ": 0.0,
        "response_pos_prop_SYM": 0.0,
        "response_pos_prop_VERB": 0.07142857142857142,
        "response_pos_prop_X": 0.04285714285714286,
        "response_prop_adjacent_dependency_relation_mean": 0.4988304093567251,
        "response_prop_adjacent_dependency_relation_std": 0.017298478897952083,
        "response_proportion_bullet_points": 0.0,
        "response_proportion_ellipsis": 0.0,
        "response_proportion_unique_tokens": 0.6166666666666667,
        "response_rix": 3.6666666666666665,
        "response_sentence_length_mean": 10.0,
        "response_sentence_length_median": 13.0,
        "response_sentence_length_std": 6.506407098647712,
        "response_syllables_per_token_mean": 1.8833333333333333,
        "response_syllables_per_token_median": 1.0,
        "response_syllables_per_token_std": 1.2528855583101843,
        "response_symbol_to_word_ratio_#": 0.0,
        "response_token_length_mean": 5.916666666666667,
        "response_token_length_median": 6.0,
        "response_token_length_std": 3.742956347891626,
        "response_top_ngram_chr_fraction_2": 0.13333333333333333,
        "response_top_ngram_chr_fraction_3": 0.09285714285714286,
        "response_top_ngram_chr_fraction_4": 0.14285714285714285
    },
    "responses": [],
    "suggestions": [
        {
            "agent": null,
            "question_name": "response",
            "score": null,
            "type": null,
            "value": "1. Homogeneity: The segment should consist of customers who share similar characteristics and behaviors.\n2. Distinctiveness: The segment should be different from other segments in terms of their characteristics and behaviors.\n3. Stability: The segment should remain relatively stable over time and not change drastically. The characteristics and behaviors of customers within the segment should not change significantly."
        }
    ]
}
```

While the same record in HuggingFace `datasets` looks as follows:

```json
{
    "context": null,
    "external_id": null,
    "metadata": "{\"prompt_flesch_reading_ease\": 78.87285714285717, \"prompt_flesch_kincaid_grade\": 3.997142857142858, \"prompt_gunning_fog\": 8.514285714285714, \"prompt_automated_readability_index\": 1.24642857142857, \"prompt_coleman_liau_index\": 3.9114285714285693, \"prompt_lix\": 28.428571428571427, \"prompt_rix\": 1.5, \"prompt_entropy\": 0.4249943780917443, \"prompt_perplexity\": 1.5295818204705425, \"prompt_per_word_perplexity\": 0.0955988637794089, \"prompt_passed_quality_check\": \"True\", \"prompt_n_stop_words\": 7.0, \"prompt_alpha_ratio\": 0.8125, \"prompt_mean_word_length\": 3.6875, \"prompt_doc_length\": 16.0, \"prompt_symbol_to_word_ratio_#\": 0.0, \"prompt_proportion_ellipsis\": 0.0, \"prompt_proportion_bullet_points\": 0.0, \"prompt_duplicate_line_chr_fraction\": 0.0, \"prompt_duplicate_paragraph_chr_fraction\": 0.0, \"prompt_duplicate_ngram_chr_fraction_5\": 0.0, \"prompt_duplicate_ngram_chr_fraction_6\": 0.0, \"prompt_duplicate_ngram_chr_fraction_7\": 0.0, \"prompt_duplicate_ngram_chr_fraction_8\": 0.0, \"prompt_duplicate_ngram_chr_fraction_9\": 0.0, \"prompt_duplicate_ngram_chr_fraction_10\": 0.0, \"prompt_top_ngram_chr_fraction_2\": 0.0, \"prompt_top_ngram_chr_fraction_3\": 0.0, \"prompt_top_ngram_chr_fraction_4\": 0.0, \"prompt_oov_ratio\": 0.0, \"prompt_dependency_distance_mean\": 2.3181818181818183, \"prompt_dependency_distance_std\": 0.3181818181818181, \"prompt_prop_adjacent_dependency_relation_mean\": 0.28181818181818186, \"prompt_prop_adjacent_dependency_relation_std\": 0.08181818181818182, \"prompt_pos_prop_ADJ\": 0.0, \"prompt_pos_prop_ADP\": 0.0625, \"prompt_pos_prop_ADV\": 0.0625, \"prompt_pos_prop_AUX\": 0.0625, \"prompt_pos_prop_CCONJ\": 0.0, \"prompt_pos_prop_DET\": 0.0625, \"prompt_pos_prop_INTJ\": 0.0, \"prompt_pos_prop_NOUN\": 0.25, \"prompt_pos_prop_NUM\": 0.0625, \"prompt_pos_prop_PART\": 0.0625, \"prompt_pos_prop_PRON\": 0.0, \"prompt_pos_prop_PROPN\": 0.0, \"prompt_pos_prop_PUNCT\": 0.125, \"prompt_pos_prop_SCONJ\": 0.125, \"prompt_pos_prop_SYM\": 0.0, \"prompt_pos_prop_VERB\": 0.125, \"prompt_pos_prop_X\": 0.0, \"prompt_token_length_mean\": 4.071428571428571, \"prompt_token_length_median\": 3.5, \"prompt_token_length_std\": 2.5763841138387766, \"prompt_sentence_length_mean\": 7.0, \"prompt_sentence_length_median\": 7.0, \"prompt_sentence_length_std\": 3.0, \"prompt_syllables_per_token_mean\": 1.4285714285714286, \"prompt_syllables_per_token_median\": 1.0, \"prompt_syllables_per_token_std\": 0.7284313590846836, \"prompt_n_tokens\": 14, \"prompt_n_unique_tokens\": 14, \"prompt_proportion_unique_tokens\": 1.0, \"prompt_n_characters\": 59, \"prompt_n_sentences\": 2, \"response_flesch_reading_ease\": 37.35500000000002, \"response_flesch_kincaid_grade\": 10.533333333333335, \"response_gunning_fog\": 14.0, \"response_automated_readability_index\": 11.4375, \"response_coleman_liau_index\": 16.030000000000005, \"response_lix\": 46.666666666666664, \"response_rix\": 3.6666666666666665, \"response_entropy\": 1.925080903607536, \"response_perplexity\": 6.855703294591874, \"response_per_word_perplexity\": 0.09793861849416963, \"response_passed_quality_check\": \"True\", \"response_n_stop_words\": 26.0, \"response_alpha_ratio\": 0.7857142857142857, \"response_mean_word_length\": 5.214285714285714, \"response_doc_length\": 70.0, \"response_symbol_to_word_ratio_#\": 0.0, \"response_proportion_ellipsis\": 0.0, \"response_proportion_bullet_points\": 0.0, \"response_duplicate_line_chr_fraction\": 0.0, \"response_duplicate_paragraph_chr_fraction\": 0.0, \"response_duplicate_ngram_chr_fraction_5\": 0.14761904761904762, \"response_duplicate_ngram_chr_fraction_6\": 0.0, \"response_duplicate_ngram_chr_fraction_7\": 0.0, \"response_duplicate_ngram_chr_fraction_8\": 0.0, \"response_duplicate_ngram_chr_fraction_9\": 0.0, \"response_duplicate_ngram_chr_fraction_10\": 0.0, \"response_top_ngram_chr_fraction_2\": 0.13333333333333333, \"response_top_ngram_chr_fraction_3\": 0.09285714285714286, \"response_top_ngram_chr_fraction_4\": 0.14285714285714285, \"response_oov_ratio\": 0.02857142857142857, \"response_dependency_distance_mean\": 2.0984405458089666, \"response_dependency_distance_std\": 1.2368394170758057, \"response_prop_adjacent_dependency_relation_mean\": 0.4988304093567251, \"response_prop_adjacent_dependency_relation_std\": 0.017298478897952083, \"response_pos_prop_ADJ\": 0.05714285714285714, \"response_pos_prop_ADP\": 0.1, \"response_pos_prop_ADV\": 0.04285714285714286, \"response_pos_prop_AUX\": 0.07142857142857142, \"response_pos_prop_CCONJ\": 0.05714285714285714, \"response_pos_prop_DET\": 0.07142857142857142, \"response_pos_prop_INTJ\": 0.0, \"response_pos_prop_NOUN\": 0.2571428571428571, \"response_pos_prop_NUM\": 0.0, \"response_pos_prop_PART\": 0.02857142857142857, \"response_pos_prop_PRON\": 0.02857142857142857, \"response_pos_prop_PROPN\": 0.0, \"response_pos_prop_PUNCT\": 0.14285714285714285, \"response_pos_prop_SCONJ\": 0.0, \"response_pos_prop_SYM\": 0.0, \"response_pos_prop_VERB\": 0.07142857142857142, \"response_pos_prop_X\": 0.04285714285714286, \"response_token_length_mean\": 5.916666666666667, \"response_token_length_median\": 6.0, \"response_token_length_std\": 3.742956347891626, \"response_sentence_length_mean\": 10.0, \"response_sentence_length_median\": 13.0, \"response_sentence_length_std\": 6.506407098647712, \"response_syllables_per_token_mean\": 1.8833333333333333, \"response_syllables_per_token_median\": 1.0, \"response_syllables_per_token_std\": 1.2528855583101843, \"response_n_tokens\": 60, \"response_n_unique_tokens\": 37, \"response_proportion_unique_tokens\": 0.6166666666666667, \"response_n_characters\": 365, \"response_n_sentences\": 6}",
    "prompt": "How to tell if a customer segment is well segmented? In 3 bullet points.",
    "response": [],
    "response-suggestion": "1. Homogeneity: The segment should consist of customers who share similar characteristics and behaviors.\n2. Distinctiveness: The segment should be different from other segments in terms of their characteristics and behaviors.\n3. Stability: The segment should remain relatively stable over time and not change drastically. The characteristics and behaviors of customers within the segment should not change significantly.",
    "response-suggestion-metadata": {
        "agent": null,
        "score": null,
        "type": null
    }
}
```

### Data Fields

Among the dataset fields, we differentiate between the following:

* **Fields:** These are the dataset records themselves, for the moment just text fields are supported. These are the ones that will be used to provide responses to the questions.

    * **prompt** is of type `text`.
    * (optional) **context** is of type `text`.

* **Questions:** These are the questions that will be asked to the annotators. They can be of different types, such as `RatingQuestion`, `TextQuestion`, `LabelQuestion`, `MultiLabelQuestion`, and `RankingQuestion`.

    * **response** is of type `text`, and description "Write the response to the instruction.".

* **Suggestions:** As of Argilla 1.13.0, the suggestions have been included to provide the annotators with suggestions to ease or assist during the annotation process. Suggestions are linked to the existing questions, are always optional, and contain not just the suggestion itself, but also the metadata linked to it, if applicable.

    * (optional) **response-suggestion** is of type `text`.

Additionally, we also have two more fields that are optional and are the following:

* **✨ NEW** **metadata:** This is an optional field that can be used to provide additional information about the dataset record. This can be useful to provide additional context to the annotators, or to provide additional information about the dataset record itself. For example, you can use this to provide a link to the original source of the dataset record, or to provide additional information about the dataset record itself, such as the author, the date, or the source. The metadata is always optional, and can be potentially linked to the `metadata_properties` defined in the dataset configuration file in `argilla.yaml`.
* **external_id:** This is an optional field that can be used to provide an external ID for the dataset record. This can be useful if you want to link the dataset record to an external resource, such as a database or a file.

### Data Splits

The dataset contains a single split, which is `train`.