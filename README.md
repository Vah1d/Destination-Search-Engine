Places of the world
==============================

![image](https://github.com/user-attachments/assets/e4002c35-6b3d-4664-b611-ac081a236013)

Travelling is a pleasant activity which has increased since the end of the COVID-19 pandemic. Nowadays, people look for places to visit which are attractive, affordable, with a rich history and which have recommended activities. Using user-generated content, Atlas Obscura, an American online magazine and travel firm, catalogues unusual and obscure tourist locations. The website's articles span many subjects, including history, science, cuisine, and unique places.

You and your team have been hired to provide your Data Science knowledge to create a search engine which will facilitate specific searches towards a topic related to the most popular places to visit. Important: In general, you can use functions from libraries such as scikit-learn, NumPy, pandas, etc., which will help you to make intermediate calculations. But, you are not allowed to use, for example, a function that automatically creates a search engine. Then, let's get started!


Data collection
---------------------------------
For this homework, there is no provided dataset. Instead, you have to build your own. Your search engine will run on text documents. So, here we detail the procedure to follow for the data collection.

1.1. Get the list of places
We start with the list of places to include in your corpus of documents. In particular, we focus on the Most popular places. Next, we want you to collect the URL associated with each site in the list from this list. The list is long and split into many pages. Therefore, we ask you to retrieve only the URLs of the places listed in the first 400 pages (each page has 18 places, so that you will end up with 7200 unique place URLs).

The output of this step is a .txt file whose single line corresponds to the place's URL.

1.2. Crawl places
Once you get all the URLs in the first 400 pages of the list, you:

Download the HTML corresponding to each of the collected URLs.
After you collect a single page, immediately save its HTML in a file. In this way, if your program stops for any reason, you will not lose the data collected up to the stopping point.
Organize the entire set of downloaded HTML pages into folders. Each folder will contain the HTML of the places on page 1, page 2, ... of the list of locations.
Tip: Due to a large number of pages you should download, you can use some methods that can help you shorten the time it takes. If you employed a particular process or approach, kindly describe it.

1.3 Parse downloaded pages
At this point, you should have all the HTML documents about the places of interest, and you can start to extract the places' information. The list of the information we desire for each place and their format is as follows:

Place Name (to save as placeName): String.
Place Tags (to save as placeTags): List of Strings.
# of people who have been there (to save as numPeopleVisited): Integer.
# of people who want to visit the place(to save as numPeopleWant): Integer.
Description (to save as placeDesc): String. Everything from under the first image up to "know before you go" (orange frame on the example image).
Short Description (to save as placeShortDesc): String. Everything from the title and location up to the image (blue frame on the example image).
Nearby Places (to save as placeNearby): Extract the names of all nearby places, but only keep unique values: List of Strings.
Address of the place(to save as placeAddress): String.
Latitud and Longitude of the place's location(to save as placeAlt and placeLong): Floats
The username of the post editors (to save as placeEditors): List of Strings.
Post publishing date (to save as placePubDate): datetime.
The names of the lists that the place was included in (to save as placeRelatedLists): List of Strings.
The names of the related places (to save as placeRelatedPlaces): List of Strings.
The URL of the page of the place (to save as placeURL):String

Search Engine
---------------------------
Now, we want to create two different Search Engines that, given as input a query, return the places that match the query.

First, you must pre-process all the information collected for each place by:

Removing stopwords
Removing punctuation
Stemming
Anything else you think it's needed
For this purpose, you can use the nltk library.

2.1. Conjunctive query
For the first version of the search engine, we narrow our interest to the description of each place. It means that you will evaluate queries only concerning the place's description.

Note: You should use the longer description placeDesc column and not the short description placeShortDesc.

2.1.1) Create your index!
Before building the index,

Create a file named vocabulary, in the format you prefer, that maps each word to an integer (term_id).
Then, the first brick of your homework is to create the Inverted Index. It will be a dictionary in this format:

{
term_id_1:[document_1, document_2, document_4],
term_id_2:[document_1, document_3, document_5, document_6],
...}
where document_i is the id of a document that contains that specific word.

Hint: Since you do not want to compute the inverted index every time you use the Search Engine, it is worth thinking about storing it in a separate file and loading it in memory when needed.

2.1.2) Execute the query
Given a query input by the user, for example:

american museum
The Search Engine is supposed to return a list of documents.

What documents do we want?
Since we are dealing with conjunctive queries (AND), each returned document should contain all the words in the query. The final output of the query must return, if present, the following information for each of the selected documents:

placeName
placeDesc
placeURL
Example Output:



If everything works well in this step, you can go to the next point and make your Search Engine more complex and better at answering queries.

2.2) Conjunctive query & Ranking score
For the second search engine, given a query, we want to get the top-k (the choice of k it's up to you!) documents related to the query. In particular:

Find all the documents that contain all the words in the query.
Sort them by their similarity with the query.
Return in output k documents, or all the documents with non-zero similarity with the query when the results are less than k. You must use a heap data structure (you can use Python libraries) for maintaining the top-k documents.
To solve this task, you must use the tfIdf score and the Cosine similarity. The field to consider is still the placeDesc. Let's see how.

2.2.1) Inverted index
Your second Inverted Index must be of this format:

{
term_id_1:[(document1, tfIdf_{term,document1}), (document2, tfIdf_{term,document2}), (document4, tfIdf_{term,document4}), ...],
term_id_2:[(document1, tfIdf_{term,document1}), (document3, tfIdf_{term,document3}), (document5, tfIdf_{term,document5}), (document6, tfIdf_{term,document6}), ...],
...}
Practically, for each word, you want the list of documents in which it is contained and the relative tfIdf score.

Tip: TfIdf values are invariant for the query. Due to this reason, you can precalculate and store them accordingly.

2.2.2) Execute the query
In this new setting, given a query, you get the proper documents (i.e., those containing all the query's words) and sort them according to their similarity to the query. For this purpose, as the scoring function, we will use the Cosine Similarity concerning the tfIdf representations of the documents.

Given a query input by the user, for example:

american museum
The search engine is supposed to return a list of documents, ranked by their Cosine Similarity to the query entered in the input.

More precisely, the output must contain:

placeName
placeDesc
placeURL
The similarity score of the documents with respect to the query (float value between 0 and 1)

Define a new score!
----------------
Now it's your turn. Build a new metric to rank places based on the queries of their users.

In this scenario, a single user can give input more information than a single textual query, so you need to consider all this information and think of a creative and logical way to answer the user's requests.

Practically:

The user will enter a text query. As a starting point, get the query-related documents by exploiting the search engine of Step 3.1.

Once you have the documents, you need to sort them according to your new score. In this step, you won't have any more to take into account just the plot of the documents; you must use the remaining variables in your dataset (or new possible variables that you can create from the existing ones). You must use a heap data structure (you can use Python libraries) for maintaining the top-k documents.

Q: How to sort them? A: Allow the user to specify more information that you find in the documents and define a new metric that ranks the results based on the new request. You can also use other information regarding the place to score some places above others.

N.B.: You have to define a scoring function, not a filter!

The output, must contain:

placeName
placeDesc
placeURL
The new similarity score of the documents with respect to the query
Are the results you obtain better than with the previous scoring function? Explain and compare results.

Visualizing the most relevant places
-----------------------------
Using maps can help people understand how far one place is from another so they can plan their trips more adequately. Here we challenge you to show a map with the places found with the score defined in point 3. Ensure you can at least identify and visualize the name, city, country, address and the number of people who visited each place. You can find some ideas on how to create maps in Python here and here but don't limit yourselves, let your minds fly!!

IMPORTANT: This is a bonus step, so it's not mandatory. You can get the maximum score also without doing this. We will take this into account, only if the rest of the homework has been completed.

For the Bonus part, we want to ask you more sophisticated search engine. Here we want to let users issue more complex queries. The options of this new search engine are:

Give the possibility to specify queries for the following features (the user should have the option to issue none or all of them):
placeName
placeDesc
placeAddress
Specify a list of usernames to only retrieve the posts that all of these users contributed to.
Specify a list of tags which the search engine should only return the places that are tagged with all of those tags.
Filter based on the number of people who have already been there. The user should be able to adjust the upperbound, lowerbound or only one of the two.
Specify a list of the list names that the engine should only filter the documents that have been included in all of the given list names.
Note 1: You should be aware that you should give the user the possibility to select any of the abovementioned options. How should the user use the options? We will accept any manual that you provide to the user.

Note 2: As you may have realized from 1st option, you need to build inverted indexes for those values and return all of the documents that have the similarity more than 0 concerning the given queries. Choose a logical way to aggregate the similarity coming from each of them and explain your idea in detail.

Note 3: The options other than 1st one can be considered as filtering criteria so the retrieved documents must respect all of those filters.

The output must contain the following information about the places:

placeName
placeURL



# adm_hw3_tarantino_popolla_ghanbarizadehv
## Homework 3 ADM
## Ramona Tarantino - ramonatarantino00@gmail.com - 2082006
## Valeria Popolla - valeria.popolla00@gmail.com - 1918542
## Vahid ghanbarizadeh -  ghanbarizadeh.2002527@studenti.uniroma1.it - 2002527

### The following files are found in the repository:
- ADM_HW3_code: the file that contains the python script of all the homework
- CommandLine.sh : 6. Command line question
- Answers to the command line question : a file .txt containing the explained results of the command line file
- Theoretical_question  and another .txt files named as 'RankingList5.txt' , 'RankingList7.txt' , 'RankingList8.txt':  the files that contain the final output of the three sorting algorithms
- Map.html : the html page containing the output map of exercise 4 (added because it was not visible in ADM_HW3_code) 
- places.txt : the list of places
- places.tsv
- inverted_index.pkl and tfidfinvindex.pkl 
- vocabulary.pkl 
- dfquestion3new.csv : dataframe of the 3rd point of the homework 
### Some files are located in the 'files-used-in-the-code' branch
