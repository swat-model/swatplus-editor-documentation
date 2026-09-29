# Weather Generator

Weather generator (wgn) data is required for SWAT+ to run. If you do not have your own wgn data, you may use the database supplied with the SWAT+ installer, or [download it here](https://plus.swat.tamu.edu/downloads/swatplus_wgn.zip).

While you can create each station and its 12 months of values individually, it is much simpler to use the Import Data button at the bottom of the screen.

## Usage with Observed Weather Data

If you are using observed weather data and prefer to have weather stations created based on this data (recommended), check this box&mdash;stations will not be created when you start wgn import, and instead they will be created for you when you import your observed weather data files.

If you are not using observed weather data, it is important to leave the box unchecked so that weather stations are created for you.

## Import from Database

If you have the global wgn database installed, it will be selected as the default data format as well as the CFSR global data table. USA wgn data is also available from this database; type wgn_us to use this table. You may also add your own data to this database using the wgn and corresponding wgn_mon tables. See the [How to Use SQLite](../sqlite.md) page for working with the database.

## Import from Two CSV Files

If you do not want to use the SQLite database, you may import CSV files of your weather generator data. The two file format allows for more vertical organization rather than 14 variables multipled by 12 months of horizontal columns. However, the two-file method requires you to create and keep track of an ID field to tie your stations and monthly values. Formatting requirements:

1. Stations CSV file:
   * Columns `id, name, lat, lon, elev, rain_yrs`
   * `id` should be uniquely numbered
2. Monthly values CSV file:
   * Columns `id, wgn_id, month, tmp_max_ave, tmp_min_ave, tmp_max_sd, tmp_min_sd, pcp_ave, pcp_sd, pcp_skew, wet_dry, wet_wet, pcp_days, pcp_hhr, slr_ave, dew_ave, wnd_ave`
   * `id` should be uniquely numbered
   * `wgn_id` corresponds to the `id` column from the stations file

Download a sample of the two-file CSV format [here](https://plus.swat.tamu.edu/downloads/sample_files/wgn/swatplus_tf_wgn_template.zip).

## Import from One CSV File

The last option is to import from a single CSV file with one wgn per row. Each measurement variable will have the month number 1-12 at the end. Trimmed for brevity below:

```
name,lat,lon,elev,rain_yrs,tmp_max_ave1,tmp_min_ave1,tmp_max_sd1, [...] pcp_hhr12,slr_ave12,dew_ave12,wnd_ave12
```

Download a sample of the one-file CSV format [here](https://plus.swat.tamu.edu/downloads/sample_files/wgn/swatplus_sf_wgn_template.csv).

## Field Definitions and Units

All inputs match the SWAT+ inputs. Documentation may be found [here](https://swatplus.gitbook.io/io-docs/introduction-1/climate/weather-wgn.cli){ target="_blank"}.