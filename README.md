# nosql-challenge
## Module 12 Challenge - NoSQL Databases
Contracted by the fictitious magazine, "Eat Safe, Love" to help evaluate UK establishments' ratings for potential articles.

### Files in this repository include:
1. `establishments.json` (located in Resources folder) - contains the data needed for the assignment.
2. `NoSQL_setup.ipynb` - used to import the data from 'establishments.json' to MongoDB Compass then update and clean the data.
3. `NoSQL_analysis.ipynb` - used to analyze our data.

### Part 1: Database and Jupyter Notebook Set Up

(Note: `NoSQL_setup.ipynb` shows outputs that are out of order. This is due to changes made to the code after dropping all the 'Dover' documents.)
* Import data from `establishments.json` to MongoDB Compass. The following code was used in the terminal:
    * `mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json`
* In the Jupyter notebook file `NoSQL_setup`, import PyMongo and Pretty Print. Then create an instance of Mongo Client.
* Check that database created and loaded correctly with the functions `list_database_names`, `list_collection_names`, and `find_one`.
* Check the data types for the coordinates and 'RatingValue'.

### Part 2: Update the Database

Continue using `NoSQL_setup` to:
* add a new restaurant (using `insert_one()`).
* use a query to find the BusinessTypeID for 'Restaurant/Cafe/Canteen' establishments.
* update the new restaurant's BusinessTypeID with `update_one()`.
* Delete the 994 establishments in Dover from the collection.
* Use `update_many` function to change latitude and longitude values from string to decimal, and RatingValue from string to integer.
* Also, update the RatingValue field to show only numbers by changing values of "AwaitingInspection", "Awaiting Inspection", "AwaitingPublication", "Pass", "Exempt" to `Null`.

### Part 3: Exploratory Analysis

* Use `NoSQL_analysis` to help answer specific questions and convert results to Pandas DataFrame:
    1. Which establishments have a hygiene score equal to 20?
        * Answer: 41
        * Used a query and `count_documents` to solve.
    2. Which establishments in London have a RatingValue greater than or equal to 4?
        * Answer: 33
        * Used a query and `count_documents` to solve.
    3. What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?
        * Answer: 1-Volunteer, 2-Plumstead Manor Nursery, 3-Atlantic Fish Bar, 4-Iceland, 5-Howe and Co Fish and Chips (Van 17)
        * Used a query to find establishments with a RatingValue of 5 and within 0.01 degree of longitude and latitude of Penang Flavours, sorted the results by hygiene, and limited to 5.
    4. How many establishments in each Local Authority area have a hygiene score of 0?
        * There are 55 local authority areas, so the answer for the top 10 are displayed in `est_count_zero_hygiene` DataFrame.
        * Used aggregation pipeline and aggregate method.
