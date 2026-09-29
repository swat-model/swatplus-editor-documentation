# Programmatic Access

You may use the editor's API executables to automate project workflow tasks without having to use the GUI. This may be found in the SWAT+ Editor install directory under `\resources\app.asar.unpacked\static\api_dist`. You will use the `swatplus_api` executable. The `swatplus_rest_api` executable is for connecting to the GUI.

Refer to the [`/src/api/swatplus_api.py`](https://github.com/swat-model/swatplus-editor/blob/main/src/api/swatplus_api.py){ target="_blank"} file in the SWAT+ Editor GitHub repository for a full list of available actions and parameters.

## Create a Project Database

Initialize a new project database file with the following command. Your `swatplus_datasets.sqlite` file must already exist.

```
swatplus_api create_database
    --db_type=project
    --db_file="/full_path_to/my_project.sqlite"
    --db_file2="/full_path_to/swatplus_datasets.sqlite"
    --project_name=MyProject
    --editor_version=4.0.3
```

## Import WGN Data

```
swatplus_api import_weather
    --project_db_file="/full_path_to/my_project.sqlite"
    --delete_existing=y
    --import_type=wgn
    --create_stations=n
    --import_method=two_file
    --file1="/full_path_to/stations.csv"
    --file2="/full_path_to/monthly_values.csv"
    --delete_existing_stations=n
```

Options definitions:

| Flag Option   | Definition                  |
| ------------- | --------------------------- |
| `--delete_existing` | Enter y or n to delete existing WGN stations |
| `--import_type`     | Enter wgn                                    |
| `--create_stations` | Enter y or n to create weather stations based on wgn data; recommend n unless not using observed weather data |
| `--import_method`   | Enter database, two_file, or one_file        |
| `--file1`           | Full path to stations CSV file for two_file, or full WGN csv for one_file method; not needed for database method |
| `--file2`           | Full path to month values CSV file for two_file method; not needed for other methods |
| `--delete_existing_stations` | Enter y or n to delete existing weather stations (note: this refers to your weather-sta.cli stations) |

## Import Observed Weather Data

```
swatplus_api import_weather
    --project_db_file="/full_path_to/my_project.sqlite"
    --delete_existing=y
    --import_type=observed2012
    --create_stations=y
    --source_dir="/full_path_to/weather_files"
```

Options definitions:

| Flag Option   | Definition                  |
| ------------- | --------------------------- |
| `--delete_existing` | Enter y or n to delete existing weather stations |
| `--import_type`     | Enter observed2012 for SWAT2012 format, or observed for SWAT+ format |
| `--create_stations` | Enter y or n to create weather stations; recommend y unless data already exists that you want to reuse |
| `--source_dir`      | Full path to your weather files directory; not needed for SWAT+ format |

Note: you should manually set the `weather_data_dir` column of your `project_config` table in your project sqlite database. Typically this is set to `Scenarios/Default/TxtInOut` unless your want to keep your weather files in a separate location for reuse.

## Write Input Files

Input files are written based on the contents of your project sqlite database. Data entry to the database can be done with standard SQL commands. Refer to the [How to Use SQLite](../sqlite.md) page to get started.

```
swatplus_api write_files
    --project_db_file="/full_path_to/my_project.sqlite"
    --swat_version="62.0.1"
```

## Read Output

Running the model can be done directly with the SWAT+ model executable; it does not go through the editor. When model run is complete, read the output csv files (IMPORTANT: csv format must be selected in print.prt) into a sqlite database that can be used in SWAT+ Check and visualization.

```
swatplus_api read_output
    --output_files_dir="/full_path_to/Scenarios/Default/TxtInOut"
    --output_db_file="/full_path_to/Scenarios/Default/Results/swatplus_output.sqlite"
    --swat_version="62.0.1"
    --editor_version=4.0.3
    --project_name=MyProject
    --only_read_swatcheck=n
```

## Get SWAT+ Check Data

Return the output data read by SWAT+ Check and save to a `.json` file.

```
swatplus_api get_swatplus_check
    --project_db_file="/full_path_to/my_project.sqlite"
    --output_db_file="/full_path_to/Scenarios/Default/Results/swatplus_output.sqlite"
    --file1="/full_path_to/Scenarios/Default/Results/swatplus_check.json"
```