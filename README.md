# DataVicGovAuPTDataCleaner
A series of Jupyter notebooks that process raw data from Data.Vic.Gov.Au relating to public transport so they can be used for mapping.

This github also provides an audit trail to document my assumptions and to ensure the maps are reproducible.

## Goal 1: A "Mode Agnostic" ranking of Public Transport stops.
Convert bus, tram and train boarding, alighting and station entry information to a consistent data format,
Then map as by colour coded 'Metlink Stop ID' points using qgis.

### Bus Boardings and Alightings at Bus Stops
Data Source https://www.data.vic.gov.au/data/dataset/bus-boardings-and-alightings-at-bus-stops-new
Data Coverage Perod 01/01/2007 to 31/12/2010 (7:00am to 7:00pm weekday weighted observations)

#### Step 1: Download raw tram boarding data, save a local copy in ./raw directory
Download Bus boardings and alightings xls file manually.
The web page has a 'I consent to terms and conditions / I am not a robot' button that prevents automated downloading (or at least makes it harder than I expected).
Save file to './raw' directory

#### Step 2: Run BusBoardingAlighting_DataCleaner.ipynb
This script groups all the reported bus boardings and alightings for a given stop
If multiple buses use the same stop the output it will return one value for boardings and a second for alightings.

Notebook creates'./clean/BusStopTraffic.csv' with index 'Metlink_Stop_ID' and columns 'Boardings', 'Alightings' and 'DailyUse' ('DailyUse' is sum of Boardings and Alightings)



### Tram Boardings and Alightings at Tram Stops
https://www.data.vic.gov.au/data/dataset/tram-boardings-and-alightings-at-tram-stops-2015
Data Coverage period 01/01/2011 to 31/12/2011 (7:00am to 7:00pm weighted observations)

Data appears to have a the missing column  'Day Type' column, a categorical variable classifying boarding alighting result as either "Weekday", "Saturday" or "Sunday".  This column is mentioned in the data definition but missing from the data.
Most of the tram boarding / alighting data appears to be grouped into collections of three rows where the first nine columns are identical.   Data that does not match this pattern has only a single row. 

It is assumed that the first instance of a row with nine identical columns is "Weekday",  
The second and third (when they exist) are assumed to be "Saturday" and "Sunday" respectively.  

For the purposes of comparison with bus boarding alighting data, only Weekday columns are of interest.

### Train Station Entries
https://www.data.vic.gov.au/data/dataset/train-station-entries-2008-09-to-2011-12-new
Data Temporal Coverage:	01/07/2008 to 30/06/2012  ('Normal Weekeday' results cover an entire day)

Does not include a Metlink Stop ID field


### Mapping results:
Download Base Public Transport Shape Files
Available from 'Public Transport a collection of PTV datasets'
https://www.data.vic.gov.au/data/dataset/public-transport-a-collection-of-ptv-datasets

#### Use QGIS to join layer ptv_tram_stop to 'TramStopTraffic.csv'
Where 'layer ptv_tram_stop.MET_STOPID = TramsStopTraffic.Metlink_Stop_ID
