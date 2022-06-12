---
layout: post
title:  2020 도쿄 패럴림픽 선수들의 비전 시각화 🥇
date:   2021-09-19
tags: data analysis 
---

[올림픽위원회 홈페이지](https://www.paralympic.org/tokyo-2020)는 패럴림픽에 출전한 모든 선수들의 프로필을 제공합니다. 선수들의 프로필에는 나이, 성별, 종목 등 기본적인 정보뿐만 아니라, 그들의 운동 철학(Philosophy), 목표(Ambition), 롤모델(Hero) 등의 정보도 있습니다. 

이번 도쿄 패럴림픽에서 보치아 금메달을 따낸 최예진 선수의 프로필인데요. 목표(Ambition)는 도쿄 패럴림픽에서 금메달을 따는 것, 운동 철학(Philosophy)은 "보치아는 2012 패럴림픽 전까지는 내 꿈이었고, 이후엔 내 미래에 대한 희망이다"라고 합니다! 목표를 이뤘다니 정말 멋지네요 :)

<br><br>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/d5f846fb-849a-4215-be8c-12b8409cceeb.png" width=800>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/f54c5f15-39bd-44f2-9b04-9b5e35f66bc7.png" width=800>
<br>

2020년 도쿄 패럴림픽에 참가한 선수들은 총 4,500여명입니다. 이들의 <b>운동 철학(Philosophy), 목표(Ambition), 롤모델(Hero)</b>은 무엇인지 분석해보았습니다. 

<br>
<br>
<h2> 1. 운동 철학(Philosophy) </h2>

모든 선수들의 운동 철학을 하나의 텍스트로 합치고, [Spacy](https://spacy.io/api/lemmatizer)를 이용해 표제어로 변형한 뒤(lemmatization) N-gram을 구했습니다. N-gram이란, N개의 연속적인 단어 나열을 말하는데, 이를 이용하면 단순히 한 단어의 빈도수를 구하는 것보다 의미있는 결과를 얻을 수 있습니다. 저는 Bigram(2개의 연속적인 단어 나열)과 Trigram(3개의 연속적인 단어 나열)을 선택했고, 이를 빈도수대로 정렬하면 다음과 같습니다.

<br><br>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/ce0bced4-b640-444e-97b6-cf24cb3bf9f1.JPG" width=800>
<br>

"절대 포기하지 않는다(never give up)", "열심히 훈련한다(work hard, hard work)", "할 수 있다(able to)" 등 끈기와 긍정에 대한 메시지가 많이 보입니다. 

* _Never surrender and **never give up**. (절대 물러서지 말아라. 절대 포기하지 말아라.)_
* _There is hope **as long as** there is life, so do not give up the fight. (살아있는 한 희망은 있으니, 포기하지 말라.)_
* _**The most important thing** that will make you dreams come true is courage. (당신의 꿈을 이뤄주는 가장 중요한 것은 용기다.)_
* _Never quit **no matter what**. Always fight it out. (무엇이든 포기하지 말아라. 항상 맞서 싸워라.)_
* _I encourage every person **with an impairment** to believe in themselves, that they can achieve anything they want. Don't give up. (나는 장애가 있는 모든 사람들이 그들 자신을, 그리고 그들이 원하는 모든 것을 이뤄낼 수 있다고 믿게 만든다. 포기하지 말아라.)_
* _Athletics is not a profession, but **a way of life**. (운동은 직업이 아니라, 삶의 방식이다.)_
* _Always try to be the **best version of** yourself that you can be, whatever happens. (어떤 일이 일어나든지, 항상 당신이 될 수 있는 최고가 되도록 노력하라.)_

<br><br>

"keyword-in-context" 방법을 그래프로 나타내는 [word tree](https://www.jasondavies.com/wordtree/)를 이용해 운동 철학을 시각화하면 다음과 같습니다. 수영에 출전한 선수가 많아서 Swimming이 가장 첫 키워드로 뽑혔는데요, 이외에도 word tree 사이트에서 다양한 키워드를 검색해보며 더 자세히 살펴볼 수 있습니다.
<br><br>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/50940ced-ce1c-44ba-8983-a9dbcee3983f.JPG" width=800>
<br>

<br><br>

마지막으로 Pretrained [Pegasus Model](https://ai.googleblog.com/2020/06/pegasus-state-of-art-model-for.html)을 이용해 선수들의 운동 철학을 요약했습니다. 이 모델은 BBC 뉴스를 요약하는 것으로 학습되어서, 여러 선수들의 운동 철학을 요약하는데 뛰어난 성능을 보여주진 않았습니다. 그러나 의미있는 요약도 있어 공유해보려고 합니다. 선수들을 국적에 따라 나눈 후, 국적에 따라 운동 철학을 요약해보았습니다.
<br> 
* _**Afghanistan**: You were made to do hard things, so believe in yourself. (너는 어려운 일을 해내도록 태어났다. 너 자신을 믿어라.)_
* _**Guatemala**: If you want to succeed in life you have to be willing to suffer. (성공하고 싶다면, 고통을 극복할 수 있어야 한다.)_
* _**Nicaragua**: To be the best I can be. (나의 최선이 되기 위해)_
* _**Spain**: Sport has given me everything. (스포츠는 나의 전부다.)_
* _**Republic of Moldova**: I would say we have special abilities, skills that others do not use. (우리는 다른 사람들이 쓰지 않는 특별한 재능을 가졌다.)_

<h2>2. 목표(Ambition)</h2>

이번에도 모든 선수들의 목표를 하나의 텍스트로 합치고, Spacy를 이용해 표제어로 변형한 뒤(lemmatization) N-gram을 구했습니다. 운동 철학과 달리, 목표는 선수들간의 차이가 적고 중복이 매우 많았습니다.
<br><br>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/ea8e6b2f-0f15-484f-a448-27ac3f3b404c.JPG" width=800>
<br>

대부분의 선수가 패럴림픽에 출전하는 것, (금)메달을 따는 것, 세계 신기록을 세우는 것을 목표로 가졌습니다. 
* _**To compete at** the 2020 Paralympic Games in Tokyo. (2020 도쿄 패럴림픽에 출전하는 것)_
* _**To win gold medals** at the Paralympic Games and the world championships. (패럴림픽과 세계 선수권 대회에서 금메달을 따는 것)_
* _To break **the world record** in his category. (본인 종목에서 세계 신기록을 세우는 것)_
<br><br>
word tree 시각화 결과는 다음과 같습니다. 선수들의 목표가 운동 철학보다 균일해서 그런지, 여러 선수들의 목표를 더 잘 요약해줍니다. 패럴림픽에 출전하기, (금)메달 따기 외에도 "코치가 되는 것(To become a coach)"과 같은 목표도 눈에 띕니다. 
<br><br>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/9a17c9f3-0af3-44af-ae79-684e0b03574b.JPG" width=800>
<br>

목표 역시 Pretrained Pegasus Model을 이용해 요약해봤는데요. 목표는 나이, 성별, 국적 등에 관계없이 매우 균일했습니다. 그래서 전체 선수들의 목표를 요약했고, 그 결과는 다음과 같습니다.
* _To win a medal at the 2020 Paralympic Games in Tokyo, to set a world record, and to compete at the 2024 Paralympic Games in Paris. (2020 도쿄 패럴림픽에서 메달을 따고, 세계 신기록을 세우고, 2024 파리 패럴림픽에 출전하는 것)_

<h2>3. 롤모델(Hero) </h2>

텍스트로 이루어진 운동 철학이나 목표와 달리, 롤모델 항목은 롤모델들의 리스트로 이루어져 있습니다. 따라서 전체 선수들의 롤모델 순위뿐만 아니라, 국적, 성별, 종목별 롤모델의 순위를 분석해보았습니다. 
<br>
먼저 전체 선수들의 롤모델 순위입니다. 미국의 수영 선수 마이클 팰프스와 자메이카의 육상 선수 우사인 볼트가 압도적인 비율로 1,2위를 차지했습니다. 4위와 10위를 차지한 선수들의 아버지, 어머니도 눈에 띕니다. 롤모델을 지목한 선수가 남성인 경우 'His'를, 여성인 경우 'Her'를 쓰는데, 아버지를 롤모델로 지목한 선수는 여성보다 남성 선수가 많았고 반대로 어머니를 지목한 선수는 남성보다 여성 선수가 많았다는 점이 흥미롭습니다. 또한, 하늘색으로 표시한 선수는 패럴림픽에 출전하는 선수입니다. 영국의 패럴림픽 수영 선수 엘리 시몬즈, 브라질의 패럴림픽 수영 선수 다니엘 디아즈가 순위권에 들었습니다.
<br><br>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/d7946973-84bd-48b8-a317-494e530eeb20.JPG" width=800>
<br>

다음으로 롤모델로 지목된 선수들의 국적(왼쪽)과 롤모델을 지목한 선수, 즉 이번 패럴림픽에 출전한 선수들의 국적(오른쪽)을 비교해봤습니다. 미국의 선수가 가장 많이 롤모델로 지목받았으나(15.6%), 이번 패럴림픽에 출전한 미국 선수는 9.5%에 그칩니다. 이렇게 패럴림픽에 출전한 선수들의 비중보다 롤모델로 지목받은 선수들의 비중이 더 높은 나라는 미국과 자메이카, 이렇게 두 나라가 있습니다. 아무래도 미국의 수영 선수 마이클 팰프스와 자메이카의 육상선수 우사인 볼트의 영향인 것 같네요.
<br><br>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/099e397b-f152-4b0a-abbe-b661b7704501.JPG" width=1000>
<br>

다음은 성별에 따른 롤모델 순위입니다. 여성 선수들의 롤모델에는 부모님뿐만 아니라 할머니(grandmother)까지 포함되는 것이 흥미롭습니다. 또한 앞서 언급했다시피 여성 선수는 아버지보다 어머니를 롤모델로 많이 지목했습니다. 패럴림픽 선수도 3명이 순위권 안에 들었습니다.
<br><br>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/b86a8d85-ae8f-4c97-9a4f-c8ebc0f9c086.JPG" width=800>
<br>

남성 선수의 롤모델은 어떻게 다를까요? 어머니와 할머니는 순위권에 없고 아버지와 부모님만 있다는 점이 여성 선수와 다릅니다. 또한, 남성 선수가 패럴림픽 선수를 롤모델로 지목한 비중(0.80%)은 여성 선수가 그러한 비중(1.92%)의 절반입니다.
<br><br>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/4199217a-1c72-4502-9561-5bc8ae2daa85.JPG" width=800>
<br>

마지막으로 종목별 롤모델입니다. 항상 1, 2위를 차지한 수영 선수 마이클 팰프스와 육상 선수 우사인 볼트의 종목을 먼저 살펴볼까요?
역시 육상 종목에서 우사인 볼트가 압도적 1위를 차지했습니다.
<br><br>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/2e3d1304-ab5e-47af-9f04-5906a11374c0.JPG" width=800>
<br>

마이클 팰프스는 본인 종목인 수영뿐만 아니라, 철인 3종에서도 1위를 차지했습니다.
<br><br>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/4e668fca-f346-4730-837d-6f6b53ea9824.JPG" width=1000>
<br>

패럴림픽 고유 종목인 보치아의 경우, 어떤 종목의 선수가 롤모델로 지목되었을까요? 1위는 축구 선수 크리스티아누 호날두가 차지했고, 2위는 테니스 선수, 그 외는 모두 보치아 선수가 차지했습니다. 모두 구기 종목이라는 공통점을 찾을 수 있습니다.
<br><br>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/2a516f72-fc86-4bf2-8225-8c6831c0f0c8.JPG" width=800>
<br>

마지막으로 재밌는 점을 발견했는데요. 부모님 또는 아버지가 롤모델 1위를 차지한 종목들이 4개 있었습니다. 이들 중 두 종목은 동양에서 유래한 종목이고(태권도, 유도) 나머지 두 종목은 앉아서 하는 구기 종목(휠체어 농구, 좌식 배구)이라는 공통점이 있었습니다! 태권도와 유도의 경우 효를 중시하는 문화 때문에 이런 결과가 나온 걸까요?
<br><br>
<img src="https://media.soprize.so/AnswerImage/2021-09-19/fe7c5cc6-42df-4a71-b396-9362668a81cf.JPG" width=1000>
<br>

<br><br>
지금까지 2020 도쿄 패럴림픽에 참여한 선수들의 운동 철학(Philosophy), 목표(Ambition), 롤모델(Hero)을 분석해봤습니다. 모두 열심히 노력해서 목표를 이루고 누군가의 롤모델이 되길 바랍니다 :) 


* 모든 코드와 데이터는 [Github](https://github.com/yeounyi/paralympics-goals-analysis)에서 확인하실 수 있습니다.
