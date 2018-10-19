# sg-neighborhood

# SG Neighbourhood segmentation

## Introduction

For many people, the idea of relocating to a new country is an exciting and daunting prospect. This could be for work commitments, or simply for a lifestyle change. Finding the right accommodation and housing is never easy. In this project I consider the city like Singapore because it is very attractive for expats around the world. When a foreigner is in Singapore, he or she might face difficulty finding an apartment, very much of a time is when you can't decide on the location, and you don't know what's best for your family and yourself. Consider the amenities nearby, like do I require an MRT nearby? Or do you need a supermarket nearby. These are also critical to your everyday life, as they will pose convenience.

So, in this project I am going to segment the Singapore into different neighborhoods using the geographical coordinates of different buildings, and the geographical coordinates of top 100  venues around this particular building (within 500 meters). Finally, I applied the machine learning to group the neighbourhoods into clusters.

## Business Problem

My project may be useful for real estate agencies (or relocation agencies) and their customers to find the right accommodation and house for them. For instance, Mr Smith currently staying at The Paterson Edge Condo. This condo is locate in the posh are Orchard whith a great neighborhood venues (MRT station, shopping centers, cinema, grocery stores, hospital, primary school). Howevere, Mr Smith's youngest daughter is going to an international school soon, which is located near East Coast Area. Therefore, Mr Smith would like to move to the new area, but with similar neighborhood. 
The neighborhood clustering approach is one of the possible recommendation system which Mr Smith may use in his search.

## DATA

The main dataset is collected from the open repository: https://github.com/xkjyeah/singapore-postal-codes. It provides the .json file which is a dump of all Singapore postal codes retrieved from Onemap.sg API. From the input json file I extracted only: 'Postcode', 'Building', 'Latitude', 'Longitude'. After cleaning data by removing all NIL values I got 155 744 rows. This is a big number. For a further analysis (and because I have a limit of using external libray like Foursquare API), I randomly select 500 buildings. Next, I found that some buildings, out of 500, appers multiple times. Therefore, after removing all duplicates I left with 353 unique Buildings.

In addition, to the building's geographical coordinates, I incorporated the Foursquare API, to extend my dataset. The final dataset contains  the building's names and their geographical coordinates, all venues names  within 500 meters and their geographical coordinates, and in addition venue's categories. In total I have 7371 rows, with 353 buildings, 3815 unique venues from 320 unique venue categories. All data are attached in this repository.

## Methodology section
### Data Cleaning
The raw data from contains 155 744 rows. Each row represents one neighbourhood with postcode and geographical coordinates. Some neighbourhood has a NIL values for it's name, therefore, I droped them. Next, for a further analysis, I sample the data by randomly selecting only 500 rows. This was done because the Foursquare API free account has a limit on number of server-calls I can do every day. Out of 500 random Neighbourhoods 58 were duplicates. All duplicates were removed.

Then, using Foursquare API, for each Neighbourhood I found all venues within 500 meters, their geographical coordinates and categories. The merged dataset has 3815 unique venues from 320 unique categories. 

### Exploratory Data Analysis
Let's explore the neighborhoods in our dataset. For such place like PAGODA HOUSE, which is located in the central part, Foursquare returned 100  venues. This is the maximum number of returned venues. Also results suggested that all Neighbourhoods has at least 1 venue within 500 meters.

Then I analysed each Neighborhood. First, I grouped rows by neighborhood and by taking the mean of the frequency of occurrence of each category. Next I calculate top 5 venue's categories that located most often. For this porpose, for each venue category sum up the frequency. Not surprisingly, t most common venue's  categories are Bus Station, Coffee Shop,  Food Court, Cafe, Chinese Restaurant.

### Cluster Neighborhoods
To cluster  neighbourhood the KMeans method was used. The number of clusters was set to 8. I vary different numbers, but with more number of clusters the model prodused many cluster of size 1, with less number of clusters the model prodused one cluster with a huge number of members.
In the next section we will continue to discuss our results.

## Results.

From the results, I observed that clusters have different size. There is one large cluster with 195 members. THis result is expected, because in Singapore the urban development is very uniform, which means that every neighbourhood is developed to be convinient for its residents. Others clusters size is vary from 7 to 44,and one cluster very small of size 2. 

For the clustering problem one bussines problem was investigated.
### The Business Problem: 
We have a customer who recently relocated to Singapore. The first month he was staying in the Paterson Edge Condo. Unfortunately, his monthes fees are very high in this area, but the neirborhood is very lovely. Therefore, our customer is looking for a new house in a less expencive area but with a nice community around him.

### SOLUTION:
Using our clusters, we are going to find to which cluster The Paterson Edge is belong. Then we will highlight all members of this cluster on the SG MAP, and analise it.

From my results, The Paterson Edge  belongs to the biggest cluster. This is good, because our customer can select from different options. For instance, we can propose to our customer consider the SEA VIEW PARK condo in the East Coast Area. It will be much cheaper than Orchard area, but with a lovely neighborhood.

## Discussion 
### The Business Problem: 
During relocation to a new country some expats prefer to stay near cultural centers, for instance close to Art galleries. Using our dataset, I can quickly get all residential properties withing a working distance from art galleries. For this porpose I simply filtered my merged dataset by the venue category "Art Gallery". As expected, most places, which are close to some art gallery, are located in the Central parts of Singapore.

## Conclusion
This project shows that neigbourhood segmentation may be very useful in Singapore, and can be applied to a different business cases. Even using a sample data we got a meaningful results. With current sample dataset we tried a simple kMean clustering. Potentially, this project should be extended to a large dataset. The more advanced clustering algorithms have a potential to produce  interesting  results. 
