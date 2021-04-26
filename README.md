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
  4. Interpret model results and diagnostics. 
  5. Give business recommendations from analysis.

## Initial Obtain/Scrub/Exploration of Data

### Based on this [**2017 U.S. Census press release for fastest growing states**](https://www.census.gov/newsroom/press-releases/2017/estimates-idaho.html#:~:text=DEC.,state%20population%20estimates%20released%20today), the three photos below are sourced from the article. 

![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/US_Census_Data_Cleaning_and_Sorting/US_Census_Top10_1.PNG)
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/US_Census_Data_Cleaning_and_Sorting/US_Census_Top10_2.PNG)
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/US_Census_Data_Cleaning_and_Sorting/US_Census_Top10_3.PNG)


### I took this info and color coded which states showed up multiple times. Although Idaho is the main winner, we see that Texas shows up in all 3 categories of Numeric, Populous, and Percentage Growth. Therefore we will go with Texas as our choice. 
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/US_Census_Data_Cleaning_and_Sorting/US_Census_excel_analysis.PNG)
  
### Using Texas as our starting point, we see that based on value_counts() for the Zillow Data, Houston has the highest number of zip codes. Therefore the city we will look at is Houston. 


Houston           86
San Antonio       47
Austin            38
Dallas            33
Fort Worth        26
                  ..
Aldine             1
Weatherford        1
Mount Pleasant     1
Canton             1
Mart               1
Name: City, Length: 540, dtype: int64

### After choosing Houston, I obtained a list of all the zip codes which are in Houston and pulled the population data for each Houston zip code to find the top five most populous zip codes. 

Census data can be [**found here**](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Data%20Files/US%20Census%20Analysis.xlsx)

Custom Link can be accessed with [**this link**](https://data.census.gov/cedsci/table?q=DP05&t=Age%20and%20Sex&g=8600000US77002,77003,77004,77005,77006,77007,77008,77013,77014,77015,77016,77017,77018,77019,77020,77021,77024,77025,77027,77028,77029,77030,77031,77032,77033,77034,77035,77036,77037,77038,77040,77041,77042,77043,77044,77045,77047,77048,77049,77050,77051,77053,77054,77055,77056,77057,77058,77059,77060,77061,77062,77063,77066,77067,77068,77069,77070,77071,77072,77073,77074,77075,77077,77078,77079,77080,77081,77082,77084,77085,77086,77087,77088,77089,77090,77091,77092,77093,77094,77095,77096,77098,77099,77339,77345&tid=ACSST5Y2019.S0101&hidePreview=false)

I did the following with the Census dataset:
  1. Removing all columns I don't need. I only want zip code column and population column
  2. Fixing the data type to int in order to sort properly
  3. Sorting the dataframe by population highest to lowest
  4. .head() to find the top 5

### Now that we have the top 5 zip codes we do the following:
1. Use pd.melt() method to keep only the columns that we want and turn price data from row of values to column of values
2. I create new .csv files which only contain the zip code and the associated value of homes
3. Change column names to "ds" and "y" in order for the dataset to play nice with Facebook Prophet time series analysis
4. Run quick check for any nulls/Nans for my sanity

### Once the zip codes are chosen, I made a separate .csv file for each zip code to prep it for time series analysis with FBProphet.
The prepped data files can be fround [**here**](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/tree/main/Data%20Files)

## Analysis of each zip code:

### [PICK #1] 77084
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77084_1.PNG)
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77084_2.PNG)
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77084_3.PNG)

### [PICK #2] 77036
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77036_1.PNG)
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77036_2.PNG)
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77036_3.PNG)

### [PICK #3] 77095
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77095_1.PNG)
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77095_1.PNG)
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77095_1.PNG)

### [PICK #4] 77072
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77072_1.PNG)
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77072_1.PNG)
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77072_1.PNG)

### [PICK #5] 77077 
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77077_1.PNG)
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77077_1.PNG)
![](https://github.com/akuppan1/Flatiron-Mod4Proj-FINAL/blob/main/Notebook%20Pics/77077_1.PNG)
