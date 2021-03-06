# COVID-19 and Social Media

Epidemija COVID-19 se razširja v pandemijo. Trenutno smo v samoizolaciji. Vsi čutimo posledice, nekateri direktno, drugi bolj posredno. Upamo, da se stanje čim prej izboljša in da lahko naš projekt v majhni meri k temu prispeva, če tudi le tako da nas ohranja zaposlene in pri zdravi pameti. 
Projekt smo pričeli s kreiranjem podatkovne množice, ki smo jo transformirali v uporabno obliko. Poleg tega smo uporabili nekatere podatkovne množice iz Kaggle za natančne podatke in statistike o širjenju okužb, ozdravelih ter smrtnih žrtev.

Zadnjih nekaj tednov smo se sestajali preko različnih medijev ter skongruirali 3 različne vire v 3 lastne podatkovne množice. Nato smo z uporabo metod naravnega procesiranja jezika prvotne podatke še nadgradili.

Radi bi razdelili napredek na tri glavne faze, v katerih smo posamezne naloge razdelili med člane skupine. Več podrobnosti v nadaljnih sekcijah.

## 1. faza: Webscrape API za socialne medije
Takoj smo naleteli na oviro, katere podatke lahko pridobimo.  Odločili smo se za Twitter, Reddit ter GTrends, saj so se nam zdeli najbolj zanimivi in dostopni za uporabo njihovih podatkov. Moramo izpostaviti, da so taki API-ji, ki ponujajo možnost pridobivanja tekstovne vsebine objav precej omejeni s klici. Prav tako smo morali to prilagoditi časovnem intervalu za nekaj mesecov nazaj, kar je za socialne medije precej veliko. Posledično je bila ta faza najdaljša.

# Reddit - https://pushshift.io/
Gledali smo zgolj primerne subreddit-e, ker bi bilo drugače zbiranje podatkov predolg proces za namene tega projekta (če ne celo v splošnem?).
## Analiza podatkov
Najprej smo pridobljene podatke poslali v Text Analysis and Sentiment Recognition API-ja. Želeli smo več ne-tekstovnih podatkov. 
Izbrali smo si množico, ki vsebuje:
Datum, Ocena Komentarja, Ocena Submmissiona, Naslov Submissiona, Text Komentarja
Ter poleg vseh teh tudi atribute za prisotnost okoli 150 najpogosteje omenjenih ključnih besed ter oceno razpoloženja (sentiment).
Najpogostejše klučne besede v izbrani podmnožici so bile:
```
'coronavirus', 'people',  'questions',  'comments',  'cases',  'one',  'reports',  'videos',  'suggestions',  'images',  'theories',  'daily discussion post',  'virus',  'china',  'italy',  'us',  'government',  'covid',  'country',  'covid-19',  'home',  'masks',  'accounts',  'coronavirus outbreak',  'deaths',  'trump',  'health',  'schools',  'testing',  'everyone',  'message',  'uk',  'action',  'u.s.',  'two',  'symptoms',  'moderators',  'hospital',  'usa',  'pandemic',  'subreddit',  'cdc',  'bot',  'thing',  'countries',  'way',  'sources',  'twitter',  'tests',  'policy',  'world',  'things',  'youtube',  'patients',  'numbers',  'president',  'all',  'number',  'politicians',  'chinese',  'info',  'flu',  'spread',  'case',  'ban',  'rules',  'everything',  'something',  'discussions',  'facebook',  'someone',  'lot',  'south korea',  'professionals',  'state',  'highlights',  'accusations',  'discretion',  'offences',  'attacks',  'repeat offenders',  'pages',  'support resources',  'daily discussion thread',  'advice.',  'giving',  'anyone',  'anything',  'work',  'americans',  'measures',  'hospitals',  'death',  'person',  'point',  'risk',  'nothing',  'europe',  'united states',  'wuhan',  'money',  'italian',  'doctors',  'quarantine',  'population',  'state of emergency',  'test',  'distancing',  'man',  'information',  'article',  'outbreak',  'situation',  'children',  'reason',  'school',  'lockdown',  'source',  'times',  'response',  'restaurants',  'thousands',  'supplies',  'others',  'bars',  'no one',  'kids',  'life',  'area',  'vaccine',  'shit',  'america',  '1 million',  'coronavirus test',  'infections',  'news',  'gatherings',  'herd immunity',  'total',  'france',  'job',  'officials',  'post',  'employees',  'four',  'emergency',  'states',  'coronavirus cases',  'corona',  'experts',  'scientists',  'hands',  'events',  'germany',  'some',  'travel ban',  'link',  'friends',  'british',  'ohio',  'australia',  'disease',  'idea',  'food',  'india',  'nyc',  'many',  'contact',  'wife',  'staff',  'family',  'part',  'more',  'lives',  'spain',  'who',  'crisis',  'place',  'posts',  'nba',  'test kits',  'thanks',  'american',  'flight',  'doctor',  'rome',  'community',  'house',  'economy',  'boomers',  'zero',  'fact',  'order',  'guy',  'icu',  'curve',  'problem',  'sense'
```
Po obdelavi dobimo naslednjo podatkovno množico:
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>date</th>
      <th>comment_score</th>
      <th>submission_score</th>
      <th>negative</th>
      <th>neutral</th>
      <th>positive</th>
      <th>people</th>
      <th>coronavirus</th>
      <th>questions</th>
      <th>...</th>
      <th>economy</th>
      <th>boomers</th>
      <th>zero</th>
      <th>fact</th>
      <th>order</th>
      <th>guy</th>
      <th>icu</th>
      <th>curve</th>
      <th>problem</th>
      <th>sense</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>2020-03-16</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2020-03-16</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2020-03-16</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>2020-03-16</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>2020-03-16</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>9995</th>
      <td>9995</td>
      <td>2020-03-12</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9996</th>
      <td>9996</td>
      <td>2020-03-12</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9997</th>
      <td>9997</td>
      <td>2020-03-12</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9998</th>
      <td>9998</td>
      <td>2020-03-12</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9999</th>
      <td>9999</td>
      <td>2020-03-12</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>

Še statistika podatkovne množice:
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>comment_score</th>
      <th>submission_score</th>
      <th>negative</th>
      <th>neutral</th>
      <th>positive</th>
      <th>people</th>
      <th>coronavirus</th>
      <th>questions</th>
      <th>comments</th>
      <th>...</th>
      <th>economy</th>
      <th>boomers</th>
      <th>zero</th>
      <th>fact</th>
      <th>order</th>
      <th>guy</th>
      <th>icu</th>
      <th>curve</th>
      <th>problem</th>
      <th>sense</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>10000.00000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.00000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.00000</td>
      <td>...</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.0000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>4999.50000</td>
      <td>1.666200</td>
      <td>1.318000</td>
      <td>-4.623600</td>
      <td>-4.459800</td>
      <td>-4.91560</td>
      <td>0.198300</td>
      <td>0.126700</td>
      <td>0.037500</td>
      <td>0.11420</td>
      <td>...</td>
      <td>0.009800</td>
      <td>0.001400</td>
      <td>0.004500</td>
      <td>0.009600</td>
      <td>0.009700</td>
      <td>0.009400</td>
      <td>0.0001</td>
      <td>0.009500</td>
      <td>0.009400</td>
      <td>0.009800</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2886.89568</td>
      <td>9.168979</td>
      <td>3.523821</td>
      <td>223.548644</td>
      <td>223.552338</td>
      <td>223.54176</td>
      <td>0.398739</td>
      <td>0.332653</td>
      <td>0.189993</td>
      <td>0.31807</td>
      <td>...</td>
      <td>0.098514</td>
      <td>0.037392</td>
      <td>0.066934</td>
      <td>0.097513</td>
      <td>0.098015</td>
      <td>0.096502</td>
      <td>0.0100</td>
      <td>0.097009</td>
      <td>0.096502</td>
      <td>0.098514</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.00000</td>
      <td>-39.000000</td>
      <td>0.000000</td>
      <td>-9999.000000</td>
      <td>-9999.000000</td>
      <td>-9999.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2499.75000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>4999.50000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>7499.25000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>9999.00000</td>
      <td>558.000000</td>
      <td>70.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.00000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.00000</td>
      <td>...</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.0000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




## Priprava podatkov
Redditov lastni API, ki ponuja poleg agregiranih statistik, tudi možnost pridobivanja vsebin tako-imenovanih 'submission'-ov ter komentarjev. Podatki so skonstruirani na naslednji način:

Datum, Ocena Komentarja, Ocena Submmissiona, Naslov Submissiona, Text Komentarja

Po zgornjem formatu imamo trenutno podatke od 16. marca do 27. januarja tega leta. 
Naslednji odsek kode je bil uporabljen za zgradbo te množice, delo je precej olajšala uporaba modula psaw:
```Python
from psaw import PushshiftAPI
import datetime as dt
import csv
api = PushshiftAPI()
start_epoch=int(dt.datetime(2020, 1, 1, 0, 0, 0).timestamp())
before = int(dt.datetime(2020, 1, 21, 2, 0, 0).timestamp())

 
cache = 0
f =  open(r'reddit21.csv', 'w')
writer = csv.writer(f)
while( before>start_epoch ):
    gen = api.search_comments(after=start_epoch, before=before,  subreddit="Coronavirus")
    for c in gen:
        print(cache)
        print(dt.datetime.fromtimestamp( c.created_utc ))
        submission = list(api.search_submissions(ids = [c.link_id.split("_")[1]]))
        if(len(submission)>0):
            submission = submission[0]
        else:
            continue
        writer.writerow([ dt.datetime.fromtimestamp( c.created_utc ).date(), c.score, submission.score, (submission.title).replace("\n"," ") , (c.body).replace("\n"," ") ])
        #before = c.created_utc 
        cache += 1   
        if( cache%105==0 ):
            before -= 60 * 60
            gen = api.search_comments(after=start_epoch, before=before,  subreddit="Coronavirus")
```

# Twitter
## Analiza podatkov o Tweetih iz strani Kaggle

Medtem ko se pripravlja naša baza, bomo uporabili podatke o Tweetih is Kaggla. V naši bazi bomo zbrali Tweete od 1.1.2020 do 16.3.2020. Za vsak dan zbiramo šest tisoč Tweetov, ki omenjajo Koronavirus. 
Za sprotno poročilo smo se odločili da naredimo hitro analizo na podobnih podatkih iz Kaggla, ki jih nato lahko uporabimo za primerjavo z našimi podatki, ko bodo na voljo. V ta namen smo Kagglovo bazo pretvorili v format, ki smo ga izbrali za našo bazo: 
Datum - Lokacija - Tweet - Število všečkov - Število retweetov. 
Za enkrat bodo te podatki služili kot vzorec, da se seznanimo z vrsto podatkov ter lahko z njimi delamo, dokler pripravljamo svojo bazo. Kaggle baza sicer vsebuje podatke zgolj od 1. do 22. marca, vzeli smo vzorec prvih 6000 za vsak dan in dobili 114000 tweetov velik vzorec.

## Pregled osnovnih statističnih podatkov

Najbolj osnovna statistika, ki jo lahko pregledamo je povprečno število všečkov in retweetov na tweet, ter povprečni standardni odklon le teh.
Dobimo rezultate da je povprečje všečkov na tweet 15391.429 s standardnim odklonom 43243.936, za retweet-e pa dobimo rezultate da je povprečnje na tweet 5.115 s standardnim odklonom 138.549. Iz tega vidimo da je pri obeh velik standardni odklon. Seveda je to pričakovano saj imajo različni računi različno število sledilcev in posledično različno "prometa", ki gre čez njihov račun. Lahko razberemo, da je takih, ki imajo manj sledilcev veliko več kot pa teh z velikim številom. To na nek način potrdi našo izbiro vzorca, saj vemo, da je število sledilcev na Twitterju sledi Paretovi distribuciji. Sicer podatkov kot je število sledilcev, ali je račun potrjen itd. v naši bazi ne bomo imeli, je pa zanimivo razmisliti kako vplivajo na podatke.

Podatke lahko predstavimo, kot da gre za normalno porazdelitev. Če to storimo lahko bodimo nasledne grafe.
![3graphs.png](./images/3graphs.png)
Vidimo da število tweetov glede na število všečkov, praktično logaritmično pada z večjim število všečkov. To je uvidno tako v tweetih, ki imajo okoli 4000 všečkovi in manj (zeleni graf) kot na tistih, ki imajo okoli 40000 všečkov in manj (modri graf). Pri vseh treh percentilih za katere smo naredili graf po normalni porazdelitvi, torej 75-percentil, 50-percentil in 40-percentil, se opazi enak vzorec padanja števila tweetov z večjih številom všečkov. 

Zanima nas tudi število všečkov in retweetov glede na posamezni dan, tako lahko nekako vidimo kako je potekal "promet".
![promet.png](./images/promet.png)
Če promet po določenem dnevu opredelimo kot seštevek všečkov in retweetov, vidimo da je bilo največ prometa okoli desetega ali pa enajstega marca. Ker bodo te dnevi prisotni tudi v naši bazi, bomo lahko na podlagi tega naredili primerjave med načinon zajemanja podatkov, ki smo ga uporabili mi, in tem, ki so ga uporabili za Kaggle baze.

Ker bomo v naših podatkih pregledovali tudi tweete glede na lokacije, nas zanima, kako so loakcije razporejene v Kaggle bazah. Kar nam vrne spodnji graf.
![locations.png](./images/locations.png)
Iz vseh 114000 tweetov, ki smo jih vzeli za vzorec, jih je le 5976 imelo navedeno lokacijo. Izmed teh 5976 tweetov dobimo 111 različnih držav. Te smo za potrebe grafa omejili na tiste, ki so imeli več kot 30 tweetov v obdobju od prvega do dvaindvajsetega marca. Izkaže se da je takih le 24. Izmed teh 24 se vidi da Amerika množično prevladuje, sledita ji še Kanda in Velika Britanija, torej še dve angleško govoreči državi, ampak Ameriki nista blizu. To je podatek, ki ga bomo tudi mi lahko spremljaji v naši bazi, in ga primerjali s podatki, ki smo jih dobili iz Kaggle-ove baze. 

Za zaključek, lahko te podatke še simplistično pregledamo na podlagi vsebine samega tweeta. Zanima nas naprimer koliko ljudje govorijo o obolelih, o novih primerih, o smrtih in ozdravelih.
![words.png](./images/words.png)
Iz zgornjega prikaza lahko vidimo da jih največ (po našem zelo omejenem iskanju) govori o teh, ki so ozdraveli, temu pa sledijo tweeti, ki vsebujejo besedo death. Z hitrim pogledom v podatke vidimo, da gre dejansko za avtomatiziran profil, ki objavlja statusne spremembe.

## Priprava naše podatkovne baze
Našo podatkovno bazo bomo pripravili z pomočjo twitter scrapperja in ne direktno z uporabo Twitter API. Uporabili bomo twint, GitHub modul, ki je namenjen javni uporabi. Ima opcijo iskanja tako po besedah kot po uporabnikih. Koda za samo proces pridobivanja podatkov je bila sledeča:
```python
import twint

c = twint.Config()
c.Search = "\"COVID-19\" OR \"Coronavirus\" OR \"SARS-CoV-2\""
c.Output = "searches.csv"
c.Stats = True
c.Since = since.strftime("2020-01-01")
c.Until = (since + datetime.timedelta(1)).strftime("2020-01-02")
c.Limit = 6000
#c.Hide_output = True
c.Store_csv = True
twint.run.Search(c)
```
Kodo smo pognali za vsak dan od 1.1.2020 do 15.3.2020, tako da smo dobili vzorec 6000 tweetov dnevno. To pa za potrebe naše analize ni zadostovalo saj ne vsebuje lokacije. Na srečo nam pa twint omogoča pogledati lokacijo uporabnika, ki je objavil tweet. 

Ko smo enkrat imeli vse tweete za našo bazo smo morali dati vse še čez program, ki je za vsak tweet pogledal njegovo lokacijo. To smo zapisali v txt datoteko, nato pa iz nje prebrali to vrednost in jo shraili v csv, katerega bomo kasneje uporabili za analizo vseh podatkov. Ker je nekaj uporabnikov, ki imajo za lokacijo podano nekaj kar ni realna geografska lokacija, bomo ob končanem preračunavanju lokacij, morali še pregledati katere lokacije so pravilne. To lahko storimo z python modulom GeoPy, ki nam ne bo vrnil vrednosti, če lokacija ne bo pravilna. S pomočjo tega bomo nato lahko izvedli analizo nad podatki glede na države.

# Gtrends

Google trends je spletna stran kjer Google objavlja podatke o najbolj iskanih izrazih in omogoča iskanje podatkov o iskanosti posameznih izrazov glede na čas, regije, province, mesta in države. Vrednost iskanosti je normalizirana na vrednost od 0 do 100 glede na delež vseh iskanj pri danih pogojih in predstavlja relativno popularnosti iskanosti izraza. Enaka vrednost pri isti pogojih za dve različni državi to ne pomeni enako število iskanj. Google trends malo iskane izraze označi z 0, tiste z posebnimi znaki (npr apostrofi= in tiste, ki jih uporabnik v kratkem času velikokrat ponovi pa ne upošteva. Za to spletno stran obstaja API Pytrends, ki z pythonom omogoči avtomatizacijo poizvedb. Ker ima tudi arhiv popularnosti poizvedb sem spisal program, ki za vsak dan od 1.1.2020 do izbranega datuma najde popularnost poizvedb za vse države in teritorije sveta in jih spravi v pandas dataframe, ter ga združi z tabelami prejšnjih dni. Zbrane podatke zapiše v CSV datoteko.

# Vizualization



```python
import numpy as np
import pandas as pd
import plotly as py
import plotly.express as px
import plotly.graph_objs as go
from plotly.subplots import make_subplots
from plotly.offline import download_plotlyjs, init_notebook_mode, plot, iplot
```

### Prikaz širjenja COVID-19
Uporabili smo dataset iz Kaggle, ki vsebuje podatke do 3.31.2020. Kasneje bomo seveda uporabili svoje podatke. Želimo primerjati dejansko širjenje COVID-19 s širjenjem panike na socialnih omrežjih.


```python

#load csv, sort by date, get rid of nan
#Province/State,Country/Region,Lat,Long,Date,Confirmed,Deaths,Recovered
data = pd.read_csv('data\covid_19_data.csv')
data = data.rename(columns={'ObservationDate':'Date'})
data= data.groupby(['Country/Region', 'Date']).max().reset_index().sort_values('Date', ascending=False)
#data['Date'] = pd.to_datetime(data['Date'])
#data = data.sort_values('Date', ascending=True)
# replace NaN Provinces with string
#data['Province/State'] = data['Province/State'].fillna('No_Province')

data2 = data[data['Confirmed']>0]
data2 = data2.groupby(['Date','Country/Region']).sum().reset_index()
#data2['Date'] = pd.to_string(data2['Date'])
data2

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Country/Region</th>
      <th>SNo</th>
      <th>Confirmed</th>
      <th>Deaths</th>
      <th>Recovered</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01/22/2020</td>
      <td>Japan</td>
      <td>36</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01/22/2020</td>
      <td>Macau</td>
      <td>21</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01/22/2020</td>
      <td>Mainland China</td>
      <td>35</td>
      <td>444.0</td>
      <td>17.0</td>
      <td>28.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01/22/2020</td>
      <td>South Korea</td>
      <td>38</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01/22/2020</td>
      <td>Taiwan</td>
      <td>29</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>5461</th>
      <td>03/31/2020</td>
      <td>Venezuela</td>
      <td>10530</td>
      <td>135.0</td>
      <td>3.0</td>
      <td>39.0</td>
    </tr>
    <tr>
      <th>5462</th>
      <td>03/31/2020</td>
      <td>Vietnam</td>
      <td>10531</td>
      <td>212.0</td>
      <td>0.0</td>
      <td>58.0</td>
    </tr>
    <tr>
      <th>5463</th>
      <td>03/31/2020</td>
      <td>West Bank and Gaza</td>
      <td>10532</td>
      <td>119.0</td>
      <td>1.0</td>
      <td>18.0</td>
    </tr>
    <tr>
      <th>5464</th>
      <td>03/31/2020</td>
      <td>Zambia</td>
      <td>10533</td>
      <td>35.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>5465</th>
      <td>03/31/2020</td>
      <td>Zimbabwe</td>
      <td>10534</td>
      <td>8.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>5466 rows × 6 columns</p>
</div>


# Spread of Coronavirus
![Spread of Coronavirus](./images/SpreadOfCoronavirus.png)

# Spread of Information - Google Trends
![Spread of Information](./images/GoogleTrendsCorona.png)

# Deaths - Coronavirus
![Deaths of Coronavirus](./images/DeathsCoronavirus.png)
