# Chapter 1


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

text4 = Text(inaugural.wrods(), name="Inaugural Address Corpus")

# and 

sent5 = ["I", "have", "a", "problem", "with", "people",
         "PMing", "me", "to", "lol", "JOIN"]
```


```python
# methods of the `nltk.text.Text` class

text1.concordance("monstrous")
text1.similar("monstrous")
text1.common_contexts(["monstrous", "very"])
text4.dispersion_plot(["citizens", "democracy", "freedom", "duties", "America"])
text3.generate()
```

Per the API Docs:

> A wrapper around a sequence of simple (string) tokens, which is intended to support initial exploration of texts (via the interactive console). Its methods perform a variety of analyses on the text’s contexts (e.g., counting, concordancing, collocation discovery), and display the results. If you wish to write a program which makes use of these analyses, then you should bypass the Text class, and use the appropriate analysis function or class directly instead.





## Listing of NLTK packages and modules

nltk.__init__	
nltk.app	
nltk.ccg	
nltk.chat	
nltk.chunk	
nltk.classify	
nltk.cluster	
nltk.collocations (1)
nltk.corpus	
nltk.data (2)
nltk.downloader (3)
nltk.draw	
nltk.featstruct (4)
nltk.grammar	
nltk.help	
nltk.inference	
nltk.metrics	
nltk.misc	
nltk.parse	
nltk.probability	
nltk.sem	
nltk.sentiment	
nltk.stem	
nltk.tag	
nltk.tbl	
nltk.test	
nltk.text	
nltk.tokenize	
nltk.toolbox	
nltk.translate	
nltk.tree	
nltk.treetransforms	
nltk.twitter	
nltk.util	
nltk.wsd	

