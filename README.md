# Geodomains
> Geodomains blur the lines between natural human organization and geopolitical barriers. 

We'll introduce the concept of geodomains as an **open source EOSIO standard**, as well as provide working implementations for **Free Food Forests, Communal Gardens, and Reforestation Projects**.

These geodomains feature: 
> Note: piggyback means we can hopefully use something from TLOS, SEEDS or others
1. Geojson domains (ESRI 4326)
2. Funding structure (piggyback I hope)
3. Constitution (Rights + Restrictions, piggyback)
4. Elected leaders in charge of directing funds to publicly-proposed and provable addresses, and manually approving distribution of funds according to work done, verified by IPFS hash of proof media. (partially piggyback)
5. Separate (exclusive) elected leaders in charge of periodically ratifying any publicly-proposed changes the constitution 

## Geodomains are declared 
1. According to a **5-layer geopolitical system** common throughout the world. (Globe, Nation, Department [state in USA], County, City) 
2. According to a sub- and superset system, where a subset is composed of part of one County, and a superset is any collection of sets (geodomains) or sub- or supersets.

Our goal is to introduce these concepts in a harmonious effort to organize not only human interests, but for Mother Earth herself, so that we can become the "Gardeners of Earth" like so many of our ancestors sought to be. 

Geodomains also have many other use cases yet to be discovered.

## How a Geodomain is Stored
Shapefiles in a PostgreSQL database are used on the front end for display and on the backend for all geometric calculation (ex. to compare a location sent from a cell phone to a geodomain)

ISO or similar abbreviation (ID) sets for each geopolitical layer are stored on-chain, and new super and subset IDs are stored directly in tables. These shorthands are used to save resources. 

## How it all works

Someone can draw an area on a map (they must own the land) and declare a set of legally-binding permissions and restrictions for that area on-chain. These permissions are aimed at allowing people to come and help the land without fear of trespassing or wondering what is Okay to do, AND rewarding people who do help the land from a pool of donors who want to help but would rather send EOSIO.tokens

Rewards for defined actions come from the donation pool, with IPFS proof pictures / videos. 

We'll be drawing up the rules / permissions for Food Forrests, Communal gardens, and regenerative areas where people may re-plant native trees, or simply protect the land and let mother nature take her course. 

I think this is a lot like SEEDS, but we're building a lower layer standard that any project can use. SEEDS also lacks a strong geographic element. 

# How We'll Build it

> Nothing is final, Everything is meant to be discussed by the team

Frontend - Node.js frontend with Leaflet or Google Maps UI. 

On-chain
- Geodomains
    - Table structure to store ISO 3166+ abbreviations
        - Table for each of the 5 layers mentioned (Note: City tables not actually needed to sub / supersets of geodomains, as there are 10s of thousands just in the US, best to leave this off chain)
        - Figure out the best way to store Sub / Superset info, perhaps just on Postgres with hash of shapefile or geojson info.
- Permissions / Restrictions modular information  
	- We will make a table(s) of permissions / restriction with numbered ids for each one. Anyone can add their own Permission / Restriction into the table as text (uses RFC-2119, May require publishing further standard of definitions), which others can use by referencing the ID number, or of course, modify another and add it to get a new ID. 

- Rewards Structure Modular Information
	- Reward Declaration System
		- Leaders declare rewards that can be receive, and the way to receive them. (Simple table: reward id, desc) New projects can use rewards used in older projects by referencing IDs.
	- Funding system
		- Hoping we can work with an existing contract, so need to re-invent the wheel. 
	- Proof System 
		- Simple table with user, id of reward id, IPFS hash (or array of hashes) of proof media. 