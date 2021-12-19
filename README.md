TODO: 
https://docs.atlas.mongodb.com/atlas-search/tutorial/run-query/#std-label-fts-tutorial-run-query
Query data from node app ^

Got venmo data from https://github.com/sa7mon/venmo-data

Load in BSON data to atlas:
 mongorestore --uri mongodb+srv://[USERNAME]:[PASSWORD]@cluster0.abbj1.mongodb.net/[DATABASE] venmo.bson


How docs sayLoad in JSON data to atlas:
mongoimport --uri "mongodb+srv://[USERNAME]:[PASSWORD]@cluster0.abbj1.mongodb.net/[DATABASE]?ssl=true&replicaSet=myAtlasRS&authSource=admin" --collection venmo --drop --file ./atlas_export.json

This actually worked:
mongoimport --uri "mongodb+srv://[USERNAME]:[PASSWORD]@cluster0.abbj1.mongodb.net/[DATABASE]" --collection venmo --drop --file ./atlas_export.json --jsonArray 

NOTE: my database is named 'test'

Ideas
since there is only 512 MB for the free tier of atlas, maybe I should cull the 
transaction list down to the most interesting ones

This is only about 342,000 venmo transactions

create a "page rank" for venmo transactions 
rank up for:
- note length
- more comments 
- more likes
- more mentions

assign every transaction a score
+1 point for every word or emoji in the `note`
+1 point for every word or emoji in every comment
~~+1 point for every mention~~
~~+2 points for every like~~

Looped through 7 million records to calculate the score on each one
This nearly set my 2.6GHZ 6Core i7 32GB MBPro on fire
In hindsight maybe I should have calculated a virtual field w/ mongoose, but this was the easy, dumb way of doing it. 
After about an hour I had at least 500,000 scores calculated, which was a big enough dataset to load into atlas

So I created a view and sorted by 


OR 

filter by power-users? 
- No: we want to leverage full text search to find insights, so even if a user performs a lot of txns, we might not get much interesting
data from them if they do not leave notes. 

---

1. scrape venmo for structured transaction data and load into mongodb
https://github.com/sa7mon/venmo-data

aggregate various sources of data then use full text search to look for 
similarites

mongodb+srv://USERNAME:PASSWORD@cluster0.abbj1.mongodb.net/test


connecting to atlas
mongosh "mongodb+srv://cluster0.abbj1.mongodb.net/venmo" --username USERNAME 

Twitter 

Finding a good data set
Performing searches on that data

Maybe something to do with SF parklets 
outdoor dining
scrape reddit, twitter for posts about san francisco outdoor dining
full text search for 

we need multiple datasets on which we can perform full text search into

aggregate datasets into one or two collections

3 related collections


https://github.com/awesomedata/awesome-public-datasets#readme

https://archive.org/details/2015_reddit_comments_corpus