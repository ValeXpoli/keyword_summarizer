# Keyword Summarizer

**Keyword Summarizer** is a Python library that automates text summarization by:
1. Extracting **keywords** with [KeyBERT](https://github.com/MaartenGr/KeyBERT).
2. Enriching the input text with these keywords as special tokens.
3. Summarizing the enriched text using **fine-tuned BART** models, such as:
   - [`VexPoli/distilbart-summarization-top-single`](https://huggingface.co/VexPoli/distilbart-summarization-top-single)  
   - [`VexPoli/distilbart-summarization-top-list`](https://huggingface.co/VexPoli/distilbart-summarization-top-list)

## Installation

To install from this GitHub repository, run:

```bash
pip install git+https://github.com/ValeXpoli/keyword_summarizer.git
```

Model Selection

    model_type="single" uses VexPoli/distilbart-summarization-top-single.
    model_type="list" uses VexPoli/distilbart-summarization-top-list.

Function Parameters

    text (str): The article or text to be summarized.
    model_type (str): Either "single" (one <keyword>...</keyword> block) or "list" (multiple <keyword>...</keyword> blocks).
    top_n_keywords (int): Number of keywords to extract (default: 10).
    keyphrase_ngram_range (tuple): Range for KeyBERT’s keyword extraction (default: (1, 2)).
    stop_words (str): Language or set of stopwords for KeyBERT (default: "english").
    use_mmr (bool): Whether to use Maximal Marginal Relevance (MMR) for reducing redundancy among keywords (default: True).
    diversity (float): MMR diversity level (0.0 = minimal diversity, 1.0 = maximal diversity).
    max_length (int): Maximum length of the generated summary (default: 128).
    num_beams (int): Number of beams for beam search during generation (default: 4).
