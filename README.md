# Python impl for TextRank

A pure Python implementation of *TextRank*, 
based on the [Mihalcea 2004](http://web.eecs.umich.edu/~mihalcea/papers/mihalcea.emnlp04.pdf) paper.
Leading toward integration with the [Text Summarization](http://mike.place/2016/summarization/)
example by Mike Williams.

Modifications to the original algorithm include:

  * fixed bug; see [Java impl, 2008](https://github.com/ceteri/textrank)
  * use of lemmatization instead of stemming
  * verbs included in the graph (but not in the resulting keyphrases)
  * normalized keyphrase ranks used in summarization


## Dependencies and Installation

The code here has dependencies on several other projects:

  * [NLTK](http://www.nltk.org/)
  * [TextBlob](http://textblob.readthedocs.io/)
  * [NetworkX](http://networkx.readthedocs.io/)
  * [datasketch](https://github.com/ekzhu/datasketch)

To install:

    conda config --add channels https://conda.binstar.org/sloria
    conda install textblob
    sudo python -m nltk.downloader punkt
    sudo python -m nltk.downloader wordnet
    pip install datasketch -U


## Example Usage

Run a test case based on the Mihalcea paper:

    ./stage1.py dat/mih.json > out1.json
    ./stage2.py out1.json > out2.json

That test case should result as:

```
0.2230	  minimal supporting set
0.1345	  types systems
0.1339	  linear diophantine equations
0.0802	  mixed types
0.0541	  strict inequations
0.0505	  nonstrict inequations
0.0368	  linear constraints
0.0356	  natural numbers
0.0252	  corresponding algorithms
0.0116	  upper bounds
0.0091	  solutions
0.0027	  components
0.0025	  construction
0.0014	  compatibility
0.0010	  criteria
```

Run another test based on the [Williams talk](http://mike.place/2016/summarization/):

    ./stage1.py dat/ars.json > out1.json
    ./stage2.py out1.json > out2.json
    ./stage3.py out1.json out2.json

Those results show a summarization similar to that shown on slide 30.
