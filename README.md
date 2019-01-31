# sg-neighborhood

# SG Neighbourhood segmentation

## DATA

The main dataset is collected from the open repository: https://github.com/xkjyeah/singapore-postal-codes. It provides the .json file which is a dump of all Singapore postal codes retrieved from Onemap.sg API. From the input json file I extracted only: 'Postcode', 'Building', 'Latitude', 'Longitude'. After cleaning data by removing all NIL values I got 155 744 rows. This is a big number. For a further analysis (and because I have a limit of using external libray like Foursquare API), I randomly select 500 buildings. Next, I found that some buildings, out of 500, appers multiple times. Therefore, after removing all duplicates I left with 353 unique Buildings.

In addition, to the building's geographical coordinates, I incorporated the Foursquare API, to extend my dataset. The final dataset contains  the building's names and their geographical coordinates, all venues names  within 500 meters and their geographical coordinates, and in addition venue's categories. In total I have 7371 rows, with 353 buildings, 3815 unique venues from 320 unique venue categories. All data are attached in this repository.
