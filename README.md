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
![image](https://user-images.githubusercontent.com/78997343/219908191-0d50a91a-0a34-4c36-9ef0-9d050165490b.png)

