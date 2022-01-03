# Venmo Search 

Deployed here:

https://reidjs.github.io/venmo-search-frontend/

## About

Uses MongoDB's Atlas Search to search hundreds of thousands of Venmo transactions. Made for dev.to's mongodb hackathon

![demo](demo.gif)

## Why

I built this to explore using MongoDB's Atlas Search as an alternative to ElasticSearch for full text search. I used Venmo data because

1) it's public
2) users are forced to leave a text "comment" for every transaction


## Usage

Production
1. Go to https://reidjs.github.io/venmo-search-frontend/
2. Type a query

Local Development
1. Start backend https://github.com/reidjs/venmo-search-server
2. Start frontend with `npm run dev`
3. Open browser to localhost:8000


## Notes

Venmo dataset from https://github.com/sa7mon/venmo-data 
- Out of the 7,000,000 transactions, I only used about 342,000 venmo transactions (free tier Mongo Atlas)
- To decide which transactions went into the database, I 'ranked' each transaction according to how long the comment was. Longer comment = more likely to be in database. 

How to load in BSON data to atlas:
`mongorestore --uri mongodb+srv://[USERNAME]:[PASSWORD]@cluster0.abbj1.mongodb.net/[DATABASE] venmo.bson`


How to Load in JSON data to atlas:

`mongoimport --uri "mongodb+srv://[USERNAME]:[PASSWORD]@cluster0.abbj1.mongodb.net/[DATABASE]" --collection venmo --drop --file ./atlas_export.json --jsonArray`

