# DataVicGovAuPTDataCleaner
A series of Jupyter notebooks that process raw data from Data.Vic.Gov.Au relating to public transport so they can be used for mapping.

This github also provides an audit trail to document my assumptions and to ensure the maps are reproducible.

## Goal 1: Create a "Mode Agnostic" ranking of Public Transport stops
Performance reporting for Victorian Buses, Trams and Trains are all slightly different
However, all reports include a stop identifier and some stop use information for a typical weekday in 2011 for the period 7am to 7pm.

Use jupyter notebooks to convert excel spreadsheets containing bus, tram and train boarding, alighting and station entry reports into .csv files listing 
 * stop identifier (use 'Metlink Stop ID' where available), 
 * boarding and alighting numbers (where available) and  
 * daily stop use - the sum of boarding and alighting results.
 
Use QGIS to join these results to the bus stop, tram stop and railway station layers in 
Base Public Transport Shape Files
Available from 'Public Transport a collection of PTV datasets'
https://www.data.vic.gov.au/data/dataset/public-transport-a-collection-of-ptv-datasets

Use QGIS display symbology to identify busy public transport stops.

### Why is this useful?
Nearly every public transport journey begins and ends with a walking trip.  Knowing which stops are currently the busiest helps road managers to prioritise bus, tram and train stop improvement projects to benefit the largest number of existing public transport users.  

Cavet: "Remember, when asked to prove that #bikelanes would be well used, it's hard to justify a bridge by the # of people swimming across a river." @BrentToderian 29 April 2014
