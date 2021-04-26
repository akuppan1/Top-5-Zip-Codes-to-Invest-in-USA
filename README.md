# Top 5 Zip Codes to Invest Real Estate

## What this project is about: 
  We were tasked by a real estate firm to help them decide which zip codes they should invest in.
  
## Summary
  We approached the problem with a top-down approach. First we leveraged U.S. Census data in order to narrow down to which state we want to invest in. Then we utilized the given dataset from Zillow to further narrow down our choices. We focused mainly on where the people are going and which zip codes were the largest in the area. Once we had our zip codes, we used Facebook Prophet to run a time series analysis on each zip code. We created a model to forecast what the prices would look like for the next few years. Based on our observations, the top five zip codes we chose showed promise in the future for rising home values. 
  
## The Data

  I utilized a custom dataset from the U.S. Census where I obtained the population of each zip code in the chosen state in order to order the zip codes by population. 
  Dataset is taken from the U.S. Census API with a [**custom link that I made**](https://data.census.gov/cedsci/table?q=DP05&t=Age%20and%20Sex&g=8600000US77002,77003,77004,77005,77006,77007,77008,77013,77014,77015,77016,77017,77018,77019,77020,77021,77024,77025,77027,77028,77029,77030,77031,77032,77033,77034,77035,77036,77037,77038,77040,77041,77042,77043,77044,77045,77047,77048,77049,77050,77051,77053,77054,77055,77056,77057,77058,77059,77060,77061,77062,77063,77066,77067,77068,77069,77070,77071,77072,77073,77074,77075,77077,77078,77079,77080,77081,77082,77084,77085,77086,77087,77088,77089,77090,77091,77092,77093,77094,77095,77096,77098,77099,77339,77345&tid=ACSST5Y2019.S0101&hidePreview=false)

Additionally, the Zillow Dataset from our partners at Flatiron School was used. [**Link to the Dataset**](https://github.com/learn-co-curriculum/dsc-phase-4-project/blob/main/time-series/zillow_data.csv)

## Agenda
  1. Look at general population trends for every state in the U.S.
  2. Narrow down from state to city and then to the most populous zip codes in that city. 
  3. Run time series analysis using Facebook Prophet and forecast with model.
  4. Interpret model results and model diagnostics. 


