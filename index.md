## Introduction

## Considerations

## What is Adventure Time

## Downloading the Transcript

We need a dataset to train our model. We will use Beautiful Soup to scrape the trancripts, use loops to clean, then save the data as individual sentences in a csv file. For a list of episodes that aired in the first seaosn of Adventure Time, navigate to https://adventuretime.fandom.com/wiki/Season_1.


```py
import requests
from bs4 import BeautifulSoup as BS
import lxml
import re
import pandas as pd
import csv

# create list of episode titles from season 1

s1 = [
    "Slumber Party Panic",
    "Trouble in Lumpy Space",
    "Prisoners of Love",
    "Tree Trunks",
    "The Enchiridion!",
    "The Jiggler",
    "Ricardio the Heart Guy",
    "Business Time",
    "My Two Favorite People",
    "Memories of Boom Boom Mountain",
    "Wizard",
    "Evicted!",
    "City of Thieves",
    "The Witch's Garden",
    "What is Life?",
    "Ocean of Fear",
    "When Wedding Bells Thaw",
    "Dungeon",
    "The Duke",
    "Freak City",
    "Donny",
    "Henchman",
    "Rainy Day Daydream",
    "What Have You Done?",
    "His Hero",
    "Gut Grinder"
]

# format episode titles for use in url

season_1 = []

for i in s1:
    if ' ' in i:
        i = i.replace(' ', '_')
        season_1.append(i)
    else:
        season_1.append(i)

# fetch trancripts for each episode and add to single list
# NOTE: this Community content is available under CC-BY-SA unless otherwise noted.

s1_transcript = []

for ep in season_1:
    url = f'https://adventuretime.fandom.com/wiki/{ep}/Transcript'
    site = requests.get(url)
    source_code = site.content
    soup = BS(source_code, 'lxml')
    transcript = soup.find_all('dd')
    for i in transcript:
        s1_transcript.append(i)

# convert b4.element.tag to strings

s1_trans_str = []

for i in s1_transcript:
    string = str(i)
    s1_trans_str.append(string)

# remove superflous stuff

s1_sentences = []

for x in s1_trans_str:
    x = x.replace(']', '')
    x = x.replace('[', '')
    x = x.replace('(', '')
    x = x.replace(')', '')
    x = re.sub('<.+?>', '', x)
    x = x.replace(':', ' says') # the ':' signifies a character line
    s1_sentences.append(x)

df = pd.DataFrame({
    'text' : s1_words # import to name text for transformers training
})

df.to_csv('at_s1_text.csv')

```

## Training the Model

```py
# python code goes here
```

## Loading in the Model

```py
# python code goes here
```

## Bias Test

```py
# python code goes here
```
### Analysis

## Generating Statements from Season 1

## Generating Statements from Season 10

## Analysis

```py
# python code goes here
```

## Discussion

## Conclusion

## Positionality Statement 