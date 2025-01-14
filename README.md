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
