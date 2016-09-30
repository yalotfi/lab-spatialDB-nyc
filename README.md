# MSBA Lab: lab-spatialDB-nyc

A class lab designed to introduce spatial database management systems in PostgreSQL, ODBC workflow, and using R as a GIS from data wrangling to visualization.

## Installing PostgreSQL and PostGIS

I suggest downloading the OpenGeo stack distributed by [BoundlessGeo](http://boundlessgeo.com/products/downloads/).  It is completely free but in order to get the download files, you need to fill out a quick form and they should email you.  It makes installation of PostgreSQL, PostGIS, GeoServer and more super easy and hassle free.  Sometimes it takes some time to receive the files, so I will include direct installation of PostgreSQL and PostGIS for Windows and Mac OS.

### Windows:

* Retrieve the executables for [PostgreSQL from the EnterpriseDB distribution](http://www.enterprisedb.com/products-services-training/pgdownload) and choose the appropriate OS.
* Install PostgreSQL
* After installing it on your system, launch Application Stack Builder
  * Start -> Programs -> PostGreSQL 9.6 -> Application Stack Builder
  * Under Spatial Extensions, select the most recent PostGIS extension
* At this point, you should have a local postgres server on port 5432 and postGIS.

### Mac OS:

There is a very simple PostgreSQL distribution for Mac OSX called [postgres.app](http://postgresapp.com).  Just download the application and move the blue elephant icon into your applications folder, and run it.  Once pgsql is running you should see a small elephant in profile appear in your menu bar, which is normally located along the top of your desktop.  

You will also be interested in installing a GUI tool that will assist with a variety of functions, including viewing your tables and executing scripts.  A very popular and widely used GUI is pgAdmin4.  Please go ahead and install it from [pgadmin](https://www.pgadmin.org/download/macos4.php).  Some other popular PostgreSQL GUI tools are Postico, PG Commander, and Induction, which you can find links to from the [postgress.app page] (http://postgresapp.com/documentation/gui-tools.html).

## Create a New DataBase

With our new local server, let's create a new Database called `nyc`.
* Open pgAdmin and log into the localhost server with port 5432.
  * Password and username should be postgres
* Right click on Databases and create a new one.
  * Name it nyc and set owner to postgres

## Load Shapefiles

### OpenGeo:

The great thing about OpeGeo is that they include a Graphical User Interface (GUI) for the shp2pgsql command line interface called [pgShapeLoader or shp2pgsql-gui](http://suite.opengeo.org/opengeo-docs/dataadmin/pgGettingStarted/pgshapeloader.html).  At this point, it is very straightforward uploading your shapefiles from the data file into the database you just created.  Follow this guide if you received the OpenGeo distirbution in a timely manner.

### shp2pgsql:

PostGIS Command-Line Interface: [shp2pgsql-gui](http://suite.opengeo.org/opengeo-docs/dataadmin/pgGettingStarted/shp2pgsql.html)

## Explore Tables (PostgreSQL)

We can perform traditional `SELECT` queries to get a sense of the data we imported and what it can tell us.

## Geometric, GIS-related Queries (PostGIS Functions)

Notice the `geom` column in our tables.  This is a metadata column for storing the spatial information for each row.  We can use this to perform spatial joins and geometric functions like area or length calculations.

## ODBC with R

Our workflow will deal primairly with homicide and demographic stats.  We were able to get a sense of our data in SQL.  Now, we are ready to get into analysis which is best done in a tool like QGIS, ArcGIS, or R.  The first task is to connect our R session to our local Postgres database.  This is called Open DataBase Connection (ODBC) and is akin to how you can connect to a database in Excel.  The `ODBC.R` script loads the reuired packages and code so that we can run SQL queries natively in R.

Most real world data is going to be stored on a database, whether its Postgres, MySQL, MS SQL Server ect.  Understanding how we can combine the benefits of a relational database and a language like R is truly powerful.  The concept of ODBC applies across languages and tools.  Similar functionality exists in Python, for example.

## Data Wrangling in R 

Thanks to ODBC and multiple R libraries that facilitate communication with our RDBMS, we can pull data into R, clean it, and ultimately build beautiful maps!

We want to prepare our data in order to easily plot it using Hadley Whickham's awesome grammar of graphics syntax from `ggplot2`.  That means executing relevent queries from within R, perform multiple steps like fortifying the spatial elements and joining dataframes.  Thanks to the fact that data in an RDBMS is already structured and organized, there are relatively few steps we need to do.  There also is not missing or other issues that generally haunt data scientists.  That is another benefit of pulling from a database populated by pre-processed data.  That is certainly not always the case.

## R and ggplot2 as a GIS
With the right packages, we can turn R into an effective GIS.  That means importing shapefiles, transforming them, and of course mapping them.  Take a look at the `sourcePackages.R` scripts which calls GIS packages.  While PostGIS is by far the best way to organize sptial data and perform spatial manipulations, we can't actually present the data without connecting this back-end to a front-end system.  By front-end, I mean something like QGIS, CartoDB, ArcGIS, or in this case, R.  Keep in mind R is excellent at statistical modeling and packages like `spatstat` allow for powerful spatial statistical modeling as well. 

If you do not have PostgreSQL installed on your computer, you can also directly import shapefiles into R.  While not ideal when dealing with several layers, it is still nice to know that you can import, project, organize, and visualize basic shapefiles within R given the right packages.
