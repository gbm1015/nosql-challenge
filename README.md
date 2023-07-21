# NoSQL Challenge - "Eat Safe, Love" food magazine

## Background

The UK Food Standards Agency evaluated various establishments across the United Kingdom, and gave them a food hygiene rating. The editors of a food magazine, Eat Safe, Love, requested the evaluation of some of the ratings data in order to help their journalists and food critics decide where to focus future articles.

### Before opening the starter code in Jupyter Notebook

1. I created a new repository in GitHub for this project called `nosql-challenge`. 
2. Inside the new repository I cloned the new repository to my computer.
3. Inside my local Git repository, I added and renamed the Jupitor notebook starter codes NoSQL_setup_starter.ipynb to NoSQL_setup_final.ipynb, and             NoSQL_analysis_starter.ipynb to NoSQL_analysis_final.ipynb.
4. I then added the Resources folder containing the establishments.json file.

## Part 1 - Database and Jupyter Notebook Set up

Used NoSQL_setup_final.ipynb for this section of the challenge.

1. Imported the data provided in the establishments.json file from the Terminal. Named the database uk_food and the collection establishments, and then copied the used text to import the data from the Terminal to a markdown cell in the notebook.
2. Within the notebook, imported the libraries that were needed: PyMongo and Pretty Print (pprint).
3. Createed an instance of the Mongo Client.
4. Confirmed that the database was created and the data was loaded properly:
   - Listed the databases that are in MongoDB. Confirmed that uk_food was listed.
   - Listed the collection(s) in the database to ensure that establishments is there.
   - Found and displayed one document in the establishments collection using find_one and displayed with pprint.
5. Assigned the establishments collection to a variable to prepare the collection for use.
    
## Part 2 - Updated the Database

Used NoSQL_setup_final.ipynb for this section of the challenge.

The magazine editors had requested some modifications for the database before any queries or analysis could be performed for them. The following changes were made to the establishments collection:

1. An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine asked to include it in the analysis. Therefore, the following information was added to the database:

{   "BusinessName":"Penang Flavours",
    "BusinessType":"Restaurant/Cafe/Canteen",
    "BusinessTypeID":"",
    "AddressLine1":"Penang Flavours",
    "AddressLine2":"146A Plumstead Rd",
    "AddressLine3":"London",
    "AddressLine4":"",
    "PostCode":"SE18 7DY",
    "Phone":"",
    "LocalAuthorityCode":"511",
    "LocalAuthorityName":"Greenwich",
    "LocalAuthorityWebSite":"http://www.royalgreenwich.gov.uk",
    "LocalAuthorityEmailAddress":"health@royalgreenwich.gov.uk",
    "scores":{
        "Hygiene":"",
        "Structural":"",
        "ConfidenceInManagement":""
    },
    "SchemeType":"FHRS",
    "geocode":{
        "longitude":"0.08384000",
        "latitude":"51.49014200"
    },
    "RightToReply":"",
    "Distance":4623.9723280747176,
    "NewRatingPending":True
}

2. The BusinessTypeID for "Restaurant/Cafe/Canteen" was found and returned only the BusinessTypeID and BusinessType fields.
3. Updated the new restaurant with the BusinessTypeID that was found.
4. The magazine was not interested in any establishments in Dover, so checked how many documents contained the Dover Local Authority. Then, removed any establishments within the Dover Local Authority from the database, and checked the number of documents to ensure they were deleted.
5. Some of the number values were stored as strings, when they should be stored as numbers.
   - Used update_many to convert latitude and longitude to decimal numbers.
   - Used update_many to convert RatingValue to integer numbers.

## Part 3 - Exploratory Analysis

"Eat Safe, Love" food magazine had specific questions they wanted answered, which will help them find the locations they wished to visit and/or avoid.
Used NoSQL_analysis_final.ipynb for this section of the challenge.

Some notes to be aware of while exploring the dataset:
- RatingValue refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating.
  This field also included non-numeric values such as 'Pass', where 'Pass' meant that the establishment passed their inspection but wasn't given a number rating. Non-         numeric values changed to nulls during the database setup before converting ratings to integers.
- The scores for Hygiene, Structural, and ConfidenceInManagement worked in reverse. This meant, the higher the value, the worse the establishment is in these areas.

The magazine editors questions were:
1) Which establishments have a hygiene score equal to 20?
2) Which establishments in London have a RatingValue greater than or equal to 4?
3) What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?
4) How many establishments in each Local Authority area have a hygiene score of 0? Sorted the results from highest to lowest, and printed out the top ten local authority areas.

## References

UK Food Standards Agency at https://www.food.gov.uk (2022). 
UK food hygiene rating data API. https://ratings.food.gov.uk/open-data/en-GB contains public sector information licensed under the Open Government Licence v3.0 (https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)
Accessed Sept 9, 2022 and Sept 12, 2022 with the establishment settings as follows: longitude=51.5072, latitude=-0.1276, maxdistancelimit=4567, pagesize=10000, sortoptionkey=distance, pagenumber=(1,2,3,4,5,6,7,8).
