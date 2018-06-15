# Chapter 2

### Gutenberg

* [Gutenberg Corpus](http://www.gutenberg.org)

List available file identifiers:

```python
import nltk
nltk.corpus.gutenberg.fileids()
```

```
>>> ['austen-emma.txt',
>>>  'austen-persuasion.txt',
>>>  'austen-sense.txt',
>>>  'bible-kjv.txt',
>>>  'blake-poems.txt',
>>>  'bryant-stories.txt',
>>>  'burgess-busterbrown.txt',
>>>  'carroll-alice.txt',
>>>  'chesterton-ball.txt',
>>>  'chesterton-brown.txt',
>>>  'chesterton-thursday.txt',
>>>  'edgeworth-parents.txt',
>>>  'melville-moby_dick.txt',
>>>  'milton-paradise.txt',
>>>  'shakespeare-caesar.txt',
>>>  'shakespeare-hamlet.txt',
>>>  'shakespeare-macbeth.txt',
>>>  'whitman-leaves.txt']
```

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

```
>>> ['firefox.txt',
>>>  'grail.txt',
>>>  'overheard.txt',
>>>  'pirates.txt',
>>>  'singles.txt',
>>>  'wine.txt']
```

### Naval Postgraduate School

```python
from nltk.corpus import nps_chat
nps_chat.fileids()
```

```
>>> ['10-19-20s_706posts.xml',
>>>  '10-19-30s_705posts.xml',
>>>  '10-19-40s_686posts.xml',
>>>  '10-19-adults_706posts.xml',
>>>  '10-24-40s_706posts.xml',
>>>  '10-26-teens_706posts.xml',
>>>  '11-06-adults_706posts.xml',
>>>  '11-08-20s_705posts.xml',
>>>  '11-08-40s_706posts.xml',
>>>  '11-08-adults_705posts.xml',
>>>  '11-08-teens_706posts.xml',
>>>  '11-09-20s_706posts.xml',
>>>  '11-09-40s_706posts.xml',
>>>  '11-09-adults_706posts.xml',
>>>  '11-09-teens_706posts.xml']
```

### Brown Corpus

* [Brown Corpus](http://icame.uib.no/brown/bcm-los.html)

```python
from nltk.corpus import brown
brown.categories()
```

```
>>> ['adventure',
>>>  'belles_lettres',
>>>  'editorial',
>>>  'fiction',
>>>  'government',
>>>  'hobbies',
>>>  'humor',
>>>  'learned',
>>>  'lore',
>>>  'mystery',
>>>  'news',
>>>  'religion',
>>>  'reviews',
>>>  'romance',
>>>  'science_fiction']
```

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

```
>>>  who SF: 0.0008984105044920525
>>>  who  F: 0.001635322976287817
>>>  what SF: 0.0028334485141672428
>>>  what  F: 0.0027158042284779814
>>>  when SF: 0.0019350380096751902
>>>  when  F: 0.0028034108164934003
>>>  where SF: 0.0010366275051831375
>>>  where  F: 0.0012994977222287117
>>>  why SF: 0.0005528680027643401
>>>  why  F: 0.0006132461161079313
>>>  how SF: 0.0011057360055286801
>>>  how  F: 0.0012994977222287117
```

Use conditional distributions to analyze counts across
multiple genres:

```python
cfd = nltk.ConditionalFreqDist(
  (genre, word) 
  for genre in brown.categories()
  for word in brown.words(categories=genre)
)
  
genres = ['news', 'religion', 'hobbies', 'science_fiction', 'romance', 'humor']
wh = ['who', 'what', 'when', 'where', 'why', 'how']

cfd.tabulate(conditions=genres, samples=wh)
```

```
>>>                    who  what  when where   why   how
>>>             news   268    76   128    58     9    37
>>>         religion   100    64    53    20    14    23
>>>          hobbies   103    78   119    72    10    40
>>>  science_fiction    13    27    21    10     4    12
>>>          romance    89   121   126    54    34    60
>>>            humor    48    36    52    15     9    18
```

### Reuters Corpus

* news documents
  * 10,788 file ids
  * 90 categories
* categories overlap
* classified into 90 topics
* grouped into training & test sets


Retrieve the categories covered by a set of documents:

```python
from nltk.corpus import reuters
reuters.categories(['training/11490', 'training/11491'])
```

`>>>  ['crude', 'earn', 'gas', 'heat']`

Retrieve the files that cover a given set of categories

```python
reuters.fileids(['housing', 'income'])
```

```
>>>  ['test/16118',
>>>   'test/18534',
>>>   'test/18540',
>>>   'test/18664',
>>>   'test/18665',
>>>   'test/18672',
>>>   'test/18911',
>>>   'test/19875',
>>>   'test/20106',
>>>   'test/20116',
>>>   'training/1035',
>>>   'training/1036',
>>>   'training/10602',
>>>   'training/10604',
>>>   'training/11170',
>>>   'training/11665',
>>>   'training/2618',
>>>   'training/29',
>>>   'training/3105',
>>>   'training/3708',
>>>   'training/3720',
>>>   'training/3723',
>>>   'training/3898',
>>>   'training/5883',
>>>   'training/5886',
>>>   'training/6000',
>>>   'training/6067',
>>>   'training/6197',
>>>   'training/7005',
>>>   'training/7006',
>>>   'training/7015',
>>>   'training/7036',
>>>   'training/7098',
>>>   'training/7099',
>>>   'training/9615']
```

Get words associated with a given set of fileids or categories:

```python
reuters.words(categories=['housing', 'income'])
# reuters.words(['training/5886', 'training/5887'])
```

`>>>  ['YUGOSLAV', 'ECONOMY', 'WORSENED', 'IN', '1986', ',', ...]`

### Inaugural Address Corpus

* collection of 55 texts, one for each presidential address


```python
from nltk.corpus import inaugural
inaugural.fileids()
```

```
>>>  ['1789-Washington.txt',
>>>   '1793-Washington.txt',
>>>   '1797-Adams.txt',
>>>   '1801-Jefferson.txt',
>>>   '1805-Jefferson.txt',
>>>   '1809-Madison.txt',
>>>   '1813-Madison.txt',
>>>   '1817-Monroe.txt',
>>>   '1821-Monroe.txt',
>>>   '1825-Adams.txt',
>>>   '1829-Jackson.txt',
>>>   '1833-Jackson.txt',
>>>   '1837-VanBuren.txt',
>>>   '1841-Harrison.txt',
>>>   '1845-Polk.txt',
>>>   '1849-Taylor.txt',
>>>   '1853-Pierce.txt',
>>>   '1857-Buchanan.txt',
>>>   '1861-Lincoln.txt',
>>>   '1865-Lincoln.txt',
>>>   '1869-Grant.txt',
>>>   '1873-Grant.txt',
>>>   '1877-Hayes.txt',
>>>   '1881-Garfield.txt',
>>>   '1885-Cleveland.txt',
>>>   '1889-Harrison.txt',
>>>   '1893-Cleveland.txt',
>>>   '1897-McKinley.txt',
>>>   '1901-McKinley.txt',
>>>   '1905-Roosevelt.txt',
>>>   '1909-Taft.txt',
>>>   '1913-Wilson.txt',
>>>   '1917-Wilson.txt',
>>>   '1921-Harding.txt',
>>>   '1925-Coolidge.txt',
>>>   '1929-Hoover.txt',
>>>   '1933-Roosevelt.txt',
>>>   '1937-Roosevelt.txt',
>>>   '1941-Roosevelt.txt',
>>>   '1945-Roosevelt.txt',
>>>   '1949-Truman.txt',
>>>   '1953-Eisenhower.txt',
>>>   '1957-Eisenhower.txt',
>>>   '1961-Kennedy.txt',
>>>   '1965-Johnson.txt',
>>>   '1969-Nixon.txt',
>>>   '1973-Nixon.txt',
>>>   '1977-Carter.txt',
>>>   '1981-Reagan.txt',
>>>   '1985-Reagan.txt',
>>>   '1989-Bush.txt',
>>>   '1993-Clinton.txt',
>>>   '1997-Clinton.txt',
>>>   '2001-Bush.txt',
>>>   '2005-Bush.txt',
>>>   '2009-Obama.txt']
```

### Annotated Text Corpora

* corpora with text annotations such as
  - part-of-speech tags,
  - named entities,
  - syntactic structures,
  - semantic roles,
  - etc.
* see <http://www.nltk.org/data> for downloading
* [ ] Investigate the different corpora in list on pgs 46-47.

### Corpora in Other Languages

* nltk.corpus.cess_esp
* nltk.corpus.floresta
* nltk.corpus.indian
* nltk.corpus.udhr

```python
len(nltk.corpus.udhr.fileids())  # >>> 310
nltk.corpus.udhr.fileids()[:10]
```

```
>>> ['Abkhaz-Cyrillic+Abkh',
>>>  'Abkhaz-UTF8',
>>>  'Achehnese-Latin1',
>>>  'Achuar-Shiwiar-Latin1',
>>>  'Adja-UTF8',
>>>  'Afaan_Oromo_Oromiffa-Latin1',
>>>  'Afrikaans-Latin1',
>>>  'Aguaruna-Latin1',
>>>  'Akuapem_Twi-UTF8',
>>>  'Albanian_Shqip-Latin1']
```

### Text Corpus Structure

Types:

* isolated (e.g. gutenberg)
* categorized (e.g. brown)
* overlapping (e.g. reuters)
* temporal (e.g. inaugural)

### Loading Your Own Corpus

* `PlaintextCorpusReader` handles corpora that consist of a set of unannotated text files
* `BracketParseCorpusReader` handles corpora that consist of files containing parenthesis-delineated parse trees
   - e.g. Penn Treebank

* using `PlaintextCorpusReader`
* - specify corpus root
* - specify fileids: either specific, or pattern

```python
root = "/foo/bar/bat"
fileids = '.*\.txt'

my_corpus = PlaintextCorpusReader(root, fileids)
my_corpus.fileids()
```

`>>> ['file1.txt', 'file2.txt']`

## Conditional Frequency Distributions

* **conditional frequency distribution**: a collection of frequency
  distributions, each one for a different condition.
* use pairs of `(condition, event)` as elements in distribution

```python
from nltk.corpus import brown

cfd = nltk.ConditionalFreqDist(
  (genre, word.lower()) 
  for genre in brown.categories()
  for word in brown.words(categories=genre))
  
cfd['news'].most_common()[:30]
```

```
>>> [('the', 6386),
>>>  (',', 5188),
>>>  ('.', 4030),
>>>  ('of', 2861),
>>>  ('and', 2186),
>>>  ('to', 2144),
>>>  ('a', 2130),
>>>  ('in', 2020),
>>>  ('for', 969),
>>>  ('that', 829),
>>>  ('is', 733),
>>>  ('``', 732),
>>>  ('was', 717),
>>>  ("''", 702),
>>>  ('on', 691),
>>>  ('he', 642),
>>>  ('at', 636),
>>>  ('with', 567),
>>>  ('be', 526),
>>>  ('as', 517)]
``` 

### Plotting and Tabulating Distributions

```python
cfd.tabulate(
    conditions=['news', 'fiction', 'humor'],
    samples=['president', 'their', 'you'],
    cumulative=False
)
```

```
        president     their       you
   news       142       231        66
fiction        10       166       282
  humor         1        53       148
```

```python
cfd.plot(
    conditions=['news', 'fiction', 'humor'],
    samples=['president', 'their', 'you'],
    cumulative=False
)
```

[ ] todo: add image output of plot call

### Generating Random Text with Bigrams

Generate bigrams from a text:

```python
words = [w.lower() for w in gutenberg.words('shakespeare-macbeth.txt')]
bi_grams = nltk.bigrams(words)

list(bi_grams)[20:40]
```

```
[('enter', 'three'),
 ('three', 'witches'),
 ('witches', '.'),
 ('.', '1'),
 ('1', '.'),
 ('.', 'when'),
 ('when', 'shall'),
 ('shall', 'we'),
 ('we', 'three'),
 ('three', 'meet'),
 ('meet', 'againe'),
 ('againe', '?'),
 ('?', 'in'),
 ('in', 'thunder'),
 ('thunder', ','),
 (',', 'lightning'),
 ('lightning', ','),
 (',', 'or'),
 ('or', 'in'),
 ('in', 'raine')]
```

Generate a conditional frequency distribution using bigrams

```python
words = [w.lower() for w in gutenberg.words('melville-moby_dick.txt')]
bigrams = nltk.bigrams(words)

cfd = nltk.ConditionalFreqDist(bigrams)

cfd['whale'].most_common()[:20]
```

```
[(',', 215),
 ("'", 125),
 ('-', 123),
 ('.', 79),
 (';', 68),
 ('is', 45),
 ('was', 24),
 ('in', 20),
 ('and', 17),
 ('fishery', 17)]
```

Generate random text from the cfd of a text's bigrams and a seed word

```python
def generate_model(cfdist, word, num=15):
    for i in range(num):
        print(word, end=' ')
        word = cfdist[word].max()


generate_model(cfd, 'fishery')
```

```
fishery , and the whale , and the whale , and the whale , and
```

Note the repetition.

## Lexical Resources

### Wordlist Corpora

Find a list of all the words in a document that _aren't_ in the wordlist corpus

```python
wordlist = set(w.lower() for w in nltk.corpus.words.words())
moby_vocab = set(w.lower() for w in words if w.isalpha())  # from moby dick
diff = moby_vocab.difference(wordlist)

print(sorted(diff)[:30])
```

```
['abated', 'abating', 'abednego', 'abhorred', 'abided', 'abjectus',
 'ablutions', 'abominated', 'aboriginalness', 'abortions', 'abounded', 'abstained',
 'accelerating', 'accidents', 'accommodated', 'accompanied', 'accompanies', 'accompaniments',
 'accompanying', 'accomplishing', 'accountants', 'accounted', 'accounts', 'accumulated',
 'accumulating', 'acerbities', 'ached', 'achieved', 'achilles', 'acknowledges']
```

**Stopwords**

```python
from nltk.corpus import stopwords
sw = stopwords.words('english')
print(sw[:30])
```

```
['i', 'me', 'my', 'myself', 'we', 'our',
 'ours', 'ourselves', 'you', "you're", "you've", "you'll",
 "you'd", 'your', 'yours', 'yourself', 'yourselves', 'he',
 'him', 'his', 'himself', 'she', "she's", 'her',
 'hers', 'herself', 'it', "it's", 'its', 'itself']
```

Calculate stopword content

```python
def stopword_fraction(text):
  stopwords = nltk.corpus.stopwords.words('english')
  text_sw = [w for w in text if w.lower() in stopwords]
  return len(text_sw) / len(text)
  

text = gutenberg.words('melville-moby_dick.txt')
print(stopword_fraction(text))
```

```
0.4137045230600531
```


Puzzle:

```
 E  G  I
 V  R  V
 O  N  L
```

```python
puzzle_letters = 'egivrvonl'
puzzle_freq = nltk.FreqDist(puzzle_letters)
obligatory = 'r'

wordlist = nltk.corpus.words.words()
[w for w in wordlist if len(w) >= 6
                     and obligatory in w
                     and nltk.FreqDist(w) <= puzzle_freq]
```

```
['glover',
 'gorlin',
 'govern',
 'grovel',
 'ignore',
 'involver',
 'lienor',
 'linger',
 'longer',
 'lovering',
 'noiler',
 'overling',
 'region',
 'renvoi',
 'revolving',
 'ringle',
 'roving',
 'violer',
 'virole']
```

### Names Corpora

* contains 8,000 first names categorized by gender

```python
names = nltk.corpus.names
names.fileids()
```

```
['female.txt', 'male.txt']
```

```pyton
male_names = names.words('male.txt')
male_names[:10]
```

```
['Aamir',
 'Aaron',
 'Abbey',
 'Abbie',
 'Abbot',
 'Abbott',
 'Abby',
 'Abdel',
 'Abdul',
 'Abdulkarim']
```

Compare the most frequent letters in male and female names:

```python
male_letters = [c for word in names.words('male.txt') for c in list(word.lower())]
female_letters = [c for word in names.words('female.txt') for c in list(word.lower())]

mfd = nltk.FreqDist(male_letters)
ffd = nltk.FreqDist(female_letters)
```

```python
mfd.most_common()[:10]
```

```
[('e', 1958),
 ('a', 1683),
 ('r', 1631),
 ('n', 1302),
 ('i', 1248),
 ('l', 1135),
 ('o', 1129),
 ('t', 857),
 ('s', 804),
 ('d', 757)]
```

## A Pronouncing Dictionary

* CMU Pronouncing Dictionary
  * provides a list of phonetic codes for each word
  * 
* see http://en.wikipedia.org/wiki/Arpabet
* each entry consists of a word and a list of _phones_ describing its pronunciation
  
```python
entries = nltk.corpus.cmudict.entries()
entries[40010:40020]
```

```
[('exquisite', ['EH1', 'K', 'S', 'K', 'W', 'AH0', 'Z', 'AH0', 'T']),
 ('exquisitely',
  ['EH2', 'K', 'S', 'K', 'W', 'IH1', 'Z', 'IH0', 'T', 'L', 'IY0']),
 ('extant', ['EH1', 'K', 'S', 'T', 'AH0', 'N', 'T']),
 ('extel', ['EH1', 'K', 'S', 'T', 'EH2', 'L']),
 ('extend', ['IH0', 'K', 'S', 'T', 'EH1', 'N', 'D']),
 ('extendable',
  ['EH2', 'K', 'S', 'T', 'EH1', 'N', 'D', 'AH0', 'B', 'AH0', 'L']),
 ('extended', ['IH0', 'K', 'S', 'T', 'EH1', 'N', 'D', 'AH0', 'D']),
 ('extended', ['IH0', 'K', 'S', 'T', 'EH1', 'N', 'D', 'IH0', 'D']),
 ('extender', ['EH1', 'K', 'S', 'T', 'EH2', 'N', 'D', 'ER0']),
 ('extenders', ['EH1', 'K', 'S', 'T', 'EH2', 'N', 'D', 'ER0', 'Z'])]
```
