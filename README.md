---
title: "Capstone Documentation"
author: "Jeff K"
date: '2022-04-12'
output: pdf_document
---  

# Covid Fatality Rates  

## Ask
Question: How have Covid Fatality Rates changed in the U.S. since the beginning of the pandemic, and what is the current case fatality rate and the infection fatality rate?

This question is important because if the Covid fatality rate is decreasing, this may indicate it is less of a danger than it was 2 years ago.  It also may indicate that Covid is becoming more of an "endemic" disease like influenza, and its danger to the public may becoming more similar to other endemic diseases, such as influenza.



## Prepare
Data from this project came from ourworldindata.org.   
Hannah Ritchie, Edouard Mathieu, Lucas Rodés-Guirao, Cameron Appel, Charlie Giattino, Esteban Ortiz-Ospina, Joe Hasell, Bobbie Macdonald, Diana Beltekian and Max Roser (2020) - "Coronavirus Pandemic (COVID-19)". Published online at OurWorldInData.org. Retrieved from: 'https://ourworldindata.org/coronavirus' [Online Resource]

In examining the source data carefully, they dataset that I used came from the [COVID-19 Data Repository by the Center for Systems Science and Engineering (CSSE) at Johns Hopkins University.](https://github.com/CSSEGISandData/COVID-19). This data appears to have a high-level of quality and reliability, as evidenced by its being maintained by a large and prestigious public health research university.



## Process
The data was contained in a .csv file called owid-covid-data.csv. This file was imported into BigQuery where it was explored using a series of queries. 

[Link to the SQL Queries in GitHub](https://github.com/jeffkerrpdx/covid-fatality-rates/blob/main/SQL%20Queries)  

--Deaths in the US, cumulative  
SELECT location, date, population, new_cases, total_cases, new_deaths, total_deaths  
FROM `portfolioproject1-346623.covid_deaths.deaths-by-country`  
WHERE location = "United States"  
ORDER BY date  

The last query (shown above) was saved/exported as a .csv file and opened in MS Excel.  A pivot table was created which summarized the number of new cases and the number of deaths per month, from February 2020 until April 2022.  Data from Feb-May 2020 was removed because reliable Covid tests were not available at that time, and the case fatality rate was clearly unreliable without tests being available to the public. Also, the data from March and April 2022 was removed because data on new cases and new deaths is still being compiled at the time of this project.

## Analyze
The question that we are interested in is: how have Covid fatality rates changed since the beginning of the pandemic, and what is the current case fatality rate and infection fatality rates.

The data from Our World in Data clearly shows how the Case Fatality Rate has changed from month to month.  Case Fatality is a simple calculation of the number of deaths each month divided by the number of new cases that month.  There is an issue with the fact that deaths are often a "lagging indicator" and can happen anywhere from 3 days to 60 days after someone contracts Covid. However, this problem should resolve itself since all deaths and all new cases were counted from June 2020 until February 2022.  Some deaths counted the following month may be from cases that were identified the previous month, but they were still counted in the analysis.

Infection Fatality Rate was calculated by multiplying the number of new cases by 4. The CDC estimates that for every Covid case which is identified, there are 4 actual cases that are not identified through testing. There are many reasons for this, but one of the biggest ones is that many infections are asymptomatic and the individuals do not seek testing.  See the CDC website [Estimated Covid-19 Burden](https://www.cdc.gov/coronavirus/2019-ncov/cases-updates/burden.html) for more details. 

The IFR was simply calculated by multiplying the number of new cases by 4 and then dividing the number of new deaths by the IFR. 

These calculations were completed in MS Excel and the results were saved into a .csv file that was then imported into Tableau. 

## Share

The graphic used to illustrate how the Covid Fatality Rate was changed was created in Tableau.  "Date" was used as the Column, and the rows were the SUM(Case Fatality) and SUM(Infection Fatality). The axis was syncronized so that the two rates can be seen in relation to each other.  Marks were created to give each line a separate color and labels were created with a percentage for each month.

The completed line graph can be found here: https://public.tableau.com/app/profile/jeff2871/viz/CovidFatalityEstimatesareDeclining/Sheet5  

## Act

Accurate data about Covid is extremely important to protect both public health and also public trust in our institutions.  If the public is not alerted to the danger of a new virus and steps are not taken to protect them, many people will die needlessly. On the other hand, exaggerations and false information about the seriousness of the threat can erode public trust in institutions and result in a large degree of unwillingness and skepticism on the part of the public to follow public health protocols.

This analysis suggests that fatality rate of Covid has been steadily decreasing from the beginning of the pandemic, based on the data that we have.  It appears that in the first half of 2020, about 2% of reported cases resulted in death, whereas it now appears that about 1% of reported cases result in death. That is good news.  There has been a lot of reporting on the efficacy of vaccines and how vaccines can save lives.

This analysis also suggests that the actual fatality rate is less than the Case Fatality Rate (CFR). Because there are so many underreported cases, the number of Covid infections that result in death is less than the CFR shows. It is actually closer to .5% of cases that result in death.  This is also good news and suggests that for every 1000 people who contract Covid, 995 of them can be expected to survive.

Again, there has been a lot of reporting on how the disease burden of Covid falls on older people and people with co-morbidities such as obesity, diabetes and respiratory conditions which complicate recovery from this illness. 

One limitation to this project is the possible underreporting of Covid deaths. The CDC estimates that Covid-related deaths are being under-reported and for every reported death there are 1.32 actual deaths.  This was not included in the analysis because it requires further research.  There are others who believe that Covid deaths are being over-reported because it sometimes difficult to distinguish between a death CAUSED by Covid, and a person dying who happens to HAVE Covid at the time of their death. More research is needed on this important question. 
