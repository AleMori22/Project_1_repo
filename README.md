# Ontario Travel Project 1

## Description of the Project 

This project aims to examine the impact of the COVID-19 impact on Ontario's tourism industry, by comparing trends across the airline, hotel & restaurant industries both before, during, and after COVID-19.  

The analysis we're going to do is .. 
1. Total passengers screened at Canada's Top 8 & 17 airports from 2018-2023
2. Hospitality industry pre and post pandemic status. 
3. Hotel/Vacation Rentals Occupancies from 2018-2023
4. Traveler changes from Pre-COVID & Post-COVID

The questions we're going to answer are: 
1. How do inbound flights post-COVID compare to pre-COVID?
2. Is there a difference in passenger volumne between the Top 8 Airports & Top 17 Airports? 
3. How has Hotels' Average Daily Rate(ADR) and Occupancy changed during these time periods?
4. How has Hotels' ADR changed through 2022, and is there a significant difference between different geographical areas? 
5. How have drink sales changed during this period? 
6. 

## Members of the group

The members in this group are: 
1. Amy Dryden (@acedryden)
2. Alessandro Mori (@AleMori22)
3. Arti Bhatia (@Artib03)
4. Khemaka Oo (@Khemaka14)
5. Sunghea Cho (@sunghea)

## Work breakdown structure

Flights: Amy
Restaurants: Alessandro & Khemaka 
Hotels: Arti & Sunghea 

## Datasets used: 

1. Geoapify (https://www.geoapify.com/)
2. Catsa-Acsta Passenger Data (https://www.catsa-acsta.gc.ca/en/screened-passenger-data)
3. Tripadvisor API (https://api.content.tripadvisor.com/api/v1/location/)
4. Traveladvisor API (https://rapidapi.com/apidojo/api/travel-advisor)
5. Google Places API (https://developers.google.com/maps/documentation/places/web-service/overview)
6. Sales of Drinking Places Canada 2023 (https://www.statista.com/statistics/323660/sales-of-drinking-places-in-canada/)
7. Hotel Statistics (multi-year)
(https://data.ontario.ca/dataset/947f4c51-7613-4279-9fd8-2e3d09be307a/resource/fdbd6ea8-a664-4422-8aab-8abca205df44/download/mtcs-hotel-performance-en-2022.xlsx)

## Code snippets
'locations = [["43.651070,-79.347015"],["45.5019,-73.5674"],["51.0447,-114.0719"]
             ,["45.4215,-75.6972"],["53.5461,-113.4937"],["49.8954,-97.1385"],
             ["43.5890,-79.6441"],["49.2827,-123.1207"],["43.7315,-79.7624"],
             ["43.2557,-79.8711"]]
gmaps = googlemaps.Client(key = google_api_key)'
'res_add = []
res_status = []
res_name = []

for locs in locations:
    places_result = gmaps.places_nearby(location = locs[0], radius = 40000, open_now = False,type = "restaurant")


    for place in places_result["results"]:

        place_details = gmaps.place(place_id = place["place_id"])
        res_add.append(place_details["result"]["formatted_address"])
        res_status.append(place_details["result"]["business_status"])
        res_name.append(place_details["result"]["name"])

res_data = {
    "Name" : res_name,
    "Address" : res_add,
    "Status" : res_status,

}


df_res = pd.DataFrame(res_data)'

## Analysis 

## Flights
![alt text](https://github.com/AleMori22/Project_1_repo/blob/main/output/Screened_Passengers_Top_8_Airports.png)

## Hotels 
## Restaurants

## Limitations

For what concerns the tripadvisor API drill we found some limitations when it came to finding restaurant reviews. In fact the API, for every call, returns just the last five reviews for each restaurant in the book. This limitation though is neglectable. We used this API to analyze a sample of the restaurants located in the hotspots in analysis, in order to have a general understanding of the state of the restaurant's market right now.
