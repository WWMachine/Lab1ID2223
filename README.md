# Lab 1 (Air-Quality Prediction using XGBoost)

This Lab was completed by Nils Wiebe Werner and Oliver Westfahl Knezevic.

We have implemented all 7 steps of the assignment. The version available in the repo is the final version that fulfills the A extension.  

For the E and C extensions the station selected was: Gakuendai Station in Saitama-ken, Japan.

For the E extension we simply followed the tutorial of the lab and got the pipelines up and running such that they fetched weather and air quality data daily, trained a model, created a forecast and created a graph that showed how accurate the forecast was for past predictions. This was then used in a scheduled pipeline through github actions to create a dashboard that updates daily.

For the C extension we have added 4 features to the data that the model is trained on, a rolling mean of the air quality (pm2.5) for past 3 days as well as three separate values for the pm2.5 value delayed by 1, 2 and 3 days respectively. These features helped improve the model as can be seen below. In terms of changes to the code this meant writing logic to get and insert these values for each data point, expanding the features the model was trained on and changing the logic for forecasting from batch inference to sequential since each prediction is now dependent on the last.

For the A extension we parametrized the code given for the assignment such that each notebook could be run for any given weather station available (with data). This was done by moving the different parts of each notebooks pipeline into functions such that they could be called easily with input parameters allowing us to loop over the pipeline for multiple stations. We then did this for the selected city's weather stations. We fetch data from each individual station, train a model for each respective station and generate forecasts for each station which are represented in the dashboard. This extension entailed changing file paths and names in hopsworks so that each station was treated separetly. 



Here are the results of training in the E extension:

The model got an MSE value of 323.60623 and r2 of -0.4696496595319144

(SHOW FEATURE IMPORTANCE AND TRAINING PLOT)

Here are the results of training in the C extension: 

The model got an MSE value of 164.34091 and r2 of 0.2520640155696643

(SHOW FEATURE IMPORTANCE AND TRAINING PLOT)


We can see that including the information of pm2.5 data for previous days has a significant improvement in the model quality. Most likely because pm2.5 is a time-dependent on the trend of pm2.5 of the days before. 

The final dashboard (showing predictions for the stations in Toyohashi, Japan) can be viewed here [Dashboard for Tokushima Prefecture](https://wwmachine.github.io/Lab1ID2223/)



##  Run pipelines with make commands

    make aq-backfill
    make aq-features
    make aq-train
    make aq-inference
    make aq-clean

or 
    make aq-all
