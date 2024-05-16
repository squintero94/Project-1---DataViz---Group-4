# Project_1_Group_4_Masterfile
Create a project repository in GitHub with collaborators.
Work as a group to source data through exploration and research datasets.
Follow the requirements set in the Project Grading Rubric that was provided by instructor via google sheets https://docs.google.com/spreadsheets/d/1f-o6QscCQujfDsjkuqoJjKLLP7wwSvfzZpIPvZ0zoDE/edit#gid=1071228409
Document steps in jupyter notebook as to how the data was clean, organized, and staged to complete analysis.

# Project Title: What is the most popular National Park in the United States?
Team Members: Daniel Pulliam, Kayla Blais, Madeline Rondino, Savi Rahiman & Steven Quintero

# Project Observation and Analysis
If you have ever wondered "What is the most popular National Park in the United States? you've probably searched it on the internet to find countless post surrounding the topic. 

The official NPS.gov website offers a data for traffic counts. This analysis was a complete data export for 2023 at each of the 63 National Parks in the US.
There are 63 National Park in the US. ![alt text](<63 NP plotted on Map.png>)Each of which are plotted on the map. the size of the bubble represents the total Recreation Visits by the park for the year 2023. The Color density represents the % of Recreation Visits. Ranging from 0.012% at the Gates of the Artic National Park in Alaska to 14.4% at the Great Smokey Mountain National Park in Tennessee. 
To determine which National Park was the most popular, our team looked at both the total hours spent in the parks over the 2023 year, and the total number of visits to the parks in the year 2023. The Great Smokey Mountains Park came out on top of both categories with 98,083,629 visitor hours logged in 2023, and 13,297,647 guest visits in 2023. With these numbers, we draw the conclusion that the Great Smokey Mountains Park is the most popular National Park. ![alt text](<Popularity of NP by Visits-1.png>) ![alt text](<Popularity of NP by Hours-1.png>)

Seasonality is also an important factor in visitor traffic. By implementing a seasonality into our data we see that 10.8% of traffic is during the Winter months, 22% is during the Spring months, 26.2% is during the Fall months, and 41% of travel is during the Summer months. ![alt text](<National Park Visitation by Season.png>)

Further more in the data set we calculated the Average Time Spent per Visit by dividing the total hours spent in the park by the total visits. 
Summer had the highest average time spent per person at the parks. During the Summer visitors spent an average of 9.43 hours, during the Spring visitors spent an average of 8.55 hours, during the Fall visitors spent an average of 8.11 hours, and during the Winter visitors spent an average of 7.29 hours in the park. ![alt text](<Average Time Spent per Visit.png>)
![alt text](<Average Time Spent(hrs) per Visit by Season and Region.png>)

Interestingly out of the 6 regions, Alaska had the highest time spent in its parks with an overall of 17 hours spent by visit, with Wrangell-St. Elias National Park at an astounding 46 hours spent. 
![alt text](<Average Time Spent per Visit (Annually).png>)

Utilizing the NPS Data API the park activities were retrieved and showcased exactly why the average time spent at Great Smokey Mountains National Park and Wrangell-St. Elias National Park was vastly different due to the types of activites that are catered to its visitors. ![alt text](<Activities at Wrangell-St. Elias National Park.png>) ![alt text](<Great Smokey Mountains National Park.png>)

In summary the Great Smokey Mountain National Park is the most popular National Park by both the total hours spent in the park and the total number of visits, however based on the interest of the visitors and the type of activity there are countless options such as flying at Wrangell-St. Elias National Park. 


# Data Set
1. National Parks, National Reports Query Builder for Traffic Counts (1985-Last Calendar Year). This report displays monthly or annual traffic counts. 
Link to query builder https://irma.nps.gov/Stats/SSRSReports/National%20Reports/Query%20Builder%20for%20Traffic%20Counts%20(1985%20-%20Last%20Calendar%20Year)
Data for all of 2023 was downloaded and saved in the Resource folder titled "2023_national_park_public_data.csv".
2. The query data set did not include the Latitude and Longitude. Resource on the web such as https://www.latlong.net/ was leveraged to create a list of National Park Names with it's Lat & Lon. This was saved in the Resource folder titled "national_park_names.csv".
3. National Park Service NPS Data API to retrieve activities in select park leveraging the Unit Code provided from the query builder. Documentation on NPS Data API can be found here https://www.nps.gov/subjects/digital/nps-data-api.htm and saved as a jupyter notebook National_Parks_API.ipynb
4. Jupyter notebook that contains methods and codes for cleaning, merging, and coding for analysis and visualizations. Saved as [text](<National Park API/National_Parks.ipynb>)

# Resources
# Jupyter Notebook
Project_1_Group_4_Masterfile.ipynb
National_Parks_API.ipynb
# CSV Files
2023_national_park_public_data.csv
national_park_names.csv
National_Parks_API.csv
# png 
![alt text](<63 NP plotted on Map-2.png>)
![alt text](<Popularity of NP by Visits-3.png>)
![alt text](<Popularity of NP by Hours-3.png>)
![alt text](<National Park Visitation by Season-2.png>)
![alt text](<Average Time Spent per Visit-1.png>)
![alt text](<Average Time Spent(hrs) per Visit by Season and Region-1.png>)
![alt text](<Average Time Spent per Visit (Annually)-1.png>)
![alt text](<Activities at Wrangell-St. Elias National Park-1.png>)
![alt text](<Activities at Great Smokey Mountains National Park.png>)


# Project Description/Outline: 
Using the dataset team 4 will answer the below questions in the form of a powerpoint presentation leveraging visualizations from jupyter notebook  - [text](<National Park API/National_Parks.ipynb>)
1. What is the most popular National Park in the United States?
2. How many National Parks are there and where are they located?
3. What Park is the most popular by hours spend in the park?
4. What park is the most popular by the number of visits?
5. What is the most popular season?
6. What is the average time per visitor spent in the park by season and region?
7. What activities contributed to the most popular National Park?

# Data Cleaning: 

# Import Dependencies
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
from pathlib import Path
from numpy import array
import hvplot.pandas

# CSV Data Set
csv_path_1= Path("Resources/2023_national_park_public_data.csv")
csv_path_2=Path("Resources/national_park_names.csv")
national_parks_complete_df= pd.read_csv(csv_path_1)
location_data_df = pd.read_csv(csv_path_2)

# Clean national_parks_complete_df
# Remove unnecessary columns from the DataFrame and save the new DataFrame
national_parks_reduced_df=national_parks_complete_df[["ParkName","Region", "State","Month","RecreationVisits","RecreationHours","RecreationHoursTotal"]
# Rename headers
national_parks_headers_renamed_df= national_parks_reduced_df.rename(columns={"ParkName":"Park Name",
                                                                    "RecreationVisits":"Recreation Visits by Month",
                                                                    "RecreationHours":"Recreation Hours by Month",
                                                                    "RecreationHoursTotal":"Total Recreation Hours"})
# Rename Park Name to show the official Name of the National Park which is documented in csv_path_2=Path("Resources/national_park_names.csv")
national_parks_rows_renamed_df=national_parks_headers_renamed_df.replace({"Acadia NP":"Acadia National Park",
                                                                          "Arches NP":"Arches National Park",
                                                                          "Badlands NP":"Badlands National Park",
                                                                          "Big Bend NP":"Big Bend National Park",
                                                                          "Biscayne NP":"Biscayne National Park",
                                                                          "Black Canyon of the Gunnison NP":"Black Canyon of the Gunnison National Park",
                                                                          "Bryce Canyon NP":"Bryce Canyon National Park",
                                                                          "Canyonlands NP":"Canyonlands National Park",
                                                                          "Capitol Reef NP":"Capitol Reef National Park",
                                                                          "Carlsbad Caverns NP":"Carlsbad Caverns National Park",
                                                                          "Channel Islands NP":"Channel Islands National Park",
                                                                          "Congaree NP":"Congaree National Park",
                                                                          "Crater Lake NP":"Crater Lake National Park",
                                                                          "Cuyahoga Valley NP":"Cuyahoga Valley National Park",
                                                                          "Death Valley NP":"Death Valley National Park",
                                                                          "Denali NP":"Denali & PRES National Park",
                                                                          "Dry Tortugas NP":"Dry Tortugas National Park",
                                                                          "Everglades NP":"Everglades National Park",
                                                                          "Gates of the Arctic NP":"Gates of the Arctic & PRES National Park",
                                                                          "Gateway Arch NP":"Gateway Arch National Park",
                                                                          "Glacier Bay NP":"Glacier Bay & PRES National Park",
                                                                          "Glacier NP":"Glacier National Park",
                                                                          "Grand Canyon NP":"Grand Canyon National Park",
                                                                          "Grand Teton NP":"Grand Teton National Park",
                                                                          "Great Basin NP":"Great Basin National Park",
                                                                          "Great Sand Dunes NP":"Great Sand Dunes & PRES National Park",
                                                                          "Great Smoky Mountains NP":"Great Smoky Mountains National Park",
                                                                          "Guadalupe Mountains NP":"Guadalupe Mountains National Park",
                                                                          "Haleakala NP":"Haleakala National Park",
                                                                          "Hawaii Volcanoes NP":"Hawaii Volcanoes National Park",
                                                                          "Hot Springs NP":"Hot Springs National Park",
                                                                          "Indiana Dunes NP":"Indiana Dunes National Park",
                                                                          "Isle Royale NP":"Isle Royale National Park",
                                                                          "Joshua Tree NP":"Joshua Tree National Park",
                                                                          "Katmai NP":"Katmai & PRES National Park",
                                                                          "Kenai Fjords NP":"Kenai Fjords National Park",
                                                                          "Kings Canyon NP":"Kings Canyon National Park",
                                                                          "Kobuk Valley NP":"Kobuk Valley National Park",
                                                                          "Lake Clark NP":"Lake Clark & PRES National Park",
                                                                          "Lassen Volcanic NP":"Lassen Volcanic National Park",
                                                                          "Mammoth Cave NP":"Mammoth Cave National Park",
                                                                          "Mesa Verde NP":"Mesa Verde National Park",
                                                                          "Mount Rainier NP":"Mount Rainier National Park",
                                                                          "National Park of American Samoa":"American Samoa National Park",
                                                                          "New River Gorge NP":"New River Gorge & PRES National Park",
                                                                          "North Cascades NP":"North Cascades National Park",
                                                                          "Olympic NP":"Olympic National Park",
                                                                          "Petrified Forest NP":"Petrified Forest National Park",
                                                                          "Pinnacles NP":"Pinnacles National Park",
                                                                          "Redwood NP":"Redwood National Park",
                                                                          "Rocky Mountain NP":"Rocky Mountain National Park",
                                                                          "Saguaro NP":"Saguaro National Park",
                                                                          "Sequoia NP":"Sequoia National Park",
                                                                          "Shenandoah NP":"Shenandoah National Park",
                                                                          "Theodore Roosevelt NP":"Theodore Roosevelt National Park",
                                                                          "Virgin Islands NP":"Virgin Islands National Park",
                                                                          "Voyageurs NP":"Voyageurs National Park",
                                                                          "White Sands NP":"White Sands National Park",
                                                                          "Wind Cave NP":"Wind Cave National Park",
                                                                          "Wrangell-St. Elias NP":"Wrangell-St. Elias & PRES National Park",
                                                                          "Yellowstone NP":"Yellowstone National Park",
                                                                          "Yosemite NP":"Yosemite National Park",
                                                                          "Zion NP":"Zion National Park",})
# Renamed the abbreviations for the State with the entire name of the state
national_parks_rows_renamed_df=national_parks_rows_renamed_df.replace({"AK": "Alaska",
                       "AR": "Arizona",
                       "AS": "American Samoa",
                       "AZ": "Arizona",
                       "CA": "California",
                       "CO": "Colorado",
                       "FL": "Florida",
                       "HI": "Hiawaii",
                       "IN": "Indiana",
                       "KY": "Kentucky",
                       "ME": "Maine",
                       "MI": "Michigan",
                       "MN": "Minnesota",
                       "MO": "Missouri",
                       "MT": "Montana",
                       "ND": "North Dakota",
                       "NM": "New Mexico",
                       "NV": "Nevada",
                       "OH": "Ohio",
                       "OR": "Oregon",
                       "SC": "South Carolina",
                       "SD": "South Dakota",
                       "TN": "Tennessee",
                       "TX": "Texas",
                       "UT": "Utah",
                       "VA": "Virginia",
                       "VI": "Virgin Islands",
                       "WA": "Washington",
                       "WV": "West Virginia",
                       "WY": "Wyoming"
                      })       
 # Renamed the number of the month to the name of the month
month_names={1:"Jan", 2:"Feb", 3:"Mar", 4:"April", 5:"May", 6:"June", 7:"July", 8:"Aug", 9:"Sept", 10:"Oct", 11:"Nov", 12:"Dec"}
national_parks_rows_renamed_df['Month']=national_parks_rows_renamed_df['Month'].replace(month_names)
national_parks_rows_renamed_df["Recreation Hours by Month"] = national_parks_rows_renamed_df["Recreation Hours by Month"].str.replace(",","").astype(float)
national_parks_rows_renamed_df["Recreation Visits by Month"] = national_parks_rows_renamed_df["Recreation Visits by Month"].str.replace(",","").astype(float)
national_parks_rows_renamed_df["Total Recreation Hours"] = national_parks_rows_renamed_df["Total Recreation Hours"].str.replace(",","").astype(float)
# Create a new column for "Average Time Spent per Visit" and calculate
                                                                         
national_parks_rows_renamed_df["Average Time Spent per Visit"] = national_parks_rows_renamed_df["Recreation Hours by Month"] /national_parks_rows_renamed_df["Recreation Visits by Month"]
                                                                       
# Merge the DataFrames on a common column
merged_df = pd.merge(national_parks_rows_renamed_df, location_data_df, on='Park Name', how='left')

# With the clean and merged data merged_df is leveraged for analysis and visualization
# Savi
# Turn off warning messages
import warnings
warnings.filterwarnings("ignore")

#group the dataframe for Geo Map
geo_summary_df=merged_df.groupby(["Lat","Lon"]).agg({"Region": np.unique, "Park Name": np.unique, "State": np.unique, "Recreation Visits by Month": np.sum, "Recreation Hours by Month": np.sum})

# Create a column and calculation for % of Recreation Visits
geo_summary_df["% of Recreation Visits"] = (round( (geo_summary_df["Recreation Visits by Month"]/geo_summary_df["Recreation Visits by Month"].sum()) * 100,2))
# Plot Map for visual
map_plot_1 = geo_summary_df.hvplot.points(
    "Lon",
    "Lat",
    geo = True,
    tiles = "EsriNatGeo",
    frame_width = 1300,
    frame_height = 800,
    title= "National Parks in the US",
    size = "Recreation Visits by Month",
    scale = 0.015,
    color = "% of Recreation Visits" 
)
# Display the map plot
map_plot_1
# Create variable for Bar graph to show Counts of Parks by Region
regionbar=merged_df["Region"].value_counts()/12
regionbar
# Create the visual and plot regionbar
regionbar.plot(kind="bar", color="darkgoldenrod",alpha=0.5, align="center", fontsize=14
            )
plt.ylabel("Count of Parks by Region")
# Create variable for Bar graph to show Counts of Parks by State
statebar=merged_df["State"].value_counts()/12
# Create the visual and plot statebar
statebar.plot(kind="bar",color="darkgoldenrod",alpha=0.5, align="center", fontsize=14)
plt.ylabel("Count of Parks by State")

# MADDIE
# Popularity of Park by Total Hours
# Create a smaller dataframe with only Park Name and Total Recreation Hours, and group by Park Name
pre_sorted = national_parks_rows_renamed_df[['Park Name','Recreation Hours by Month']]
shortened = pre_sorted.sort_values('Recreation Hours by Month')
hours_by_park = pre_sorted.groupby(['Park Name']).sum()
sorted = hours_by_park.sort_values('Recreation Hours by Month')

a_axis_temp = shortened['Park Name'].unique()
hours_by_park.head()

# Create a list of the Park Names
x_axis = national_parks_rows_renamed_df['Park Name'].unique()
x_axis_list = a_axis_temp.tolist()

# Plot the graph
plt.figure(figsize=(20,4))
plt.bar(x_axis_list, sorted["Recreation Hours by Month"], color='r', alpha=0.5, align="edge")
tick_locations = [value+0.4 for value in range(len(x_axis))]
plt.xticks(tick_locations, x_axis_list, rotation="vertical")
plt.tight_layout
plt.xlabel('Parks')
plt.ylabel('Recreation Hours by Month')
plt.title('Popularity of National Parks by Hours')

plt.show()
# Popularity of Park by Total Visits
# Create a smaller dataframe with only Park Name and Total Recreation Hours, and group by Park Name
pre_sorted = national_parks_rows_renamed_df[['Park Name','Recreation Visits by Month']]
shortened = pre_sorted.sort_values('Recreation Visits by Month')
hours_by_park = pre_sorted.groupby(['Park Name']).sum()
sorted = hours_by_park.sort_values('Recreation Visits by Month')

a_axis_temp = shortened['Park Name'].unique()
hours_by_park.head()

# Create a list of the Park Names
x_axis = national_parks_rows_renamed_df['Park Name'].unique()
x_axis_list = a_axis_temp.tolist()

# Plot the graph
plt.figure(figsize=(15,5))
plt.bar(x_axis_list, sorted["Recreation Visits by Month"], color='r', alpha=0.5, align="edge")
tick_locations = [value+0.4 for value in range(len(x_axis))]
plt.xticks(tick_locations, x_axis_list, rotation="vertical")
plt.tight_layout()
plt.xlabel('Parks')
plt.ylabel('Recreation Visits by Month')
plt.title('Popularity of National Parks by Visits')

plt.show()

# Kayla & Daniel
# Create a conditional statement to sort the months into seasons
def get_season(month):
    if month in ['Dec', 'Jan', 'Feb']:
        return 'Winter'
    elif month in ['Mar', 'April', 'May']:
        return 'Spring'
    elif month in ['June', 'July', 'Aug']:
        return 'Summer'
    else:
        return 'Fall'

merged_df['seasons'] = merged_df['Month'].apply(get_season)
# DANIEL
seasons_df = merged_df.groupby("seasons")["Average Time Spent per Visit"].mean()
seasons_df.head()

x_axis = merged_df['seasons'].unique()
x_axis_list = x_axis.tolist()
y_axis = seasons_df

tick_locations = [i + 0.4 for i in range(len(x_axis_list))]
plt.figure(figsize=(20,10))
plt.bar(x_axis_list, y_axis, color='darkgoldenrod', alpha=0.5, align='edge')

plt.xticks(tick_locations, x_axis, rotation='horizontal', fontsize=16)
plt.tight_layout()
plt.title("Average Time Spent per Vist", fontsize=20)
plt.xlabel("Season", fontsize=20)
plt.ylabel("Time Spent", fontsize=20)

plt.show()

spring_df = merged_df.loc[merged_df["seasons"] == "Spring"]
summer_df = merged_df.loc[merged_df["seasons"] == "Summer"]
fall_df = merged_df.loc[merged_df["seasons"] == "Fall"]
winter_df = merged_df.loc[merged_df["seasons"] == "Winter"]

spring = 'violet'
summer = 'teal'
fall = 'olive'
winter = 'brown'

spring_region = spring_df.groupby("Region")["Average Time Spent per Visit"].mean()
summer_region = summer_df.groupby("Region")["Average Time Spent per Visit"].mean()
fall_region = fall_df.groupby("Region")["Average Time Spent per Visit"].mean()
winter_region = winter_df.groupby("Region")["Average Time Spent per Visit"].mean()


season_region_data = {
    'Spring': spring_region,
    'Summer': summer_region,
    'Fall': fall_region,
    'Winter': winter_region
}

df = pd.DataFrame(season_region_data)

colors = [spring, summer, fall, winter]

df.plot(kind='bar', figsize=(12, 6), color=colors)
plt.xlabel('Region')
plt.ylabel('Average Time Spent per Visit')
plt.title('Average Time Spent(hrs) per Visit by Season and Region')
plt.legend(title='Season')

plt.show()

# KAYLA

# Calculate the total visitation for each season
season_visits = merged_df.groupby('seasons')['Recreation Visits by Month'].sum()

# Plot the pie chart
plt.pie(season_visits, labels=season_visits.index, autopct='%1.1f%%',colors=['olive', 'violet', 'teal', 'brown'])
plt.title('National Park Visitation by Season')
plt.axis('equal')

plt.show()

# Steven
# NPS API
# Dependencies
import pandas as pd
import numpy as np
import requests
import json

# Import the API key
from config import nps_key
# Load the Parks CSV into a DataFrame
complete_parks_df = pd.read_csv("Resources/2023_national_park_public_data.csv")
# Extract "ParkName", "UnitCode", "ParkType", "Region", "State" to simplify the DataFrame
reduced_parks_df = complete_parks_df.loc[:, ["ParkName", "UnitCode", "ParkType",
                                    "Region", "State"]]
reduced_parks_df
# Create a new DataFrame to find each park's unique park code that we can use to reach data from the API
by_code_df = reduced_parks_df["UnitCode"].unique()
by_code_df
# set up a parameters dictionary
params = {
    "API_KEY":nps_key
}

# Set Base URL
base_url = "https://developer.nps.gov/api/v1/activities/parks" 
# Set the parameters for the type of search
parkCode = "grsm"
# set up a parameters dictionary
params = {
    "parkCode":parkCode,
    "API_KEY":nps_key
}
# Make an API request using the params dictionary
grsm_park_info = requests.get(base_url, params=params)

# Convert the API response to JSON format
grsm_park_info = grsm_park_info.json()

# Use json.dumps to print the json
print(json.dumps(grsm_park_info, indent=4, sort_keys=True))
# Set the parameters for the type of search
parkCode = "wrst"
# set up a parameters dictionary
params = {
    "parkCode":parkCode,
    "API_KEY":nps_key
}
# Make an API request using the params dictionary
wrst_park_info = requests.get(base_url, params=params)

# Convert the API response to JSON format
wrst_park_info = wrst_park_info.json()

# Use json.dumps to print the json
print(json.dumps(wrst_park_info, indent=4, sort_keys=True))
# I wanted to clean up the json.dump to show only the activies for this park ("name" parameter)
# First, drilled into the "data" category to create a list we can use with a for loop 
# to call out the name of each activity
wrst_activities = wrst_park_info["data"]

# Then, print the name of each activity for Wrangell - St Elias 
for activity in wrst_activities:
    print(activity["name"])
# Here I wanted to confirm that this number matched the number listed for "total" on the 
# json.dump for wrst_park_info
len(wrst_activities)
# Now doing the same for Great Smoky Mountains National Park
grsm_activities = grsm_park_info["data"]

# Then, print the name of each activity for Great Smoky Mountains National Park 
for activity in grsm_activities:
    print(activity["name"])
# checking again
len(grsm_activities)


