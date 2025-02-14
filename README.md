# Keyword Summarizer

**Keyword Summarizer** is a Python library that automates text summarization by:
1. Extracting **keywords** with [KeyBERT](https://github.com/MaartenGr/KeyBERT).
2. Enriching the input text with these keywords as special tokens.
3. Summarizing the enriched text using **fine-tuned BART** models:
   - [`VexPoli/distilbart-summarization-top-single`](https://huggingface.co/VexPoli/distilbart-summarization-top-single)  
   - [`VexPoli/distilbart-summarization-top-list`](https://huggingface.co/VexPoli/distilbart-summarization-top-list)

## Installation

To install from this GitHub repository, run:

```bash
pip install git+https://github.com/ValeXpoli/keyword_summarizer.git
```

## Model Selection

    model_type="single" uses VexPoli/distilbart-summarization-top-single.
    model_type="list" uses VexPoli/distilbart-summarization-top-list.

## Function Parameters

    text (str): The article or text to be summarized.
    model_type (str): Either "single" (one <keyword>...</keyword> block) or "list" (multiple <keyword>...</keyword> blocks).
    top_n_keywords (int): Number of keywords to extract (default: 10).
    keyphrase_ngram_range (tuple): Range for KeyBERT’s keyword extraction (default: (1, 2)).
    stop_words (str): Language or set of stopwords for KeyBERT (default: "english").
    use_mmr (bool): Whether to use Maximal Marginal Relevance (MMR) for reducing redundancy among keywords (default: True).
    diversity (float): MMR diversity level (0.0 = minimal diversity, 1.0 = maximal diversity).
    max_length (int): Maximum length of the generated summary (default: 128).
    num_beams (int): Number of beams for beam search during generation (default: 4).
## Usage

After installing, import and use the main function summarize_with_keywords from the keyword_summarizer package:


<pre>
   
from keyword_summarizer import summarize_with_keywords

text_example = (
    "Manchester City have been restricted to a net transfer spend of £49m. "
    "The club also had to keep its overall wage bill to the current level of £205m. "
    "These punishments were imposed by UEFA for breaching Financial Fair Play rules. "
    "The spending restrictions apply to this season and the next one, "
    "but City are confident they will be lifted early after their compliance."
)

# Summarize using the single-token approach (VexPoli/distilbart-summarization-top-single)
summary_single = summarize_with_keywords(
    text_example,
    model_type="single",  # "single" or "list"
    top_n_keywords=5      # Extract 5 keywords
)
print("Single-token model summary:\n", summary_single)

# Summarize using the multi-token (list) approach (VexPoli/distilbart-summarization-top-list)
summary_list = summarize_with_keywords(
    text_example,
    model_type="list",
    top_n_keywords=5
)
print("\nList model summary:\n", summary_list)
</pre>
## Requirements

    Python 3.7+
    PyTorch >= 1.9.0
    Transformers >= 4.0.0
    Sentence-Transformers >= 2.2.2
    KeyBERT >= 0.7.0
    
    By installing via the GitHub link, these dependencies are automatically fetched and installed.

## Acknowledgments

    Hugging Face Transformers and Sentence-Transformers for core NLP components.
    KeyBERT for keyword extraction.
    annalisa-belloni,demidavi7, valepetr and VexPoli for publishing fine-tuned DistilBART models on the Hugging Face Hub.
