# sg-neighborhood

# SG Neighbourhood segmentation

## DATA

The main dataset is collected from the open repository: https://github.com/xkjyeah/singapore-postal-codes. It provides the .json file which is a dump of all Singapore postal codes retrieved from Onemap.sg API. From the input json file I extracted only: 'Postcode', 'Building', 'Latitude', 'Longitude'. After cleaning data by removing all NIL values I got 155 744 rows.

In addition, to the building's geographical coordinates, I incorporated the Foursquare API, to extend my dataset. The final dataset contains  the building's names and their geographical coordinates, all venues names  within 500 meters and their geographical coordinates, and in addition venue's categories. 
