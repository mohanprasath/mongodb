# M001 Mongo DB Basics

## Chapter 0 Setup

* Tools: Compass(visual interface), Atlas(DB as a Service), shell
* start the mongo shell using the following command in the prompt in win, without connecting to any instances of the db
    `mongo --nodb`
* For installing mongodb in other OS, refer the docs in the download center
* Atlas:
  * DB as a service solution
  * replication is handled
  * clusters can be deployed
  * use the free tier for this course, no expiry date
  * look for other services provided by mongodb: like Data Explorer, charts, stitch, etc

## Chapter 1 Introduction

* JSON - JavaScript Object Notation
* suppoted data types are string, number, object, array, boolean, null
* Databases, collections and documents(each contains the following stuff)
* the above three in combinations creates a namaspace
* Scalar Value Types <https://youtu.be/N4E3TBHul0w>
* Aggregate Value Types - Fields with Documents as Values <https://youtu.be/KM_GMvAinG8>
* Aggregate Value Types - Fields with Arrays as Values <https://youtu.be/gz3Hpd_Sl9U>
* Aggregate Value Types - Geospatial Data <https://youtu.be/hgPuNdCZfAw>
* Filtering Collections with Queries <https://youtu.be/R6RKfhpHfd8>
  * schema in compass gui, lets you see visibly the data and their info
  * geo data can be viewed as well
  * any selection of types of data automatically makes an equality filter
  * $gte, $lt are operators in mongodb
* CRUD - Create, Read, Update, Delete
