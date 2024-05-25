today and first we'll start from um final preparations of the unified data set um right now because we have everything stored in in one table and we don't separate it into different
entities it's um quite important to
um to understand uh which features um
needs to be included where so that's why
I create created a several lists of
features um first list is uh called to
to predict um so it is everything about
future is positive growth future 5 day
so it's a um Zer or1 it can be one day
forward 30 days forward 90 days forward
prediction and you can get generate 10
of them and then um use your modeling
phase and generate many models covering
and different features to predict um and
select some model and some strategy
which works better probably um our
approach to to generate a predictions
for one week ahead is not that strong
and we need to um to look to look at the
30 days ahead 30 periods ahead
prediction then there is a growth future
5 day it's a numerical uh value for for
the exact growth and it it is useful not
only for the uh regression or numerical
prediction but it it's also useful to
evaluate your um strategy um efficiency
uh and and profits from the
strategy because um if you have this
this model and you know when you um
predict growth and invest in in that
growth and when you sell it in in five
days you can um have um the the final
answer on the profitability of of your
um model um just um running a few uh
Vector commands in in pandas then the
next category is to to drop it's it can
be um many many features which uh you
might leave in the data frame like Year
date index
_ X which is an artifact from some joint
quarter uh even original open high low
close volume uh feature um I I don't uh
use them all uh because they are
absolute values and this is not a very
good uh thing to include absolute values
to to oh to to the models predictions
unless it's a statistical model and they
have some tricks like predicting not
absolute value but predicting growth one
exception is that um I do a
transformation for a volume and uh I
include logarithm of volume um just to
have a smaller number which is
distributed between Zer and 10 and not
between 0 and 10
billion um then uh there there are a few
features um which we call categorical uh
normally it's a text features or some
features that are derived from from
text um we will exclude them um but we
will generate um many additional um
binary uh Fe features which are called
damis and which are based on categorical
um variables and next uh um we have all
num numerical features and this is the
the most important set of um uh features
that we have um currently there are
about 200 features in in the data set of
maybe with the categorical damis it is
about 240 features in in the data set
that are used uh for prediction and as
you can guess uh it is much more
powerful or it should be much more
powerful uh than just using one CCI
index or one growth feature or uh or
even two three features U that uh you
might think about first of all um but of
course it's it's all needs to be checked
and um these numerical features um can
be grouped into um these um
subcategories first it's growth
everything that is related to to growth
and that that's our
um understanding about previous uh state
of the stock of a other assets or um
benchmarks
um some periods uh ago so we are saving
um information from the past um what

happened 3 days ago 5 days ago 30 days

ago 90 days ago um in in these features

and um flatten the the whole table that

um one um one record uh which is about

200 features and something that we want

to predict is is actually a state of the

world so having this record um only this

record only one line we should be able

um to to predict uh some answer on the

test data or on the latest data that

will arrive um just today if you run the

data today uh so that um you can use

that for for your um Investments so next
uh is technical indicators and patterns
it's U many features and about 100 of
them and I think I used most of the
features listed in t lip um there are
many books written about it if you see
the technical indicators especially for
um some assets like crypto when you
don't have many other fundamental
factors um I think um technical features
are more important for for that and
asset class macro I included just a few
macro indicators maybe 10 of them I have

an article about 60 micro indicators

again uh if we see that these these

indicators are important and we will see

later in in uh this lecture and that

brings us to idea that we might want to

to Source more micro indicators or more
uh local micro indicators for uh Indian
markets or for European markets because
we have tickers from from the US Indian
and European markets but macro are all

about uh the US market

it can be custom numerical features and

um I think uh that you you still need to

think about it and don't assume that

everything is already covered and uh

just use your imagination try to find

some patterns try to look into data and

generate something that belongs to to

you and uh many categorical damis

uh for today's um um data set we will

generate dam is for months uh for if

it's a January February so it's it's not

year and months if it's a

January

2020 um because uh it's it's not a very

useful feature we just want to

understand whether there is a spike on a

specific month on January February and

we want to model that so we generate one

feature for each month one feature for

each weekday then um um ticker we have

33 tickers and I have a question mark

because I'm not sure that we we need to

have this diis and

um uh you can check it um the there

there is a tradeoff so if you add 33

features uh for each of the tickers you

will have more flexibility for models

and more um parameters so you you can

model the individual effect of um each

stock but um the other idea is that your

model can be too specific to to to a

market it can over predict um and if you

decide to use your model for the a newly

listed stock which is not among those 33

ticket you won't be able to do that

because your model never saw that stock

so that's a question if you need to have

it uh but I included this in in in our

current data set then next is a ticker

type um it's a Indian stock European

stock or US Stock I think it's a

different markets and it's um necessary

to separate them there um some key

assumptions um SL considerations for the

data um especially if you studed

statistics and ecometrics often times

um um people assume that observations

are

independent and identically distributed

which is a certainly a simplification

because we have a dependency between

tiers so it can be close on business

companies and between time so two

different records uh yesterday and today

and uh one week ago may be very

dependent but we treat it um as

independent um if you run um statistical

methods like linear regression it's not

that important if you go for a neural

network or if you have many more uh

features uh many more parameters to to

estimate estimate um but um we need to

think about

potential um assumptions and biases that

we might have in the data and also we we

assume that our our data consists from

the um Atomic data types um and what I

mean by saying Atomic that is only

numerical integers and flow types and um

nothing else for example um why do I

need to include 10 different features um

of growth one day ago or 5 day ago uh or

10 days ago can I include just one array

of um 30 latest um growth rates as one

feature um and create some model that

will unpack this this array or do some

estimation with it um it's called nested

features there are models and approaches

we just do not cover it here or if you

do some uh new modeling

um approaches like graph neural networks

um or ltcm or recurrent neural networks

um you may need to have a different data

organization and this may be not

enough okay now let's let's create um

categorical variables and um before I go

uh to to the code snippet I want to

highlight um that before um having

damis we had 184 numerical

features and uh it uh all features they

they were of type float or integer and

the whole data frame um which consists

about um

182 um, trackers it it um it had 200

megabytes of of

memory then if we generate um additional

damis and that is

um

approximately 60 dummies um 12 on months

uh six or seven on weekdays or five on

week days because trading is on on um

five week days um and 33 for each of the

um stocks and three for the tier

types um we will need to uh do some

preparations um if we want to use

standard methods um which is called uh

pt. getor damis so we will need to

convert months and weekday and other

features to string so that uh that

method could understand um that there

there are a few cohorts um of a variable

so it can split it to 10 um variables or

20 or 30

variables okay let's look at the Cod

snippet number one

so everything is already shared with you

you can uh upload it uh to your local

computer or open with the collab and

follow with with

me so dam is um there are just four

categorical

variables and um I convert two of them

to stream

um then I use one um one call pt.

damis um and

um submit those categorical variables

into that function um so that it

produces many dummy features and by

default it it will produce boan features

which is not ideal for for us because

it's true or false we want everything to

be in numeric value that's why I

specified gtype equals to integer 32 and

that's uh what what you will see um in

in the data frame that's the original

column name month and underscore April

August December so it will automatically

understand what what the values for that

feat for that feature and generate 12

additional columns um with the zeros or

ones um from every single record same

thing for weekday from zero to to six

and same for tickers and ticker

types that's how we get dami variables

and then um we extend our numerical

features with the dami names this is Dam

dami's list and we also concatenate uh

two data frames original data frame with

uh new data frame with damis uh just to

have everything in in one data frame and

that's how we have TF uh with damis with

209 39

entries let's move

on uh next thing um is a correlation

analysis um that's uh some of you may

say that it's um not very

insightful it's can change considerably

in terms of features importance um

dependent on the model you use but I

still believe that it should be uh your

first step um in understanding U data

relations for example here we have um

two uh columns I truncated uh the um

columns and I showed only most

negatively correlated and most

positively correlated features um so as

you can see from here most negatively

correlated features are

mcro uh dgs 10 it's a 10s t u Bond uh

rate um this is GDP potential Year bye

and quarter on quarter growth Brands

growth um oil oil growth in 90 days and

but the thing is that um the absolute

number is not very close uh to minus one

or to plus one so it's actually quite

close to zero so you can guess that

individually these features are not very

powerful um that's a good and a bad sign

uh good sign is that um you need to

create some um really intelligent uh

model or algorithm to combine those

features in in some way so that they can

predict better together

and bad thing is that

uh I think that most of

the um easy ways are for for trading

investing are are not working well

nowadays and they could be beaten with a

statistical and machine learning models

and that's why we are doing all of that

from the um most positively uh

correlated features you can see that the

um month October um is uh positively

correlated and maybe in in October um

everyone starts to invest more it's

close to the end of the year and there

is a more more activity and more growth

happening if this is a well-known fact

let's have it in a separate feature and

also um growth

BTC 7 and 30 days are included here um

what is interesting that if you compare

it with growth future five days which is

a

correlation um not with a variable that

is uh that has only two values zero and

one but with a

um continuous variable over growth um

growth can be

8.9 or one or

1.1 um so the the numbers the the

features are completely different and um

and the Order of features is is

different you can see here that two most

correlated features are growth um 3 days

ago and 7 days ago and here you see some

technical indicators features and only

one micro variable um but um most uh

positively correlated features are two

more macro variables and one technical

indicators what I also want to highlight

here that you should um try to think

about um getting more features all the

time so maybe we are missing something

maybe it is

easy to to get an additional micro

factor or um another data type um asset

type or some technical indicators and uh

I included one citation from from

meetrics uh courses there is a term

which called emitted variable bias

actually statisticians andrians they

research this fact and they said that if

there is something uh relevant and

important and you don't include this uh

into to the uh set of uh features you

may have or you almost definitely have

some bias in in estimates and um in

confidence intervals um like basically

in the results of of your

model but um of course uh it's not

realistic uh to to think that you know

everything and you can Source easily

everything so

we live with some model of the world and

we we have uh uh everything that we can

get but not more than that next idea and

this idea is um quite familiar to

um um many machine learning

practitioners uh is that you you need to

split your data set into three subsets

and what is different

um in um in this exercise with time

series data is um that you can't use

Shuffle you can't uh split randomly your

data um because you will see data

leakage and because model if um you

include something which happened just

recently um from your test data set you

include in the train data set model will

quickly learn uh this um

dependency and it will try to find that

pattern from the future to make

predictions so um as you could guess it

it leads to to wrong predictions and if

you try to use that model for your out

of sample for the your newest data you

won't receive good good results that's

why I suggest you to use um temporal

split and the idea is simple you take 70

80% of of the data and here I mean um

same um time cut for every single stock

um from our 33 stocks um data set uh not

all stocks uh were listed before 2000

and some of them are listed um just 5

years ago or 10 years ago or 15 years

ago um that's um not the Great it's the

greatest sign for us but still I suggest

that we select some um thresholds based

on the overall time period um so I

normally take a minimum date and maximum

date and uh get um 70 80%

threshold um between train and

validation data and um add another 10

15% between validation and test data um

so this is only Nvidia stock um graph

but you you can do it for every single

uh stock in your data frame and you use

all data available in a training data

set to train your model whatever model

you have then you use a few yes um from

a validation set

to um find the best hyperparameters of a

model so if even if if a model um is of

a specific class like a binary decision

tree or a logistic regression or ar Rema

it it um has parameters or

hyperparameters sometimes uh for a

neural network uh these U parameters can

be number of hidden layers and number of

neurons in in each layer and that's why

uh you you train each time um a model on

a train data set then you use

validation uh data set to find the

optimal hyper parameters um combination

and then um you come up with the best uh

model that that you have of that

particular class and of specified hyper

parameters and use that that model on a

test data set so that um

the the model uh during the training and

validation phase it never saw that that

data and um you can pretend that you you

are submitting um new data to to the

model you see how it predicts but you

can compare with the future results

because you know for this historical

data set what happened in the future and

you can actually say what is a good

model what is

not um one good

idea um to to do finally with with the

data set is to check the distribution

the distributions of the features that

you want to predict or uh distributions

of uh the most important features that

you found in the correlation analysis

and what you want to find there is that

um visual distrib utions for train

validation and test sets are

approximately the

same the the idea is that um you train

the model on some historical data and to

capture some patterns but if there is

some structural shift or markets are

totally different um that's um never

happened before or some pattern that was

never seen before or we we have bit coin

appeared 10 years ago and um previous uh

train data set didn't have it um the

distribution of a test set and your

latest um data will be different either

on uh on the things that you want to

predict or on the um features um that

that you have as U that you used to

predict and you try to to balance them

you try to have uh them um of a similar

distribution so maybe for us if if we

see a big disbalance in in the in the

features we will have not 25 years but

20 years or 10 years of data and uh less

data can be better for um capturing new

patterns but uh it's uh worse to to

train um models in a quality way so

there is always a

tradeoff and for for this chart we see

that left chart train validation and

test set it's approximately um

distributed around one so that uh growth

in in five days um normally it it

doesn't go far away from from your

previous um um value uh that's uh that's

a value one but um

it's it looks like a bell um curve

bell-shaped uh distribution and Visually

it is it is similar it just train train

data set has has more data than

validation and test data set and on the

next slide we we can actually um compare

um more precisely these

um um distributions and on the right

hand side uh chart

uh we check the distribution of e

Positive Growth 5 day and um here for U

for

NVIDIA um there there is some um

distribution problem for a train data

set it was 46% of cases when the stock

was not growing and

53.7 cases when the stock was growing

just uh first um 20 years of the data

but then in the validation set which is

probably between 205 and

2020 the number of points when uh the

the stock was growing um increased to

63% so it is some

difference uh what is good that um now

it's it's lower so it's 56% it's closer

to the train data set and I don't see a

big problem here and actually if you

include more uh observations for other

stocks uh this uh distribution will be

different and here I umum

also um included um one additional way

of um comparing um graph

distributions um especially if you are

uh running a regression and you want to

to predict not the binary variable Z or

one but you want to predict a specific

growth or decline whether it was 5% 10%

or minus 5% and you are actually very

cautious about this

distributions because um if a test set

never saw um the uh growth um lower uh

than 6 or higher than

1.4 it it oh actually it's a test set

that the train set was much wider uh but

um it it can be a reverse picture as

well so that's train data set never saw

um the cases when stock um was growing

quickly and it it will never predict at

the test set that uh the high growth um

numbers and um one additional thing that

um you may want to to do here is to

compare this U Bar Bar plots uh so this

is uh 25 50 and

75% um quantiles um just visually

presented uh at the graph if you look

visually and the distributions look very

similar um they are all Bell sh bell

shaped uh they are all a um of same

width and of a same um um shape but um

there are a different number of outliers

and you can see it from from these

numbers and from um maximum and minimum

um stats here so you might have an idea

that maybe you want to remove one 2% of

outliers completely and your uh

estimation for uh regression will be

more robust um but it may not predict uh

exact uh numbers um for a for a big

growth or decline dayses which you're

fine with it's hard to predict but on

all other cases it will be more

robust so that's that's the idea now

let's um start uh doing some more daing

exercises and first uh we will talk

about hand prediction rules um that's a

very similar idea with what we had

previously in home homeworks uh simple

uh strategies um next will it will be

ARA statistical model and finally it

will be one binary model decision three

I won't cover today logistic uh

regression which is another binary model

or ordinary regression which is a

numeric model random Force neural

network or even emble learning but but I

will prepare you uh if you have um this

this data filled in the data frame it's

quite easy um to expand uh that data

frame with a slightly more predictions

and um combine those predictions

together um which is called Ensemble um

learning approach to create a even

better prediction so first uh and

probably the most important concept ual

uh slides today um if we think um about

manual predictions or or naive

predictions or puristic how we can

generate those predictions to

um to the to the data frame and um we

will look um at um Cod snippet number

three in a few minutes but before that

I'll explain you what are we going to do

here first um we have a big um data

frame that has everything um numerical

features categorical features some other

artifacts and we will add um one column

for um each new prediction and these

columns will have the same prefix it

will start from PR and PR zero PR one PR

two um and we will add some details

about the type of the prediction first

PR zero manual

CCI same idea that we had CCI more than

200 how we predict this we do one line

of code and we add this um prediction to

the data frame um then

um I want to add um one thing that you

want want to keep in uh mind is how many

features did you use uh for the

prediction this is the first thing and

second thing whe whether you used any

parameters to to estimate your your best

um decision rule so here um we use a

fixed decisions rules uh so it's it's

all TCI more than 200 or growth more

than zero but maybe CCI should be more

than 300 100 and grow should be more

than

um

0.5 so

um that's what I call parameters and

that's what

you may need to study to improve your

prediction rule um but um when you when

when you're done with with these uh

predictions you will have uh three

prediction columns

so prediction zero is CCI more than 200

we saw this uh it's a rare event not

many times it happens and most of the

times it will predict zero then another

prediction growth one day is more than

more than zero actually it should be

more more than one here because uh uh we

have a distribution of growth um around

one I'll check in the code that um it's

it's not a mistake um the idea is that

we just um look at the latest available

um one period growth so growth um

adjusted close today versus adjusted

close yesterday and if it was growing

today uh then it it it will be growing

um for the next 5 days which is a

simplification of course um next idea is

that you may add some additional

um conditions and you may may need to

use more features here let's assume that

you include growth one day uh is more

than one and growth of Benchmark SNP is

more than more than one so here it's

more than 0% uh what what I meant here

and that's how you you produce uh this

uh prediction number one and prediction

number two um I included all original

values uh um that that are used uh for

the prediction CCI growth one day and

growth S&P 500 uh to the data

frame and um I can see here that the

code is probably correct because

prediction one uh on uh growth one day

is zero when growth one day is less than

one and one when growth one day is more

than one so the code is

correct um and we have several

predictions here and then we have a a

real um value that um we want to compare

with and uh here um

actually we we care only uh about

positive predictions it it is another

simplification that it's much easier to

do long um strategy or invest in in

growth so we want to predict growth and

we look look only at the positive

predictions when predictions are equals

to one and here we have one observations

when predictions um were one but actual

growth was

negative uh and this is called false

positive so that's we we predicted to be

positive but it's it's false and then um

another um line actually both

predictions uh they um predicted one

and that it will be a positive growth

and this Positive Growth uh

happened what you can think about here

is that prediction one and prediction

two they are um very similar and
prediction two is actually more strict
so it says that um I want to um focus um
on only on those days where my growth
was positive for for the ticker but also
the growth of overall Market was
positive so it it
will predict one on the same predictions
for prediction one but sometimes it will
predict zero when growth um for the
market was negative so it can be good it
can be a bad sign we don't
know and next um thing is that's um
we want to evaluate somehow um the the
quality of the predictions and if we
work with the binary predictions and we
want to to have
um um predictions whether the the stock
will grow that is one or whether it is
not it won't grow it is
zero um we can calculate the metric
which is called precision and this is

unusual for binary models uh

um often uh when um when you do some

educational binary

predictions uh those uh models are are

um selected uh by looking at the

accuracy metric which uh treats not only
correct predictions but also um not only

uh correctly predictive positive

predictions but also correctly predicted

negative predictions here we say let us
have less predictions uh but we want it

to
be um more precise that's why we divide
true positives on true positives plus
false positives on all predictions that

that we we predicted to be
positive and for for the first case uh

you can see that there were only maybe

about 800 positive predictions

um and 500 450 of them were truly

positive and 344 were negative so it's

it's about 5 6.9% were positive it's not
much more than 50% so here in time
serious prediction for uh Finance uh

stats you won't expect 70 80 or 90%

Precision um or accuracy as you can see
some times in in many other problems uh
these numbers are already a good start
whether it is it is a good enough uh
thing for us uh whether it it can drive
us um to to earn some money and to have

um profitable strategy um we don't know

yet we will know um on the next

lecture um so the the next uh prediction

is manual

prediction just on growth one day ago

and this time it's it predicts um 14 or

15,000 U times positive uh uh Positive

Growth uh predictions out of 30k test

data points approximately 50% times and

um the Precision is is quite

close uh still every single percent may

be very important for for the

profitability of your strategy and we

will try to leave um those models which

are we which have higher Precision so

this one is 0

55 and the next one um the strict uh

prediction uh about growth one day and

S&P growth one day it it has um less um

data 10K data predicted but the

prediction accuracy so our rule is

probably not working for us in terms of

it's not increasing the Precision we we

will have only 40
54.7% of um accurate uh or or correct uh

positive
predictions um there are a few things to

think about if if you do these manual

predictions first in what is the best

model and and here the can the first

candidate is um CCI model but um you

never know because um it uh happens not
very often only 800 predictions um over

over the last four four years I think

test test data 15% out of 25 yes it's

it's just last four years and if you

calculate the um money that you can earn

with these uh few trades um it can be

less or it can be more um than the other
model the main idea is that yes we are
selecting um models by the by some

Metric by some machine learning metric

uh Precision accuracy or root mean

square a or anything

else um but this is not uh the the end

rule for us and the end result and we
need to come with something more

complicated um so it's it's not enough

to have only uh one quality metric next

um uh is um next idea is why don't we
introduce uh some parameter to estimate

our to to improve to improve our our

rules for example we we can um have a

rule CCI more than x and um we can

select this value of x between 200 and

400 and find some precise value of 250

or 300 exactly in the same way that we

we were trying to do in uh in the

homework with

um

um with the number of days to invest uh

after IPO here we int introduce some

degree of Freedom we introduce a

parameter um and if if you worked with

the machine learning models it's um

exactly a decision Tre with one node if

you have only one feature CCI so that's

that's what um what we have uh

here um another idea why why do we have

uh growth 1 3 5 7 30 and 90 maybe we

need to include growth 45 days or 15

days

so um you you need to experiment usually

markets uh don't have that long memory

but it depends if you want to predict

growth for one day one week or one year

the memory for these predictions uh will

be completely

different um then um now we we also need

to think about what strategies um of of

trading we we might have do we want to

invest only in in growth in like in a

long position that we predict that

something will grow We Buy It Now and

sell later and it grows or we can

actually trade on uh short positions

when we predict that it will um go down

and we can make money from from that

strend and uh last but not least is um

you also want to think

about the distribution of positive

predictions uh let's assume that we we

had um some period of U uh of growth uh

and this period actually happened just

recently in 2020 202 1 just after or

during covid and our models can show

very happily that um um we predict a lot

of growth but these these predictions

are concentrated only on on that period

that means that

um yes um you you could trade there when

everything was growing but what about

now if if you have a market that is not

moving anywhere where you you still want

to to have some ideas where to

invest and now okay I forgot to to

switch uh to the

um to the code snippet number three

because this is an important

snippet um I think correlation analysis

C snippet number two is just two lines

of code is it's quite simple you can

read it by yourself and now C Cod

snippet

number um number three and it's combined

with

the okay it seems to be a

around

um around numbers here it should be

uh okay I have two Cod snippit number

three in the in collab um here are

manual handroll predictions

um first uh why does it work um if

you

um if you have this expression _ DF

docci it will return you a serious of

values and if you have uh some simple

expression like more than 200 it will do

um value after a value comparison uh

with 200 and it will generate a column

or a vector of uh true and false um

values so that's why

um it it works when when you define

these new columns using this Vector

operation

um so this is prediction number zero we

generate um this this column of uh true

and false numbers and we convert this uh

these um string values or bulling values

to integer so that false is zero and uh

one is um

true uh same idea is uh for a new DF do

growth one day is more than one um and

same idea with

um uh and with combining two conditions

so that we want uh to to be uh to to

have

um first condition to be true and second

condition to be true in order to to have

the resulting uh condition to to be true

and we convert it to to zero and one

that's how we generate uh this this

predictions next uh thing I Define a new

feature uh set which is called

predictions and I have everything that

we ever have um during our uh work here

uh I I'll have it uh um in a prediction

um feature set so for now it is just
three
predictions and I also generate um
a column which is um which tells me

whether the prediction is correct or not

so I look into all columns um that that

they have for now or or later so the the
function is is exactly the same and I

compare the the prediction we just need

to to know whether it's a binary

prediction or um uh numerical prediction

so whether you compare with the Positive

Growth 5 days which is a binary variable

or with a growth five future growth uh 5

days which is a numerical variable uh
for now it's it's simple we have only
binary predictions and we compare
prediction with um actual value and
that's how we have one if it's true if

it's a true positive it's if it's a

right uh prediction and uh zero if it's

a wrong prediction if it's a false uh

positive or false negative

and and that's how I calculated these
these numbers on on the
Precision um when I have these uh
columns uh generated is underscore
correct prediction zero or isore

corrector prediction one or prediction

two you can quickly see the the quality

of of the uh Matrix um just with a one

Loop

we have just a few more slides but they

are becoming more complicated I won't
spend much time on on this um and I

won't go into the details of c snippit

number four what I wanted to highlight

here that if you studied uh statistics

or animetrics

um it's a it's a great knowledge and

please try to to use it please try to

have it in in your prediction and to

compare versus and hand rules and versus
uh well-known machine learning

predictions like a neural network what

happens here is that we have 20 years of

um of data history and the idea of a ara

model or Auto regressive integrated

moving average model is that it doesn't

look at at any any features it looks

only at the previous value

of Time series and here um values are um

adjusted close price so we have a train

plus validation data set for 20 years

and this is a green line I just tranced

it um and then at some point uh

we found the best combination or best

hyperparameters for this model p q and R

and I know that uh P equals to 6 it it

actually means that this model will look

only at uh six previous values of of the

time

series and it will try to estimate a

perfect uh combin perfect parameters or

ideal parameters that minimize the the

error um the prediction error uh for for

that um time serus at that moment of

time that's that's why we try to to we

start to predict um on the first day of

a test data and that's why uh you you

have uh some Gap uh it's because um I

predict on one period ahead two periods

three four and five periods we want to

know whether a

future um stock price will be positive

or negative and uh future in in this

context uh because our uh um variable

that we compare with is called future

growth five days we need to make five

five predictions and uh for these

statistical model it's not very good

because further you go away from the

current prediction and here I have

um red uh real stock and um blue

predicted stock which seems to be very

close but um if you think about small

fluctuations of uh grow growing up or

down like 1 2 3 5% even these um clo

visually closed graphs uh can provide

very different accuracy uh what else did

they found that this method it's

actually it's um it's very slow and um I

I ran only 500 out of 900 uh points for

one stock not all 33 stock dos and it
took me almost 1 and a half
hours and It produced um suspiciously
High
Precision um of

88% so if any of you uh did this before

probably I made a mistake somewhere um

please let me know where the mistake is

but the general sentiment about this

model and when it is usually used uh

still widely used uh is when when you

have some generic time series like

interest rates or you have a financial

planning over sales something that you

don't know um what are the factors that

actually uh influence uh this or that

variable and you want to build a

shortterm generic model for us it it may

be enough if if uh we we try to predict

what five five days ahead and we are

fine with uh retraining the model every

single day and that's why it is slow so

retrain uh for this model it it takes
only 10 10 seconds but if you go into
neural network retrain can be 1 hour or
one day depending on the size of the

network and size of the data so you

can't afford it for for Pik

models but um my point is that um yes um

these um these classic uh statistical
models uh and hand rules and ml models

they they should all compete with each

other and you should select the best uh

from it and ideally try all of that and

now um what what we have here um this is

a binary model or decision which is

called a decision tree and this is why

we we buil uh these big data set which

uh consists of 200 features um

previously in all our hand rules and

manual predictions and ARA model we

didn't use most of the features this
time we are starting to use all of them

and the the idea with a decision for for

a decision three is is quite similar to

to what we had you can read about in in

textbooks but um let's let's assume uh

that we we don't know what um uh

features are um are the best we we know

that there are 200 features and it just

some of them are correlated more or less

but which features uh needs to be

selected we don't know and um let's ask

model to Define this these features uh

and uh the model will try to to have a
serious of of uh
simple uh rules or or
experiments um to to make a final

decision about investment so we still

have um as an input of for that model we

we have one record with 200 numerical

features and one feature that we want to
predict um let's assume that we fixed um
hyper parameter for that model it can be
10 or 15 or five or 20 and it it's up to

you to select

and actually it it will be your home

assignment to to find a better tree
model um and for for for this uh
experiment we we have a tree with 10 um

um 10 layers that means that um this
tree uh won't have more than 10 features

used we used previously for hand rules

one feature or two features this time we

will have 10 features and not just 10

features that we know but 10 features um

that make um overall predictions um

accurate enough or optimal in some way

so you can you can read how decision
trees um are working and estimated um
but here is the result and and there is
a

visualization that uh if we if we have

some some record that we want to predict

and uh the decision three actually um

says to us that look first at the GDP

potential us year-over-year growth and

if it is less than 2.7 go to the left
sub three and if it is um more than 2.7

go the right sub three it's quite

natural because there are two macro

regimes of growth for the US economy if

it's less than 2.5 or 3% it's close

close to recession if it's more than

2.5% it's close to growth so it it

actually confirms well known economic

facts and this is a good sign that you

can explain and that's another thing

that you you should try to explain

things that you see and don't treat any

model as a black box and this is

extremely important for uh for financial

time

series then uh um we we checked the

first feature and move to the left to

the right sub tree um dependent on the

subtree that we are in on the left sub

tree it will check fast D feature if

it's um it's it's a technical indicator

if it's less than 0 25 again it it's

already showing some optimal parameter

you might not know about it if you are

in the right sub tree uh it will look at

the um oil growth in the last 30 days uh

if it's uh

less than .5% of
growth um then you go into the left sub
three if it's more than .5% growth you

go to the right sub tree um I don't

remember actually what is a fast d uh

technical indicator but for the oil

growth again it's um it's it can be

explained perfectly um oil is a is
another big um asset um for Investments
and if oil is

growing maybe Traders investors um can

switch their demand to to Commodities to
to
oil
to uh these types of assets uh so that's
why it tries to to separate uh with with
the condition um and um separate in such

a way that um the

um the division between left sub three

and right sub three is is more

pure um so you can read about the Purity

or gen coefficient but that's how it

selects the the the optimal parameter

for estimation at the level number four

we have four different options and uh we

have uh growth of Brent oil of gold of

do Jones in IND and month September we

used to have um months October in the

correlated uh features in the most

correlated features but for this

particular model which treats all

features together uh we have month

September as a as an important parameter

so if you think about this model uh it's

it is lineer on on parameters so you can

think about like see simple model if if

there is a nonlinear uh combination or

dependency it it won't predict perfectly

but it will predict something uh and

parameters that that um are estimated uh

when when

you fix uh when you fix number of um

levels it's it's more than one two

parameters but it's less than thousands

parameters um in in order to to do this

exercise I actually had to do um two

more steps on data cleaning because I

generated variable logarithm of of

volume um it equals to minus infinity

when volume is zero and uh I had to find

all those cases when it is minus
infinity or plus infinity and replace

that with zero and another thing which

was not visible straight away in the D

said that I need to do something with

the missing values with NS and um first

uh thing to do and first
um normally uh analyst they they they
just try to drop that that um that data

but uh we have uh features of Bitcoin

growth included and that means that uh

we we can drop half of the data before

2010 just because one feature is not

defined so I replaced all those features

with with zeros even if it has some

coefficient estimated if you multiply

that coefficient on zero it normally

means to zero it it equals to zero

that's

uh uh it's it's it's a different

strategy for for non repacement but I I

still have the same uh number of

observations I don't lose the data and

this is a good

sign um so we talked about visual

representation and one more slide and

we'll check um the the

code one thing uh which is often times

um forgotten um when we talk about

machine learning models is

explainability and and um explainability

is very developed for statistical models
with confidence intervals with
the um goodness of feed for for the
models with
um many other um things or methods uh to
to look at um you can find some
explainability uh in most other models
as well for example if it is a linear
regression or a neural network you can
calculate gradients or there is a module
called shly or in this case um actually

the the model um from the library Cy

learn the decision three it already

provides you with the with the features

importance and um you can see here that

first uh if you compare with our uh

previous um hand rules the Precision is

slightly better it is 56.5 and 57%

versus 54 55 and 56% so this is a good

sign that we used more features and we

used in in a smart way that we are not

overfitting we have a better model um

but uh these these models are quite

close to each other but the features

importance is somewhat different the

first model which has only 10 layers it

it is um like a macro model it it

doesn't look at at the Historical growth

of a stock or a technical indicators of

a stock it says I can predict relatively

well um just by looking at the macro

conditions and the inflation growth do

Jones interest rates gold oil

uh growth

SNP um and GDP growth and the right

model with slightly higher Precision

it's uh says that no actually let's um

let's look not only at the mcro

parameters at Gold Growth Oil growth
with different

um uh time periods the 365 days versus

30 days but also let's check technical

indicators net obv ad and tricks and um

previous growth in in 90 days um it's

slightly surprising that growth one two

three five um seven days ago is is not

uh among the most important features but

this is another way of understanding of

um the whole market so now we know that

maybe we want to include more mcro

variables maybe we want to look into

other factors that influence oil gold

May or like maybe we want to include

silver here so that uh brings us to to

the idea of how we can Source more more

data and if uh we check the code we are

slightly over time and it will be a

brief um explanation for the for the

last piece of code

okay it's a few lines of of code first

um I I have features list um I know what

I want to predict I

generate um train data frame or actually

it's a train and validation data frame

and you will be asked to split it back

into train and validation and find the

best hyperparameters for a for a model

three and a test test data frame and

then

I um have only features

um uh data frames xcore train and xcore

test wide known um abbreviations so we

use uh exactly the same ones um I do The

Replacements of infinite uh infinite

values and feel n so that uh we we don't

have any problems with the data I have

here remove outliers um but I decided

that I won't go for a binary prediction

um for removing outliers it's more for

regression

models and when I have
um X train and X test and uh y train and
Y test it's um what should be what
should we see um in train and test stats
I do the estimation use psychic learn
Library one line of codes I specify
maximum depth which is a hyper parameter
it can be 5 10 or 20 um and it works

relatively quickly one minutes but it's
longer than 10 seconds and you can do
these estimations for 30,000 of
observations uh so we need to estimate

to find some model fix that model and

use for all predictions in the nearest

Future and maybe

reestimate periodically once in a month

once in a quarter and that's why we um
split this uh so we have inference in a
decision three we already have a
classifier and we provide some data
frame and True Values uh that we want to
to see and that's show to me um the uh
accuracy and precision 57% for 20 um
levels uh three and 56.5% for 10 levels
three okay uh so just to recap what
we've learned today uh we finalized the
unified data set we did a bit of um data
Transformations um we defined uh feature
uh feature sets we generated more
dummies
we created a temporal split which is a
specific column in our data frame and it
says whether this observation belongs to
a train data set validation or a test
data set we talked about um binary hand
rules or naive
predictions um then we briefly looked at
the statistical model ARA there are many
more statistical time serious models um
and we discuss decision trees out of
scope for today uh random Forest
logistic regression orinary regression
and neural network so first three they
are very easy to adjust to what we see
here maybe one two three lines of code
you can read about it in psychic learn
perfect Library feel free to try it
neural network is slightly more
complicated um you can do it in that
flow for example um you you can have
many more parameters so and you can have
a nonlinear estimation that means that
the model is uh more complex and it has
more degrees of freedom if it is
properly trained uh this neural network
can cover all previous examples that
that uh that we had so that's that's why
you might want to have it in your
project um maybe just a simple um simple
neural network included to compare
against all other
models 
