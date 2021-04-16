# 2021-04-13 Introduction to Parallel Programming in Python - Day 2

Welcome to The Workshop Collaborative Document 
 

This Document is synchronized as you type, so that everyone viewing this page sees the same text. This allows you to collaborate seamlessly on documents. 

All content is publicly available under the Creative Commons Attribution License 

https://creativecommons.org/licenses/by/4.0/ 

 ---------------------------------------------------------------------------- 

This is the Document for today: [link](https://hackmd.io/@O0tsDNPbTlyhyGiiCMaLIw/By912hbBd)

Collaborative Document day 1: [link](https://hackmd.io/@O0tsDNPbTlyhyGiiCMaLIw/r1l9ohWSu) 

Collaborative Document day 2: [link](https://hackmd.io/@O0tsDNPbTlyhyGiiCMaLIw/By912hbBd)
  

## 👮Code of Conduct 

Participants are expected to follow these guidelines: 
* Use welcoming and inclusive language 
* Be respectful of different viewpoints and experiences 
* Gracefully accept constructive criticism 
* Focus on what is best for the community 
* Show courtesy and respect towards other community members 
 

## ⚖️ License 

All content is publicly available under the Creative Commons Attribution License: https://creativecommons.org/licenses/by/4.0/ 

 

## 🙋Getting help 
to ask a question, type `/hand` in the chat window 

to get help, type `/help` in the chat window 

you can ask questions in the document or chat window and helpers will try to help you 
 

## 🖥 Workshop website 

[Workshop website](https://escience-academy.github.io/2021-04-12-parallel-python/) 

🛠 Setup 

See workshop website

## 📋 Post-workshop survey

[Survey link here](https://www.surveymonkey.com/r/FL5ZZZV)

## 👩‍🏫👩‍💻🎓 Instructors 

Johan Hidding, Djura Smits
 

## 🧑‍🙋 Helpers 

Hanno Spreeuw, Leon Oostrum
 

## 👩‍💻👩‍💼👨‍🔬🧑‍🔬🧑‍🚀🧙‍♂️🔧 Roll Call 
Name/ pronouns (optional) / job, role / social media (twitter, github, ...) / background or interests (optional) / city

## 🧬🔬🧫📡🔭🧪 Yesterday's concepts

Please add a :+1: behind each concept you feel familiar with.

| Concept | I think I know what this means |
|---|---|
| serial algorithms |:+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1:|
| parallel algorithms |:+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1:|
| dependency diagrams | :+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1:|
| profiling |:+1::+1::+1::+1::+1::+1::+1::+1::+1::+1:|
| physical vs. logical cores |:+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1:| 
| native Python |:+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1:|
| vectorized expressions |:+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1:|
| just-in-time compilation |:+1::+1::+1::+1::+1::+1::+1::+1::+1::+1:|
| machine code |:+1::+1::+1::+1::+1::+1::+1::+1::+1::+1:|
| threading |:+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1:|
| multi-processing |:+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1::+1:|
| Global Interpreter Lock |:+1::+1::+1::+1::+1::+1::+1::+1:|
 

## 🗓️ Agenda 

<div class="row">
  <div class="col-md-6">
    <h3>Day 1</h3>
    <table class="table table-striped">
     <tr> <td>09:00</td>  <td>Welcome and icebreaker</td> </tr>
      <tr> <td>09:15</td>  <td>Introduction</td></tr>
      <tr> <td>09:50</td>  <td>Break</td></tr>
      <tr> <td>10:00</td>  <td>Measuring performance</td> </tr>
      <tr> <td>10:50</td>  <td>Coffee break</td> </tr>
      <tr> <td>11:00</td>  <td>Computing Pi</td> </tr>
      <tr> <td>12:45</td>  <td>Wrap-up</td> </tr>
      <tr> <td>13:00</td>  <td>END</td></tr>
    </table>
  </div>
  <div class="col-md-6">
    <h3>Day 2</h3>
    <table class="table table-striped">
      <tr> <td>09:00</td>  <td>Welcome and icebreaker</td> </tr>
      <tr> <td>09:15</td>  <td>Recap</td> </tr>
      <tr> <td>09:30</td>  <td><b>Parallel design patterns</b></td> </tr>
      <tr> <td>10:00</td>  <td>Coffee break</td> </tr>
      <tr> <td>10:10</td>  <td><b>Parallel design patterns (continued)</b></td> </tr>
      <tr> <td>11:00</td>  <td>Tea break</td> </tr>
      <tr> <td>11:10</td>  <td><b>Introduction to Snakemake</b></td></tr>
      <tr> <td>12:00</td>  <td>Lemonade break</td></tr>
      <tr> <td>12:10</td>  <td><b>Converting a script to Snakemake</b></td></tr>
      <tr> <td>12:45</td>  <td>Post-workshop Survey</td> </tr>
      <tr> <td>13:00</td>  <td>END</td> </tr>
    </table>
  </div>
</div>
 

## 🧠 Collaborative Notes 

 
## Parallel design patterns

```python
import dask.bag as db
bag = db.from_sequence(['good', 'morning'])
bag

def shout(word):
    return word + '!'

bag.map(shout).visualize()
bag.map(shout).compute()
```

```python
def contains_d(word):
    return 'd' in word

contains_d('good')

bag.filter(contains_d).compute()
```

#### Exercise (2 min) Difference between filter and map

Without executing it, try to forecast what would be the output of 
`bag.map(contains_d).compute()`

* Return the output of the function, so [True, False]
* True, False
* `[True, False]` :+1::+1::+1::+1::+1::+1::+1::+1::+1::+1:
* [true, false]
* Returns True,False
* ['good']
* [True, False]
* "good"
* Returns True for good and False for morning

```python
bag.map(contains_d).compute()
# [True, False]
```

```python
bag = db.from_sequence(range(10))
bag.reduction(sum, sum).visualize()
bag.reduction(sum, sum).compute()
```

```python
def is_even(x):
    return x % 2 == 0
    
bag.map(is_even).compute()
bag.groupby(is_even).compute()
```

```python
bag = db.from_sequence(['good', 'morning', 'have', 'a', 'nice', 'day'])

def chars_part(x):
    c = 0
    
    for w in x:
        c += len(w)
    return c

chars_part(['good', 'morning'])
bag.reduction(chars_part, sum).compute()
```

```python=
bag = db.from_sequence(range(10))

```

###  Exercise (5 min) Programming patterns

Look at the `mean`, `pluck`, `distinct`, and `topk` methods. Match them up with map, filter, groupby and reduce methods. https://docs.dask.org/en/latest/bag-api.html


* mean -> reduce, distinct -> groupby, pluck -> filter, topk -> filter 

* mean -> reduce; distinct / pluck -> filter; topk -> groupby + filter


* `mean`: reduce, `pluck`: filter, `distinct`: groupby, `topk`: filter

-
    * mean --> reduce
    * distinct --> groupby
    * pluck --> map
    * topk --> filter


* `mean`: reduction;
`pluck`: filter, groupby;
`distinct`: filter, groupby;
`topk`: filter, groupby

* filter: -- /
map: distinct /
groupby:  pluck /
reduce: mean, topk

|
mean -> reduce,
pluck -> filter/map,
distinct -> filter/groupby,
topk -> filter


```python
bag = db.from_sequence(['good', 'morning'])
bag.pluck(0).compute()

bag = db.from_sequence(range(10))
bag.mean().visualize()
bag.distinct().visualize()
bag.topk(4).visualize()
```

### Challenge (15 min) count unique words with dask

Rewrite the following program in terms of a Dask bag. Make it spicy by using your favourite literature classic from project Gutenberg as input.

```python
!pip install nltk
from nltk.stem.snowball import PorterStemmer

stemmer = PorterStemmer()

stemmer.stem('dancing')
stemmer.stem('danced')

def good_word(w):
    return len(w) > 0 and not any(i.isdigit() for i in w)
    
def clean_word(w):
    return w.strip("*!?.:;'\",“’‘”()_").lower()
    
text = 'All work and no play makes jack a dull boy'
words = set()

```

- Mapes Dodge - https://www.gutenberg.org/files/764/764-0.txt
- Melville - https://www.gutenberg.org/files/15/15-0.txt
- Conan Doyle - https://www.gutenberg.org/files/1661/1661-0.txt
- Shelley - https://www.gutenberg.org/files/84/84-0.txt
- Stoker - https://www.gutenberg.org/files/345/345-0.txt
- E. Bronte - https://www.gutenberg.org/files/768/768-0.txt
- Austen - https://www.gutenberg.org/files/1342/1342-0.txt
- Carroll - https://www.gutenberg.org/files/11/11-0.txt
- Christie - https://www.gutenberg.org/files/61262/61262-0.txt

All urls in a list:
```python
[
 'https://www.gutenberg.org/files/764/764-0.txt',
 'https://www.gutenberg.org/files/15/15-0.txt', 
 'https://www.gutenberg.org/files/1661/1661-0.txt',
 'https://www.gutenberg.org/files/84/84-0.txt',
 'https://www.gutenberg.org/files/345/345-0.txt',
 'https://www.gutenberg.org/files/768/768-0.txt',
 'https://www.gutenberg.org/files/1342/1342-0.txt',
 'https://www.gutenberg.org/files/11/11-0.txt',
 'https://www.gutenberg.org/files/61262/61262-0.txt'
]
```

Function to load text from a url:
```python
import requests
def load_url(url):
    response = requests.get(url)
    return response.text
```

-- group 1:

-- group 2:

-- group 3:
we were about to...
```python=
import dask.bag as db
import requests
def from_url(url):
    response = requests.get(url)
    return response.text
bag = from_url('https://www.gutenberg.org/files/1661/1661-0.txt')
words = set()
for w in bag.split():
    cw = clean_word(w)
    
    if good_word(cw):
       words.add(stemmer.stem(cw))
        
print(f'This corpus contains {len(words)} unique words.')
```
-- group 4:
```python
bag = db.from_sequence(load_url(texts[0]).split())
words=set()
wordcount=bag.map(clean_word).filter(good_word).map(stemmer.stem).distinct().count().compute()
print(f'This text contains {wordcount} unique words')

```

-- group 5:
```python
text = load_url(list_of_urls[-1])
bag = db.from_sequence(text.split())
clean_words = bag.map(clean_word)
good_words = clean_words.filter(good_word)
stems = good_words.map(stemmer.stem)
word_count = stems.distinct().count().compute()
```
-- group 6:

```python
bag = db.from_sequence(text.split())
words =len(bag.filter(good_word).map(clean_word).distinct().compute())
print(f'This text contains {words} unique words')
```


**Solution**:
```python
urls = [
 'https://www.gutenberg.org/files/764/764-0.txt',
 'https://www.gutenberg.org/files/15/15-0.txt', 
 'https://www.gutenberg.org/files/1661/1661-0.txt',
 'https://www.gutenberg.org/files/84/84-0.txt',
 'https://www.gutenberg.org/files/345/345-0.txt',
 'https://www.gutenberg.org/files/768/768-0.txt',
 'https://www.gutenberg.org/files/1342/1342-0.txt',
 'https://www.gutenberg.org/files/11/11-0.txt',
 'https://www.gutenberg.org/files/61262/61262-0.txt'
]

bag = db.from_sequence(urls)
computation = bag.map(load_url)\
                 .str.split()\
                 .flatten()\
                 .map(clean_word)\
                 .filter(good_word)\
                 .map(stemmer.stem)\
                 .distinct()\
                 .count()
computation.visualize()
count = computation.compute()
print(f'These texts contain {count} unique words')
```

## Snakemake
Please make sure to have downloaded [this Github repository](https://github.com/escience-academy/parallel-python-workshop)

### Exercise: Create the combine rule in the below Snakefile
```
rule all:
    input:
        "combined.txt"
        
rule generate_message:
    output:
        "message.txt"
    # If not on windows, you can use this shell command:
    # shell:
    #     "echo 'Hello, World' > {output}"
    # If on windows, you can use this python version:
    run:
        with open(output[0], 'w') as f:
            print("Hello, world", file=f)
            
rule shout_message:
    input:
        "message.txt"
    output:
        "allcaps.txt"
    run:
        with open(output[0], 'w') as f_out, \
             open(input[0], 'r') as f_in:
            content = f_in.read()
            f_out.write(content.upper())
            
rule combine:
    input:
        "message.txt", "allcaps.txt"
    output:
        "combined.txt"
    run:
        text = [open(path).read() for path in input]
        with open(output[0], 'w') as f_out:
            f_out.write("".join(text))
    # shell:
    #     "cat {input} > {output}"
```

```
snakemake -j1 
snakemake --dag | dot -Tsvg > graph.svg
```


My solution [Manuel]:
```
rule all:
    input:
        "combined_messages.txt"
        
rule generate_message:
    output:
        "real_message.txt"
    # If not on windows, you can use this shell command:
    # shell:
    #     "echo 'Hello, World' > {output}"
    # If on windows, you can use this python version:
    run:
        with open(output[0], 'w') as f:
            print("Hello, world", file=f)
            
rule shout_message:
    input:
        "real_message.txt"
    output:
        "allcaps.txt"
    run:
        with open(output[0], 'w') as f_out, \
             open(input[0], 'r') as f_in:
            content = f_in.read()
            f_out.write(content.upper())
            
rule combine_messages:
    input:
        "real_message.txt", "allcaps.txt"
    output:
        "combined_messages.txt"
    run:
        with open(output[0], 'w') as f_out, open(input[0], 'r') as f_in1, open(input[1], 'r') as f_in2:
            content = f_in1.read() + f_in2.read()
            f_out.write(content)
        
```

Snakemake documentation: https://snakemake.readthedocs.io/en/stable/


DAG of the second example [feel free to delete] (Thanks!)
![](https://i.imgur.com/ERD1FI8.png)


## 📚 Resources 

 [Post-workshop survey](https://www.surveymonkey.com/r/FL5ZZZV)

 [Data carpentry with Python](https://3zpb11r.momice.events/page/854828)
 
 [Future eScience Center workshops](https://escience-academy.github.io/)
 
 [MPI with Dask](https://mpi.dask.org/en/latest/)
 
 [Python implementation with JIT](https://pypy.org)
 
 [Dask documentation](https://docs.dask.org/en/latest)
 
 [Snakemake documentation](https://snakemake.readthedocs.io/en/stable/)
 
 [Calling external C and C++](https://carpentries-incubator.github.io/lesson-parallel-python/08-calling_external_C_libraries/index.html)