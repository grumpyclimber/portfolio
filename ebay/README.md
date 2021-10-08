# Ebay car sales data analysis

This is the first project I've decided to publish. Apart from doing the usual data cleaning as requested by Dataquest for this project, I have chalanged myself to do a few additional tasks:
* extracted engine size from 'name' column where it was easily achieveble (in about 14500 rows)
* filled 4000 cells of power column with average power value for each brand respectively (instead of filling it with an average power value for the whole database)
* inspected rows with 'sontiage_autos' brand and reassigned 80% of these entries to their correct brand
* came across faulty data in post-2015 entries (and removed it)
* plotted average price data on the map of Germany

# Index 

1. Data inspection and cleaning
    * 1.1.   General 
    * 1.2.   Column names
    * 1.3.   Odometer column
    * 1.4.   Price column
        * 1.4.1. Inspecting expensive cars
        * 1.4.2. Inspecting low prices
    * 1.5.   Brands - sonstige_autos
    * 1.6.   Dates
    * 1.7.   Registration year column
    * 1.8.   Power
        * 1.8.1. Filling in the missing power values
    * 1.9. Engine size   
2. Lets start analyzing
    * 2.1. How cars change
    * 2.2. back to brands
        * 2.2.1. Brands with unrepaired damage
    * 2.3. Power and engine size
    * 2.4. Are engines becoming more efficient
        * 2.4.1. Which models are the most power efficient
    * 2.5. Gearbox
    * 2.6. Location
    * 2.7. Conclusions
