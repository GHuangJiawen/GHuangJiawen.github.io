---
layout: notebook
title: "Research Project"
permalink: /research-project/
showcase: true
tools: ["Python"]
date: 2025-05-04
description: >
  This is a research project.
---









## 
 Escaping Slavery: A Quantitative Study of Age, Gender, and
 Regional Trends from the Freedom on the Move Database[¶](#Escaping-Slavery:-A-Quantitative-Study-of-Age,-Gender,-and-Regional-Trends-from-the-Freedom-on-the-Move-Database)












***Jiawen Huang***


**Research Project (CU Denver spring 2025)**













> 
> 
> *Note: Generative AI was used to help generate some of the
>  code in this project.*
> 
> 
> 
> 













![Description of image](../assets/img/jefferson.jpg)

 The Freedom on the Move
 












[View the original dataset](https://database.freedomonthemove.org/)













### 
 Introduction[¶](#Introduction)



 In the first half of the 19th century, the slavery system in the
 United States continued to develop with the expansion of its
 territory, and the contradiction between the North and the South
 regarding slavery also intensified increasingly. Against this
 historical backdrop, a large number of enslaved African
 Americans chose to seek freedom by runaway (becoming "fugitive
 slaves"), but the scale and characteristics of these escape
 events lack detailed personal records, and it has been difficult
 to conduct quantitative research on the demographic
 characteristics of the fugitive slave group in history. The
 Freedom on the Move (FOTM) project led by Cornell University has
 created a comprehensive database of fugitive slave
 advertisements in North America, gathering tens of thousands of
 fugitive slave notices from American newspapers and periodicals
 in the 19th century. These advertisements were usually published
 by slave owners, detailing the personal information of the
 escapees such as their names, genders, ages, and physical
 features. FOTM data provides valuable information for studying
 the struggles of the enslaved during the slavery period,
 enabling us to systematically examine the scale and patterns of
 the phenomenon of runaway slavery from a data perspective. Some
 existing studies have also explored similar directions. For
 example, Shaun Wallace (2017), by analyzing over 5,000
 advertisements for runaway slaves in Georgia and Maryland
 between 1790 and 1810, revealed the connection between the
 gender, age, literacy ability and rebellious behavior of runaway
 slaves, emphasizing that these advertisement texts not only
 recorded the runaway events, It also retains the details and
 subjectivity of the struggles of the enslaved. Other studies
 have focused more on the analysis of the advertisement itself,
 while this study focuses on extensive statistics. Based on the
 text data of the FOTM database, it analyzes the basic
 demographic patterns and changes of the fugitive slaves in the
 United States in the 19th century. In other words, we attempt to
 answer the following several specific questions through data:
 


1. 
 Gender composition: What are the proportions of men and women
 in the group of runaway slaves?
2. 
 Age distribution: What is the age distribution of the runaway
 slaves? Are there any significant differences in the age
 structure between male and female runaway slaves?
3. 
 Geographical distribution: Which states or regions did these
 runaway slaves mainly flee from? Is there a regional
 concentration phenomenon?
4. 
 Gender Influence of Slave Owners: Are there differences in the
 frequency of slave escapes experienced by slave owners of
 different genders and the gender composition of escapees?
5. 
 Time Trend: How does the number of runaway slaves recorded
 each year change? Do these annual changes coincide with the
 major historical events during the expansion of slavery and
 the intensification of the conflict between the North and the
 South?



 Through the statistical and visual analysis of these variables,
 this project attempts to answer the following core question:
 Against the historical background of the expansion of slavery
 and the intensification of North-South contradictions, what
 structural characteristics do the gender, age and geographical
 distribution of the group of runaway slaves present? How did
 these characteristics interact with the gender of the slave
 owners, institutional pressure and historical events?
 










In [52]:




```
import pandas as pd
import plotly.io as pio
import plotly.offline as pyo
pio.renderers.default = "jupyterlab"
pyo.init\_notebook\_mode(connected=True)

file\_path = 'C:/Users/GAVIN/Desktop/research-project/data/original/FOTM-Dataset-Full-Flattened.csv' 
df\_1 = pd.read\_csv(file\_path, low\_memory=False)
pd.set\_option('display.max\_columns', None)  
pd.set\_option('display.expand\_frame\_repr', False)  

df\_1.head() 

```













 window.PlotlyConfig = { MathJaxConfig: "local" };
 if (
 window.MathJax &&
 window.MathJax.Hub &&
 window.MathJax.Hub.Config
 ) {
 window.MathJax.Hub.Config({ SVG: { font: "STIX-Web" } });
 }
 if (typeof require !== "undefined") {
 require.undef("plotly");
 requirejs.config({
 paths: {
 plotly: ["https://cdn.plot.ly/plotly-2.35.2.min"],
 },
 });
 require(["plotly"], function (Plotly) {
 window.\_Plotly = Plotly;
 });
 }
 



Out[52]:



 .dataframe tbody tr th:only-of-type {
 vertical-align: middle;
 }

 .dataframe tbody tr th {
 vertical-align: top;
 }

 .dataframe thead th {
 text-align: right;
 }
 


|  | runaway\_id | enslaved\_person\_id | enslaved\_person\_name\_id 1 | enslaved\_person\_name\_fullname 1 | enslaved\_person\_name\_is\_alias 1 | enslaved\_person\_name\_id 2 | enslaved\_person\_name\_fullname 2 | enslaved\_person\_name\_is\_alias 2 | enslaved\_person\_name\_id 3 | enslaved\_person\_name\_fullname 3 | enslaved\_person\_name\_is\_alias 3 | enslaved\_person\_name\_id 4 | enslaved\_person\_name\_fullname 4 | enslaved\_person\_name\_is\_alias 4 | enslaved\_person\_name\_id 5 | enslaved\_person\_name\_fullname 5 | enslaved\_person\_name\_is\_alias 5 | enslaved\_person\_name\_id 6 | enslaved\_person\_name\_fullname 6 | enslaved\_person\_name\_is\_alias 6 | enslaved\_person\_name\_id 7 | enslaved\_person\_name\_fullname 7 | enslaved\_person\_name\_is\_alias 7 | enslaved\_person\_name\_id 8 | enslaved\_person\_name\_fullname 8 | enslaved\_person\_name\_is\_alias 8 | enslaved\_person\_name\_id 9 | enslaved\_person\_name\_fullname 9 | enslaved\_person\_name\_is\_alias 9 | enslaved\_person\_name\_id 10 | enslaved\_person\_name\_fullname 10 | enslaved\_person\_name\_is\_alias 10 | enslaved\_person\_name\_id 11 | enslaved\_person\_name\_fullname 11 | enslaved\_person\_name\_is\_alias 11 | enslaved\_person\_name\_id 12 | enslaved\_person\_name\_fullname 12 | enslaved\_person\_name\_is\_alias 12 | enslaved\_person\_name\_id 13 | enslaved\_person\_name\_fullname 13 | enslaved\_person\_name\_is\_alias 13 | enslaved\_person\_name\_id 14 | enslaved\_person\_name\_fullname 14 | enslaved\_person\_name\_is\_alias 14 | enslaved\_person\_name\_id 15 | enslaved\_person\_name\_fullname 15 | enslaved\_person\_name\_is\_alias 15 | enslaved\_person\_name\_id 16 | enslaved\_person\_name\_fullname 16 | enslaved\_person\_name\_is\_alias 16 | enslaved\_person\_name\_id 17 | enslaved\_person\_name\_fullname 17 | enslaved\_person\_name\_is\_alias 17 | enslaved\_person\_name\_id 18 | enslaved\_person\_name\_fullname 18 | enslaved\_person\_name\_is\_alias 18 | enslaved\_person\_name\_id 19 | enslaved\_person\_name\_fullname 19 | enslaved\_person\_name\_is\_alias 19 | enslaved\_person\_name\_id 20 | enslaved\_person\_name\_fullname 20 | enslaved\_person\_name\_is\_alias 20 | enslaved\_person\_name\_id 21 | enslaved\_person\_name\_fullname 21 | enslaved\_person\_name\_is\_alias 21 | enslaved\_person\_name\_id 22 | enslaved\_person\_name\_fullname 22 | enslaved\_person\_name\_is\_alias 22 | enslaved\_person\_name\_id 23 | enslaved\_person\_name\_fullname 23 | enslaved\_person\_name\_is\_alias 23 | enslaved\_person\_name\_id 24 | enslaved\_person\_name\_fullname 24 | enslaved\_person\_name\_is\_alias 24 | enslaved\_person\_name\_id 25 | enslaved\_person\_name\_fullname 25 | enslaved\_person\_name\_is\_alias 25 | enslaved\_person\_name\_id 26 | enslaved\_person\_name\_fullname 26 | enslaved\_person\_name\_is\_alias 26 | gender | literacy | skills | ran\_before | profess\_freedom | racial\_description | ethnic\_description | approximate\_age | min\_age | max\_age | approximate\_height | min\_height | max\_height | approximate\_weight | min\_weight | max\_weight | injuries\_scars | self\_presentation | other\_physical\_descriptions | possessions | runaway\_event\_id | escapee\_count | runaway\_event\_min\_occurred | runaway\_event\_max\_occurred | outside\_involvement | advertisement\_id | advertisement\_transcription | advertisement\_language | publication\_date | page\_number | newspaper\_id | newspaper\_name | newspaper\_location\_name | newspaper\_location\_city | newspaper\_location\_county | newspaper\_location\_state | newspaper\_location\_country | advertiser\_id | advertiser\_type | advertiser\_name | advertiser\_location\_name | advertiser\_location\_city | advertiser\_location\_county | advertiser\_location\_state | advertiser\_location\_country | enslaved\_person\_language\_id 1 | enslaved\_person\_language\_name 1 | enslaved\_person\_language\_does\_speak 1 | enslaved\_person\_language\_id 2 | enslaved\_person\_language\_name 2 | enslaved\_person\_language\_does\_speak 2 | enslaved\_person\_language\_id 3 | enslaved\_person\_language\_name 3 | enslaved\_person\_language\_does\_speak 3 | enslaved\_person\_language\_id 4 | enslaved\_person\_language\_name 4 | enslaved\_person\_language\_does\_speak 4 | enslaved\_person\_language\_id 5 | enslaved\_person\_language\_name 5 | enslaved\_person\_language\_does\_speak 5 | enslaved\_person\_language\_id 6 | enslaved\_person\_language\_name 6 | enslaved\_person\_language\_does\_speak 6 | runaway\_location\_location\_id 1 | runaway\_location\_name 1 | runaway\_location\_city 1 | runaway\_location\_county 1 | runaway\_location\_state 1 | runaway\_location\_country 1 | runaway\_location\_type 1 | runaway\_location\_reason 1 | runaway\_location\_location\_id 2 | runaway\_location\_name 2 | runaway\_location\_city 2 | runaway\_location\_county 2 | runaway\_location\_state 2 | runaway\_location\_country 2 | runaway\_location\_type 2 | runaway\_location\_reason 2 | runaway\_location\_location\_id 3 | runaway\_location\_name 3 | runaway\_location\_city 3 | runaway\_location\_county 3 | runaway\_location\_state 3 | runaway\_location\_country 3 | runaway\_location\_type 3 | runaway\_location\_reason 3 | runaway\_location\_location\_id 4 | runaway\_location\_name 4 | runaway\_location\_city 4 | runaway\_location\_county 4 | runaway\_location\_state 4 | runaway\_location\_country 4 | runaway\_location\_type 4 | runaway\_location\_reason 4 | runaway\_location\_location\_id 5 | runaway\_location\_name 5 | runaway\_location\_city 5 | runaway\_location\_county 5 | runaway\_location\_state 5 | runaway\_location\_country 5 | runaway\_location\_type 5 | runaway\_location\_reason 5 | runaway\_location\_location\_id 6 | runaway\_location\_name 6 | runaway\_location\_city 6 | runaway\_location\_county 6 | runaway\_location\_state 6 | runaway\_location\_country 6 | runaway\_location\_type 6 | runaway\_location\_reason 6 | runaway\_location\_location\_id 7 | runaway\_location\_name 7 | runaway\_location\_city 7 | runaway\_location\_county 7 | runaway\_location\_state 7 | runaway\_location\_country 7 | runaway\_location\_type 7 | runaway\_location\_reason 7 | runaway\_location\_location\_id 8 | runaway\_location\_name 8 | runaway\_location\_city 8 | runaway\_location\_county 8 | runaway\_location\_state 8 | runaway\_location\_country 8 | runaway\_location\_type 8 | runaway\_location\_reason 8 | runaway\_location\_location\_id 9 | runaway\_location\_name 9 | runaway\_location\_city 9 | runaway\_location\_county 9 | runaway\_location\_state 9 | runaway\_location\_country 9 | runaway\_location\_type 9 | runaway\_location\_reason 9 | runaway\_location\_location\_id 10 | runaway\_location\_name 10 | runaway\_location\_city 10 | runaway\_location\_county 10 | runaway\_location\_state 10 | runaway\_location\_country 10 | runaway\_location\_type 10 | runaway\_location\_reason 10 | runaway\_location\_location\_id 11 | runaway\_location\_name 11 | runaway\_location\_city 11 | runaway\_location\_county 11 | runaway\_location\_state 11 | runaway\_location\_country 11 | runaway\_location\_type 11 | runaway\_location\_reason 11 | runaway\_location\_location\_id 12 | runaway\_location\_name 12 | runaway\_location\_city 12 | runaway\_location\_county 12 | runaway\_location\_state 12 | runaway\_location\_country 12 | runaway\_location\_type 12 | runaway\_location\_reason 12 | runaway\_location\_location\_id 13 | runaway\_location\_name 13 | runaway\_location\_city 13 | runaway\_location\_county 13 | runaway\_location\_state 13 | runaway\_location\_country 13 | runaway\_location\_type 13 | runaway\_location\_reason 13 | runaway\_location\_location\_id 14 | runaway\_location\_name 14 | runaway\_location\_city 14 | runaway\_location\_county 14 | runaway\_location\_state 14 | runaway\_location\_country 14 | runaway\_location\_type 14 | runaway\_location\_reason 14 | runaway\_reward\_id 1 | runaway\_reward\_amount 1 | runaway\_reward\_currency 1 | runaway\_reward\_criteria 1 | runaway\_reward\_id 2 | runaway\_reward\_amount 2 | runaway\_reward\_currency 2 | runaway\_reward\_criteria 2 | runaway\_reward\_id 3 | runaway\_reward\_amount 3 | runaway\_reward\_currency 3 | runaway\_reward\_criteria 3 | runaway\_reward\_id 4 | runaway\_reward\_amount 4 | runaway\_reward\_currency 4 | runaway\_reward\_criteria 4 | runaway\_reward\_id 5 | runaway\_reward\_amount 5 | runaway\_reward\_currency 5 | runaway\_reward\_criteria 5 | runaway\_reward\_id 6 | runaway\_reward\_amount 6 | runaway\_reward\_currency 6 | runaway\_reward\_criteria 6 | runaway\_reward\_id 7 | runaway\_reward\_amount 7 | runaway\_reward\_currency 7 | runaway\_reward\_criteria 7 | runaway\_reward\_id 8 | runaway\_reward\_amount 8 | runaway\_reward\_currency 8 | runaway\_reward\_criteria 8 | enslaver\_id 1 | enslaver\_fullname 1 | enslaver\_type 1 | enslaver\_gender 1 | enslaver\_location\_id 1 | enslaver\_location\_name 1 | enslaver\_location\_city 1 | enslaver\_location\_county 1 | enslaver\_location\_state 1 | enslaver\_location\_country 1 | enslaver\_id 2 | enslaver\_fullname 2 | enslaver\_type 2 | enslaver\_gender 2 | enslaver\_location\_id 2 | enslaver\_location\_name 2 | enslaver\_location\_city 2 | enslaver\_location\_county 2 | enslaver\_location\_state 2 | enslaver\_location\_country 2 | enslaver\_id 3 | enslaver\_fullname 3 | enslaver\_type 3 | enslaver\_gender 3 | enslaver\_location\_id 3 | enslaver\_location\_name 3 | enslaver\_location\_city 3 | enslaver\_location\_county 3 | enslaver\_location\_state 3 | enslaver\_location\_country 3 | enslaver\_id 4 | enslaver\_fullname 4 | enslaver\_type 4 | enslaver\_gender 4 | enslaver\_location\_id 4 | enslaver\_location\_name 4 | enslaver\_location\_city 4 | enslaver\_location\_county 4 | enslaver\_location\_state 4 | enslaver\_location\_country 4 | enslaver\_id 5 | enslaver\_fullname 5 | enslaver\_type 5 | enslaver\_gender 5 | enslaver\_location\_id 5 | enslaver\_location\_name 5 | enslaver\_location\_city 5 | enslaver\_location\_county 5 | enslaver\_location\_state 5 | enslaver\_location\_country 5 | enslaver\_id 6 | enslaver\_fullname 6 | enslaver\_type 6 | enslaver\_gender 6 | enslaver\_location\_id 6 | enslaver\_location\_name 6 | enslaver\_location\_city 6 | enslaver\_location\_county 6 | enslaver\_location\_state 6 | enslaver\_location\_country 6 | enslaver\_id 7 | enslaver\_fullname 7 | enslaver\_type 7 | enslaver\_gender 7 | enslaver\_location\_id 7 | enslaver\_location\_name 7 | enslaver\_location\_city 7 | enslaver\_location\_county 7 | enslaver\_location\_state 7 | enslaver\_location\_country 7 | enslaver\_id 8 | enslaver\_fullname 8 | enslaver\_type 8 | enslaver\_gender 8 | enslaver\_location\_id 8 | enslaver\_location\_name 8 | enslaver\_location\_city 8 | enslaver\_location\_county 8 | enslaver\_location\_state 8 | enslaver\_location\_country 8 | enslaver\_id 9 | enslaver\_fullname 9 | enslaver\_type 9 | enslaver\_gender 9 | enslaver\_location\_id 9 | enslaver\_location\_name 9 | enslaver\_location\_city 9 | enslaver\_location\_county 9 | enslaver\_location\_state 9 | enslaver\_location\_country 9 | enslaver\_id 10 | enslaver\_fullname 10 | enslaver\_type 10 | enslaver\_gender 10 | enslaver\_location\_id 10 | enslaver\_location\_name 10 | enslaver\_location\_city 10 | enslaver\_location\_county 10 | enslaver\_location\_state 10 | enslaver\_location\_country 10 | enslaver\_id 11 | enslaver\_fullname 11 | enslaver\_type 11 | enslaver\_gender 11 | enslaver\_location\_id 11 | enslaver\_location\_name 11 | enslaver\_location\_city 11 | enslaver\_location\_county 11 | enslaver\_location\_state 11 | enslaver\_location\_country 11 | enslaver\_id 12 | enslaver\_fullname 12 | enslaver\_type 12 | enslaver\_gender 12 | enslaver\_location\_id 12 | enslaver\_location\_name 12 | enslaver\_location\_city 12 | enslaver\_location\_county 12 | enslaver\_location\_state 12 | enslaver\_location\_country 12 | enslaver\_id 13 | enslaver\_fullname 13 | enslaver\_type 13 | enslaver\_gender 13 | enslaver\_location\_id 13 | enslaver\_location\_name 13 | enslaver\_location\_city 13 | enslaver\_location\_county 13 | enslaver\_location\_state 13 | enslaver\_location\_country 13 | enslaver\_id 14 | enslaver\_fullname 14 | enslaver\_type 14 | enslaver\_gender 14 | enslaver\_location\_id 14 | enslaver\_location\_name 14 | enslaver\_location\_city 14 | enslaver\_location\_county 14 | enslaver\_location\_state 14 | enslaver\_location\_country 14 | enslaver\_id 15 | enslaver\_fullname 15 | enslaver\_type 15 | enslaver\_gender 15 | enslaver\_location\_id 15 | enslaver\_location\_name 15 | enslaver\_location\_city 15 | enslaver\_location\_county 15 | enslaver\_location\_state 15 | enslaver\_location\_country 15 | enslaver\_id 16 | enslaver\_fullname 16 | enslaver\_type 16 | enslaver\_gender 16 | enslaver\_location\_id 16 | enslaver\_location\_name 16 | enslaver\_location\_city 16 | enslaver\_location\_county 16 | enslaver\_location\_state 16 | enslaver\_location\_country 16 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 9914fc1c-bdfc-481a-bdf8-b4a615e82177 | 203165a3-b857-4f4a-99c2-afcde435d12b | df611bce-8549-4e8e-a2c0-7ad0e803f494 | SAM | False | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | MALE | NOT\_PROVIDED | cst bon forgeron (good blacksmith) | NaN | NaN | negro | NOT\_PROVIDED | NOT\_PROVIDED | 30.0 | 30.0 | NOT\_PROVIDED | 62.0 | 62.0 | NOT\_PROVIDED | -9.0 | -9.0 | NOT\_PROVIDED | NOT\_PROVIDED | 
 bien constitué, figure pleine, l'air un pou so...
  | NOT\_PROVIDED | dfb6e607-9a42-4016-ab69-80d7bf710000 | 1 | 1970-01-01 | 1970-01-01 | NaN | 88346743-ce96-4d70-a1c4-968b45a48bad | 
 $100 Parti marron de l'habitation de madam. Ve...
  | French | 1828-07-18 | NaN | 829b9331-eb8b-4fc6-bc7a-f7830e04547e | New-Orleans Argus | NaN | New Orleans | NaN | US-LA | US | NaN | NOT\_PROVIDED | NaN | NaN | NaN | NaN | NaN | US | ea967b68-c8a9-478e-b8f3-a6ab3ae23d99 | French | False | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | 0dbfc2f6-255b-4d67-a52e-d2eb430350b5 | NaN | New Orleans | Orleans | US-LA | US | ran | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | c2945367-c7a4-4dc6-a09b-a07d68165c42 | 100.0 | USD | delivery to prison | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | 0897c810-1104-40c0-8180-dc5dfb9f8715 | madam's house | current | FEMALE | e9bcf742-5955-4709-ae8e-eeafcccacdb2 | St. Jacques Parish | New Orleans | St. Jacques | US-LA | US | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| 1 | 8c884621-053e-420c-8ea2-7a2c9c44c84c | 3f420aa4-3d9c-4ff0-8c21-ba8a9b537928 | 3d333ee9-90cb-46d6-8d83-e265b8d3dbba | Henry | False | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | MALE | NaN | NaN | True | NaN | negro | Negro | NOT\_PROVIDED | 20.0 | 20.0 | NOT\_PROVIDED | 65.0 | 65.0 | NaN | NaN | NaN | NaN | NaN | NaN | NaN | d7dd3ab1-a0a9-440e-947a-9646d65f9caa | 1 | 1970-01-01 | 1970-01-01 | False | 8d384e0b-9d79-40e3-b469-c23d0c65fd20 | NaN | NaN | 1839-01-08 | NaN | 2b017d87-53a2-43b3-b27d-bbc507ea340b | Milledgeville Federal Union | NaN | Milledgeville | NaN | US-GA | US | NaN | NaN | NaN | NaN | NaN | NaN | NaN | US | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| 2 | 827b5340-73fe-4fdc-8f93-16146cfb3537 | 23a1cdaf-7482-47d6-ac89-40c134fca9d0 | 48dd594f-9532-457f-9db9-60e941bcad6e | Isain | False | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | MALE | NOT\_PROVIDED | NOT\_PROVIDED | NaN | NaN | mulatto, negro | NOT\_PROVIDED | NOT\_PROVIDED | 28.0 | 28.0 | NOT\_PROVIDED | 69.0 | 69.0 | NOT\_PROVIDED | -9.0 | -9.0 | 
 The runaway has a missing front tooth in his u...
  | He says that he belongs to doctor Rigaud. | NOT\_PROVIDED | NOT\_PROVIDED | c3bf9175-6d91-47dd-9ec8-4d4b71733126 | 1 | 1828-08-08 | 1828-08-08 | False | 00e53b4e-58a3-43a0-ab7b-9bb17d0bf9ab | 
 Detained at the jail of Baton Rouge, a mulatto...
  | French | 1828-08-28 | NaN | 829b9331-eb8b-4fc6-bc7a-f7830e04547e | New-Orleans Argus | NaN | New Orleans | NaN | US-LA | US | efe5df33-d7a2-4c37-9661-acc6509be8a1 | JAILER | J. Simpson | Baton Rouge Jail | Baton Rouge | East Baton Rouge | US-LA | US | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | 22a1a6d1-b1a0-4280-badd-b4c59c6515bc | On the coast a little higher than New Orleans | NaN | NaN | US-LA | US | ran | NaN | 22a8d601-2346-44d0-bcbc-b8314e379b64 | Baton Rouge Jail | Baton Rouge | East Baton Rouge | US-LA | US | jailed | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | 067b9733-0850-42b8-8826-e51d805ac328 | Dr. Rigaud | alleged | MALE | 22a1a6d1-b1a0-4280-badd-b4c59c6515bc | On the coast a little higher than New Orleans | NaN | NaN | US-LA | US | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| 3 | 6c0fa920-e7c2-49c4-905f-7b5fc9d60788 | 64d5761e-9f5b-4a02-ac6c-e7c03768aecf | 2a12bfc0-0397-4a3c-8cc5-fddabfe5638f | JIm | False | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | MALE | NOT\_PROVIDED | The runaway was an iron worker. | NaN | NaN | black | NOT\_PROVIDED | NOT\_PROVIDED | 22.0 | 22.0 | NOT\_PROVIDED | 73.0 | 73.0 | NOT\_PROVIDED | -9.0 | -9.0 | NOT\_PROVIDED | NOT\_PROVIDED | NOT\_PROVIDED | NOT\_PROVIDED | c7c16558-592e-4eae-b5f7-0fe420bcdd87 | 5 | 1837-09-08 | 1837-09-08 | False | 02aea888-86e7-40f7-a337-0eb2889102dd | 
 RAN-AWAY,\r\nFROM the subscribers' Iron Works,...
  | English | 1837-11-04 | NaN | fe2d1681-702a-46c9-a08f-9174d5339c14 | Nashville Union | NaN | Nashville | NaN | US-TN | US | NaN | ENSLAVER | NaN | NaN | NaN | NaN | NaN | US | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | bf8f9ab6-2e66-4598-8975-2de15725c54a | Iron Works in Perry County | Nashville | Perry | US-AL | US | ran | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | e2a54194-184d-486e-85fc-be2e0d5376a3 | Dr. Wm. M. Gwin | former | MALE | cb31bfb7-6e63-48b3-bb11-24b1c25e0715 | Mississippi | Cinton | Hinds | US-MS | US | ddc0c00e-69c9-4bf9-8554-0944e9b68dc9 | Mr. Thompson | current | MALE | bdb8d347-3e3b-4676-838c-a7a6a4cd83b9 | Davidson county | Nashville | Davidson | US-TN | US | 1db18d85-aca9-4fa6-bc95-3fd759a2d2d1 | A. D. DUVAL & S. T. LOVE | current | NOT\_PROVIDED | a9878710-fb57-4059-afcd-873dd4fedea8 | Iron Works in Perry | Nashville | Perry | US-AL | US | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |
| 4 | d3e471c8-da3f-4959-8996-a09a58e50d8e | 947d36be-a251-4533-824e-9cf4b61c8704 | 73b0fba0-aca5-492b-b5da-72fca8e158c1 | Five Children | False | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | OTHER | NOT\_PROVIDED | picking black moss\r\nmaking baskets | NaN | NaN | negro | NOT\_PROVIDED | children | -9.0 | -9.0 | NOT\_PROVIDED | -9.0 | -9.0 | NOT\_PROVIDED | -9.0 | -9.0 | NOT\_PROVIDED | NOT\_PROVIDED | NOT\_PROVIDED | NOT\_PROVIDED | 15117d05-b4e9-4cd4-be2d-fd1c377f231c | 12 | 1825-02-21 | 1825-02-21 | False | 60c61ab7-166a-49be-8da5-638269f9aee1 | 
 Two Hundred Dollars Reward.\r\nRanaway on the ...
  | English | 1825-07-07 | NaN | 12d38785-dfdf-4dbc-a9c6-3ccb0e8d6448 | Charleston Mercury | Charleston | Charleston | NaN | US-SC | US | NaN | ENSLAVER | NaN | NaN | NaN | NaN | NaN | US | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | cf77ee57-6909-4f1a-ada0-81c8cc025ca1 | Mr. Rowland's Mowberry Plantation | Charleston | Charleston | US-SC | US | possibleDestination | NaN | 55aa4487-cc9b-4d1d-aa45-597ed786dc50 | In the woods near Col. Cattell's place Retreat | Charleston | Charleston | US-SC | US | possibleDestination | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | 8d68fa5c-6a90-46d2-a74a-f7ca7b03e477 | 200.0 | USD | 
 delivery of these Negroes to the master of the...
  | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | 6a6c34a8-86a1-4ca3-99ef-aa03853cf91a | GEORGE W. MORRIS | current | MALE | 11316fd9-4594-4cdf-b8ba-7f3faabc0235 | NaN | NaN | NaN | US-SC | US | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN | NaN |














### 
 Methodology[¶](#Methodology)



 The data of this project is derived from the Freedom on the Move
 (FOTM) database, which is a fugitive slave advertising archive
 resource jointly promoted by multiple institutions and
 constructed through crowdsourcing. The original form of the data
 was the runaway slave notices published in newspapers across the
 United States in the early 19th century, usually issued by slave
 owners or prison guards. These advertisements were originally
 intended to assist in the pursuit of runaway slaves, but they
 detailedly recorded the appearance, age, gender, escape
 locations and other contents of the enslaved people. The project
 uses structured data files in CSV format. Each line represents
 an advertisement message, including multiple fields such as the
 basic information of the enslaved and slave owners, the time and
 place of escape and advertisement release.
 



 This project first conducted a systematic cleaning of the
 missing values, non-standard fields and abnormal values in the
 data. For example, in the approximate\_age field, the original
 content often contains vague formats such as "about 25" and
 "estimated 30". The project extract the numbers and filter out
 unreasonable extreme values (such as records over 100 years old
 or under 5 years old). The remaining null values such as
 "Not\_Provided" are reserved. Furthermore, the project have also
 standardized the state name fields (such as
 newspaper\_location\_state and runaway\_location\_state), uniformly
 converting the original forms like "US-NY" into standard
 abbreviations of Us states to support map visualization. The
 gender-related fields have also been formatted uniformly and
 null cleaned to ensure that categorical variables such as
 "Male", "Female" and "Not\_Provided" remain consistent in the
 analysis.
 



 In the analysis stage, this project conducts exploration
 starting from dimensions such as gender, time, geography and
 age. In terms of gender, the gender ratio of the enslaved and
 the slave owners is presented through pie charts and bar charts,
 and the gender combination relationship between the two is
 further cross-analyzed. At the geographical level, this project
 uses a map of the United States to show the state distribution
 of the number of advertisements. In terms of age, the project
 divides the age data into multiple intervals and combines gender
 to draw bar charts and line graphs to reveal the relative number
 differences between male and female deserters in different age
 groups. In terms of time, this project draws an annual line
 trend chart based on publication\_year, attempting to compare and
 explain the changes in the number of fugitive slave
 advertisements with specific historical events.
 












### 
 Analysis[¶](#Analysis)












#### 
**Gender of the runaway slaves**[¶](#Gender-of-the-runaway-slaves)



 When analyzing the historical data of advertisements for runaway
 slaves, gender is an important dimension that cannot be ignored.
 The gender of the enslaved not only affects their division of
 labor and social roles within the slavery system, but may also
 profoundly influence the possibility of their escape.
 










In [56]:




```
import plotly.express as px
df\_s = pd.read\_csv('C:/Users/GAVIN/Desktop/research-project/data/processed/cleaned-FOTM-Dataset-Full-Flattened.csv')
df\_gender\_valid = df\_s[df\_s['gender'] != 'Not\_Provided']
fig = px.pie(
    df\_gender\_valid,
    names='gender',
    title='Gender Distribution of Runaway Enslaved Persons (Excluding Not\_Provided)',
    hole=0.4  
)
fig.show()

```















 require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {}; if (document.getElementById("205003ee-dbe3-4b29-b950-e4925c7a06ef")) { Plotly.newPlot( "205003ee-dbe3-4b29-b950-e4925c7a06ef", [{"domain":{"x":[0.0,1.0],"y":[0.0,1.0]},"hole":0.4,"hovertemplate":"gender=%{label}\u003cextra\u003e\u003c\u002fextra\u003e","labels":["Male","Male","Male","Male","Other","Female","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Female","Female","Male","Female","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Female","Female","Female","Male","Male","Female","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Female","Male","Female","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Female","Female","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Female","Female","Female","Male","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Female","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Female","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Other","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Female","Male","Male","Female","Male","Female","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Male","Female","Female","Female","Male","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Other","Male","Female","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Male","Male","Female","Male","Female","Female","Female","Male","Male","Male","Female","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Female","Female","Male","Female","Male","Female","Female","Male","Female","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Female","Male","Male","Male","Female","Male","Female","Other","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Female","Female","Female","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Female","Male","Male","Female","Female","Female","Female","Female","Female","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Female","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Female","Female","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Female","Female","Female","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Female","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Female","Female","Female","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Female","Female","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Female","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Other","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Female","Female","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Female","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Female","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Other","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Female","Other","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Other","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Female","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Other","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Female","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Female","Female","Male","Female","Female","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Female","Male","Male","Female","Male","Female","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Female","Female","Female","Female","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Male","Female","Female","Male","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Female","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Female","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Female","Female","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Female","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Female","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Female","Female","Male","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Male","Male","Female","Male","Female","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Other","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Female","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Female","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Other","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Female","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Female","Female","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Other","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Female","Male","Female","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Female","Female","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Female","Male","Female","Female","Female","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Female","Female","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Female","Male","Female","Male","Female","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Female","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Female","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Male","Female","Male","Female","Male","Female","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Female","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Female","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Other","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Female","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Female","Male","Female","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Female","Female","Female","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Male","Female","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Female","Male","Male","Male","Female","Female","Male","Female","Male","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Male","Female","Female","Female","Male","Female","Male","Female","Female","Male","Female","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Female","Male","Male","Female","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Male","Male","Male","Female","Female","Male","Male","Male","Male","Male","Female","Male","Male","Male","Female","Male","Male","Female","Female","Male","Female","Male","Male","Male","Male","Female","Female","Female","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Male","Male","Male","Male","Female","Male","Female","Male","Male","Female","Male","Male"],"legendgroup":"","name":"","showlegend":true,"type":"pie"}], {"template":{"data":{"histogram2dcontour":[{"type":"histogram2dcontour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"choropleth":[{"type":"choropleth","colorbar":{"outlinewidth":0,"ticks":""}}],"histogram2d":[{"type":"histogram2d","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmap":[{"type":"heatmap","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"heatmapgl":[{"type":"heatmapgl","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"contourcarpet":[{"type":"contourcarpet","colorbar":{"outlinewidth":0,"ticks":""}}],"contour":[{"type":"contour","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"surface":[{"type":"surface","colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]}],"mesh3d":[{"type":"mesh3d","colorbar":{"outlinewidth":0,"ticks":""}}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"parcoords":[{"type":"parcoords","line":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolargl":[{"type":"scatterpolargl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"bar":[{"error\_x":{"color":"#2a3f5f"},"error\_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"scattergeo":[{"type":"scattergeo","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterpolar":[{"type":"scatterpolar","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"scattergl":[{"type":"scattergl","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatter3d":[{"type":"scatter3d","line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattermapbox":[{"type":"scattermapbox","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scatterternary":[{"type":"scatterternary","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"scattercarpet":[{"type":"scattercarpet","marker":{"colorbar":{"outlinewidth":0,"ticks":""}}}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"pie":[{"automargin":true,"type":"pie"}]},"layout":{"autotypenumbers":"strict","colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"hovermode":"closest","hoverlabel":{"align":"left"},"paper\_bgcolor":"white","plot\_bgcolor":"#E5ECF6","polar":{"bgcolor":"#E5ECF6","angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"ternary":{"bgcolor":"#E5ECF6","aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]]},"xaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"yaxis":{"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","automargin":true,"zerolinewidth":2},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white","gridwidth":2}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"geo":{"bgcolor":"white","landcolor":"#E5ECF6","subunitcolor":"white","showland":true,"showlakes":true,"lakecolor":"white"},"title":{"x":0.05},"mapbox":{"style":"light"}}},"legend":{"tracegroupgap":0},"title":{"text":"Gender Distribution of Runaway Enslaved Persons (Excluding Not\_Provided)"}}, {"responsive": true} ).then(function(){

 var gd = document.getElementById('205003ee-dbe3-4b29-b950-e4925c7a06ef');
 var x = new MutationObserver(function (mutations, observer) {{
 var display = window.getComputedStyle(gd).display;
 if (!display || display === 'none') {{
 console.log([gd, 'removed!']);
 Plotly.purge(gd);
 observer.disconnect();
 }}
 }});

 // Listen for the removal of the full notebook cells
 var notebookContainer = gd.closest('#notebook-container');
 if (notebookContainer) {{
 x.observe(notebookContainer, {childList: true});
 }}

 // Listen for the clearing of the current output cell
 var outputEl = gd.closest('.output');
 if (outputEl) {{
 x.observe(outputEl, {childList: true});
 }}

 }) }; });
 













 This chart shows the gender distribution of the enslaved in the
 slave escape advertisement, and only includes the records that
 have provided gender information. The results show that the
 proportion of men fleeing from slavery (78.5%) is significantly
 higher than that of women (21.5%), indicating that men may have
 attempted to escape from slavery more frequently or were more
 often emphasized by slave owners in advertisements. This trend
 might be related to the fact that men often undertook heavy
 manual labor in the slavery system, which gave them a higher
 chance and risk of escape, and also made them more likely to be
 regarded as "important property" by slave owners and wanted. In
 contrast, there are relatively fewer escape advertisements for
 female enslaved people, which may be related to the fact that
 their labor positions are more concealed and the risk of escape
 is higher. This gender difference not only reflects the power
 structure under slavery, but also demonstrates the different
 roles played by gender in resistance behavior.
 












### 
**Age**[¶](#Age)



 The age of the enslaved not only affects their labor role and
 living conditions in the slavery system, but also directly
 relates to the possibility of their escape. Analyzing the age
 distribution recorded in the advertisements of runaway slaves
 helps us understand which groups are most likely to adopt
 resistance behaviors and which ones may be under stricter
 control or in a more vulnerable position.
 










In [61]:




```
df\_age\_valid = df\_s[df\_s['approximate\_age'].apply(lambda x: str(x).isdigit())].copy()
df\_age\_valid['approximate\_age'] = df\_age\_valid['approximate\_age'].astype(int)
fig = px.histogram(
    df\_age\_valid,
    x='approximate\_age',
    nbins=20,
    title='Age Distribution of Runaway Enslaved Persons',
    labels={'approximate\_age': 'Approximate Age'},
    opacity=0.75
)
fig.update\_layout(
    xaxis\_title='Age',
    yaxis\_title='Number of Ads',
    bargap=0.1
)
fig.show()

```















 require(["plotly"], function (Plotly) {
 window.PLOTLYENV = window.PLOTLYENV || {};
 if (
 document.getElementById(
 "81bb22f5-3814-4969-8000-2b5c28ff5928",
 )
 ) {
 Plotly.newPlot(
 "81bb22f5-3814-4969-8000-2b5c28ff5928",
 [
 {
 alignmentgroup: "True",
 bingroup: "x",
 hovertemplate:
 "Approximate Age=%{x}\u003cbr\u003ecount=%{y}\u003cextra\u003e\u003c\u002fextra\u003e",
 legendgroup: "",
 marker: {
 color: "#636efa",
 opacity: 0.75,
 pattern: { shape: "" },
 },
 name: "",
 nbinsx: 20,
 offsetgroup: "",
 orientation: "v",
 showlegend: false,
 x: [
 21, 24, 30, 50, 40, 21, 15, 23, 25, 27, 30, 28,
 20, 50, 23, 40, 25, 45, 26, 40, 30, 27, 50, 23,
 22, 30, 20, 35, 18, 34, 40, 10, 40, 25, 14, 34,
 30, 20, 32, 28, 32, 19, 33, 27, 35, 18, 40, 50,
 15, 27, 25, 35, 18, 50, 23, 24, 35, 35, 20, 30,
 35, 20, 18, 21, 40, 24, 14, 43, 14, 21, 28, 26,
 35, 24, 30, 20, 21, 14, 30, 35, 40, 21, 35, 29,
 30, 20, 20, 16, 25, 23, 25, 30, 35, 25, 21, 30,
 25, 50, 21, 36, 40, 30, 24, 26, 18, 25, 21, 18,
 45, 21, 30, 21, 26, 18, 21, 27, 30, 27, 22, 22,
 30, 25, 30, 25, 30, 23, 21, 18, 14, 45, 28, 26,
 30, 25, 22, 20, 45, 22, 22, 27, 13, 21, 25, 25,
 40, 23, 28, 24, 27, 48, 50, 25, 28, 30, 30, 27,
 18, 36, 22, 40, 28, 35, 17, 50, 25, 17, 30, 25,
 55, 25, 35, 30, 22, 25, 22, 21, 35, 25, 40, 25,
 55, 15, 25, 19, 25, 20, 19, 20, 40, 25, 20, 30,
 21, 18, 40, 45, 21, 27, 25, 22, 30, 30, 20, 30,
 17, 30, 21, 30, 30, 17, 21, 22, 21, 21, 18, 24,
 45, 35, 15, 15, 22, 25, 26, 20, 25, 40, 28, 10,
 21, 45, 40, 28, 36, 21, 30, 29, 21, 28, 25, 20,
 29, 22, 20, 24, 26, 30, 25, 26, 15, 28, 30, 35,
 50, 34, 20, 20, 27, 25, 20, 30, 50, 21, 50, 30,
 25, 50, 30, 40, 30, 14, 17, 20, 26, 24, 24, 38,
 26, 60, 40, 30, 45, 16, 20, 30, 20, 18, 19, 17,
 21, 26, 45, 22, 22, 25, 26, 35, 14, 22, 35, 40,
 18, 40, 28, 13, 25, 25, 26, 30, 18, 11, 24, 17,
 30, 50, 25, 45, 20, 22, 28, 35, 45, 25, 21, 30,
 20, 40, 25, 14, 17, 40, 13, 40, 35, 28, 21, 17,
 18, 25, 21, 40, 30, 30, 50, 22, 24, 18, 28, 30,
 20, 26, 28, 30, 21, 25, 40, 24, 20, 26, 45, 50,
 35, 30, 19, 25, 45, 24, 30, 40, 11, 40, 25, 22,
 30, 35, 21, 20, 40, 25, 25, 20, 23, 21, 25, 40,
 13, 40, 23, 21, 32, 40, 14, 24, 20, 25, 22, 25,
 25, 30, 16, 28, 15, 28, 22, 30, 28, 22, 22, 25,
 26, 20, 45, 40, 45, 52, 35, 18, 24, 40, 30, 36,
 17, 14, 30, 30, 22, 26, 35, 26, 12, 22, 21, 45,
 25, 25, 23, 32, 35, 50, 23, 13, 20, 45, 20, 20,
 45, 23, 26, 26, 8, 40, 20, 28, 19, 35, 21, 28,
 31, 21, 23, 30, 29, 34, 25, 25, 22, 40, 24, 27,
 50, 35, 20, 35, 26, 23, 20, 30, 40, 13, 21, 17,
 21, 40, 18, 26, 32, 50, 35, 20, 20, 21, 24, 17,
 45, 35, 26, 21, 15, 18, 21, 21, 21, 30, 50, 25,
 28, 30, 26, 18, 19, 35, 28, 30, 26, 25, 14, 24,
 22, 40, 19, 24, 30, 30, 21, 20, 30, 15, 30, 22,
 20, 5, 32, 22, 20, 30, 22, 15, 25, 30, 36, 18,
 22, 7, 18, 34, 50, 28, 40, 20, 35, 50, 15, 17,
 25, 11, 21, 20, 24, 35, 27, 30, 30, 13, 21, 20,
 22, 22, 28, 25, 40, 20, 25, 30, 30, 21, 50, 30,
 25, 22, 9, 35, 22, 20, 30, 20, 30, 30, 22, 24,
 35, 19, 24, 35, 18, 45, 20, 30, 18, 40, 22, 45,
 40, 28, 22, 20, 33, 18, 28, 24, 22, 23, 26, 20,
 24, 26, 21, 20, 18, 18, 25, 35, 26, 23, 30, 40,
 25, 23, 24, 18, 18, 18, 40, 25, 65, 13, 26, 21,
 45, 45, 28, 20, 24, 20, 21, 20, 40, 50, 25, 17,
 45, 30, 45, 27, 30, 15, 16, 30, 23, 22, 13, 35,
 38, 25, 20, 40, 16, 25, 16, 20, 24, 33, 50, 28,
 25, 17, 18, 20, 26, 11, 14, 35, 30, 23, 35, 26,
 24, 25, 26, 25, 20, 24, 30, 20, 21, 28, 24, 50,
 24, 30, 20, 35, 26, 50, 25, 50, 35, 21, 35, 17,
 37, 20, 48, 26, 25, 22, 21, 45, 40, 24, 8, 40,
 25, 30, 27, 50, 25, 16, 24, 21, 60, 26, 26, 32,
 9, 23, 26, 38, 27, 25, 20, 40, 25, 19, 30, 55,
 25, 35, 24, 45, 28, 25, 28, 22, 20, 24, 35, 18,
 30, 6, 32, 30, 40, 20, 25, 24, 50, 25, 24, 26,
 30, 27, 23, 21, 17, 30, 24, 28, 26, 45, 25, 40,
 23, 14, 35, 24, 28, 28, 40, 40, 32, 21, 27, 24,
 20, 20, 17, 32, 26, 30, 21, 25, 20, 27, 26, 23,
 25, 20, 17, 24, 20, 36, 22, 26, 25, 16, 24, 15,
 25, 25, 14, 30, 24, 30, 25, 45, 17, 35, 24, 30,
 25, 18, 45, 22, 45, 26, 24, 30, 35, 22, 25, 35,
 37, 20, 30, 40, 25, 21, 21, 35, 17, 17, 35, 45,
 25, 25, 35, 25, 30, 19, 26, 50, 40, 32, 24, 26,
 21, 30, 28, 56, 40, 25, 24, 16, 20, 25, 18, 24,
 24, 23, 30, 40, 50, 23, 21, 21, 20, 24, 24, 20,
 20, 35, 25, 24, 30, 21, 25, 25, 35, 30, 30, 25,
 30, 17, 22, 20, 21, 40, 30, 18, 40, 21, 28, 14,
 20, 30, 25, 35, 20, 40, 40, 21, 20, 13, 35, 20,
 22, 40, 45, 18, 28, 23, 35, 28, 30, 23, 25, 12,
 14, 25, 40, 28, 35, 18, 15, 22, 21, 20, 30, 35,
 26, 25, 8, 25, 25, 20, 29, 20, 25, 12, 20, 35,
 30, 25, 17, 40, 25, 14, 13, 35, 18, 25, 21, 25,
 21, 21, 50, 30, 15, 22, 24, 47, 25, 24, 22, 20,
 50, 15, 35, 23, 35, 45, 50, 50, 17, 21, 25, 30,
 36, 35, 33, 21, 19, 22, 22, 45, 15, 52, 30, 13,
 26, 20, 14, 40, 24, 50, 25, 60, 18, 40, 22, 45,
 25, 24, 21, 20, 24, 34, 35, 40, 30, 20, 20, 6,
 21, 35, 18, 18, 25, 35, 20, 55, 40, 7, 28, 40,
 14, 25, 35, 30, 21, 30, 40, 35, 50, 38, 25, 25,
 20, 22, 30, 30, 25, 32, 30, 30, 21, 30, 22, 42,
 45, 28, 20, 21, 45, 8, 13, 28, 19, 23, 20, 28,
 40, 40, 40, 21, 28, 15, 25, 8, 35, 24, 21, 14,
 22, 28, 18, 37, 25, 24, 20, 28, 40, 45, 22, 26,
 40, 32, 40, 40, 45, 18, 28, 30, 28, 45, 35, 18,
 24, 25, 22, 20, 26, 12, 40, 30, 15, 40, 20, 26,
 40, 20, 35, 50, 50, 13, 30, 18, 28, 22, 20, 38,
 25, 34, 35, 19, 10, 23, 18, 26, 30, 25, 30, 18,
 20, 24, 20, 25, 30, 26, 19, 36, 40, 30, 19, 20,
 24, 25, 21, 27, 25, 18, 30, 29, 23, 24, 58, 26,
 25, 26, 20, 26, 25, 25, 41, 12, 32, 20, 26, 22,
 35, 30, 30, 20, 14, 35, 35, 30, 13, 26, 23, 35,
 40, 17, 14, 24, 19, 13, 24, 24, 25, 22, 34, 20,
 24, 30, 50, 25, 26, 25, 25, 40, 25, 30, 21, 11,
 36, 25, 60, 25, 35, 22, 20, 20, 7, 25, 22, 45,
 24, 24, 16, 12, 26, 20, 35, 18, 20, 30, 32, 19,
 25, 30, 20, 23, 18, 20, 26, 25, 12, 25, 24, 23,
 40, 18, 24, 21, 14, 25, 20, 30, 21, 24, 35, 25,
 27, 18, 28, 40, 28, 30, 20, 20, 28, 30, 17, 22,
 35, 25, 24, 20, 20, 30, 26, 40, 30, 18, 25, 12,
 21, 36, 21, 25, 20, 21, 18, 30, 19, 35, 26, 35,
 25, 40, 21, 30, 50, 35, 40, 10, 40, 11, 30, 15,
 22, 21, 24, 30, 25, 50, 24, 19, 35, 15, 25, 24,
 22, 20, 19, 24, 22, 12, 30, 26, 26, 26, 22, 26,
 25, 40, 25, 25, 34, 50, 30, 17, 35, 14, 15, 28,
 20, 14, 17, 40, 26, 18, 15, 25, 30, 30, 30, 25,
 19, 24, 21, 30, 22, 40, 45, 55, 14, 50, 21, 23,
 30, 21, 30, 24, 26, 22, 30, 21, 25, 21, 19, 40,
 21, 21, 30, 40, 40, 37, 6, 22, 50, 40, 50, 40,
 40, 25, 37, 40, 35, 24, 23, 23, 20, 25, 30, 24,
 20, 17, 40, 24, 25, 22, 50, 25, 21, 40, 30, 24,
 26, 22, 35, 30, 50, 23, 28, 21, 20, 40, 35, 28,
 40, 40, 30, 21, 30, 40, 36, 22, 28, 19, 30, 18,
 20, 30, 17, 24, 26, 14, 20, 5, 6, 22, 24, 24,
 30, 30, 25, 25, 25, 33, 10, 30, 7, 50, 36, 30,
 18, 27, 21, 25, 30, 30, 27, 30, 35, 34, 13, 40,
 25, 40, 40, 28, 38, 30, 22, 17, 25, 19, 23, 35,
 25, 20, 13, 50, 40, 13,
 ],
 xaxis: "x",
 yaxis: "y",
 type: "histogram",
 },
 ],
 {
 template: {
 data: {
 histogram2dcontour: [
 {
 type: "histogram2dcontour",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 choropleth: [
 {
 type: "choropleth",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 histogram2d: [
 {
 type: "histogram2d",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 heatmap: [
 {
 type: "heatmap",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 heatmapgl: [
 {
 type: "heatmapgl",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 contourcarpet: [
 {
 type: "contourcarpet",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 contour: [
 {
 type: "contour",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 surface: [
 {
 type: "surface",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 mesh3d: [
 {
 type: "mesh3d",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 scatter: [
 {
 fillpattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 type: "scatter",
 },
 ],
 parcoords: [
 {
 type: "parcoords",
 line: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterpolargl: [
 {
 type: "scatterpolargl",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 bar: [
 {
 error\_x: { color: "#2a3f5f" },
 error\_y: { color: "#2a3f5f" },
 marker: {
 line: { color: "#E5ECF6", width: 0.5 },
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "bar",
 },
 ],
 scattergeo: [
 {
 type: "scattergeo",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterpolar: [
 {
 type: "scatterpolar",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 histogram: [
 {
 marker: {
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "histogram",
 },
 ],
 scattergl: [
 {
 type: "scattergl",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatter3d: [
 {
 type: "scatter3d",
 line: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scattermapbox: [
 {
 type: "scattermapbox",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterternary: [
 {
 type: "scatterternary",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scattercarpet: [
 {
 type: "scattercarpet",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 carpet: [
 {
 aaxis: {
 endlinecolor: "#2a3f5f",
 gridcolor: "white",
 linecolor: "white",
 minorgridcolor: "white",
 startlinecolor: "#2a3f5f",
 },
 baxis: {
 endlinecolor: "#2a3f5f",
 gridcolor: "white",
 linecolor: "white",
 minorgridcolor: "white",
 startlinecolor: "#2a3f5f",
 },
 type: "carpet",
 },
 ],
 table: [
 {
 cells: {
 fill: { color: "#EBF0F8" },
 line: { color: "white" },
 },
 header: {
 fill: { color: "#C8D4E3" },
 line: { color: "white" },
 },
 type: "table",
 },
 ],
 barpolar: [
 {
 marker: {
 line: { color: "#E5ECF6", width: 0.5 },
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "barpolar",
 },
 ],
 pie: [{ automargin: true, type: "pie" }],
 },
 layout: {
 autotypenumbers: "strict",
 colorway: [
 "#636efa",
 "#EF553B",
 "#00cc96",
 "#ab63fa",
 "#FFA15A",
 "#19d3f3",
 "#FF6692",
 "#B6E880",
 "#FF97FF",
 "#FECB52",
 ],
 font: { color: "#2a3f5f" },
 hovermode: "closest",
 hoverlabel: { align: "left" },
 paper\_bgcolor: "white",
 plot\_bgcolor: "#E5ECF6",
 polar: {
 bgcolor: "#E5ECF6",
 angularaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 radialaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 },
 ternary: {
 bgcolor: "#E5ECF6",
 aaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 baxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 caxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 },
 coloraxis: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 colorscale: {
 sequential: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 sequentialminus: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 diverging: [
 [0, "#8e0152"],
 [0.1, "#c51b7d"],
 [0.2, "#de77ae"],
 [0.3, "#f1b6da"],
 [0.4, "#fde0ef"],
 [0.5, "#f7f7f7"],
 [0.6, "#e6f5d0"],
 [0.7, "#b8e186"],
 [0.8, "#7fbc41"],
 [0.9, "#4d9221"],
 [1, "#276419"],
 ],
 },
 xaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 title: { standoff: 15 },
 zerolinecolor: "white",
 automargin: true,
 zerolinewidth: 2,
 },
 yaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 title: { standoff: 15 },
 zerolinecolor: "white",
 automargin: true,
 zerolinewidth: 2,
 },
 scene: {
 xaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 yaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 zaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 },
 shapedefaults: { line: { color: "#2a3f5f" } },
 annotationdefaults: {
 arrowcolor: "#2a3f5f",
 arrowhead: 0,
 arrowwidth: 1,
 },
 geo: {
 bgcolor: "white",
 landcolor: "#E5ECF6",
 subunitcolor: "white",
 showland: true,
 showlakes: true,
 lakecolor: "white",
 },
 title: { x: 0.05 },
 mapbox: { style: "light" },
 },
 },
 xaxis: {
 anchor: "y",
 domain: [0.0, 1.0],
 title: { text: "Age" },
 },
 yaxis: {
 anchor: "x",
 domain: [0.0, 1.0],
 title: { text: "Number of Ads" },
 },
 legend: { tracegroupgap: 0 },
 title: {
 text: "Age Distribution of Runaway Enslaved Persons",
 },
 barmode: "relative",
 bargap: 0.1,
 },
 { responsive: true },
 ).then(function () {
 var gd = document.getElementById(
 "81bb22f5-3814-4969-8000-2b5c28ff5928",
 );
 var x = new MutationObserver(function (
 mutations,
 observer,
 ) {
 {
 var display = window.getComputedStyle(gd).display;
 if (!display || display === "none") {
 {
 console.log([gd, "removed!"]);
 Plotly.purge(gd);
 observer.disconnect();
 }
 }
 }
 });

 // Listen for the removal of the full notebook cells
 var notebookContainer = gd.closest(
 "#notebook-container",
 );
 if (notebookContainer) {
 {
 x.observe(notebookContainer, { childList: true });
 }
 }

 // Listen for the clearing of the current output cell
 var outputEl = gd.closest(".output");
 if (outputEl) {
 {
 x.observe(outputEl, { childList: true });
 }
 }
 });
 }
 });
 













 It can be seen from the chart that the ages of the enslaved are
 mainly concentrated between 20 and 40 years old, especially the
 age group of 21 to 30 years old is the most concentrated age
 group for fleeing. This trend indicates that the young and
 middle-aged years may be the stage when fleeing behavior is most
 frequent. In contrast, the number of runaway slaves aged 5 to 15
 and over 60 was significantly smaller. This age distribution
 might be because young and middle-aged enslaved individuals
 usually undertake more arduous labor, are under greater pressure
 and surveillance, and also possess better physical strength,
 energy and the will to escape. Children or the elderly have a
 relatively lower chance of escaping due to reasons such as
 physical ability or family ties. Slave owners might be more
 inclined to invest in "productive" enslaved individuals and
 therefore would advertise more frequently for this age group
 












#### 
**Age-Gender**[¶](#Age-Gender)



 The intersection of gender and age is a key clue to
 understanding the living conditions of the enslaved and the
 possibility of resistance. Under the slavery system, the
 division of labor was highly dependent on gender and age
 structure. Different working environments also meant different
 possibilities of escape.
 










In [65]:




```
df\_age\_gender = df\_s[
    df\_s['approximate\_age'].apply(lambda x: str(x).isdigit()) &
    (df\_s['gender'] != 'Not\_Provided')
].copy()
df\_age\_gender['approximate\_age'] = df\_age\_gender['approximate\_age'].astype(int)
bins = [0, 10, 20, 30, 40, 50, 60, 100]
labels = ['0–10', '11–20', '21–30', '31–40', '41–50', '51–60', '61+']
df\_age\_gender['age\_group'] = pd.cut(df\_age\_gender['approximate\_age'], bins=bins, labels=labels, right=True)
age\_gender\_counts = df\_age\_gender.groupby(['age\_group', 'gender']).size().reset\_index(name='count')
fig = px.line(
    age\_gender\_counts,
    x='age\_group',
    y='count',
    color='gender',
    markers=True,  
    text='count',
    title='Gender Distribution Across Age Groups of Runaway Enslaved Persons (Line Chart)',
    labels={'age\_group': 'Age Group', 'count': 'Number of Ads'}
)
fig.update\_traces(textposition='top center')
fig.update\_layout(
    xaxis\_title='Age Group',
    yaxis\_title='Number of Ads',
    uniformtext\_minsize=8,
    uniformtext\_mode='hide'
)

fig.show()

```













```

C:\Users\GAVIN\AppData\Local\Temp\ipykernel\_97484\1018323412.py:9: FutureWarning:

The default of observed=False is deprecated and will be changed to True in a future version of pandas. Pass observed=False to retain current behavior or observed=True to adopt the future default and silence this warning.


```









 require(["plotly"], function (Plotly) {
 window.PLOTLYENV = window.PLOTLYENV || {};
 if (
 document.getElementById(
 "37dfff1e-79b5-4ab0-b96e-1501f47aeb99",
 )
 ) {
 Plotly.newPlot(
 "37dfff1e-79b5-4ab0-b96e-1501f47aeb99",
 [
 {
 hovertemplate:
 "gender=Female\u003cbr\u003eAge Group=%{x}\u003cbr\u003eNumber of Ads=%{text}\u003cextra\u003e\u003c\u002fextra\u003e",
 legendgroup: "Female",
 line: { color: "#636efa", dash: "solid" },
 marker: { symbol: "circle" },
 mode: "lines+markers+text",
 name: "Female",
 orientation: "v",
 showlegend: true,
 text: [3.0, 104.0, 132.0, 82.0, 18.0, 1.0, 0.0],
 x: [
 "0\u201310",
 "11\u201320",
 "21\u201330",
 "31\u201340",
 "41\u201350",
 "51\u201360",
 "61+",
 ],
 xaxis: "x",
 y: [3, 104, 132, 82, 18, 1, 0],
 yaxis: "y",
 type: "scatter",
 textposition: "top center",
 },
 {
 hovertemplate:
 "gender=Male\u003cbr\u003eAge Group=%{x}\u003cbr\u003eNumber of Ads=%{text}\u003cextra\u003e\u003c\u002fextra\u003e",
 legendgroup: "Male",
 line: { color: "#EF553B", dash: "solid" },
 marker: { symbol: "circle" },
 mode: "lines+markers+text",
 name: "Male",
 orientation: "v",
 showlegend: true,
 text: [
 15.0, 219.0, 643.0, 169.0, 80.0, 12.0, 1.0,
 ],
 x: [
 "0\u201310",
 "11\u201320",
 "21\u201330",
 "31\u201340",
 "41\u201350",
 "51\u201360",
 "61+",
 ],
 xaxis: "x",
 y: [15, 219, 643, 169, 80, 12, 1],
 yaxis: "y",
 type: "scatter",
 textposition: "top center",
 },
 ],
 {
 template: {
 data: {
 histogram2dcontour: [
 {
 type: "histogram2dcontour",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 choropleth: [
 {
 type: "choropleth",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 histogram2d: [
 {
 type: "histogram2d",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 heatmap: [
 {
 type: "heatmap",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 heatmapgl: [
 {
 type: "heatmapgl",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 contourcarpet: [
 {
 type: "contourcarpet",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 contour: [
 {
 type: "contour",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 surface: [
 {
 type: "surface",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 mesh3d: [
 {
 type: "mesh3d",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 scatter: [
 {
 fillpattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 type: "scatter",
 },
 ],
 parcoords: [
 {
 type: "parcoords",
 line: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterpolargl: [
 {
 type: "scatterpolargl",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 bar: [
 {
 error\_x: { color: "#2a3f5f" },
 error\_y: { color: "#2a3f5f" },
 marker: {
 line: { color: "#E5ECF6", width: 0.5 },
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "bar",
 },
 ],
 scattergeo: [
 {
 type: "scattergeo",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterpolar: [
 {
 type: "scatterpolar",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 histogram: [
 {
 marker: {
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "histogram",
 },
 ],
 scattergl: [
 {
 type: "scattergl",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatter3d: [
 {
 type: "scatter3d",
 line: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scattermapbox: [
 {
 type: "scattermapbox",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterternary: [
 {
 type: "scatterternary",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scattercarpet: [
 {
 type: "scattercarpet",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 carpet: [
 {
 aaxis: {
 endlinecolor: "#2a3f5f",
 gridcolor: "white",
 linecolor: "white",
 minorgridcolor: "white",
 startlinecolor: "#2a3f5f",
 },
 baxis: {
 endlinecolor: "#2a3f5f",
 gridcolor: "white",
 linecolor: "white",
 minorgridcolor: "white",
 startlinecolor: "#2a3f5f",
 },
 type: "carpet",
 },
 ],
 table: [
 {
 cells: {
 fill: { color: "#EBF0F8" },
 line: { color: "white" },
 },
 header: {
 fill: { color: "#C8D4E3" },
 line: { color: "white" },
 },
 type: "table",
 },
 ],
 barpolar: [
 {
 marker: {
 line: { color: "#E5ECF6", width: 0.5 },
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "barpolar",
 },
 ],
 pie: [{ automargin: true, type: "pie" }],
 },
 layout: {
 autotypenumbers: "strict",
 colorway: [
 "#636efa",
 "#EF553B",
 "#00cc96",
 "#ab63fa",
 "#FFA15A",
 "#19d3f3",
 "#FF6692",
 "#B6E880",
 "#FF97FF",
 "#FECB52",
 ],
 font: { color: "#2a3f5f" },
 hovermode: "closest",
 hoverlabel: { align: "left" },
 paper\_bgcolor: "white",
 plot\_bgcolor: "#E5ECF6",
 polar: {
 bgcolor: "#E5ECF6",
 angularaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 radialaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 },
 ternary: {
 bgcolor: "#E5ECF6",
 aaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 baxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 caxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 },
 coloraxis: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 colorscale: {
 sequential: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 sequentialminus: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 diverging: [
 [0, "#8e0152"],
 [0.1, "#c51b7d"],
 [0.2, "#de77ae"],
 [0.3, "#f1b6da"],
 [0.4, "#fde0ef"],
 [0.5, "#f7f7f7"],
 [0.6, "#e6f5d0"],
 [0.7, "#b8e186"],
 [0.8, "#7fbc41"],
 [0.9, "#4d9221"],
 [1, "#276419"],
 ],
 },
 xaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 title: { standoff: 15 },
 zerolinecolor: "white",
 automargin: true,
 zerolinewidth: 2,
 },
 yaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 title: { standoff: 15 },
 zerolinecolor: "white",
 automargin: true,
 zerolinewidth: 2,
 },
 scene: {
 xaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 yaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 zaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 },
 shapedefaults: { line: { color: "#2a3f5f" } },
 annotationdefaults: {
 arrowcolor: "#2a3f5f",
 arrowhead: 0,
 arrowwidth: 1,
 },
 geo: {
 bgcolor: "white",
 landcolor: "#E5ECF6",
 subunitcolor: "white",
 showland: true,
 showlakes: true,
 lakecolor: "white",
 },
 title: { x: 0.05 },
 mapbox: { style: "light" },
 },
 },
 xaxis: {
 anchor: "y",
 domain: [0.0, 1.0],
 title: { text: "Age Group" },
 },
 yaxis: {
 anchor: "x",
 domain: [0.0, 1.0],
 title: { text: "Number of Ads" },
 },
 legend: {
 title: { text: "gender" },
 tracegroupgap: 0,
 },
 title: {
 text: "Gender Distribution Across Age Groups of Runaway Enslaved Persons (Line Chart)",
 },
 uniformtext: { minsize: 8, mode: "hide" },
 },
 { responsive: true },
 ).then(function () {
 var gd = document.getElementById(
 "37dfff1e-79b5-4ab0-b96e-1501f47aeb99",
 );
 var x = new MutationObserver(function (
 mutations,
 observer,
 ) {
 {
 var display = window.getComputedStyle(gd).display;
 if (!display || display === "none") {
 {
 console.log([gd, "removed!"]);
 Plotly.purge(gd);
 observer.disconnect();
 }
 }
 }
 });

 // Listen for the removal of the full notebook cells
 var notebookContainer = gd.closest(
 "#notebook-container",
 );
 if (notebookContainer) {
 {
 x.observe(notebookContainer, { childList: true });
 }
 }

 // Listen for the clearing of the current output cell
 var outputEl = gd.closest(".output");
 if (outputEl) {
 {
 x.observe(outputEl, { childList: true });
 }
 }
 });
 }
 });
 













 Among all age groups, the number of male runaway slaves is
 generally higher than that of female slaves, especially in the
 age group of 21 to 30, where the number of men leads
 significantly. This indicates that young and middle-aged men are
 the main bearers of the fleeing behavior, which may be related
 to their more frequent engagement in outdoor labor, exposure to
 the external environment, and higher physical ability. However,
 the proportion of female runaway slaves among all age groups is
 relatively low, especially in middle and old age when there are
 almost no runaway records. This may reflect that they are
 subject to stronger spatial restrictions or constraints from
 family roles.
 












#### 
**Gender of the Enslavers**[¶](#Gender-of-the-Enslavers)



 The research holds that the gender composition of slave owners
 provides another important perspective for observing the power
 structure of the slave system. The gender of slave owners not
 only affects the language style and focus of advertisements, but
 may also have potential correlations with variables such as the
 gender of enslaved people and escape patterns.
 










In [69]:




```
df\_enslaver = df\_s[df\_s['enslaver\_gender 1'] != 'Not\_Provided'].copy()
enslaver\_counts = df\_enslaver['enslaver\_gender 1'].value\_counts().reset\_index()
enslaver\_counts.columns = ['Enslaver Gender', 'Count']
fig = px.pie(
    enslaver\_counts,
    names='Enslaver Gender',
    values='Count',
    title='Gender Distribution of Enslavers (Based on Ads)',
    hole=0.3  
)

fig.update\_traces(textposition='inside', textinfo='percent+label')
fig.show()

```















 require(["plotly"], function (Plotly) {
 window.PLOTLYENV = window.PLOTLYENV || {};
 if (
 document.getElementById(
 "3c166d11-362a-46da-b0a9-7bda8071f8af",
 )
 ) {
 Plotly.newPlot(
 "3c166d11-362a-46da-b0a9-7bda8071f8af",
 [
 {
 domain: { x: [0.0, 1.0], y: [0.0, 1.0] },
 hole: 0.3,
 hovertemplate:
 "Enslaver Gender=%{label}\u003cbr\u003eCount=%{value}\u003cextra\u003e\u003c\u002fextra\u003e",
 labels: ["Male", "Female", "Other"],
 legendgroup: "",
 name: "",
 showlegend: true,
 values: [16272, 1308, 180],
 type: "pie",
 textinfo: "percent+label",
 textposition: "inside",
 },
 ],
 {
 template: {
 data: {
 histogram2dcontour: [
 {
 type: "histogram2dcontour",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 choropleth: [
 {
 type: "choropleth",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 histogram2d: [
 {
 type: "histogram2d",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 heatmap: [
 {
 type: "heatmap",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 heatmapgl: [
 {
 type: "heatmapgl",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 contourcarpet: [
 {
 type: "contourcarpet",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 contour: [
 {
 type: "contour",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 surface: [
 {
 type: "surface",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 mesh3d: [
 {
 type: "mesh3d",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 scatter: [
 {
 fillpattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 type: "scatter",
 },
 ],
 parcoords: [
 {
 type: "parcoords",
 line: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterpolargl: [
 {
 type: "scatterpolargl",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 bar: [
 {
 error\_x: { color: "#2a3f5f" },
 error\_y: { color: "#2a3f5f" },
 marker: {
 line: { color: "#E5ECF6", width: 0.5 },
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "bar",
 },
 ],
 scattergeo: [
 {
 type: "scattergeo",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterpolar: [
 {
 type: "scatterpolar",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 histogram: [
 {
 marker: {
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "histogram",
 },
 ],
 scattergl: [
 {
 type: "scattergl",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatter3d: [
 {
 type: "scatter3d",
 line: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scattermapbox: [
 {
 type: "scattermapbox",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterternary: [
 {
 type: "scatterternary",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scattercarpet: [
 {
 type: "scattercarpet",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 carpet: [
 {
 aaxis: {
 endlinecolor: "#2a3f5f",
 gridcolor: "white",
 linecolor: "white",
 minorgridcolor: "white",
 startlinecolor: "#2a3f5f",
 },
 baxis: {
 endlinecolor: "#2a3f5f",
 gridcolor: "white",
 linecolor: "white",
 minorgridcolor: "white",
 startlinecolor: "#2a3f5f",
 },
 type: "carpet",
 },
 ],
 table: [
 {
 cells: {
 fill: { color: "#EBF0F8" },
 line: { color: "white" },
 },
 header: {
 fill: { color: "#C8D4E3" },
 line: { color: "white" },
 },
 type: "table",
 },
 ],
 barpolar: [
 {
 marker: {
 line: { color: "#E5ECF6", width: 0.5 },
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "barpolar",
 },
 ],
 pie: [{ automargin: true, type: "pie" }],
 },
 layout: {
 autotypenumbers: "strict",
 colorway: [
 "#636efa",
 "#EF553B",
 "#00cc96",
 "#ab63fa",
 "#FFA15A",
 "#19d3f3",
 "#FF6692",
 "#B6E880",
 "#FF97FF",
 "#FECB52",
 ],
 font: { color: "#2a3f5f" },
 hovermode: "closest",
 hoverlabel: { align: "left" },
 paper\_bgcolor: "white",
 plot\_bgcolor: "#E5ECF6",
 polar: {
 bgcolor: "#E5ECF6",
 angularaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 radialaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 },
 ternary: {
 bgcolor: "#E5ECF6",
 aaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 baxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 caxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 },
 coloraxis: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 colorscale: {
 sequential: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 sequentialminus: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 diverging: [
 [0, "#8e0152"],
 [0.1, "#c51b7d"],
 [0.2, "#de77ae"],
 [0.3, "#f1b6da"],
 [0.4, "#fde0ef"],
 [0.5, "#f7f7f7"],
 [0.6, "#e6f5d0"],
 [0.7, "#b8e186"],
 [0.8, "#7fbc41"],
 [0.9, "#4d9221"],
 [1, "#276419"],
 ],
 },
 xaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 title: { standoff: 15 },
 zerolinecolor: "white",
 automargin: true,
 zerolinewidth: 2,
 },
 yaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 title: { standoff: 15 },
 zerolinecolor: "white",
 automargin: true,
 zerolinewidth: 2,
 },
 scene: {
 xaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 yaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 zaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 },
 shapedefaults: { line: { color: "#2a3f5f" } },
 annotationdefaults: {
 arrowcolor: "#2a3f5f",
 arrowhead: 0,
 arrowwidth: 1,
 },
 geo: {
 bgcolor: "white",
 landcolor: "#E5ECF6",
 subunitcolor: "white",
 showland: true,
 showlakes: true,
 lakecolor: "white",
 },
 title: { x: 0.05 },
 mapbox: { style: "light" },
 },
 },
 legend: { tracegroupgap: 0 },
 title: {
 text: "Gender Distribution of Enslavers (Based on Ads)",
 },
 },
 { responsive: true },
 ).then(function () {
 var gd = document.getElementById(
 "3c166d11-362a-46da-b0a9-7bda8071f8af",
 );
 var x = new MutationObserver(function (
 mutations,
 observer,
 ) {
 {
 var display = window.getComputedStyle(gd).display;
 if (!display || display === "none") {
 {
 console.log([gd, "removed!"]);
 Plotly.purge(gd);
 observer.disconnect();
 }
 }
 }
 });

 // Listen for the removal of the full notebook cells
 var notebookContainer = gd.closest(
 "#notebook-container",
 );
 if (notebookContainer) {
 {
 x.observe(notebookContainer, { childList: true });
 }
 }

 // Listen for the clearing of the current output cell
 var outputEl = gd.closest(".output");
 if (outputEl) {
 {
 x.observe(outputEl, { childList: true });
 }
 }
 });
 }
 });
 













 The vast majority of advertisements for fleeing slaves were
 posted by male slave owners (91.6%), while the proportion of
 female slave owners was significantly lower (7.36%). This
 distribution reflects the dominant position of men in property
 rights, social status and the operation of the system under the
 slave system. Since men are more often regarded as the "heads of
 households" in the legal and economic systems, they more
 frequently dominate the matters of wanted fugitives and property
 protection. Although women also have enslaved individuals in
 some family or inheritance contexts, their "voices" in public
 Spaces are relatively weakened, which is reflected in the
 relatively marginal number of advertisements for runaway slaves.
 










In [72]:




```
df\_pair = df\_s[
    (df\_s['enslaver\_gender 1'] != 'Not\_Provided') &
    (df\_s['gender'] != 'Not\_Provided')
].copy()
enslaver\_slave\_gender = df\_pair.groupby(['enslaver\_gender 1', 'gender']).size().reset\_index(name='count')
enslaver\_slave\_gender['label'] = enslaver\_slave\_gender.apply(
    lambda row: f"{row['enslaver\_gender 1']} → {row['gender']}<br>Count: {row['count']}",
    axis=1
)
fig = px.bar(
    enslaver\_slave\_gender,
    x='enslaver\_gender 1',
    y='count',
    color='gender',
    barmode='group',
    text='label', 
    title='Relationship Between Enslaver Gender and Enslaved Person Gender',
    labels={
        'enslaver\_gender 1': 'Enslaver Gender',
        'gender': 'Enslaved Person Gender',
        'count': 'Number of Ads'
    }
)
fig.update\_traces(textposition='outside')
fig.update\_layout(
    xaxis\_title='Enslaver Gender',
    yaxis\_title='Number of Ads',
    uniformtext\_minsize=8,
    uniformtext\_mode='hide'
)
fig.show()

```















 require(["plotly"], function (Plotly) {
 window.PLOTLYENV = window.PLOTLYENV || {};
 if (
 document.getElementById(
 "16eb7c5b-971f-4f79-9a2e-b3818af4537e",
 )
 ) {
 Plotly.newPlot(
 "16eb7c5b-971f-4f79-9a2e-b3818af4537e",
 [
 {
 alignmentgroup: "True",
 hovertemplate:
 "Enslaved Person Gender=Female\u003cbr\u003eEnslaver Gender=%{x}\u003cbr\u003eNumber of Ads=%{y}\u003cbr\u003elabel=%{text}\u003cextra\u003e\u003c\u002fextra\u003e",
 legendgroup: "Female",
 marker: {
 color: "#636efa",
 pattern: { shape: "" },
 },
 name: "Female",
 offsetgroup: "Female",
 orientation: "v",
 showlegend: true,
 text: [
 "Female \u2192 Female\u003cbr\u003eCount: 504",
 "Male \u2192 Female\u003cbr\u003eCount: 2887",
 "Other \u2192 Female\u003cbr\u003eCount: 15",
 ],
 textposition: "outside",
 x: ["Female", "Male", "Other"],
 xaxis: "x",
 y: [504, 2887, 15],
 yaxis: "y",
 type: "bar",
 },
 {
 alignmentgroup: "True",
 hovertemplate:
 "Enslaved Person Gender=Male\u003cbr\u003eEnslaver Gender=%{x}\u003cbr\u003eNumber of Ads=%{y}\u003cbr\u003elabel=%{text}\u003cextra\u003e\u003c\u002fextra\u003e",
 legendgroup: "Male",
 marker: {
 color: "#EF553B",
 pattern: { shape: "" },
 },
 name: "Male",
 offsetgroup: "Male",
 orientation: "v",
 showlegend: true,
 text: [
 "Female \u2192 Male\u003cbr\u003eCount: 765",
 "Male \u2192 Male\u003cbr\u003eCount: 12973",
 "Other \u2192 Male\u003cbr\u003eCount: 154",
 ],
 textposition: "outside",
 x: ["Female", "Male", "Other"],
 xaxis: "x",
 y: [765, 12973, 154],
 yaxis: "y",
 type: "bar",
 },
 {
 alignmentgroup: "True",
 hovertemplate:
 "Enslaved Person Gender=Other\u003cbr\u003eEnslaver Gender=%{x}\u003cbr\u003eNumber of Ads=%{y}\u003cbr\u003elabel=%{text}\u003cextra\u003e\u003c\u002fextra\u003e",
 legendgroup: "Other",
 marker: {
 color: "#00cc96",
 pattern: { shape: "" },
 },
 name: "Other",
 offsetgroup: "Other",
 orientation: "v",
 showlegend: true,
 text: ["Male \u2192 Other\u003cbr\u003eCount: 8"],
 textposition: "outside",
 x: ["Male"],
 xaxis: "x",
 y: [8],
 yaxis: "y",
 type: "bar",
 },
 ],
 {
 template: {
 data: {
 histogram2dcontour: [
 {
 type: "histogram2dcontour",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 choropleth: [
 {
 type: "choropleth",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 histogram2d: [
 {
 type: "histogram2d",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 heatmap: [
 {
 type: "heatmap",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 heatmapgl: [
 {
 type: "heatmapgl",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 contourcarpet: [
 {
 type: "contourcarpet",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 contour: [
 {
 type: "contour",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 surface: [
 {
 type: "surface",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 mesh3d: [
 {
 type: "mesh3d",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 scatter: [
 {
 fillpattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 type: "scatter",
 },
 ],
 parcoords: [
 {
 type: "parcoords",
 line: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterpolargl: [
 {
 type: "scatterpolargl",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 bar: [
 {
 error\_x: { color: "#2a3f5f" },
 error\_y: { color: "#2a3f5f" },
 marker: {
 line: { color: "#E5ECF6", width: 0.5 },
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "bar",
 },
 ],
 scattergeo: [
 {
 type: "scattergeo",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterpolar: [
 {
 type: "scatterpolar",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 histogram: [
 {
 marker: {
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "histogram",
 },
 ],
 scattergl: [
 {
 type: "scattergl",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatter3d: [
 {
 type: "scatter3d",
 line: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scattermapbox: [
 {
 type: "scattermapbox",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterternary: [
 {
 type: "scatterternary",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scattercarpet: [
 {
 type: "scattercarpet",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 carpet: [
 {
 aaxis: {
 endlinecolor: "#2a3f5f",
 gridcolor: "white",
 linecolor: "white",
 minorgridcolor: "white",
 startlinecolor: "#2a3f5f",
 },
 baxis: {
 endlinecolor: "#2a3f5f",
 gridcolor: "white",
 linecolor: "white",
 minorgridcolor: "white",
 startlinecolor: "#2a3f5f",
 },
 type: "carpet",
 },
 ],
 table: [
 {
 cells: {
 fill: { color: "#EBF0F8" },
 line: { color: "white" },
 },
 header: {
 fill: { color: "#C8D4E3" },
 line: { color: "white" },
 },
 type: "table",
 },
 ],
 barpolar: [
 {
 marker: {
 line: { color: "#E5ECF6", width: 0.5 },
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "barpolar",
 },
 ],
 pie: [{ automargin: true, type: "pie" }],
 },
 layout: {
 autotypenumbers: "strict",
 colorway: [
 "#636efa",
 "#EF553B",
 "#00cc96",
 "#ab63fa",
 "#FFA15A",
 "#19d3f3",
 "#FF6692",
 "#B6E880",
 "#FF97FF",
 "#FECB52",
 ],
 font: { color: "#2a3f5f" },
 hovermode: "closest",
 hoverlabel: { align: "left" },
 paper\_bgcolor: "white",
 plot\_bgcolor: "#E5ECF6",
 polar: {
 bgcolor: "#E5ECF6",
 angularaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 radialaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 },
 ternary: {
 bgcolor: "#E5ECF6",
 aaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 baxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 caxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 },
 coloraxis: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 colorscale: {
 sequential: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 sequentialminus: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 diverging: [
 [0, "#8e0152"],
 [0.1, "#c51b7d"],
 [0.2, "#de77ae"],
 [0.3, "#f1b6da"],
 [0.4, "#fde0ef"],
 [0.5, "#f7f7f7"],
 [0.6, "#e6f5d0"],
 [0.7, "#b8e186"],
 [0.8, "#7fbc41"],
 [0.9, "#4d9221"],
 [1, "#276419"],
 ],
 },
 xaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 title: { standoff: 15 },
 zerolinecolor: "white",
 automargin: true,
 zerolinewidth: 2,
 },
 yaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 title: { standoff: 15 },
 zerolinecolor: "white",
 automargin: true,
 zerolinewidth: 2,
 },
 scene: {
 xaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 yaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 zaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 },
 shapedefaults: { line: { color: "#2a3f5f" } },
 annotationdefaults: {
 arrowcolor: "#2a3f5f",
 arrowhead: 0,
 arrowwidth: 1,
 },
 geo: {
 bgcolor: "white",
 landcolor: "#E5ECF6",
 subunitcolor: "white",
 showland: true,
 showlakes: true,
 lakecolor: "white",
 },
 title: { x: 0.05 },
 mapbox: { style: "light" },
 },
 },
 xaxis: {
 anchor: "y",
 domain: [0.0, 1.0],
 title: { text: "Enslaver Gender" },
 },
 yaxis: {
 anchor: "x",
 domain: [0.0, 1.0],
 title: { text: "Number of Ads" },
 },
 legend: {
 title: { text: "Enslaved Person Gender" },
 tracegroupgap: 0,
 },
 title: {
 text: "Relationship Between Enslaver Gender and Enslaved Person Gender",
 },
 barmode: "group",
 uniformtext: { minsize: 8, mode: "hide" },
 },
 { responsive: true },
 ).then(function () {
 var gd = document.getElementById(
 "16eb7c5b-971f-4f79-9a2e-b3818af4537e",
 );
 var x = new MutationObserver(function (
 mutations,
 observer,
 ) {
 {
 var display = window.getComputedStyle(gd).display;
 if (!display || display === "none") {
 {
 console.log([gd, "removed!"]);
 Plotly.purge(gd);
 observer.disconnect();
 }
 }
 }
 });

 // Listen for the removal of the full notebook cells
 var notebookContainer = gd.closest(
 "#notebook-container",
 );
 if (notebookContainer) {
 {
 x.observe(notebookContainer, { childList: true });
 }
 }

 // Listen for the clearing of the current output cell
 var outputEl = gd.closest(".output");
 if (outputEl) {
 {
 x.observe(outputEl, { childList: true });
 }
 }
 });
 }
 });
 













 In the advertisements for runaway slaves posted by male slave
 owners, the wanted ones were mostly male, while in the
 advertisements posted by female slave owners, the proportion of
 male and female runaway slaves was closer or even tended to be
 balanced. This phenomenon may reflect the management biases of
 slave owners of different genders towards the role of slaves:
 Male slave owners were more likely to manage male slaves engaged
 in heavy manual labor, while female slave owners might be more
 involved in the management of indoor workers, women or domestic
 slaves. Furthermore, male slave owners, having a larger number
 of enslaved individuals, also posted a much higher total amount
 of advertisements than female slave owners.
 



 This gender combination structure confirms the normalization of
 gender division of labor in slavery. Gender is not only a
 physical attribute of the enslaved, but also profoundly involved
 in institutional control and historical records.
 












#### 
**State**[¶](#State)



 The act of runaway slaves does not occur evenly in all regions,
 it shows a distinct concentration trend in geographical space.
 The places where advertisements are released reflect the active
 areas of institutional control and also reveal from the side the
 degree of infiltration of slavery in different states.
 










In [76]:




```
import folium
import requests
df\_state\_valid = df\_s[df\_s['newspaper\_location\_state'] != 'Not\_Provided'].copy()
df\_state\_valid['State Abbr'] = df\_state\_valid['newspaper\_location\_state'].str[-2:].str.upper()
state\_counts = df\_state\_valid['State Abbr'].value\_counts().reset\_index()
state\_counts.columns = ['State Abbr', 'Number of Runaway Ads']
abbr\_to\_name = {
    'AL': 'Alabama', 'AR': 'Arkansas', 'CT': 'Connecticut', 'DE': 'Delaware', 'FL': 'Florida',
    'GA': 'Georgia', 'IL': 'Illinois', 'IN': 'Indiana', 'IA': 'Iowa', 'KY': 'Kentucky',
    'LA': 'Louisiana', 'MD': 'Maryland', 'MA': 'Massachusetts', 'MI': 'Michigan', 'MN': 'Minnesota',
    'MS': 'Mississippi', 'MO': 'Missouri', 'NC': 'North Carolina', 'NJ': 'New Jersey',
    'NY': 'New York', 'OH': 'Ohio', 'PA': 'Pennsylvania', 'SC': 'South Carolina',
    'TN': 'Tennessee', 'TX': 'Texas', 'VA': 'Virginia', 'WI': 'Wisconsin', 'DC': 'District of Columbia',
    'NH': 'New Hampshire', 'RI': 'Rhode Island'
}
state\_counts['State'] = state\_counts['State Abbr'].map(abbr\_to\_name)
state\_counts = state\_counts.dropna()
geo\_url = 'https://raw.githubusercontent.com/python-visualization/folium/master/examples/data/us-states.json'
geo\_data = requests.get(geo\_url).json()
state\_coords = {
    'AL': (32.3182, -86.9023), 'AR': (34.9697, -92.3731), 'CT': (41.6032, -72.7554),
    'DE': (38.9108, -75.5277), 'FL': (27.6648, -81.5158), 'GA': (32.1656, -82.9001),
    'IL': (40.6331, -89.3985), 'IN': (40.2672, -86.1260), 'IA': (41.8780, -93.0977),
    'KY': (37.8393, -84.2700), 'LA': (30.9843, -91.9623), 'MD': (39.0458, -76.6413),
    'MA': (42.4072, -71.3824), 'MI': (44.3148, -85.6024), 'MN': (46.7296, -94.6859),
    'MS': (32.3547, -89.3985), 'MO': (37.9643, -91.8318), 'NC': (35.7596, -79.0193),
    'NJ': (40.0583, -74.4057), 'NY': (43.0000, -75.4999), 'OH': (40.4173, -82.9071),
    'PA': (41.2033, -77.1945), 'SC': (33.8361, -81.1637), 'TN': (35.5175, -86.5804),
    'TX': (31.9686, -99.9018), 'VA': (37.4316, -78.6569), 'WI': (43.7844, -88.7879),
    'DC': (38.9072, -77.0369), 'NH': (43.1939, -71.5724), 'RI': (41.5801, -71.4774)
}
state\_counts['lat'] = state\_counts['State Abbr'].map(lambda x: state\_coords.get(x, (None, None))[0])
state\_counts['lon'] = state\_counts['State Abbr'].map(lambda x: state\_coords.get(x, (None, None))[1])
m = folium.Map(location=[37.8, -96], zoom\_start=4)
folium.Choropleth(
    geo\_data=geo\_data,
    data=state\_counts,
    columns=['State', 'Number of Runaway Ads'],
    key\_on='feature.properties.name',
    fill\_color='YlOrRd',
    fill\_opacity=0.7,
    line\_opacity=0.3,
    legend\_name='Number of Runaway Ads'
).add\_to(m)
for \_, row in state\_counts.iterrows():
    if pd.notna(row['lat']) and pd.notna(row['lon']):
        folium.Marker(
            location=[row['lat'], row['lon']],
            icon=folium.DivIcon(html=f"""
 <div style="font-size: 10pt; color: black; text-align: center;">
 <b>{row['State Abbr']}</b><br>{row['Number of Runaway Ads']}
 </div>
 """)
        ).add\_to(m)
m

```










Out[76]:



Make this Notebook Trusted to load map: File -> Trust
 Notebook














 The map shows the geographical distribution of runaway slave
 advertisements in each state of the United States. It can be
 clearly seen from the map that the density of fugitive slave
 advertisements is generally high in the southern states,
 especially in states such as Louisiana (LA), South Carolina
 (SC), and North Carolina (NC), where these areas have become the
 regions with the densest fugitive slave advertisements. This
 trend is highly consistent with the spatial structure of the
 slavery system: The southern United States long relied on the
 plantation economy centered on cotton, tobacco and sugarcane,
 and was highly dependent on slave labor, directly leading to a
 large concentration of the enslaved population.
 












#### 
**Year**[¶](#Year)



 The number of advertisements released at the same time not only
 records the frequency of the act of runaway slaves themselves,
 but also reflects the changes in the slave owners' sense of
 security towards the system, the degree of social support or
 questioning of slavery, as well as the rebellious sentiments of
 the slaves themselves. By statistically analyzing the changing
 trends of the number of advertisements in different periods, we
 can identify the key historical nodes of slavery and observe
 when resistance behaviors concentrated and erupted and when they
 tended to decline.
 










In [80]:




```
df\_year\_valid = df\_s[df\_s['publication\_year'].apply(lambda x: str(x).isdigit())].copy()
df\_year\_valid['publication\_year'] = df\_year\_valid['publication\_year'].astype(int)
year\_counts = df\_year\_valid['publication\_year'].value\_counts().sort\_index().reset\_index()
year\_counts.columns = ['Year', 'Number of Runaway Ads']
top\_years = year\_counts.sort\_values('Number of Runaway Ads', ascending=False).head(5)
fig = px.line(
    year\_counts,
    x='Year',
    y='Number of Runaway Ads',
    title='Runaway Slave Advertisements by Year (Top 5 Labeled)',
    markers=True
)
offsets = [-50, -80, -30, -60, -40]
for i, (\_, row) in enumerate(top\_years.iterrows()):
    fig.add\_annotation(
        x=row['Year'],
        y=row['Number of Runaway Ads'],
        text=f"Year: {row['Year']}<br>Count: {row['Number of Runaway Ads']}",
        showarrow=True,
        arrowhead=1,
        ax=0,
        ay=offsets[i % len(offsets)],
        font=dict(size=10)  
    )
fig.update\_layout(
    xaxis\_title='Year',
    yaxis\_title='Number of Ads'
)
fig.show()

```















 require(["plotly"], function (Plotly) {
 window.PLOTLYENV = window.PLOTLYENV || {};
 if (
 document.getElementById(
 "e4ee2caf-df2e-4560-ae3a-c2279d8fee49",
 )
 ) {
 Plotly.newPlot(
 "e4ee2caf-df2e-4560-ae3a-c2279d8fee49",
 [
 {
 hovertemplate:
 "Year=%{x}\u003cbr\u003eNumber of Runaway Ads=%{y}\u003cextra\u003e\u003c\u002fextra\u003e",
 legendgroup: "",
 line: { color: "#636efa", dash: "solid" },
 marker: { symbol: "circle" },
 mode: "lines+markers",
 name: "",
 orientation: "v",
 showlegend: false,
 x: [
 1704, 1708, 1711, 1712, 1714, 1716, 1720, 1721,
 1722, 1723, 1724, 1726, 1727, 1728, 1729, 1730,
 1731, 1732, 1733, 1734, 1735, 1736, 1737, 1738,
 1739, 1740, 1741, 1742, 1743, 1744, 1745, 1746,
 1747, 1748, 1749, 1750, 1751, 1752, 1753, 1754,
 1755, 1756, 1757, 1758, 1759, 1760, 1761, 1762,
 1763, 1764, 1765, 1766, 1767, 1768, 1769, 1770,
 1771, 1772, 1773, 1774, 1775, 1776, 1777, 1778,
 1779, 1780, 1781, 1782, 1783, 1784, 1785, 1786,
 1787, 1788, 1789, 1790, 1791, 1792, 1793, 1794,
 1795, 1796, 1797, 1798, 1799, 1800, 1801, 1802,
 1803, 1804, 1805, 1806, 1807, 1808, 1809, 1810,
 1811, 1812, 1813, 1814, 1815, 1816, 1817, 1818,
 1819, 1820, 1821, 1822, 1823, 1824, 1825, 1826,
 1827, 1828, 1829, 1830, 1831, 1832, 1833, 1834,
 1835, 1836, 1837, 1838, 1839, 1840, 1841, 1842,
 1843, 1844, 1845, 1846, 1847, 1848, 1849, 1850,
 1851, 1852, 1853, 1854, 1855, 1856, 1857, 1858,
 1859, 1860, 1861, 1862, 1863, 1864, 1865, 1866,
 1867, 1868, 1872, 1874, 1894,
 ],
 xaxis: "x",
 y: [
 2, 1, 2, 4, 1, 1, 1, 2, 1, 1, 4, 1, 2, 1, 3, 6,
 1, 4, 5, 9, 7, 7, 10, 13, 2, 8, 1, 5, 3, 6, 22,
 20, 17, 28, 29, 18, 17, 10, 18, 20, 20, 24, 26,
 18, 35, 21, 28, 40, 48, 66, 74, 43, 34, 61, 65,
 43, 22, 25, 38, 97, 94, 58, 82, 89, 71, 99, 256,
 124, 163, 91, 105, 72, 87, 127, 73, 154, 39, 79,
 84, 99, 108, 103, 146, 20, 16, 36, 105, 109,
 246, 298, 303, 537, 309, 185, 215, 47, 33, 26,
 29, 35, 18, 37, 55, 153, 79, 132, 138, 521, 179,
 209, 728, 581, 89, 2761, 402, 129, 340, 658,
 159, 232, 533, 602, 858, 635, 215, 1030, 265,
 182, 130, 805, 483, 1185, 341, 178, 151, 96,
 156, 117, 377, 1709, 127, 98, 87, 86, 78, 176,
 158, 113, 164, 164, 26, 5, 4, 1, 1, 2, 1,
 ],
 yaxis: "y",
 type: "scatter",
 },
 ],
 {
 template: {
 data: {
 histogram2dcontour: [
 {
 type: "histogram2dcontour",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 choropleth: [
 {
 type: "choropleth",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 histogram2d: [
 {
 type: "histogram2d",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 heatmap: [
 {
 type: "heatmap",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 heatmapgl: [
 {
 type: "heatmapgl",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 contourcarpet: [
 {
 type: "contourcarpet",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 contour: [
 {
 type: "contour",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 surface: [
 {
 type: "surface",
 colorbar: { outlinewidth: 0, ticks: "" },
 colorscale: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 },
 ],
 mesh3d: [
 {
 type: "mesh3d",
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 ],
 scatter: [
 {
 fillpattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 type: "scatter",
 },
 ],
 parcoords: [
 {
 type: "parcoords",
 line: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterpolargl: [
 {
 type: "scatterpolargl",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 bar: [
 {
 error\_x: { color: "#2a3f5f" },
 error\_y: { color: "#2a3f5f" },
 marker: {
 line: { color: "#E5ECF6", width: 0.5 },
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "bar",
 },
 ],
 scattergeo: [
 {
 type: "scattergeo",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterpolar: [
 {
 type: "scatterpolar",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 histogram: [
 {
 marker: {
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "histogram",
 },
 ],
 scattergl: [
 {
 type: "scattergl",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatter3d: [
 {
 type: "scatter3d",
 line: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scattermapbox: [
 {
 type: "scattermapbox",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scatterternary: [
 {
 type: "scatterternary",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 scattercarpet: [
 {
 type: "scattercarpet",
 marker: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 },
 ],
 carpet: [
 {
 aaxis: {
 endlinecolor: "#2a3f5f",
 gridcolor: "white",
 linecolor: "white",
 minorgridcolor: "white",
 startlinecolor: "#2a3f5f",
 },
 baxis: {
 endlinecolor: "#2a3f5f",
 gridcolor: "white",
 linecolor: "white",
 minorgridcolor: "white",
 startlinecolor: "#2a3f5f",
 },
 type: "carpet",
 },
 ],
 table: [
 {
 cells: {
 fill: { color: "#EBF0F8" },
 line: { color: "white" },
 },
 header: {
 fill: { color: "#C8D4E3" },
 line: { color: "white" },
 },
 type: "table",
 },
 ],
 barpolar: [
 {
 marker: {
 line: { color: "#E5ECF6", width: 0.5 },
 pattern: {
 fillmode: "overlay",
 size: 10,
 solidity: 0.2,
 },
 },
 type: "barpolar",
 },
 ],
 pie: [{ automargin: true, type: "pie" }],
 },
 layout: {
 autotypenumbers: "strict",
 colorway: [
 "#636efa",
 "#EF553B",
 "#00cc96",
 "#ab63fa",
 "#FFA15A",
 "#19d3f3",
 "#FF6692",
 "#B6E880",
 "#FF97FF",
 "#FECB52",
 ],
 font: { color: "#2a3f5f" },
 hovermode: "closest",
 hoverlabel: { align: "left" },
 paper\_bgcolor: "white",
 plot\_bgcolor: "#E5ECF6",
 polar: {
 bgcolor: "#E5ECF6",
 angularaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 radialaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 },
 ternary: {
 bgcolor: "#E5ECF6",
 aaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 baxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 caxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 },
 },
 coloraxis: {
 colorbar: { outlinewidth: 0, ticks: "" },
 },
 colorscale: {
 sequential: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 sequentialminus: [
 [0.0, "#0d0887"],
 [0.1111111111111111, "#46039f"],
 [0.2222222222222222, "#7201a8"],
 [0.3333333333333333, "#9c179e"],
 [0.4444444444444444, "#bd3786"],
 [0.5555555555555556, "#d8576b"],
 [0.6666666666666666, "#ed7953"],
 [0.7777777777777778, "#fb9f3a"],
 [0.8888888888888888, "#fdca26"],
 [1.0, "#f0f921"],
 ],
 diverging: [
 [0, "#8e0152"],
 [0.1, "#c51b7d"],
 [0.2, "#de77ae"],
 [0.3, "#f1b6da"],
 [0.4, "#fde0ef"],
 [0.5, "#f7f7f7"],
 [0.6, "#e6f5d0"],
 [0.7, "#b8e186"],
 [0.8, "#7fbc41"],
 [0.9, "#4d9221"],
 [1, "#276419"],
 ],
 },
 xaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 title: { standoff: 15 },
 zerolinecolor: "white",
 automargin: true,
 zerolinewidth: 2,
 },
 yaxis: {
 gridcolor: "white",
 linecolor: "white",
 ticks: "",
 title: { standoff: 15 },
 zerolinecolor: "white",
 automargin: true,
 zerolinewidth: 2,
 },
 scene: {
 xaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 yaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 zaxis: {
 backgroundcolor: "#E5ECF6",
 gridcolor: "white",
 linecolor: "white",
 showbackground: true,
 ticks: "",
 zerolinecolor: "white",
 gridwidth: 2,
 },
 },
 shapedefaults: { line: { color: "#2a3f5f" } },
 annotationdefaults: {
 arrowcolor: "#2a3f5f",
 arrowhead: 0,
 arrowwidth: 1,
 },
 geo: {
 bgcolor: "white",
 landcolor: "#E5ECF6",
 subunitcolor: "white",
 showland: true,
 showlakes: true,
 lakecolor: "white",
 },
 title: { x: 0.05 },
 mapbox: { style: "light" },
 },
 },
 xaxis: {
 anchor: "y",
 domain: [0.0, 1.0],
 title: { text: "Year" },
 },
 yaxis: {
 anchor: "x",
 domain: [0.0, 1.0],
 title: { text: "Number of Ads" },
 },
 legend: { tracegroupgap: 0 },
 title: {
 text: "Runaway Slave Advertisements by Year (Top 5 Labeled)",
 },
 annotations: [
 {
 arrowhead: 1,
 ax: 0,
 ay: -50,
 font: { size: 10 },
 showarrow: true,
 text: "Year: 1828\u003cbr\u003eCount: 2761",
 x: 1828,
 y: 2761,
 },
 {
 arrowhead: 1,
 ax: 0,
 ay: -80,
 font: { size: 10 },
 showarrow: true,
 text: "Year: 1854\u003cbr\u003eCount: 1709",
 x: 1854,
 y: 1709,
 },
 {
 arrowhead: 1,
 ax: 0,
 ay: -30,
 font: { size: 10 },
 showarrow: true,
 text: "Year: 1846\u003cbr\u003eCount: 1185",
 x: 1846,
 y: 1185,
 },
 {
 arrowhead: 1,
 ax: 0,
 ay: -60,
 font: { size: 10 },
 showarrow: true,
 text: "Year: 1840\u003cbr\u003eCount: 1030",
 x: 1840,
 y: 1030,
 },
 {
 arrowhead: 1,
 ax: 0,
 ay: -40,
 font: { size: 10 },
 showarrow: true,
 text: "Year: 1837\u003cbr\u003eCount: 858",
 x: 1837,
 y: 858,
 },
 ],
 },
 { responsive: true },
 ).then(function () {
 var gd = document.getElementById(
 "e4ee2caf-df2e-4560-ae3a-c2279d8fee49",
 );
 var x = new MutationObserver(function (
 mutations,
 observer,
 ) {
 {
 var display = window.getComputedStyle(gd).display;
 if (!display || display === "none") {
 {
 console.log([gd, "removed!"]);
 Plotly.purge(gd);
 observer.disconnect();
 }
 }
 }
 });

 // Listen for the removal of the full notebook cells
 var notebookContainer = gd.closest(
 "#notebook-container",
 );
 if (notebookContainer) {
 {
 x.observe(notebookContainer, { childList: true });
 }
 }

 // Listen for the clearing of the current output cell
 var outputEl = gd.closest(".output");
 if (outputEl) {
 {
 x.observe(outputEl, { childList: true });
 }
 }
 });
 }
 });
 













 First of all, it is worth noting that from 1828, the number of
 advertisements for runaway slaves began to increase
 significantly. This trend occurred before the Nat Turner's
 Rebellion in 1831 and might reflect the accumulation of tensions
 within the slave society. The increase in the act of runaway
 slaves not only implies the direct resistance of individuals
 against the oppressive system, but can also be regarded as a
 precursor to the brewing process of larger-scale slave
 uprisings. Slave owners strengthened their manhunt through
 newspapers, which was also a means of enhanced control they
 adopted when trust in the system began to waver.
 



 Entering the 1850s, there was a second surge in the number of
 advertisements, and the key legal turning point behind it was
 the enactment of the "Fugitive Slave Act of 1850". This act
 forced the northern states to assist the southern slave owners
 in hunting down runaway slaves and imposed severe penalties on
 those who did so, greatly expanding the legal dissemination
 range of runaway slave advertisements. The outbreak of the
 "Bloody Kansas" incident in 1854 marked that the controversy
 over slavery had expanded into a national conflict. Under such a
 political atmosphere, the number of runaway slaves rose
 simultaneously with the volume of advertisements released,
 reflecting the high alertness of slave owners to the risk of
 institutional collapse.
 



 The chart shows a significant decline in the number of
 advertisements around 1860. This change was kind of related to
 Lincoln's election as president, the successive secession of the
 southern states from the Union. Against the backdrop of
 fundamental questioning of the legitimacy of the system and the
 country falling into a crisis of division, the executive power
 and public opinion control of the slavery system weakened
 significantly. The decline in the number of advertisements for
 runaway slaves may reflect both the problems brought about by
 the disintegration of the system and the gradual loss of the
 ability of slave owners to control "property" on the verge of
 disorder.
 












### 
 Conclusion[¶](#Conclusion)



 This study holds that the advertisements for runaway slaves
 reveal a highly structured slavery system: men, young and
 middle-aged people, and enslaved individuals in southern states
 are more likely to become the "escapees" visible in the
 advertisements, and the gender and geographical location of the
 slave owners also have significant influences. The advertisement
 of fleeing slaves not only records the individual's rebellious
 behavior, but also reflects a structured slave society where all
 the path of runaway slaves are traceable.
 



 More broadly, this dataset is located in the core cultural
 context of slavery in the United States, an era when slaves were
 managed, wanted and commercialized as property. Although these
 advertisements were written by slave owners with the original
 intention of capturing "escaped property", today, they have
 instead become evidence of the identity, resistance and
 expression of the enslaved. The use of such data requires
 sensitivity: We must be aware that the data source itself is the
 product of the oppressive system. We cannot consume its content
 from a neutral perspective, but should reveal the power
 structure, silent scars and the continuation of historical
 inequality behind it with a reflective attitude.
 













[project github page](https://github.com/GHuangJiawen/research-project)













### 
 Bibliography[¶](#Bibliography)


[Data Source](https://freedomonthemove.org/)



[Fugitive Slave Advertisements and the Rebelliousness of
 Enslaved People in Georgia and Maryland, 1790-1810.](https://dspace.stir.ac.uk/bitstream/1893/26591/1/Shaun%20Wallace%20Final%20Version%20PhD%20Thesis.pdf?)








