# Ontario Travel Project 1

## Description of the Project 

This project aims to examine the impact of the COVID-19 impact on Ontario's tourism industry, by comparing trends across the airline, hotel & restaurant industries both before, during, and after COVID-19.  

The analysis we're going to do is: 
1. Total passengers screened at Canada's Top 8 & 17 airports from 2018-2023
2. Hotels' Average Daily Rate, Occupancy and Revenue per Available Room from 2018-2023, including yearly and monthly. 
3. Overall drink sales from 2018-2023
4. Restaurant Average Reviews by Location
5. Restaurant Operation Status 

The questions we're going to answer are: 
1. How does passenger volume post-COVID compare to pre-COVID?
2. Is there a difference in passenger volume between the Top 8 Airports & Top 17 Airports? 
3. How has Hotels' Average Daily Rate(ADR) and Occupancy changed during these time periods?
4. How has Hotels' ADR changed in 2023, and is there a significant difference between different geographical areas? 
5. How have drink sales changed during this period? 
6. How has the state of the restaurant industry changed? 

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
2. Tripadvisor API (https://api.content.tripadvisor.com/api/v1/location/)
3. Traveladvisor API (https://rapidapi.com/apidojo/api/travel-advisor)
4. Google Places API (https://developers.google.com/maps/documentation/places/web-service/overview)
5. Catsa-Acsta Passenger Data (https://www.catsa-acsta.gc.ca/en/screened-passenger-data)
6. Sales of Drinking Places Canada 2023 (https://www.statista.com/statistics/323660/sales-of-drinking-places-in-canada/)
7. Hotel Statistics (multi-year) (https://data.ontario.ca/dataset/947f4c51-7613-4279-9fd8-2e3d09be307a/resource/fdbd6ea8-a664-4422-8aab-8abca205df44/download/mtcs-hotel-performance-en-2022.xlsx)

## Code snippets
Cleaning Data by Date: 
```
# Create start_date and end_date to desired date range
start_date = '2023-01-01'
end_date = '2023-12-03'

# Convert the "Date" column to a datetime object if it's not already
flight_df['Date'] = pd.to_datetime(flight_df['Date'], errors='coerce')

# Filter rows based on the specified date range
filtered_df = flight_df[(flight_df['Date'] >= start_date) & (flight_df['Date'] <= end_date)]
```
Using iloc and for loop to extract Excel data into data frame: 
```
# Extract Data by year 
for i in year_list:
    
    df = pd.read_excel('Resources/mtcs-hotel-performance-en-2022.xlsx', sheet_name = i )
    new_df = df.dropna(how ='all').dropna(how='all', axis = 1)
    new_df.reset_index(drop = True, inplace=True)

    columns_to_keep = [0,1,4,7]
    new_df = new_df.iloc[ :, columns_to_keep]
    new_columns = {
         'Unnamed: 1' : 'Area',
         'Unnamed: 2' : f'{i} Occupancy Percentage',
         'Unnamed: 6' : f'{i}Average Daily Rate',
         'Unnamed: 10': f'{i} Revenue Per Available Room'
     }

    new_df.rename(columns = new_columns, inplace = True)
    new_df = new_df.iloc[3:-2:]
    new_df.reset_index(drop = True, inplace=True)
```

Using Google Places API: 
```
locations = [["43.651070,-79.347015"],["45.5019,-73.5674"],["51.0447,-114.0719"]
             ,["45.4215,-75.6972"],["53.5461,-113.4937"],["49.8954,-97.1385"],
             ["43.5890,-79.6441"],["49.2827,-123.1207"],["43.7315,-79.7624"],
             ["43.2557,-79.8711"]]
  gmaps = googlemaps.Client(key = google_api_key)

res_add = []
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


df_res = pd.DataFrame(res_data)
```

## Analysis 

## Flights
![alt text](https://github.com/AleMori22/Project_1_repo/blob/main/output/Screened_Passengers_Top_8_Airports.png)
![alt text](https://github.com/AleMori22/Project_1_repo/blob/main/output/Screened_Passengers_Top_17_Airports.png)

By comparing the yearly summary for screened passengers, we can see that 2022 & 2023's passenger counts have significantly increased over 2020 & 2021's passenger counts, yet have not yet caught up to 2019. 2022's performance is greater when factoring smaller regional airports included in the top 17 airports compared to only the top 8 airports. 

## Hotels 

![alt text](https://github.com/AleMori22/Project_1_repo/blob/main/output/Average_Daily_Rate_by_Year.png)
![alt text](https://github.com/AleMori22/Project_1_repo/blob/main/output/Occupancy_Percentage_by_Year.png)
![alt text](https://github.com/AleMori22/Project_1_repo/blob/main/output/Revenue_Per_Available_Room_Year.png)
![alt text](https://github.com/AleMori22/Project_1_repo/blob/main/Graph_data/Figure1.png)
![alt text](https://github.com/AleMori22/Project_1_repo/blob/main/Graph_data/Figure2.png)

In analyzing statistics provided by the Ontario government, Average Daily Rates & Revenue Per Available Room have all appeared to have recovered to pre-COVID levels, however Occupancy rates are still below pre-COVID levels. 
When looking at Revenue Per Available Room across different areas in Ontario, we can see that Downtown Toronto has the highest value, followered by Greater Toronto. Eastern Ontario has the lowest value. 


## Restaurants
![alt_text](https://github.com/AleMori22/Project_1_repo/blob/main/output/Drinking_Plot.png)
![alt text](https://github.com/AleMori22/Project_1_repo/blob/main/output/Buisness%20Status.png)
![alt text](https://github.com/AleMori22/Project_1_repo/blob/main/output/Relevant_Review.png)
![alt text](https://github.com/AleMori22/Project_1_repo/blob/main/output/Locations_map.png)
![alt text](https://github.com/AleMori22/Project_1_repo/blob/main/output/average_review_plot.png)

When looking at the monthly sales of drinking restaurants throughout Canada we get a good indication of how the industry is faring. The analysis is split into three parts, pre-covid, COVID and post-covid. When looking at the pre-covid (March 2018 – February 2020) we have an average monthly sale of 208.91 thousand dollars. With July 2019 having the highest sales of 224.55 thousand dollars. his is our baseline of how the drinking industry was thriving and the point at which we are trying to return. It is to be noted that for this analysis, January and February were omitted due to the lack of data, causing the two to be outliers.
During covid (March 2020 – January 2022), sales dropped to significantly to an average of 109 thousand dollars monthly. This was expected due to the travel limitations set during the quarantine. As well as the inability to go visit bars, pubs, and restaurants. This period showcased the lowest sales with April 2020 being the lowest at 19.09 thousand dollars.
With COVID-19 still being an ongoing issue, it is hard to pinpoint an exact date at which the pandemic “ended”. For this analysis, the post-covid period was set to April 2020 – August 2023. The average monthly sales amount to an average of 209.94 thousand per month. Comparing this to our baseline, we can see that the post-covid period exceeded the pre-covid market sales. This period had the second highest number of sales with 222.04 thousand dollars in January 2023.



## Limitations
- Amadeus API initially  looked promising for flight data, but only returns success/failure messages in test environment, data is only available in production but a successful app must be developed to enter production environment. 
- For what concerns the tripadvisor API drill we found some limitations when it came to finding restaurant reviews. In fact the API, for every call, returns just the last five reviews for each restaurant in the book. This limitation though is neglectable. We used this API to analyze a sample of the restaurants located in the hotspots in analysis, in order to have a general understanding of the state of the restaurant's market right now.
- Restaurant industry does not appear to have datasets that are detailed or big enough when compared to hotel industry. This might be due to the fact that restaurants require almost no information to their customers and are not obligated to take records of their clients and operations like hotels are. 
- Hotel data sources are limited to government databases and no large datasets or APIs for Hotel Data could be found. 
- Scarce data for 2023 which made comparisons of pre-COVID and post-COVID difficult. 

