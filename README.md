# Movies_ETL
Extracting, Transforming and Loading movie data in peparation for a company hackathon.

## Overview of Movies_ETL
In preparation for their upcoming hackathon, "Amazing Prime" had me create a clean database containing movie data and ratings such that the participants of the hackathon could come up with methods for predicting what will attributes best determine whether or not a movie will be successful.

In constructing this database, I leveraged Python to extract the movie data from three sources (_Kaggle Metadata, MovieLens ratings, and Wikipedia_), clean up the columns, removed some unusuable or unnecesary data, merged the Kaggle and Wikipedia and relevent MovieLens datasets, and exported the finalized datasets to PostgreSQL, where it will accessed by the hackathon participants.

## Resources
- Data Sources: Kaggle Metadata (movies_metadata.csv), MovieLens ratings (ratings.csv), Wikipedia data (wikipedia-movies.json)
- Python: 3.7.13, Jupyter Notebook
- PostgresSQL 11.16
- pgAdmin 6.11

## Movies_ETL Results & Summary
When first loading the data from Wikipedia, the dataset initially had 193 columns. I was able to reduce the number of columns from Wikipedia to 21 by filtering out TV shows, movies that didn't contain a listed director or an imdb_link, consolidating alternate titles (_different languages_), consolidating data from columns with similar names (_through renaming columns_) and finally, removing columns that had over 90% null values.

By extracting the imdb_id from the 'imbd_link', I was able to remove duplicate rows.

Using Regular Expressions, I parsed the box office data, budget data, release dates, running times, converting the data types as needed, such that these columns could provide valuable insight during the hackathon.

Similarly, decided to remove the Adult movies, and subsequently the Adult column (_keeping the hackathon pg_), converted the video column to Boolean, converted budget, ID, and popularity to Numeric, and converted the release_date to datetime.

After all the above cleaning, I merged the Kaggle and Wiki datasets, and decided to removing/consolidating a few duplicate columns (titles, runtime, budget, revenue, release_date, language, production_companies). 

After re-organizing the structure of the columns, and renaming some such that they'd be more easily interpretable, I added counts of each reating to the movie dataframe, using a pivot table (movieID as the index, columns are ratings, and values are the counts for each user's respective rating)

Finally, I loaded the clean datasets (movie_df and ratings) to PostgreSQL.