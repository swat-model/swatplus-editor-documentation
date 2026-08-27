---
title: Home
description: Documentation for the SWAT+ Editor, and interface for editing SWAT+ model input files.
hide:
  - navigation
---

# SWAT+ Editor Documentation

SWAT+ Editor is a program that allows users to modify SWAT+ inputs easily without having to touch the SWAT+ input text files directly. The editor will import a watershed created in QSWAT+, or allow the user to create a SWAT+ project from scratch. The user may write input files and run the SWAT+ model through the editor.

[Download SWAT+ Editor](https://swat.tamu.edu/software/){ .md-button .md-button--primary target="_blank" }

## Getting Started & Troubleshooting

Visit the SWAT website for quick start guides and troubleshooting tips for SWAT+ Editor. This site focuses on advanced features and detailed documentation.

* [Quick Start Guide for QSWAT+ and SWAT+ Editor](https://swat.tamu.edu/software-test/quick-start/){ target="_blank" }
* [Troubleshooting Common Errors](https://swat.tamu.edu/software-test/troubleshooting/){ target="_blank" }
* [SWAT+ Editor User Support Group](https://groups.google.com/d/forum/swatplus-editor){ target="_blank" }

## Database Design

SWAT+ Editor uses a [SQLite](https://www.sqlite.org/){ target="_blank" } database to hold model input data to allow easy manipulation by the user. The database is structured to closely resemble the SWAT+ ASCII text files in order to keep a clean link between the model and editor. The following conventions are used in the project database:

* The table names will match the text file names, replacing any “.” or “-“ with an underscore “\_”.
* The table column names will match the model’s variable names. All names use lowercase and underscores.
* Any text file with a variable number of repetitive columns will use a related table in the database. For example, many of the connection files contain a variable number of repeated outflow connection columns (obtyp\_out, obtyno\_out, hytyp\_out, frac\_out). In the database, we represent these in a separate table, basically transposing a potentially long horizontal file to columns.
* All tables will use a numeric “id” as the primary key, and foreign key relationships will use these integer ids instead of a text name. This will allow for easier modification of these object names by the user and help keep the database size down for large projects.

A separate SQLite database containing common datasets and input metadata will be provided with SWAT+ Editor along with optional [SSURGO and STATSGO soils](https://plus.swat.tamu.edu/downloads/swatplus_soils.zip) and [weather generator](https://plus.swat.tamu.edu/downloads/swatplus_wgn.zip) databases.

### Database Access in the Python API

SWAT+ Editor uses the [Peewee ORM](http://docs.peewee-orm.com/){ target="_blank" } ([object-relational mapping](https://en.wikipedia.org/wiki/Object-relational_mapping)){ target="_blank" } to represent and work with the tables in Python. The use of an ORM provides a layer of abstraction and portability in hopes of streamlining future SWAT+ development projects.

Relationships are defined in a [Peewee ORM](http://docs.peewee-orm.com/){ target="_blank" } python class as a `ForeignKeyField`. In the python class, the field will be named after the object it is referencing. In the database, this name will automatically be appended by the referencing table’s column name, which is usually `id`.

For example, we have two tables representing soils: soils (`soils_sol`) and layers (`soils_sol_layer`). The layer table has a foreign key to the main soils table, so we know to which soil the layer belongs. In the python class, this field is named `soil`, and in the database it is called `soil_id`.

## Technologies

The following software is used to create and build SWAT+ Editor:

* [Node.js](https://nodejs.org/en/){ target="_blank" }
* [Electron](https://electron.atom.io/){ target="_blank" }
* [Vue.js 3.x](https://vuejs.org/){ target="_blank" }
* [Python 3.x](https://www.python.org/){ target="_blank" }
* [PyInstaller](http://www.pyinstaller.org/){ target="_blank" }
* [SQLite](https://www.sqlite.org/){ target="_blank" }
* [Peewee ORM](http://docs.peewee-orm.com/){ target="_blank" }