# Notes from NLP w/ Python (NLTK Book)

Text
- t[n]
  - t[n1:n2:n3]
- .index("")

- count vocab: len(text)
- unique (sorted) tokens: sorted(set(text))
- "lexical richness": len(set(t)) / len(t)

FreqDist(text)
- .most_common()
- ["__"] # => frequency of key provided
- .plot()
- .hapaxes()

## Strings


', ", """
+ => concatenation
* => repetition
can't use - or /


Corpus
- from nltk.corpus import gutenberg
- raw = gutenberg.raw('melville-moby_dick.txt')


## Unicode

# TODO: Unicode - learn more

- code points
- \uXXXX 
- decode: convert from encoded format (UTF-8, Latin-2, etc) to Unicode
- encode: convert from Unicode to encoded format
- characters are abstract entities that can be realized as one or more **glyphs**
- fonts are mappings from characters to glyphs

# file encoded in latin2
path = nltk.data.find('corpora/unicode_samples/polish-lat2.txt')

# specify encoding when opening file
f = open(path, encoding='latin2')

# display file contents:
for line in f:
  line = line.strip()
  print(line)
  
  
# OR display the non-ASCII characters via their two-digit \xXX 
# and four-digit \uXXXX representations
for line in f:
  line = line.strip()
  print(line.encode('unicode_escape'))
  
  
x = 'ó'
print(x.encode('unicode_escape'))  # => b'\\xf3'
ord(x)  # => 243  # returns the unicode code point for a one char string
hex(ord(x))  # => '0xf3'  # returns the hexadecimal repr of an integer
"{:04x}".format(ord(x))  # => '00f3'

import unicodedata
unicodedata.name(x)  # => 'LATIN SMALL LETTER O WITH ACUTE'


# `find` against unicode characters:
line = "larger string with '" + x + "' character"
# "larger string with 'ó' character"
line.find(x)  # => 20

# `re` search against unicode characters
import re
m = re.search(x, line)
m.group() => 'ó'


## REGEX's

import re

re.findall

nltk.corpus.toolbox.words('rotokas.dic')

nltk.ConditionalFreqDist(cvs)
- .tabulate()

nltk.Text.findall(regexp)

nltk.word_tokenize()

nltk.PorterStemmer()
nltk.LancasterStemmer()

{stemmer}.stem(token)

nltk.Index
nltk.tokenwrap

nltk.WordNetLemmatizer()
{lemmatizer}.lemmatize(token)


nltk.regexp_tokenize
nltk.corpus.___.raw() vs. nltk.corpus.___.words() ??
nltk.corpus.brown.words()
nltk.corpus.brown.sents()

## >>> RESUME @ http://www.nltk.org/book/ch04.html

