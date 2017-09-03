# DataVicGovAuPTDataCleaner
A series of Jupyter notebooks that process raw data from Data.Vic.Gov.Au relating to public transport so they can be used for mapping.

This github also provides an audit trail to document my assumptions and to ensure the maps are reproducible.

## Goal 1: A "Mode Agnostic" ranking of Public Transport stops.
Convert bus, tram and train boarding, alighting and station entry information to a consistent data format,
Then map as by colour coded 'Metlink Stop ID' points using qgis.


### Tram Boardings and Alightings at Tram Stops
https://www.data.vic.gov.au/data/dataset/tram-boardings-and-alightings-at-tram-stops-2015
Data Coverage period 01/01/2011 to 31/12/2011 (7:00am to 7:00pm weighted observations)

#### Step 1: Download raw tram boarding data, save a local copy in ./raw directory
Download 'Tram Boardings and Alightings 2011 - data.XLS' manually.
The web page has a 'I consent to terms and conditions / I am not a robot' that makes automated downloading hard.
Save file to './raw' directory

#### Step 2: Run TramBoardingAlighting_DataCleaner.ipynb
This script groups all the reported tram boardings and alightings for a given stop
If multiple trams use the same stop the output it will return one value for boardings and a second for alightings.
Notebook creates'./clean/TramStopTraffic.csv' with index 'Metlink_Stop_ID' and columns 'Boardings', 'Alightings' and 'DailyUse' ('DailyUse' is sum of Boardings and Alightings)

### Bus Boardings and Alightings at Bus Stops
https://www.data.vic.gov.au/data/dataset/bus-boardings-and-alightings-at-bus-stops-new
Data Coverage Perod 01/01/2007 to 31/12/2010 (7:00am to 7:00pm weekday weighted observations)
(Repeat Tram Steps)

### Tram Station Entries
https://www.data.vic.gov.au/data/dataset/train-station-entries-2008-09-to-2011-12-new
Data Temporal Coverage:	01/07/2008 to 30/06/2012  ('Normal Weekeday' results cover an entire day)
Does not include a Metlink Stop ID field

### Mapping results:
Download Base Public Transport Shape Files
Available from 'Public Transport a collection of PTV datasets'
https://www.data.vic.gov.au/data/dataset/public-transport-a-collection-of-ptv-datasets

#### Use QGIS to join layer ptv_tram_stop to 'TramStopTraffic.csv'
Where 'layer ptv_tram_stop.MET_STOPID = TramsStopTraffic.Metlink_Stop_ID
