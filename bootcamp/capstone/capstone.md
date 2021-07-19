# Bringing ML Models into Production Bootcamp
# Capstone Energy use case

## Capstone rules
- Capstone is a team-effort, supported by a mentor
- 2,5 weeks to work on the Capstone as a team
- 1 GitHub repository per team with the code and documentation, see [Deadline and submission](#deadline-and-submission)
- 1 person from a team to present a team work in 7 minutes on the 7th of August

## Capstone Description
To prevent further global warming, we want to move from fossil fueled energy to renewable sources. These sources are very volatile, so the energy system gets out of balance frequently, even leading to the large area power blackouts from time to time. The world of today is not ready yet to live on 100% renewable sources. On the contrary, you are going to show that it is possible if you leverage the power of forecasting.

Pytown, located in the remote area in the north of the Netherlands, wants to live on 100% renewable energy. Our town has enough solar panels and wind turbines to generate electricity, so we disconnected from the main electricity grid a while ago. However, we usually do not use the electricity at the moment of its generation by sun and/or wind, which is causing daily power blackouts. We are fed up with all the electricity problems and ask your team to support us. Help us to adjust our electricity demand to the electricity generation.

We want to have a dashboard telling us when it is allowed to use electricity as much as we want, use less electricity or charge only essential devices.

---
## Capstone task: Develop a solution to prevent power blackouts

Provide a forecast for the upcoming week (split per day) to be consumed by Power BI dashboard:
- normal charge (normal behaviour, charge whatever you want);
- middle charge (do not charge energy hungry devices, such as electrical bikes, electrical cars, dishwashers, washing machines);
- low charge (charge only essential devices)

### Steps

1. Data preprocessing: process data from three data sources (energy load data, wind and solar predictions data, weather data).
2. Model training: train naive forecast and linear regression, perform feature engineering with Fourier transform.
3. Model evaluation: backtest both models with a sliding window approach, optimize for MAPE.
4. Model deployment: deploy the best performing model as an Azure Machine Learning Batch pipeline and schedule it to run every Monday at 04:00 in the morning.
5. Model post-processing: compare generated energy forecast with wind and solar predictions, classify the energy consumption per day (normal, middle, low charge), persist results to Azure Blob Storage (to be used by Power BI).
6. Model monitoring: design a basic technical and model specific monitoring.

---
## Capstone task: Improve the solution to prevent power blackouts
Everyone is really happy with your dashboard. The amount of power blackouts did decrease by 50%. However, we are still facing a lot of them, as everyone arrives at home around 17:30 and plugs in. As a result we are facing a blackout again. It means that the information in your dashboard needs to be more detailed and timely to solve this.

Update your current dashboard with forecasts for the upcoming 15 min:
- normal charge (normal behaviour, charge whatever you want);
- middle charge (do not charge energy hungry devices, such as electrical bikes, electrical cars, dish washers, wachine machines);
- low charge (charge only essential devices)

### Steps

1. Data preprocessing: process data from two data sources (energy load data, wind and solar predictions data). Unfortunately weather data is not available every 15 min.
2. Model training: train naive forecast.
3. Model evaluation: backtest the naive forecast with an expanding window approach, optimize for MAPE
4. Model deployment: deploy the model as a blob-triggered Azure function, that fires every 15 min.
5. Model post-processing: compare generated energy forecast with wind and solar predictions, classify the energy consumption per 15 min (normal, middle, low charge), persist results to Azure Blob Storage (to be used by Power BI).
6. Model monitoring: design a basic technical and model specific monitoring.

---
## Deadline and submission

Last commit to the repository has to be pushed **before 12:00 CEST Amsterdam time on the 7th of August**

The link to the Github repository and the team number should be shared in [#mlops_bootcamp_pyladies_amsterdam channel](https://pyladies.slack.com/archives/C026H5HMF4L) **before 14:00 CEST Amsterdam time on the 7th of August**

---
## Video record
Watch the recording of the Capstone results [here]( https://youtu.be/aLReepA68Nk).
