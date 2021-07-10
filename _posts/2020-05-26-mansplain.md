---
layout: post
title:  Finding "Mansplaining" in korean spoken corpus 🗣
date:   2020-05-26
tags: gender sociolinguistics  
---


I experienced *'Mansplaining'* a lot, especially when men suppose I don't know what they know. These wrong suppositions are expressed by korean verb endings. Many verb endings in korean implicate speakers' guess about listeners' knowledge. According to my experience, men tend to say like they are the only one who knows what they say and women tend to say like all the participants in the conversation share common knowledge. 

This is called <b>Information Structure.</b> It refers to speakers' assumption about whether listeners are already aware of the information they are conveying or not. There are two types of Information Structure. Strategic Information Structure is giving new information as old information, i.e. when speakers presuppose that listeners know the new information. Normative Information Structure is giving new information as new one, i.e. when speakers presuppose that listeners don't know the new information. 

I hypothesized that when giving new information men tend to use normative information structure more, while women tend to use strategic information structure more. 

### 1. Identifying the context where speakers introduce new information into the conversation 
<br>
To test this hypothesis, I first looked for the context giving new information. I used *'X이라는 Y'* phrases to identify if the speaker is introducing new information into the discourse.
For an accurate analysis, I analysed POS first, then search for *'X이라는 Y'* phrases. 

```python
def check_new(speech): # 'X이라는 Y' (X must be common or proper noun) 
    new_speech = []
    num = len(BeautifulSoup(speech).find_all('s'))
    for i in range(num):
        string = str(BeautifulSoup(speech).find_all('s')[i])
        if '/NNG+이/VCP+라는/ETM' in string or '/NNP+이/VCP+라는/ETM' in string:
            new_speech.append(string)
        else:
            continue
    return new_speech
    
 df['신정보speech'] = df['speech'].apply(lambda x:check_new(x))
``` 

After identifying this context, I added information about the speakers' and listeners' gender, job or age, 
which is provided in the <a href="https://ithub.korean.go.kr/user/guide/corpus/guide1.do" target="_blank">corpus</a>.  


```python
from bs4 import BeautifulSoup
line_df = pd.DataFrame(columns=['filename', 'speaker', 'gender', 'listener','job','setting','age','new_speech'])
count=0
for i in range(len(new_df)):
    speech = BeautifulSoup(new_df['신정보speech'][i]).find_all('s')
    for j in range(len(speech)):
        filename = new_df.iloc[i,0]
        speaker = new_df.iloc[i,1]
        gender = new_df.iloc[i,2]
        listener = new_df.iloc[i,43]
        job = new_df.iloc[i,42]
        setting = new_df.iloc[i,3]
        age = new_df.iloc[i,29]
        new_speech = speech[j]
        line_df.loc[count] = [filename, speaker, gender, listener, job,setting,age,new_speech]
        count+=1
```


### 2. Identifying which information structure speakers used based on verb endings 
<br>
I classified verb endings referring to previous studies. All the variants in the corpus were included. For instance, *'-거든'* is representative of normative information structure
when giving new information, as it implicates listeners don't know the information speakers are giving. *'-잖아'* is representative of strategic information structure 
when giving new information, as it implicates listeners know the information speakers are giving. 


```python
def find_ef(speech):
    if '잖/EP' in speech:
        pattern = '잖/EP\+[가-힣]*?/EF'
    else:
        pattern = '(?<=\+)[가-힣]*?/EF'
    match = re.search(pattern, speech)
    if match:
        return match.group()
    else:
        return ''
        
 df['종결어미'] = df['new_speech'].apply(lambda x : find_ef(x)) 
```

### 3. Results 
<br>
I plotted the results using ```plotly``` and tested statistical significance using ```R```. I excluded the context where information structure was not expressed explicitly.

```r
prop <- c(0.04761905,0.023)# proportion of events
n <- c(126, 128) # number of trials
x <- prop*n # number of events

prop.test(x = x,n = n,alternative = c("two.sided"), conf.level = 0.95) 
```

### 3.1. Based on speakers' gender 

<br>
<img src="https://github.com/yeounyi/yeounyi.github.io/blob/main/assets/img/speaker.jpg?raw=true" width=800>
<br>

 The graph shows the proportion of information structure usage based on speakers' gender. Blue bar represents female speakers and red one represents male speakers. The first column shows the proportion where speakers assume both they themselves and listeners don't know well about the new information. The second column shows the proportion where speakers assume only the speakers know the new information. The last one shows the proportion where speakers assume both speakers and listeners know the new information. It turns out <b>male speakers tend to assume they're the only one who know the new information *(normative information structure)* and female speakers tend to assume listeners also know the new information *(strategic information structure)*.</b> The p-value was lower than 0.1. 

### 3.2. Based on listeners' gender 
<br>
<img src="https://github.com/yeounyi/yeounyi.github.io/blob/main/assets/img/listener.jpg?raw=true" width=800>
<br>

 The graph shows the proportion of information structure usage based on listener' gender. Blue bar represents female listeners and red one represents male listeners. The first column shows the proportion where speakers assume both they themselves and listeners don't know well about the new information. The second column shows the proportion where speakers assume only the speakers know the new information. The last one shows the proportion where speakers assume both speakers and listeners know the new information. It turns out <b>when speakers use *normative information structure*, listeners tend to be female, but when speakers use *strategic information structure* listeners tend to be male.</b> P-value was not small enough to be significant, because listeners' gender were identified only in the one-on-one conversation, naturally shrinking the data size. Still, it seems interesting that the pattern was reversed compared to the analysis based on speakers' gender.  
 
In short, <b> male speakers tend to suppose listeners' ignorance of new information and female listeners tend to be assumed as ignorant of new information. </b>
 

