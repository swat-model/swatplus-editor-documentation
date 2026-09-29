# Recall (Point Source/Inlet)

Recall objects are used for connecting point source or inlet data to your watershed. If you added point source in QSWAT+, when you import your project into SWAT+ Editor it will be connected via the recall section.

By default, constant data with all zero values during the default simulation period is added. To add your own recall data, click the recall item in the edit menu under connections.

## Sample Data

[Download sample data.](https://plus.swat.tamu.edu/downloads/sample_files/point-source/swatplus-editor-point-source.zip) Please read the README.txt file in the zip carefully.

## Constant Data

By default, your recall data is imported as constant. To insert your values, you can edit each item individually by clicking the edit button and manually entering each value. Alternatively, you may upload a CSV of your data.

From the recall section, click the import/export button from the action bar at the bottom. Import is selected by default, so click the export button toggle. Choose a folder name, and click the export data button to get a template for your data.

Constant data will be located in the `recall.csv` file in the directory you selected. Edit the CSV as needed, save, and then go back to the editor and click the import/output button again. This time toggle the import button. Choose your directory containing your modified files and click the import CSV data button. Your updated values will appear in the table.

## Time Series Data

By default recall data is imported as constant, however this can be changed by clicking the edit button next to a row in the recall data table. Select the new time step for your data: daily, monthly, or yearly. Click the save changes button. Next, press the back button to go back to the table view. Click the import/export button. Import is selected by default, so click the export button toggle. Choose a folder name, and click the export data button to get a template for your data.

Your directory may now contain two files: a recall.csv containing constant data, and another csv file named for the recall object (e.g., `pt002`) you changed to time series.

Open the time series file after it is exported to see the template for your data. Modify your data as needed matching the time step you selected previously. Be sure the years match your simulation run time.&#x20;

You change other recall objects from constant to time series, and you can mix and match all different types (constant, yearly, monthly, and daily). For any recall objects moving from constant to time series, first delete its row in `recall.csv`. Then create a new csv with the file name matching the recall object's name and insert your time series data. Similarly, if you want to move from time series back to constant, just delete the time series file and add a row back into `recall.csv` for the object.

To import your data, click the import/export data button again and this time click to toggle import. Choose your directory and click import data. Your new data will appear in the table.

## Recall Data Definitions

| Field    | Type | Description                               | Units      |
| -------- | ---- | ----------------------------------------- | ---------- |
| jday     | int  | Julian day                                |            |
| mo       | int  | Month                                     |            |
| day\_mo  | int  | Day of the month                          |            |
| yr       | int  | Year                                      |            |
| ob\_typ  | text | Type of recall (pt_day, pt_mon, or pt_yr) |            |
| ob\_name | text | Name of recall object                     |            |
| flo      | real | Volume of water                           | m^3        |
| sed      | real | Sediment                                  | metric ton |
| orgn     | real | Organic nitrogen                          | kg N       |
| sedp     | real | Organic phosphorus                        | kg P       |
| no3      | real | Nitrate                                   | kg N       |
| solp     | real | Mineral (soluble P)                       | kg P       |
| chla     | real | Chlorophyll-a                             | kg         |
| nh3      | real | Ammonia                                   | kg N       |
| no2      | real | Nitrogen dioxide                          | kg N       |
| cbod     | real | Carbonaceous biological oxygen demand     | kg         |
| doc      | real | Dissolved oxygen                          | kg         |
| sand     | real | Detached sand                             |            |
| silt     | real | Detached silt                             |            |
| clay     | real | Detached clay                             |            |
| sag      | real | Detached small ag                         |            |
| lag      | real | Detached large ag                         |            |
| gravel   | real | Gravel                                    |            |
| tmp      | real | Temperature                               | deg c      |


For more information, refer to the [SWAT+ Documentation](https://swatplus.gitbook.io/io-docs/introduction/point-sources-and-inlets){ target="_blank"}.