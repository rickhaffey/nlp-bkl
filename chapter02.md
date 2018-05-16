# Chapter 2


### Gutenberg

* [Gutenberg Corpus](http://www.gutenberg.org)

List available file identifiers:

```python
import nltk
nltk.corpus.gutenberg.fileids()
```

# >>> ['austen-emma.txt',
# >>>  'austen-persuasion.txt',
# >>>  'austen-sense.txt',
# >>>  'bible-kjv.txt',
# >>>  'blake-poems.txt',
# >>>  'bryant-stories.txt',
# >>>  'burgess-busterbrown.txt',
# >>>  'carroll-alice.txt',
# >>>  'chesterton-ball.txt',
# >>>  'chesterton-brown.txt',
# >>>  'chesterton-thursday.txt',
# >>>  'edgeworth-parents.txt',
# >>>  'melville-moby_dick.txt',
# >>>  'milton-paradise.txt',
# >>>  'shakespeare-caesar.txt',
# >>>  'shakespeare-hamlet.txt',
# >>>  'shakespeare-macbeth.txt',
# >>>  'whitman-leaves.txt']

To retrieve "parts" of a given corpus (in this case `gutenberg`):

```python
from nltk.corpus import gutenberg
fileid = 'milton-paradise.txt'

# a single string
characters = gutenberg.raw(fileid)

# a list of words
words = gutenberg.words(fileid)

# a list of sentences, each of which is a list of words 
sentences = gutenberg.sents(fileid)

# a list of paragraphs, each of which is a list of
# sentences, each of which is a list of words
paragraphs = gutenberg.paras(fileid) 
```

### Web and Chat Text

```python
from nltk.corpus import webtext
webtext.fileids()
```

# >>> ['firefox.txt',
# >>>  'grail.txt',
# >>>  'overheard.txt',
# >>>  'pirates.txt',
# >>>  'singles.txt',
# >>>  'wine.txt']

### Naval Postgraduate School

```python
from nltk.corpus import nps_chat
nps_chat.fileids()
```

# >>> ['10-19-20s_706posts.xml',
# >>>  '10-19-30s_705posts.xml',
# >>>  '10-19-40s_686posts.xml',
# >>>  '10-19-adults_706posts.xml',
# >>>  '10-24-40s_706posts.xml',
# >>>  '10-26-teens_706posts.xml',
# >>>  '11-06-adults_706posts.xml',
# >>>  '11-08-20s_705posts.xml',
# >>>  '11-08-40s_706posts.xml',
# >>>  '11-08-adults_705posts.xml',
# >>>  '11-08-teens_706posts.xml',
# >>>  '11-09-20s_706posts.xml',
# >>>  '11-09-40s_706posts.xml',
# >>>  '11-09-adults_706posts.xml',
# >>>  '11-09-teens_706posts.xml']

### Brown Corpus

* [Brown Corpus](http://icame.uib.no/brown/bcm-los.html)


```python
from nltk.corpus import brown
brown.categories()
```

# >>> ['adventure',
# >>>  'belles_lettres',
# >>>  'editorial',
# >>>  'fiction',
# >>>  'government',
# >>>  'hobbies',
# >>>  'humor',
# >>>  'learned',
# >>>  'lore',
# >>>  'mystery',
# >>>  'news',
# >>>  'religion',
# >>>  'reviews',
# >>>  'romance',
# >>>  'science_fiction']

```python
brown.words(categories=['science_fiction','adventure'])
```

* **stylistics**: studying systematics differences between genres

```python
sf = brown.words(categories='science_fiction')
f = brown.words(categories='fiction')

sf_len = len(sf)
f_len = len(f)

wh = ['who', 'what', 'when', 'where', 'why', 'how']

sf_dist = nltk.FreqDist([w.lower() for w in sf])
f_dist = nltk.FreqDist([w.lower() for w in f])

for w in wh:
    print("{} SF: {}".format(w, sf_dist[w] / sf_len))
    print("{}  F: {}".format(w, f_dist[w] / f_len))
```
