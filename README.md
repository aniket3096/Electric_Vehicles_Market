# Electric_Vehicles_Market
Market size analysis is a crucial aspect of market research that determines the potential sales volume within a given market. It helps businesses understand the magnitude of demand, assess market saturation levels, and identify growth opportunities.

## Electric Vehicles Market Size Analysis using Python
- Understand how data analysts and scientists gather and analyze data
- Perform data analysis in Python
- Combine, group, and aggregate data from multiple sources
- Create data visualizations with `pandas`, `matplotlib`, and `seaborn`
- Use Python data science libraries to analyze real-world datasets.
- Use `pandas` to solve several common data representation and analysis problems
- Utilize computer science concepts and algorithms to write more efficient code for data analysis
- Write and run simulations

## Prerequisites


### PyPI
using pip, you can install `NumPy`,`Pandas`,`matplotlib`,`seaborn` with:
```shell
pip install numpy
```
```shell
pip install pandas
```
```shell
pip install matplotlib
```
```shell
pip install seaborn
```


## SUMMARY
Market size analysis for electric vehicles involves a multi-step process that includes defining the market scope, collecting and preparing data, analytical modelling, and communicating findings through visualization and reporting. Below is the process you can follow for the task of electric vehicles market size analysis:

- Define whether the analysis is global, regional, or focused on specific countries.
- Gather information from industry associations, market research firms (e.g., BloombergNEF, IEA), and government publications relevant to the EV market.
- Use historical data to identify trends in EV sales, production, and market.
- Analyze the market size and growth rates for different EV segments.
- Based on the market size analysis, provide strategic recommendations for businesses looking to enter or expand in the EV market.

#### 1. let’s get started with the task of electric vehicles market size analysis by importing the necessary Python libraries and the dataset:
```shell
import pandas as pd
ev_data = pd.read_csv('Electric_Vehicle_Population_Data.csv')
print(ev_data.head())
```

![1](https://github.com/aniket3096/Electric_Vehicles_Market/assets/164318183/fe3dd857-7ba5-4c86-929d-11e8613bccf6)

#### 2. let’s clean the dataset before moving forward:
```shell
ev_data.info()
```

![2](https://github.com/aniket3096/Electric_Vehicles_Market/assets/164318183/ec5b5d05-34c9-4f38-856e-2f71b6ecdeb0)

#### 3. For the task of market size of electric vehicles analysis, we can explore the following areas:

- EV Adoption Over Time: Analyze the growth of the EV population by model year.
- Geographical Distribution: Understand where EVs are most commonly registered (e.g., by county or city).
- EV Types: Breakdown of the dataset by electric vehicle type (BEV, etc.).
- Make and Model Popularity: Identify the most popular makes and models among the registered EVs.
- Electric Range Analysis: Analyze the electric range of vehicles to see how EV technology is progressing.
- Estimated Growth in Market Size: Analyze and find the estimated growth in the market size of electric vehicles.

#### 4. Let’s start with analyzing the EV Adoption Over Time by visualizing the number of EVs registered by model year. It will give us an insight into how the EV population has grown over the years

```shell
import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style("whitegrid")

# EV Adoption Over Time
plt.figure(figsize=(12, 8))
ev_adoption_by_year = ev_data['Model Year'].value_counts().sort_index()
sns.barplot(x=ev_adoption_by_year.index, y=ev_adoption_by_year.values, palette="viridis")
plt.title('EV Adoption Over Time')
plt.xlabel('Model Year')
plt.ylabel('Number of Vehicles Registered')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

![3](https://github.com/aniket3096/Electric_Vehicles_Market/assets/164318183/7a0a7c95-3fe5-40bf-86dc-64cc65f3df9a)

From the above bar chart, it’s clear that EV adoption has been increasing over time, especially noting a significant upward trend starting around 2016. The number of vehicles registered grows modestly up until that point and then begins to rise more rapidly from 2017 onwards. The year 2023 shows a particularly sharp increase in the number of registered EVs, with the bar for 2023 being the highest on the graph, indicating a peak in EV adoption

#### 5. let’s start by selecting the top 3 counties based on EV registrations and then analyze the distribution of EVs within the cities of those counties

```shell
# geographical distribution at county level
ev_county_distribution = ev_data['County'].value_counts()
top_counties = ev_county_distribution.head(3).index

# filtering the dataset for these top counties
top_counties_data = ev_data[ev_data['County'].isin(top_counties)]

# analyzing the distribution of EVs within the cities of these top counties
ev_city_distribution_top_counties = top_counties_data.groupby(['County', 'City']).size().sort_values(ascending=False).reset_index(name='Number of Vehicles')

# visualize the top 10 cities across these counties
top_cities = ev_city_distribution_top_counties.head(10)

plt.figure(figsize=(12, 8))
sns.barplot(x='Number of Vehicles', y='City', hue='County', data=top_cities, palette="magma")
plt.title('Top Cities in Top Counties by EV Registrations')
plt.xlabel('Number of Vehicles Registered')
plt.ylabel('City')
plt.legend(title='County')
plt.tight_layout()
plt.show()
```

![4](https://github.com/aniket3096/Electric_Vehicles_Market/assets/164318183/cdc509e1-a48f-461b-add5-e01ebfe1ecad)

The above graph compares the number of electric vehicles registered in various cities within three counties: King, Snohomish, and Pierce. The horizontal bars represent cities, and their length corresponds to the number of vehicles registered, colour-coded by county. Here are the key findings from the above graph:

- Seattle, which is in King County, has the highest number of EV registrations by a significant margin, far outpacing the other cities listed.
- Bellevue and Redmond, also in King County, follow Seattle with the next highest registrations, though these are considerably less than 
  Seattle’s.
- Cities in Snohomish County, such as Kirkland and Sammamish, show moderate EV registrations.
- Tacoma and Tukwila, representing Pierce County, have the fewest EV registrations among the cities listed, with Tacoma slightly ahead of 
  Tukwila.
- The majority of cities shown are from King County, which seems to dominate EV registrations among the three counties.
- Overall, the graph indicates that EV adoption is not uniform across the cities and is more concentrated in certain areas, particularly in 
  King County.

#### 6. Next, let’s explore the types of electric vehicles represented in this dataset. Understanding the breakdown between different EV types, such as Battery Electric Vehicles (BEV) and Plug-in Hybrid Electric Vehicles (PHEV), can provide insights into consumer preferences and the adoption patterns of purely electric vs. hybrid electric solutions. So, let’s visualize the distribution of electric vehicle types to see which categories are most popular among the registered vehicles:

```shell
# analyzing the distribution of electric vehicle Types
ev_type_distribution = ev_data['Electric Vehicle Type'].value_counts()

plt.figure(figsize=(8, 8))
sns.barplot(x=ev_type_distribution.values, y=ev_type_distribution.index, palette="rocket")
plt.title('Distribution of Electric Vehicle Types')
plt.xlabel('Number of Vehicles Registered')
plt.ylabel('Electric Vehicle Type')
plt.tight_layout()
plt.show()
```

 ![5](https://github.com/aniket3096/Electric_Vehicles_Market/assets/164318183/1273e006-d3d0-4f4b-bc80-8713f08eae3a)

 The above graph shows that BEVs are more popular or preferred over PHEVs among the electric vehicles registered in the United States.

 #### 7. Let’s now focus on the popularity of electric vehicle manufacturers and models among the registered vehicles. This analysis will help us identify which manufacturers and specific models dominate the EV market, potentially indicating consumer preferences, brand loyalty, and the success of various manufacturers’ strategies in promoting electric mobility.

So, let’s have a look at the most popular manufacturers and then drill down into the most popular models within those manufacturers:

```shell
# analyzing the popularity of EV manufacturers
ev_make_distribution = ev_data['Make'].value_counts().head(10)  # Limiting to top 10 for clarity

plt.figure(figsize=(12, 6))
sns.barplot(x=ev_make_distribution.values, y=ev_make_distribution.index, palette="cubehelix")
plt.title('Top 10 Popular EV Makes')
plt.xlabel('Number of Vehicles Registered')
plt.ylabel('Make')
plt.tight_layout()
plt.show()
```

![6](https://github.com/aniket3096/Electric_Vehicles_Market/assets/164318183/39ff8b9e-53d2-4967-8932-fe2c03655961)

The above chart shows that:

- TESLA leads by a substantial margin with the highest number of vehicles registered.
- NISSAN is the second most popular manufacturer, followed by CHEVROLET, though both have significantly fewer registrations than TESLA.
- FORD, BMW, KIA, TOYOTA, VOLKSWAGEN, JEEP, and HYUNDAI follow in decreasing order of the number of registered vehicles.

#### 8. Next, let’s drill down into the most popular models within these top manufacturers to get a more detailed understanding of consumer preferences at the model level:

```shell
# selecting the top 3 manufacturers based on the number of vehicles registered
top_3_makes = ev_make_distribution.head(3).index

# filtering the dataset for these top manufacturers
top_makes_data = ev_data[ev_data['Make'].isin(top_3_makes)]

# analyzing the popularity of EV models within these top manufacturers
ev_model_distribution_top_makes = top_makes_data.groupby(['Make', 'Model']).size().sort_values(ascending=False).reset_index(name='Number of Vehicles')

# visualizing the top 10 models across these manufacturers for clarity
top_models = ev_model_distribution_top_makes.head(10)

plt.figure(figsize=(12, 8))
sns.barplot(x='Number of Vehicles', y='Model', hue='Make', data=top_models, palette="viridis")
plt.title('Top Models in Top 3 Makes by EV Registrations')
plt.xlabel('Number of Vehicles Registered')
plt.ylabel('Model')
plt.legend(title='Make', loc='center right')
plt.tight_layout()
plt.show()
```

![7](https://github.com/aniket3096/Electric_Vehicles_Market/assets/164318183/dc020512-f6ff-4b2b-a042-89bbdffd9fea)

The above graph shows the distribution of electric vehicle registrations among different models from the top three manufacturers: TESLA, NISSAN, and CHEVROLET. Here are the findings:

- TESLA’s MODEL Y and MODEL 3 are the most registered vehicles, with MODEL Y having the highest number of registrations.
- NISSAN’s LEAF is the third most registered model and the most registered non-TESLA vehicle.
- TESLA’s MODEL S and MODEL X also have a significant number of registrations.
- CHEVROLET’s BOLT EV and VOLT are the next in the ranking with considerable registrations, followed by BOLT EUV.
- NISSAN’s ARIYA and CHEVROLET’s SPARK have the least number of registrations among the models shown.

#### 9. Next, we’ll explore the electric range of vehicles, which is a critical factor for analyzing the market size of electric vehicles. The electric range indicates how far an EV can travel on a single charge, and advancements in battery technology have been steadily increasing these ranges over the years. So, let’s look at the distribution of electric ranges in the dataset and identify any notable trends, such as improvements over time or variations between different vehicle types or manufacturers:

```shell
# analyzing the distribution of electric range
plt.figure(figsize=(12, 6))
sns.histplot(ev_data['Electric Range'], bins=30, kde=True, color='royalblue')
plt.title('Distribution of Electric Vehicle Ranges')
plt.xlabel('Electric Range (miles)')
plt.ylabel('Number of Vehicles')
plt.axvline(ev_data['Electric Range'].mean(), color='red', linestyle='--', label=f'Mean Range: {ev_data["Electric Range"].mean():.2f} miles')
plt.legend()
plt.show()
```

![8](https://github.com/aniket3096/Electric_Vehicles_Market/assets/164318183/2b59e36d-4066-4e4c-b02d-0ae8a61131a8)

The above graph shows the mean electric range. Key observations from the graph include:

- There is a high frequency of vehicles with a low electric range, with a significant peak occurring just before 50 miles.
- The distribution is skewed to the right, with a long tail extending towards higher ranges, although the number of vehicles with higher 
  ranges is much less frequent.
- The mean electric range for this set of vehicles is marked at approximately 58.84 miles, which is relatively low compared to the 
  highest ranges shown in the graph.
- Despite the presence of electric vehicles with ranges that extend up to around 350 miles, the majority of the vehicles have a range 
  below the mean.
- It suggests that while there are EVs available with high electric ranges, the average range is skewed lower due to a substantial 
  number of vehicles with shorter ranges.

#### 10. Now, let’s delve into the trend of electric ranges over model years, which can provide insights into how advancements in battery technology and vehicle design have influenced the electric range capabilities of electric vehicles over time. A positive trend in this analysis would indicate continuous improvements, offering consumers EVs with longer driving ranges and potentially addressing one of the major concerns regarding the EV market (range anxiety)


```shell
# calculating the average electric range by model year
average_range_by_year = ev_data.groupby('Model Year')['Electric Range'].mean().reset_index()

plt.figure(figsize=(12, 6))
sns.lineplot(x='Model Year', y='Electric Range', data=average_range_by_year, marker='o', color='green')
plt.title('Average Electric Range by Model Year')
plt.xlabel('Model Year')
plt.ylabel('Average Electric Range (miles)')
plt.grid(True)
plt.show()
```

![9](https://github.com/aniket3096/Electric_Vehicles_Market/assets/164318183/61e82194-1253-4cd7-8304-314b3234201e)

The above graph shows the progression of the average electric range of vehicles from around the year 2000 to 2024. Key findings from the graph:

- There is a general upward trend in the average electric range of EVs over the years, indicating improvements in technology and battery 
 efficiency.
- There is a noticeable peak around the year 2020 when the average range reaches its highest point.
- Following 2020, there’s a significant drop in the average range, which could indicate that data for the following years might be 
  incomplete or reflect the introduction of several lower-range models.
- After the sharp decline, there is a slight recovery in the average range in the most recent year shown on the graph.
The data suggest that while there have been fluctuations, the overall trend over the last two decades has been toward increasing the electric range of EVs.

#### 11. Next, let’s explore how electric ranges vary among the top manufacturers and models. This analysis can reveal how different manufacturers are addressing the crucial aspect of electric range and highlight which models stand out for their superior range capabilities:

```shell
average_range_by_model = top_makes_data.groupby(['Make', 'Model'])['Electric Range'].mean().sort_values(ascending=False).reset_index()

# the top 10 models with the highest average electric range
top_range_models = average_range_by_model.head(10)

plt.figure(figsize=(12, 8))
barplot = sns.barplot(x='Electric Range', y='Model', hue='Make', data=top_range_models, palette="cool")
plt.title('Top 10 Models by Average Electric Range in Top Makes')
plt.xlabel('Average Electric Range (miles)')
plt.ylabel('Model')
plt.legend(title='Make', loc='center right')
plt.show()
```

![10](https://github.com/aniket3096/Electric_Vehicles_Market/assets/164318183/9bdd5099-568d-4232-a84c-ed33b93e08b7)

- The TESLA ROADSTER has the highest average electric range among the models listed. 
- TESLA’s models (ROADSTER, MODEL S, MODEL X, and MODEL 3) occupy the majority of the top positions, indicating that on average, TESLA’s 
  vehicles have higher electric ranges.
- The CHEVROLET BOLT EV is an outlier among the CHEVROLET models, having a substantially higher range than the VOLT and S-10 PICKUP from 
  the same maker.
- NISSAN’s LEAF and CHEVROLET’s SPARK are in the lower half of the chart, suggesting more modest average ranges.

### $ Estimated Market Size Analysis of Electric Vehicles in the United States
Now, let’s move forward towards finding the estimated market size of electric vehicles in the United States. I’ll first count the number of EVs registered every year:

```shell
# calculate the number of EVs registered each year
ev_registration_counts = ev_data['Model Year'].value_counts().sort_index()
ev_registration_counts
```

![11](https://github.com/aniket3096/Electric_Vehicles_Market/assets/164318183/54d49baa-534b-42f7-a191-bc4d65ce97a1)

The dataset provides the number of electric vehicles registered each year from 1997 through 2024. However, the data for 2024 is incomplete as it only contains the data till March. Here’s a summary of EV registrations for recent years:

- In 2021, there were 19,063 EVs registered.
- In 2022, the number increased to 27708 EVs.
- In 2023, a significant jump to 57,519 EVs was observed.
- For 2024, currently, 7,072 EVs are registered, which suggests partial data.

### Conclusion

So, market size analysis is a crucial aspect of market research that determines the potential sales volume within a given market. It helps businesses understand the magnitude of demand, assess market saturation levels, and identify growth opportunities. From our market size analysis of electric vehicles, we found a promising future for the EV industry, indicating a significant shift in consumer preferences and a potential increase in related investment and business opportunities



