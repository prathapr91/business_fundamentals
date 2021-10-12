## **Using Clustering to pinpoint areas that need Healthcare Investment**

Prathap Rajaraman

**Abstract**

The COVID-19 pandemic opened our eyes as to the inequality in healthcare in America. While some regions received fairly minimal damage, other regions are not so lucky. In many areas throught the US, hospital beds were overcrowded and supplies and staff are limited, impacting doctors' and nurses' ability to treat both COVID and non-COVID patients. This inspired me to locate regions where there is a high probability of shortage in healthcare resources. With this information, the US Department of Health and Human Services can locate areas to send money for staff, supplies, and infrastructure such as new facilities. To do so, I recommend analyzing demographic data across regions and applying geospatial clustering to find optimal locations.



**Design**

In this project, we aim to determine the best locations for new hospitals and staff that best serve parts of the country that (1) have limited resources and (2) have an extraordinary need for healthcare. One possible solution path is to build a model that pinpoints regions that had high hospital capacity rates and a population with problematic health, then allocate resources that better serve those communities. This is an application of prescriptive analytics and variable relationships.



*Impact Hypothesis*

The desired impact of this project is to enhance healthcare services by allocating more resources to strategic locations. My impact hypothesis is that by using COVID bed capacity as well as demographics as proxies for underserved areas, the hospitals built in those areas can help reduce mortality rates and increase life expectancy. Short term, adding staff and makeshift beds can help with COVID as the Delta Variant is still rampant.



*Solution Paths*

First, demographic data such as poverty rates, population density, obesity, life expectancy, and hospital capacity rates during the "dark winter" of COVID (December 2020 - January 2021) will be leveraged. This data will be cleaned and analyzed on a county-level, then visualized on Tableau to get a general sense of which regions are in need.



From here, there are two solution paths, with one being more robust than the other. The simpler solution path is to use EDA to locate counties and regions with unfavorable demographics and send more resources there. The more robust solution utilizes geospatial clustering. Here, data such as hospital capacity, obesity, and poverty is analyzed on a county level, then after clustering, optimal locations for investment can be determined. 



*Criteria for Success*

In the short term, this project is deemed a success if bed capacity and COVID mortality rates dropped in problematic areas. Long term, success would look like reduced obesity rates and higher life expectancy due to more attention and care invested in the areas of interest.



*Assumptions and Risks*

I am assuming that COVID bed capacity rate is an accurate proxy for resource allocation. The risk here is that geopolitical forces can skew results. For example, there could be a region in an area with stricter lockdown measures that are in need of more resources but are missed due to low bed capacity.



A second assumption I am making is that the demographics I am using are accurate proxies for general population healthcare need. I am assuming that obesity, life expectancy, and poverty captures such a wide range of health risks that it is an accurate indicator of health needs. A risk of this is that it can miss other health factors that are significant yet not captured in this data.



**Data**

For preliminary analysis, I plan to use [COVID hospitalization data](https://healthdata.gov/Hospital/COVID-19-Reported-Patient-Impact-and-Hospital-Capa/anag-cw7u) provided by the US Department of Health & Human Services. Here, I will be filtering on the months of December 2020 and January 2021. By focusing on the deadliest wave pre-vaccine rollout, I will be controlling for vaccination rates and politics.



In addition, [county level obesity data and life expectancy](http://www.healthdata.org/us-health/data-download), [Population density by zip code](https://blog.splitwise.com/2014/01/06/free-us-population-density-and-unemployment-rate-by-zip-code/) and [Poverty data on County level](https://www.census.gov/data-tools/demo/saipe/#/?map_geoSelector=aa_c) will also be leveraged. The idea here is to take into account COVID hospitalization, general health, and wealth.



**Algorithm and Analysis**

All cleaning and data analysis is done in Excel, while data visualization is done in Tableau.



From the COVID hospitalization dataset, the data was provided on a hospital by hospital basis, weekly. I took data from December 2020 - January 2021 and averaged out the weekly hospitalization capacity for reasons mentioned above. Then, I aggregated and mapped the data such that there is an average hospital capacity for each county.



Then, by using the county level demographic data described above, I combined all data together for a final summary, and analyzed all counties that have entries for all criteria involved. I then conducted some initial EDA to get a sense of how different regions fared and how different variables interact with one another, as shown below:



| Correlation  Matrix | Hospital  Capacity | Population  Density | Life Expectancy | Obesity Rate | Poverty Rate |
| ------------------- | ------------------ | ------------------- | --------------- | ------------ | ------------ |
| Hospital Capacity   | 1.000              | 0.099               | -0.031          | -0.044       | -0.004       |
| Population Density  | 0.099              | 1.000               | 0.102           | -0.163       | -0.015       |
| Life Expectancy     | -0.031             | 0.102               | 1.000           | -0.740       | -0.709       |
| Obesity Rate        | -0.044             | -0.163              | -0.740          | 1.000        | 0.634        |
| Poverty Rate        | -0.004             | -0.015              | -0.709          | 0.634        | 1.000        |

| Region           | Hospital  Capacity | Population  Density | Life Expectancy | Obesity Rate | Poverty Rate |
| ---------------- | ------------------ | ------------------- | --------------- | ------------ | ------------ |
| Northeast        | 75.1%              | 7,301               | 79.5            | 33%          | 11%          |
| Middle  Atlantic | 77.5%              | 1,981               | 78.9            | 34%          | 9%           |
| South            | 77.5%              | 779                 | 77.0            | 37%          | 15%          |
| Midwest          | 66.9%              | 1,174               | 78.3            | 36%          | 12%          |
| Mountain         | 64.6%              | 605                 | 79.2            | 31%          | 11%          |
| Southwest        | 76.0%              | 841                 | 78.2            | 36%          | 14%          |
| Pacific          | 79.6%              | 1,653               | 80.2            | 32%          | 11%          |

The key takeaways I got here is that hospital capacity during COVID does not have significant links to other variables, and that the South region is in most need when looking at all the variables holistically.



After this, I built a Tableau dashboard for visualization, which can be accessed [here](https://public.tableau.com/app/profile/prathap.rajaraman/viz/metis_business_fundamentals_Prathap_Rajaraman/HealthDashboard?publish=yes). Please see below for a screencap of the dashboard, which shows the criteria in the Southern region, which was what my analysis deemed to be the most problematic:



![Health Dashboard](/Users/prathaprajaraman/Documents/Data_Science/Metis/business_fundamentals/project/Images/Health Dashboard.png)

Here, I isolated the worst 25% percentile of every criteria. While I found minimal link between population density and the other variables, there's a clear pattern going on with the southern region and unfavorable healthcare characteristics. This can be taken a step further by zooming in further via clustering.



**Tools**

- Excel for data cleaning and exploratory data analysis
- Tableau for data visualization



**Communication**

A brief deck on my exploration and analysis, along with visualizations.

