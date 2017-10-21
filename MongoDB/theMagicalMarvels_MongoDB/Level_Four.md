
# The magical Marvels of MongoDB

## Level Four: Morphing Models

This level mostly focused on asking questions, so I have noted down my answers and where relevant I have explained my reasoning behind the answer.

### 4.2 Marvelous Merging

When we take the data from one document and place it inside another one, that's called an
*embedded*  document.

### 4.3 Related Realms

If we take a unique value like an _id from one document and store it as a value within a related document, we have just created a          *reference* document.


### 4.4 Lookout Incantations

For what reason might we want to consider referencing maker information instead of embedding it within each wand?

Answer: Duplicate Data
Explanation: Duplicating data ensures all the information is copied and saved.
This means the data will be present everywhere and would be easy to normalize (reference) later. 
It would also be useful for the data to be available for different applications to query the data in the future. 


### 4.5 Quantifying Queries
What's the minimum number of queries we'd have to write in order to retrieve a document and its referenced data?

2

### 4.6 Chalice of Choices
Which modeling option would give us all the data we need with a single query, support for atomic writes, and is great for data that is strongly related?

Answer: Embedding
Explanation: denormalization (embedding) only requires a single query and would allow the data to be accessed faster.


### 4.7 Cauldrons of Considerations
Which data modeling decision doesn't have default support for atomic writes across multiple documents and should be utilized with care?

Answer: Referenced
Explanation: referenced copies the data and ensures consistency across documents which can be a problem if one document changes a value, they will all follow. Embedded does not change details across multiple documents automatically. 


### 4.9 Casting Choices
In general, what's the best option to first consider for modeling your related data?

Answer: Embedding
Explanation: The data will be stored and easy to access via a single query. It will also provide a flexible approach regarding inconsistent data across multiple documents. Finally embedding provides and faster view across documents whereas referncing is slower. 

### 4.10 Unique Users
Which data modeling option would be the best fit for storing users and their addresses when we know that the data is used together often, won't be changing regularly, and each user will only be storing a few addresses?

Answer: Embedding
Explanation:

### 4.11 Charming Cars
We'd like to store information about cars, and each car can have a few hundred parts. Most of the time, we won't be needing specific information about each part. Which data modeling route should we take?

Answer: Referencing
Explanation: Provides a method of accessing the data with  a more general overview


### 4.12 Charming Changes
Which modeling route is best when we have data that is constantly changing and will help prevent data inconsistencies from arising?

Answer: Referencing
Explanation: Referencing ensures consistency. When data is changed it automatically changes across the documents. 



### 4.13 Bewitched Access
Which data modeling route allows us to access our data independently instead of having to use something like dot notation to get information?


Answer: Referencing
Explanation: Referencing ensures consistent data and provides access to data which can be accessed by multiple applications. 
