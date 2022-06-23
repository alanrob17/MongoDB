# Getting My RecordDB data into MongoDB

This is the process I use to upload all of my **RecordDB** SQL Server data into MongoDB.

## RecordDBToJSON

I run this program to create artists and records jSON files. This will be the latest version of the artists and records data that I have downloaded and formatted from SQL Server RecordDB data. This is the base for my MongoDB data. It contains the ``ArtistId`` but doesn't have the MongoDB ``Id``. I run ``record-db-to-mongo`` to upload the artists.json data into MongoDB. This will automatically add the MongoDB ``Id's``.

## record-db-to-mongo

Copy the ``artists.json`` data into the **_data** folder. There should already be an old ``records.json`` file in this folder. I am only interested in the ``artists.json`` file at the moment.

This program will have the artists.json and record.json files that DON'T have the MongoDB Id's in them.

First I need to run the following to delete the existing MongoDB documents in the **record-db** database.

```bash
 node index.js -d
```

Now run this process to upload the ``artists`` and ``records`` JSON files.

```bash
 node index.js -i
```

This installs the artists and records json files in the MongoDB **record-db** database.

**Note** it is important to note that the artists collection will have **NEW** MongoDB Id's and will NOT match the data in the records.json file which is old data.

## Export artists data from MongoDB

I am going to EXPORT the artists data from MongoDB to use in **ImportMongoJSON**.

----

## ImportMongoJSON

This program takes the exported **artists** data from MongoDB (with MongoDB Id's)

### Input

#### mongo-artists.json

This is the file that I **Export** from MongoDB as ``artists.json``. I rename it to ``mongo-artists.json`` and dump it into the bin\debug folder so that I can reformat it into "flattened" JSON.

Run this program and it will create ``artists.json`` and ``records.json``. Both of these files will be the latest RecordDB data combined with the generated MongoDB Id's.

I can then dump these two files into the **record-db-to-mongo\\_data** folder.

Go back to the **record-db-to-mongo** step above and re-run the *delete* and *insert* processes again to load the latest ``artists`` and ``records`` data into MongoDB.

You now have your current data in a MongoDB database.
