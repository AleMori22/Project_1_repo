# Ontario Travel Project 1

## Description of the Project 

This project talks about 
1. Traveler Profile : Who is traveling, what is their average income, the reason for their travel, are they traveling alone or with family? etc 
2. Inbound airline traffic comparison at Toronto Pearson (YYZ)
3. Restaurant Gross Revenue Comparison 

The analysis we're going to do is .. 
1. Total yearly inbound flights at Toronto Pearson from 2018-2023
2. Hospitality industry pre and post pandemic status. 
3. Hotel/Vacation Rentals Occupancies from 2018-2023
4. Traveler changes from Pre-COVID & Post-COVID

The questions we're going to answer are: 
1. How do inbound flights post-COVID compare to pre-COVID? 
2. How does overall restaurant revenues post-COVID compare to pre-COVID? 
3. How has the traveler changed post-COVID? 

## Members of the group

The members in this group are: 
1. Amy Dryden (@acedryden)
2. Alessandro Mori (@AleMori22)
3. Arti Bhatia (@Artib03)
4. Khemaka Oo (@Khemaka14)
5. Sung Hea Cho (@sunghea)

## Work breakdown structure

Flights: Amy
Restaurants: Alessandro & Khemaka 
Hotels/Vacation Rentals: Arti & Sung Hea 
Traveler Profile: All 

- Cleaning the airline data to show travellers that actually stay in Toronto/Ontario, not just connecting
- Average performance of restaurants located in touristic areas, drinking spot's monthly sales from 2018 to 2023. 
- Year Scope: Pre-COVID - 2018 & 2019, During Covid - 2020 & 2021, After Covid - 2022 & 2023

## Datasets used: 

1. Geoapify (https://www.geoapify.com/)
2. Amadeus API - Flight Volumne (https://developers.amadeus.com/self-service/category/market-insights/api-doc/flight-busiest-traveling-period/api-reference)
3. StatCan (https://www150.statcan.gc.ca/n1/pub/24-25-0001/242500012020001-eng.htm)
4. Weather API (https://openweathermap.org/api)
5. Catsa-Acsta Passenger Data (https://www.catsa-acsta.gc.ca/en/screened-passenger-data)
6. Hotel Statistics (multi-year)
(https://data.ontario.ca/dataset/947f4c51-7613-4279-9fd8-2e3d09be307a/resource/fdbd6ea8-a664-4422-8aab-8abca205df44/download/mtcs-hotel-performance-en-2022.xlsx)
7. Tripadvisor API (https://api.content.tripadvisor.com/api/v1/location/)

## Code snippets
TBD

## Analysis 

With the script we provided we are trying to analyze the touristic industry from multiple points of view, taking into consideration the flight, restaurant and hotel industry in order to have a picture of the current state of the mentioned markets in 2023 and compare it with the same market's state before the COVID-19 pandemic.

## Limitations

For what concerns the tripadvisor API drill we found some limitations when it came to finding restaurant reviews. In fact the API, for every call, returns just the last five reviews for each restaurant in the book. This limitation though is neglectable. We used this API to analyze a sample of the restaurants located in the hotspots in analysis, in order to have a general understanding of the state of the restaurant's market right now.
