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