I used beautiful soup to scrap for video game reviews at IGN and GameSpot.

The base for this project was a kaggle [dataset](https://www.kaggle.com/rush4ratio/video-game-sales-with-ratings) 
that contains games data on sales and some ratings, the objective was to add useful information to this dataset.


## Scraper  
The scraper is pretty simple and it uses three main functions to extract data from the webpages.  

get_content - Grabs the webpage content  
get_index - Search the content for a specific term and bring the index of the children containing it  
lookup - Uses get_index to dig down the children lists and return the list when it reaches a specified number of elements  
  
Those three functions are used to build the webpage specific functions that extract the fields I'm interested in.  
  
### GameSpot 
get_gs_sources - Assemble the search query, perform search and retrieve URL of the first result  
scrap_gs - Get title, release year, review score, Metacritic score, and user score from a list of gs URLs  
  
### IGN  
get_ign_sources - Assemble the search query, perform search and retrieve URL of the first result  
scrap_ign - Get title, release year and review score from a list of URLs  
  
## Cleaning 
For cleaning the scraped data I used a function to check if the most important score was collected;  
if so it checks if the name of the scraped game matches with the one we had in the .csv file;  
if it doesn't match the release year of the games are compared;  
If nothing matches, the row index is added to a list, which is returned an can be used to remove those values.

clean_text - receives as arguments a string and a list with elements to be removed, then removes the values from the string  
clean_list - check if the score was collected, if names and release years match, and return a list of unmatched rows  

## Results  
From a sample of 99 games, the program could collect 80 rows of GameSpot data and 51 rows of IGN data  

## Next  
Some games can get very complicated, like Pokemon, for example, they were released in pairs or groups like red/ blue or sun/ moon,
so some websites list them as one and some list them as separate games, some use the prefix 'version' before the subtitle and some don't.
Release dates can also get tricky as games may be released on different dates for different regions.

Another thing learned is that IGN doesn't list only games, it has reviews and articles about TV, cartoons, and technology as well. 
Going back to the Pokemon example, IGN search sometimes retrieved the tv show instead of the game.

One final question I want to explore is how much my online profile impacts the results of those searches.  
My point is, maybe I can get a better result if my online profile is anonymous.
Do the results of the queries bring suggestions based on my previous online activities? if so, does that have a negative impact on my extraction? 
  
    
    
    
#### practice_scraper
I'm exploring some methods of scraping with Beautiful Soup and Selenium
This is not the fastest or the best implementation. 
