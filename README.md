# Dementia


## What is Dementia?

Dementia is a syndrome that leads to the impairment of cognitive function and affects memory, thought and speech. In Australia, it currently affects 400,000 people and is one of the leading causes of death. Dementia has significant socioeconomic and psychological impacts for both people with dementia, and care providers. There are certain factors that may increase the risk for dementia. These include age, socioeconomic factors, obesity, smoking and exercise. 


This study explores the impacts of these factors on the incidence of dementia at the Local Government Area (LGA) level. These are administrative regions in Australia that are governed by local councils. We collected data at the LGA for factors such as health measurements (smoking, obesity, high blood pressure), along with socioeconomic factors from PHIDU. We also calculated ways to measure exercise as described below.


## Exercise

One of the risk factors for dementia is exercise. As people living in some regions can access more ways to exercise compared to others, we need to find ways to measure access to exercise. 

### Bike Paths
One way of measuring access to exercise is to find the distance between bike paths and households. First, we can find all the meshblocks in Australia, which are small geographic areas that are classified into certain groups, such as residential, industrial or commercial. We filter out only those that are categorised as 'residential' and calculate the shortest distance between each residential meshblock and a bike path. From there, we can group the meshblocks according to which LGA they are in, and average the distance in each LGA to find the average distance between bike paths and households at the LGA level. 

![image](https://user-images.githubusercontent.com/78997343/217757271-aec0b4b0-dbda-4487-9559-67351b2b8c77.png)
The red shapes represent each residential meshblock in LGAs in eastern Melbourne. The blue lines represent bike paths. 

![image](https://user-images.githubusercontent.com/78997343/217757728-91462f1a-814d-45ac-80b6-0c61419c246b.png)
The residential meshblocks have now been shaded to show the shortest distance between each residential meshblock and a bike path.

![image](https://user-images.githubusercontent.com/78997343/217968575-2682d4cd-849e-4109-8203-efd8d546d64d.png)
After grouping the meshblocks based on which LGA they are in, we can average all the meshblocks in a given LGA to find the average distance between bike paths and residential meshblocks for that LGA. This image shows the average distance for LGAs in eastern Melbourne.


### Access to Parks
Parks are places where people can exercise. The closer a park is to a neighbourhood, the easier it is for residents to access it. Similarly, the more parks there are close by to a neighbourhood, the more access residents have to parks. Home2park is a package available on R, which takes into account both of these ideas by finding the distance between all parks and each neighbourhood, and uses a distance decay method to find the supply of parks for each neighbourhood. 

To find all the parks in Australia, we filtered all the meshblocks which were classified as 'parkland'. The Australian Bureau of Statistics (ABS) considers parks, nature reserves, as well as golf courses and sporting facilities as parkland. In essence, places where people can exercise. 

![image](https://user-images.githubusercontent.com/78997343/217981390-411eb6d7-050c-40e2-a99f-3c62a01a6e4e.png)
This image shows all residential meshblocks (red) in Eastern Melbourne, as well as parks nearby (green).
![image](https://user-images.githubusercontent.com/78997343/218019626-79220ad5-eb2e-4d20-bed1-7b9b143be9bb.png)
The average supply of parks for each LGA in Eastern Melbourne

### Trees
![image](https://user-images.githubusercontent.com/78997343/218587448-3879c28e-d808-4b5e-8c4e-d4e3dbc18c9d.png)
This image shows tree cover for Eastern Melbourne. The shapefiles used to plot the map are from Data Vic, and show areas where tree cover is greater than 1 hectare. 

## Spatial Regression
LGAs are administrative regions, each having different population sizes. As a result, some LGAs may have more people with dementia simply because they are larger LGAs, rather than explanatory variables contributing to the higher incidences. Thus, to find hot spots for dementia incidence, we need to calculate the standardised dementia incidence ratio. This ratio divides the number of people with dementia in each LGA by the expected number of cases. From this, we can perform regression analysis to evaluate the contribution of the explanatory variables or covariates to the standardised dementia incidence ratio. The variables we used in this study related to either access to healthcare (2 variables), access to parks and exercise (2 variables), socioeconomic factors (2 variables), age (1 variable) or measurements of health (8 variables).

The dementia incidence in some regions may influence their neighbours. To test for this spatial autocorrelation, we can use a Global Moran I test. If Moran’s I is positive and close to 1, it means that the data of one LGA is strongly correlated to its neighbours. Conversely, a result close to 0 suggests that the data in each LGA is independent of one another. The Global Moran I statistic in this study was 0.32, indicating some spatial autocorrelation. 

A Global Moran I test only provides an indication whether there is overall clustering and may not show clustering occurring at the local scale. In other words, while some regions may show no correlation to one another, in other regions, there may be some clustering. To test for this, we can use a Local Moran I test to see whether this was the case. From this, we could find clustering at the local scale.

To determine which LGAs were considered adjacent and neighbouring, we used a Queen’s movement in chess to define neighbourhood as any point of contact along the border of LGA. Thus, two LGAs that share a border were considered to be neighbours. 

There are different libraries in R that can perform spatial regression. We used Integrated Nested Laplace Approximation (INLA) as it is quicker compared to others such as WinBUGS, which uses Markov Chain Monte Carlo methods. The R-INLA package can be downloaded from http://www.r-inla.org/. INLA uses Bayesian Inference, which first finds prior distributions of parameters before considering the observed data. INLA approximates the posterior distribution of parameters by computing the likelihood of the prior distributions based on observed data.

There are different models available in the R-INLA package. For this project, we used six models. The first model we used is the baseline Fixed Effects Model, a multivariate Poisson regression model, that only considers explanatory variables. The second model has both fixed effects as well as random effects. The third, the Intrinsic Conditional Autoregression (ICAR) or Besag Model, has a spatial random component. The Besag, York and Mollié (BYM) model, is an extension of the Besag Model, as it has both an ICAR component and a non-spatial random component. The Leroux Model combines aspects of the Besag and the BYM Models. The Spatial Lag Model considers both the covariate values of the LGA, as well as the values of the neighbouring regions' response variable.


![Rplot03](https://user-images.githubusercontent.com/78997343/221331926-69d37279-3781-478e-9c0e-b387c53d461b.png)
Here, distance to bike paths and percentage of people over 65 years old are the covariates for these models. The DIC and WAIC show how well the models fit. The lower the DIC and WAIC, the better the model. For this combination of covariates, the IID model has the best fit.

![image](https://user-images.githubusercontent.com/78997343/221332034-eba5776e-00ae-40c1-955e-0c1c817a386a.png)




