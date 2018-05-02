# Working with MongoDB

## Installation

### Installing MongoDB community edition on windows

MongoDB Community Edition requires Windows Server 2008 R2, Windows 7, or later. 

Download the latest release of MongoDB from https://www.mongodb.org/downloads. The name of the extracted file should be mongodb-win32-i386-[version] or mongodb-win32-x86_64-[version]

Double-click the .msi downloaded file, a set of screens will appear to guide you through the installation process. Choose “Custom” installation to specify an installation directory e.g. d:\mongo
#### Run MongoDB

MongoDB requires a data directory to store all data. The default location for the MongoDB data directory is c:\data\db. Create this folder by running the following command in a Command Prompt:

```
md data\db
```
In order to install the MongoDB at a different location, you need to specify an alternate path for \data\db by setting the path dbpath in mongod.exe as following (Supposing that the mongodb installation folder is D:\mongo)

```
C:\>d:
D:\>cd "mongo\Mongodb\bin"
D:\mongo\Mongodb\bin>mongod.exe --dbpath "d:\mongo\data"
```
Now to run the MongoDB, you need to open another command prompt and run the following command:

```
D:\mongo\Mongodb\bin>mongo.exe
```

### Installing mongodb on Ubunto

Run the following command to import the MongoDB public GPG key
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
```
Create a /etc/apt/sources.list.d/mongodb.list file using the following command:
```
echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' 
   | sudo tee /etc/apt/sources.list.d/mongodb.list
```
Now issue the following command to update the repository:
```
sudo apt-get update
```
Next install the MongoDB by using the following command:
```
apt-get install mongodb-10gen = 3.6.3
```
In the above installation, 3.6.3 is currently released MongoDB version. Make sure to install the latest version always. 

#### Start MongoDB

```
sudo service mongodb start
```
To use MongoDB run the following command:
```
mongo
```
This will connect you to running MongoDB instance.


#### Stop MongoDB
Use the following command in order to stop mongodb:
```
sudo service mongodb stop
```

#### Restart MongoDB
Use the following command in order to restart mongodb:
```
sudo service mongodb restart
```
## Create database

In this tutorial, we will create a database to store our application logs.
Use the following command to create a new database named Logging. “Use” command will create a new database if it doesn't exist, otherwise it will return the existing database.
```
use Logging
```
To check the currently selected database, use the command db
```
>db
```
To check the databases list, use the command show dbs
```
>show dbs
```
## Drop Database

Use the following command to delete the selected database 
```
db.dropDatabase()
```
## Create Collection

Now let’s create a collection named logs within the logging database using the command below:
```
>db.createCollection("logs")
```
You can check the created collection by using the command show collections.
```
>show collections
```
## CRUD operations

### Insert document

Use the following command to insert a document in the logs collection
```
Db.logs.insert(
{
	Ip_address: "::ffff:54.221.205.80",
	Client_id:"client1",
	User_id:"user1",
	Date_time:new Date("2018-03-1T23:07:43"),
	Method:"POST",
	Endpoint:"/v1/data/publish/ISS/position",
	Protocol:"HTTP/1.1",
   Response_code: 200,
   Content_size:4
})
```
### Insert bulk documents

Use the following command in order to insert 2 documents to the logs collection:

```
db.logs.insert([
{
	Ip_address:"::ffff:54.243.49.1",
	Client_id:"client1",
	User_id:"user1",
	Date_time:new Date("2018-05-3T11:08:11"),
	Method:"POST",
	Endpoint: "/v1/data/write/klima/Temperature",
	Protocol:"HTTP/1.1",
	Response_code: 200,
	Content_size:4
},
{
	Ip_address:"::ffff:54.221.205.80",
	Client_id:"client2",
	User_id:"user2",
	Date_time:new Date("2018-03-2T11:00:21"),
	Method:"GET",
	Endpoint: "/v1/data/read/appliance/command?limit=1&source=raw",
	Protocol:"HTTP/1.1",
	Response_code: 404,
	Content_size:5
}]
)
```
### Query document

Use the following command to get all the documents in a given collection:
```
db.logs.find().pretty()
```
Use the following command to get all documents with response code 200:
```
db.logs.find({"Response_code":200}).pretty()
```
Use the following command to get all the documents where response code = 200 and Client_id = client1:
```
db.logs.find(
   {
      $and: [
         {Response_code : 200}, {Client_id:“client1”}
      ]
   }
).pretty()
```
To query the document on the basis of some condition, you can use following operations:

```
Equality: {<key>:<value>}
Less Than: key>:{$lt:<value>}}
Less Than Equals: key>:{$lte:<value>}}
Greater : {<key>:{$gt:<value>}}
Greater Than Equals: key>:{$gte:<value>}}
Not Equals: {<key>:{$ne:<value>}}
```
