# Ebay car sales data analysis

This is the first project I've decided to publish. Apart from doing the usual data cleaning as requested by Dataquest for this project, I have chalanged myself to do a few additional tasks:
* extracted engine size from 'name' column where it was easily achieveble (in about 14500 rows)
* filled 4000 cells of power column with average power value for each brand respectively (instead of filling it with an average power value for the whole database)
* inspected rows with 'sontiage_autos' brand and reassigned 80% of these entries to their correct brand
* came across faulty data in post-2015 entries (and removed it)
* plotted average price data on the map of Germany

# Index 

* [1. Data inspection and cleaning](#inspect_clean1) 
    * 1.1.   [General info](#general11) 
    * 1.2.   [Column names](#column_names12) 
    * 1.3.   [Odometer column](#odometer13) 
    * 1.4.   [Price column](#price14)  
        * 1.4.1. [Inspecting expensive cars](#expensive141) 
        * 1.4.2. [Inspecting low prices](#lowprices142) 
    * 1.5.   [Brands - sonstige_autos](#brands15)  
    * 1.6.   [Dates](#dates16) 
    * 1.7.   [Registration year column](#registration17)  
    * 1.8.   [Power](#power18) 
        * 1.8.1. [Filling in the missing power values](#fillpower181) 
    * 1.9. [Engine size](#engine19)
    
* [2. Lets start analyzing](#analyze20) 
    * 2.1. [How cars change](#change21) 
    * 2.2. [back to brands](#brands22) 
        * 2.2.1. [Brands with unrepaired damage](#repair221) 
    * 2.3. [Power and engine size](#powerengine23) 
    * 2.4. [Are engines becoming more efficient?](#efficient24) 
        * 2.4.1. [Which models are the most power efficient?](#models241) 
    * 2.5. [Gearbox](#gearbox25) 
    * 2.6. [Location](#location26) 
    * 2.7. [Conclusions](#last27)
