# Chapter 1

## Concepts

* downloading data via `nltk.download` (UI)
* import helper `text` and `sent` values via `from nltk.book import *`
* show each occurrence of a word in a text via `text.concordance(...)`
* find words that appear in a similar context to another word with `text.similar(...)`
* find contexts shared by two or more words with `text.common_contexts([...])`
* display one or more words' location distributions within a text with `text.dispersion_plot([...])`
* generate text similar to another text via `text.generate` (deprecated)
* count the number of tokens in a text with `len(text)`
* count the number of distinct word types with `len(set(text))`
* calculate lexical diversity via `len(text) / len(set(text))`
  * i.e. the average number of times each word type occurs in a given text
* calculate the frequency of each vocabulary item in a text with `FreqDist(text)`
* view a cumulative frequency plot for the top n most common terms in a text with `fdist.plot(n, cumulative=True)`
* identify the hapaxes (words appearing only 1x) in a text with `fdist.hapaxes()`
* identify all words appearing m or more times in a text with at
  least n characters via `[w for w in set(text) if fdist[w] > m and len(w) >= n]`
* identify collocations (words occurring together unusually often) in a text with `text.collocations()`
* extract all bigrams from a text via `bigrams(text)`
* count the frequency of different word lengths in a text with `FreqDist([len(w) for w in text])`
	* review the functions an properties available on `FreqDist`
* review different ways to evaluate string values:
    * `startswith`, `endswith`, `s1 in s2`, `islower`, `isupper`, `isalpha`, etc.
* general NLP concepts
    * word sense disambiguation
    * pronoun resolution; anaphora resolution; semantic role labeling
    * generating language output
    * machine translation
    * spoken dialog systems
    * textual entailment

## Code Walkthrough

* topics: downloading corpora

```python
import nltk
nltk.download()
```

The following is just helper functionality to import a specific 
set of texts and sentences:

```python
from nltk.book import *
```

The above code basically sets up a bunch of `text` and `sent` variables, one for each corpus of
interest, using the following format:

```python
from nltk.corpus import inaugural
from nltk.text import Text

text4 = Text(inaugural.words(), name="Inaugural Address Corpus")

# and 

sent5 = ["I", "have", "a", "problem", "with", "people",
         "PMing", "me", "to", "lol", "JOIN"]
```


```python
# methods of the `nltk.text.Text` class

text1.concordance("monstrous") # ConcordanceIndex
text1.similar("monstrous")  # ContextIndex
text1.common_contexts(["monstrous", "very"]) # ContextIndex
text4.dispersion_plot(["citizens", "democracy", "freedom", "duties", "America"])  # nltk.draw.dispersion_plot
text3.generate()  # deprecated
```


```python
words = inaugural.words()
index = ConcordanceIndex(words)


```

Per the API Docs:

> A wrapper around a sequence of simple (string) tokens, which is intended to support initial exploration of texts (via the interactive console). Its methods perform a variety of analyses on the text’s contexts (e.g., counting, concordancing, collocation discovery), and display the results. If you wish to write a program which makes use of these analyses, then you should bypass the Text class, and use the appropriate analysis function or class directly instead.

Looking at the code for `nltk.text.Text`, it's methods all consist of code to leverage methods
on other nltk classes against the contained text of the `Text` object.

* [ ] review the methods and approach taken in each
* [ ] focus on the modules used in _those_ methods as a first step in investigating the nltk modules

* **nltk.text.ContextIndex**
    * `_default_context(tokens, i)`
    * `__init__(self, tokens, context_func=None, filter=None, key=lambda x:x)`
    * `tokens(self)`
    * `word_similarity_dict(self, word)`
    * `similar_words(self, word, n=20)`
    * `common_contexts(self, words, fail_on_unknown=False)`
* **nltk.text.ConcordanceIndex**
    * `__init__(self, tokens, key=lambda x:x)`
    * `tokens(self)`
    * `offsets(self, word)`
    * `__repr__(self)`
    * `find_concordance(self, word, width=80, lines=25)`
    * `print_concordance(self, word, width=80, lines=25)`
* **nltk.text.TokenSearcher**
    * `__init__(self, tokens)`
    * `findall(self, regexp)`
* **nltk.text.TextCollection**
    * `__init__(self, source)`
    * `tf(self, term, text)`
    * `idf(self, term)`
    * `tf_idf(self, term, text)`
* **nltk.text.Text**
    * `__init__(self, tokens, name=None)`
    * `__getitem__(self, i)`
    * `__len(self)__`
    * `concordance(self, word, width=79, lines=25)`
        * delegates to `ConcordanceIndex.print_concordance()`
    * `concordance_list(self, word, width=79, lines=25)`
        * delegates to `ConcordanceIndex.find_concordance()`
    * `collocations(self, num=20, window_size=2)`
        * `nltk.corpus.stopwords`
        * `BigramCollocationFinder.from_words`
        * __`.apply_freq_filter`
        * __`.apply_word_filter`
        * __`.nbest`
        * `BigramAssocMeasures`
    * `count(self, word)`
    * `index(self, word)`
    * `similar(self, word, num=20)`
        * `ContextIndex`
        * __`._word_to_contexts`
    * `common_contexts(self, words, num=20)`
        * `ContextIndex`
        * __`.common_contexts`
    * `dispersion_plot(self, words)`
        * `nltk.draw.dispersion_plot`
    * `plot(self, *args)`
        * `self.vocab().plot(*args)`
    * `vocab(self)`
        * `FreqDist`
    * `findall(self, regexp)`
        * `TokenSearcher`
        * __`.findall(regexp)`
    * `_context(self, tokens, i)`
    * `__str__(self)`
    * `__repr__(self)`
    






## Listing of NLTK packages and modules

* nltk.__init__
* nltk.app
* nltk.ccg
* nltk.chat
* nltk.chunk
* nltk.classify
* nltk.cluster
* nltk.collocations
* nltk.corpus
* nltk.data
* nltk.downloader
* nltk.draw
* nltk.featstruct
* nltk.grammar
* nltk.help
* nltk.inference
* nltk.metrics
* nltk.misc
* nltk.parse
* nltk.probability
* nltk.sem
* nltk.sentiment
* nltk.stem
* nltk.tag
* nltk.tbl
* nltk.test
* nltk.text
* nltk.tokenize
* nltk.toolbox
* nltk.translate
* nltk.tree
* nltk.treetransforms
* nltk.twitter
* nltk.util
* nltk.wsd

