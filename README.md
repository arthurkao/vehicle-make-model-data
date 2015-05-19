# vehicle-make-model-data

Year, Make, and Model data of nearly all motor vehicle manufactured between 2001 and 2015, in sql, json, and csv format.

- [Features](#features)
- [Requirement](#requirement)
- [Installation](#installation)
- [Setup](#setup)
- [Examples](#example)
  - [What models does BMW manufacture in model year 2015?](#q1)
  - [What model years was BMW R1200GS in production?](#q2)
  - [How many motor vehicle manufactures are there in model year 2015?](#q3)
- [License](#license)

## Features<a name="features"></a>

Accurate motor vehicle make & model data since year 2001. This data set includes Car, Motorcycle, Truck, and UTV manufactures and their corresponding models. 
The data is database agnostic and is user-friendly as _same_ set of data is ported to mysql, json, and csv format. Json and csv data sets are flattened while mysql data set being normalized to 3 tables.
Currently there are 19,722 models and increasing.

## Requirement<a name="requirement"></a>

None

## Installation<a name="installation"></a>

```bash
$ git clone https://github.com/arthurkao/vehicle-make-model-data.git
$ cd ./vehicle-make-model-data
```

## Setup<a name="setup"></a>

### MySQL

Replace _myDBName_ with db name to your liking. Three tables, makes, make_years, and models , will be created with proper foreign key constraint(s).

```bash
$ mysql -uroot myDBName < mysql_data.sql 
```

### Mongo

Replace _myDBName_ with db name and _myCollectionName_ with collection name to your liking.

```bash
$ mongoimport -d myDBName -c myCollectionName --jsonArray --file json_data.json
```

### CSV

Open csv_data.csv in your favorite csv editor.

## Examples<a name="example"></a>

### What models does BMW manufacture in model year 2015?<a name="q1"></a>

###### MySQL

```sql
mysql> SELECT my.year, ma.name AS make, mo.name AS model FROM models mo
    JOIN make_years my on mo.makeyear_id = my.id
    JOIN makes ma on ma.id = my.make_id
    WHERE ma.name = 'BMW' and my.year = 2015
    ORDER BY model;
    
# +------+------+-----------------------------+
# | year | make | model                       |
# +------+------+-----------------------------+
# | 2015 | BMW  | 118I                        |
# | 2015 | BMW  | 220I                        |
# | 2015 | BMW  | 228I                        |
# | 2015 | BMW  | 228I XDRIVE                 |
# | 2015 | BMW  | 320I                        |
# | 2015 | BMW  | 320I XDRIVE                 |
# | 2015 | BMW  | 328D                        |
# | 2015 | BMW  | 328D XDRIVE                 |
# | 2015 | BMW  | 328I                        |
# | 2015 | BMW  | 328I GT XDRIVE              |
# ... 
# | 2015 | BMW  | M3                          |
# | 2015 | BMW  | M4                          |
# | 2015 | BMW  | M5                          |
# | 2015 | BMW  | M6                          |
# | 2015 | BMW  | M6 GRAN COUPE               |
# | 2015 | BMW  | X1                          |
# | 2015 | BMW  | X3                          |
# | 2015 | BMW  | X4                          |
# | 2015 | BMW  | X5                          |
# | 2015 | BMW  | X6                          |
# | 2015 | BMW  | Z4                          |
# +------+------+-----------------------------+
# 77 rows in set (0.00 sec)
```

###### Mongo

Replace _collectionName_ with the collection name set during setup

```javascript
> db.collectionName.find({ year: 2015, make: "BMW" });

# { "_id" : ObjectId("5559d73bd4ad885f71d607c1"), "year" : 2015, "make" : "BMW", "model" : "118I" }
# { "_id" : ObjectId("5559d73bd4ad885f71d607c2"), "year" : 2015, "make" : "BMW", "model" : "220I" }
# { "_id" : ObjectId("5559d73bd4ad885f71d607c3"), "year" : 2015, "make" : "BMW", "model" : "228I" }
# { "_id" : ObjectId("5559d73bd4ad885f71d607c4"), "year" : 2015, "make" : "BMW", "model" : "228I XDRIVE" }
# { "_id" : ObjectId("5559d73bd4ad885f71d607c5"), "year" : 2015, "make" : "BMW", "model" : "320I" }
# { "_id" : ObjectId("5559d73bd4ad885f71d607c6"), "year" : 2015, "make" : "BMW", "model" : "320I XDRIVE" }
# { "_id" : ObjectId("5559d73bd4ad885f71d607c7"), "year" : 2015, "make" : "BMW", "model" : "328D" }
# { "_id" : ObjectId("5559d73bd4ad885f71d607c8"), "year" : 2015, "make" : "BMW", "model" : "328D XDRIVE" }
# { "_id" : ObjectId("5559d73bd4ad885f71d607c9"), "year" : 2015, "make" : "BMW", "model" : "328I" }
# { "_id" : ObjectId("5559d73bd4ad885f71d607ca"), "year" : 2015, "make" : "BMW", "model" : "328I GT XDRIVE" }
# ...
# Type "it" for more
# ...

```

---

### What model years was BMW R1200GS in production?<a name="q2"></a>

###### MySQL

```sql
mysql> SELECT my.year, ma.name AS make, mo.name AS model FROM models mo
    JOIN make_years my on mo.makeyear_id = my.id
    JOIN makes ma on ma.id = my.make_id
    WHERE ma.name = 'BMW' and mo.name LIKE 'R1200GS%'
    ORDER BY my.year, model;
	
# +------+------+-------------------+
# | year | make | model             |
# +------+------+-------------------+
# | 2004 | BMW  | R1200GS           |
# | 2005 | BMW  | R1200GS           |
# | 2006 | BMW  | R1200GS           |
# | 2006 | BMW  | R1200GS ADVENTURE |
# | 2006 | BMW  | R1200GS HP2       |
# | 2007 | BMW  | R1200GS           |
# | 2007 | BMW  | R1200GS ADVENTURE |
# | 2007 | BMW  | R1200GS HP2       |
# | 2008 | BMW  | R1200GS           |
# | 2008 | BMW  | R1200GS ADVENTURE |
# | 2009 | BMW  | R1200GS           |
# | 2009 | BMW  | R1200GS ADVENTURE |
# | 2010 | BMW  | R1200GS           |
# | 2010 | BMW  | R1200GS ADVENTURE |
# | 2011 | BMW  | R1200GS           |
# | 2011 | BMW  | R1200GS ADVENTURE |
# | 2012 | BMW  | R1200GS           |
# | 2012 | BMW  | R1200GS ADVENTURE |
# | 2013 | BMW  | R1200GS           |
# | 2013 | BMW  | R1200GS ADVENTURE |
# | 2014 | BMW  | R1200GS           |
# | 2014 | BMW  | R1200GS ADVENTURE |
# +------+------+-------------------+
# 22 rows in set (0.00 sec)
```

###### Mongo

Replace _collectionName_ with the collection name set during setup

```javascript
> db.collectionName.find({ model: /^R1200GS/ });

# { "_id" : ObjectId("5559d73bd4ad885f71d5cc7f"), "year" : 2004, "make" : "BMW", "model" : "R1200GS" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5d1ce"), "year" : 2005, "make" : "BMW", "model" : "R1200GS" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5d743"), "year" : 2006, "make" : "BMW", "model" : "R1200GS" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5d744"), "year" : 2006, "make" : "BMW", "model" : "R1200GS ADVENTURE" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5d745"), "year" : 2006, "make" : "BMW", "model" : "R1200GS HP2" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5dccb"), "year" : 2007, "make" : "BMW", "model" : "R1200GS" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5dccc"), "year" : 2007, "make" : "BMW", "model" : "R1200GS ADVENTURE" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5dccd"), "year" : 2007, "make" : "BMW", "model" : "R1200GS HP2" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5e27f"), "year" : 2008, "make" : "BMW", "model" : "R1200GS" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5e280"), "year" : 2008, "make" : "BMW", "model" : "R1200GS ADVENTURE" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5e853"), "year" : 2009, "make" : "BMW", "model" : "R1200GS" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5e854"), "year" : 2009, "make" : "BMW", "model" : "R1200GS ADVENTURE" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5eded"), "year" : 2010, "make" : "BMW", "model" : "R1200GS" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5edee"), "year" : 2010, "make" : "BMW", "model" : "R1200GS ADVENTURE" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5f309"), "year" : 2011, "make" : "BMW", "model" : "R1200GS" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5f30a"), "year" : 2011, "make" : "BMW", "model" : "R1200GS ADVENTURE" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5f831"), "year" : 2012, "make" : "BMW", "model" : "R1200GS" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5f832"), "year" : 2012, "make" : "BMW", "model" : "R1200GS ADVENTURE" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5fd68"), "year" : 2013, "make" : "BMW", "model" : "R1200GS" }
# { "_id" : ObjectId("5559d73bd4ad885f71d5fd69"), "year" : 2013, "make" : "BMW", "model" : "R1200GS ADVENTURE" }
# Type "it" for more
```

---

### How many motor vehicle manufactures are there in model year 2015?<a name="q3"></a>

###### MySQL

```sql
mysql> SELECT count(id) AS num_of_active_manufacture FROM make_years WHERE year = 2015;

# +---------------------------+
# | num_of_active_manufacture |
# +---------------------------+
# |                        56 |
# +---------------------------+
# 1 row in set (0.00 sec)
```

###### Mongo

Replace _collectionName_ with the collection name set during setup

```javascript
> db.collectionName.aggregate([
  {$match: {year: 2015}},
  {$group: { _id: "$make" }},
  {$group: {
    _id: null,
    count: {$sum: 1}
  }}
])

# { "_id" : null, "count" : 56 }
```

## License<a name="license"></a>

MIT