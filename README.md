# IMDB-Movie-Set
### Observing the givien data set we had to explore and find a appropriate research question.

{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {
    "collapsed": true
   },
   "source": [
    "<p style=\"font-family: Arial; font-size:3.35em;color:purple; font-style:bold\"><br>\n",
    "Final Project : Most Rated Genres</p><br>\n",
    "<hr>\n",
    "\n",
    "## IMDB Movie Dataset\n",
    "\n",
    "This dataset describes 5-star rating and free-text tagging activity from, a movie recommendation service. It contains 20000263 ratings and 465564 tag applications across 27278 movies.These data were created by 138493 users between January 09, 1995 and March 31, 2015. \n",
    "\n",
    "The data are contained in six files `links.csv`, `movies.csv`, `ratings.csv` and `tags.csv` etc.In this project we will use only two given data set which is **movies.csv** and **ratings.csv**. Our research question is **What types of movies genres user viewed and rated most than other movies genres ?**\n",
    "\n",
    "\n",
    "DataSet can be get from this site : <http://grouplens.org/datasets/>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "collapsed": true
   },
   "source": [
    "<p style=\"font-family: Arial; font-size:1.35em;color:#2462C0; font-style:bold\"><br>\n",
    "\n",
    "Including Pandas Module\n",
    "\n",
    "<br> </p>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    "import pandas as pd \n",
    "%matplotlib inline"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "collapsed": true
   },
   "source": [
    "<p style=\"font-family: Arial; font-size:1.35em;color:#2462C0; font-style:bold\"><br>\n",
    "\n",
    "Importing or Acquiring <strong>movies.csv</strong> and <strong>ratings.csv</strong> data sets\n",
    "\n",
    "<br> </p>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "movies = pd.read_csv('C:/Users/Innat/Desktop/WEEK 4/ml-20m/movies.csv',sep = ',')\n",
    "ratings = pd.read_csv('C:/Users/Innat/Desktop/WEEK 4/ml-20m/ratings.csv',sep = ',')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>movieId</th>\n",
       "      <th>title</th>\n",
       "      <th>genres</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>Toy Story (1995)</td>\n",
       "      <td>Adventure|Animation|Children|Comedy|Fantasy</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>Jumanji (1995)</td>\n",
       "      <td>Adventure|Children|Fantasy</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>Grumpier Old Men (1995)</td>\n",
       "      <td>Comedy|Romance</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>Waiting to Exhale (1995)</td>\n",
       "      <td>Comedy|Drama|Romance</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>Father of the Bride Part II (1995)</td>\n",
       "      <td>Comedy</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   movieId                               title  \\\n",
       "0        1                    Toy Story (1995)   \n",
       "1        2                      Jumanji (1995)   \n",
       "2        3             Grumpier Old Men (1995)   \n",
       "3        4            Waiting to Exhale (1995)   \n",
       "4        5  Father of the Bride Part II (1995)   \n",
       "\n",
       "                                        genres  \n",
       "0  Adventure|Animation|Children|Comedy|Fantasy  \n",
       "1                   Adventure|Children|Fantasy  \n",
       "2                               Comedy|Romance  \n",
       "3                         Comedy|Drama|Romance  \n",
       "4                                       Comedy  "
      ]
     },
     "execution_count": 3,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "movies.head() # showing the first 15 items in csv file"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>userId</th>\n",
       "      <th>movieId</th>\n",
       "      <th>rating</th>\n",
       "      <th>timestamp</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>2</td>\n",
       "      <td>3.5</td>\n",
       "      <td>1112486027</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>1</td>\n",
       "      <td>29</td>\n",
       "      <td>3.5</td>\n",
       "      <td>1112484676</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1</td>\n",
       "      <td>32</td>\n",
       "      <td>3.5</td>\n",
       "      <td>1112484819</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1</td>\n",
       "      <td>47</td>\n",
       "      <td>3.5</td>\n",
       "      <td>1112484727</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1</td>\n",
       "      <td>50</td>\n",
       "      <td>3.5</td>\n",
       "      <td>1112484580</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   userId  movieId  rating   timestamp\n",
       "0       1        2     3.5  1112486027\n",
       "1       1       29     3.5  1112484676\n",
       "2       1       32     3.5  1112484819\n",
       "3       1       47     3.5  1112484727\n",
       "4       1       50     3.5  1112484580"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "ratings.head(5) # showing the first 15 items in csv file"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "# deleting the timestamp and userId coloumns\n",
    "del ratings['timestamp'] \n",
    "del ratings['userId']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>movieId</th>\n",
       "      <th>rating</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2</td>\n",
       "      <td>3.5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>29</td>\n",
       "      <td>3.5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>32</td>\n",
       "      <td>3.5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>47</td>\n",
       "      <td>3.5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>50</td>\n",
       "      <td>3.5</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   movieId  rating\n",
       "0        2     3.5\n",
       "1       29     3.5\n",
       "2       32     3.5\n",
       "3       47     3.5\n",
       "4       50     3.5"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "ratings.head() # after"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h1 style=\"font-size:2em;color:#2467C0\">Merge Dataframes</h1>\n",
    "<hr>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>movieId</th>\n",
       "      <th>rating</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>3.921240</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>3.211977</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>3.151040</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>2.861393</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>3.064592</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   movieId    rating\n",
       "0        1  3.921240\n",
       "1        2  3.211977\n",
       "2        3  3.151040\n",
       "3        4  2.861393\n",
       "4        5  3.064592"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# take the average ratings value and group them by concern MovieId ....\n",
    "avg_ratings = ratings.groupby('movieId', as_index=False).mean()\n",
    "avg_ratings.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x2013b7bd940>"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x2013c43f4e0>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "# we can visualize ratings values by box ploting\n",
    "avg_ratings.boxplot(column='rating',figsize=(10,5))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "        Fig : Visualize Rating in Box Plot"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>movieId</th>\n",
       "      <th>title</th>\n",
       "      <th>genres</th>\n",
       "      <th>year</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>27273</th>\n",
       "      <td>131254</td>\n",
       "      <td>Kein Bund für's Leben (2007)</td>\n",
       "      <td>Comedy</td>\n",
       "      <td>2007</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>27274</th>\n",
       "      <td>131256</td>\n",
       "      <td>Feuer, Eis &amp; Dosenbier (2002)</td>\n",
       "      <td>Comedy</td>\n",
       "      <td>2002</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>27275</th>\n",
       "      <td>131258</td>\n",
       "      <td>The Pirates (2014)</td>\n",
       "      <td>Adventure</td>\n",
       "      <td>2014</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>27276</th>\n",
       "      <td>131260</td>\n",
       "      <td>Rentun Ruusu (2001)</td>\n",
       "      <td>(no genres listed)</td>\n",
       "      <td>2001</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>27277</th>\n",
       "      <td>131262</td>\n",
       "      <td>Innocence (2014)</td>\n",
       "      <td>Adventure|Fantasy|Horror</td>\n",
       "      <td>2014</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "       movieId                          title                    genres  year\n",
       "27273   131254   Kein Bund für's Leben (2007)                    Comedy  2007\n",
       "27274   131256  Feuer, Eis & Dosenbier (2002)                    Comedy  2002\n",
       "27275   131258             The Pirates (2014)                 Adventure  2014\n",
       "27276   131260            Rentun Ruusu (2001)        (no genres listed)  2001\n",
       "27277   131262               Innocence (2014)  Adventure|Fantasy|Horror  2014"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# extract the launching year of each movies and make a new columns named year\n",
    "movies['year'] = movies['title'].str.extract('.*\\((.*)\\).*', expand=True)\n",
    "movies.tail()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<p style=\"font-family: Arial; font-size:1.55em;color:#382196; font-style:bold\"><br>\n",
    "Merge the previous <b>avg_ratings</b> and <b>movies</b> data set<br><hr>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>movieId</th>\n",
       "      <th>title</th>\n",
       "      <th>genres</th>\n",
       "      <th>year</th>\n",
       "      <th>rating</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>26739</th>\n",
       "      <td>131254</td>\n",
       "      <td>Kein Bund für's Leben (2007)</td>\n",
       "      <td>Comedy</td>\n",
       "      <td>2007</td>\n",
       "      <td>4.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>26740</th>\n",
       "      <td>131256</td>\n",
       "      <td>Feuer, Eis &amp; Dosenbier (2002)</td>\n",
       "      <td>Comedy</td>\n",
       "      <td>2002</td>\n",
       "      <td>4.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>26741</th>\n",
       "      <td>131258</td>\n",
       "      <td>The Pirates (2014)</td>\n",
       "      <td>Adventure</td>\n",
       "      <td>2014</td>\n",
       "      <td>2.5</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>26742</th>\n",
       "      <td>131260</td>\n",
       "      <td>Rentun Ruusu (2001)</td>\n",
       "      <td>(no genres listed)</td>\n",
       "      <td>2001</td>\n",
       "      <td>3.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>26743</th>\n",
       "      <td>131262</td>\n",
       "      <td>Innocence (2014)</td>\n",
       "      <td>Adventure|Fantasy|Horror</td>\n",
       "      <td>2014</td>\n",
       "      <td>4.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "       movieId                          title                    genres  year  \\\n",
       "26739   131254   Kein Bund für's Leben (2007)                    Comedy  2007   \n",
       "26740   131256  Feuer, Eis & Dosenbier (2002)                    Comedy  2002   \n",
       "26741   131258             The Pirates (2014)                 Adventure  2014   \n",
       "26742   131260            Rentun Ruusu (2001)        (no genres listed)  2001   \n",
       "26743   131262               Innocence (2014)  Adventure|Fantasy|Horror  2014   \n",
       "\n",
       "       rating  \n",
       "26739     4.0  \n",
       "26740     4.0  \n",
       "26741     2.5  \n",
       "26742     3.0  \n",
       "26743     4.0  "
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#  merging....\n",
    "join_datasets = movies.merge(avg_ratings, on='movieId', how='inner')\n",
    "join_datasets.tail()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Index(['movieId', 'title', 'genres', 'year', 'rating'], dtype='object')"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "join_datasets.columns # coloumn in new data set"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "# get rid of the title column\n",
    "del join_datasets['title']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>movieId</th>\n",
       "      <th>genres</th>\n",
       "      <th>year</th>\n",
       "      <th>rating</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>Adventure|Animation|Children|Comedy|Fantasy</td>\n",
       "      <td>1995</td>\n",
       "      <td>3.921240</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>Adventure|Children|Fantasy</td>\n",
       "      <td>1995</td>\n",
       "      <td>3.211977</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>Comedy|Romance</td>\n",
       "      <td>1995</td>\n",
       "      <td>3.151040</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>Comedy|Drama|Romance</td>\n",
       "      <td>1995</td>\n",
       "      <td>2.861393</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>Comedy</td>\n",
       "      <td>1995</td>\n",
       "      <td>3.064592</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   movieId                                       genres  year    rating\n",
       "0        1  Adventure|Animation|Children|Comedy|Fantasy  1995  3.921240\n",
       "1        2                   Adventure|Children|Fantasy  1995  3.211977\n",
       "2        3                               Comedy|Romance  1995  3.151040\n",
       "3        4                         Comedy|Drama|Romance  1995  2.861393\n",
       "4        5                                       Comedy  1995  3.064592"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "join_datasets.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h1 style=\"font-size:2em;color:#2467C0\">Data Cleaning: Handling Missing Data</h1>\n",
    "<hr>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(26744, 4)"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Find the shape of the join data set\n",
    "join_datasets.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "movieId    False\n",
       "genres     False\n",
       "year        True\n",
       "rating     False\n",
       "dtype: bool"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# check is there any null value , if so , true boolean value will be return\n",
    "join_datasets.isnull().any()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Hmm , there're some null value , we have to drop them out."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    "# dropna () is used to drop out the null values\n",
    "join_datasets = join_datasets.dropna()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(26727, 4)"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# again check the shape of the data sets , these time row number decrease \n",
    "# indcating some rows are erased as they hold null values\n",
    "join_datasets.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "movieId    False\n",
       "genres     False\n",
       "year       False\n",
       "rating     False\n",
       "dtype: bool"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# again check is their any null values\n",
    "join_datasets.isnull().any()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "hmm , all null values are gone.It's Ok now."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h1 style=\"font-size:2em;color:#2467C0\">Data Visualization</h1>\n",
    "<hr>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Comparing Genres VS Ratings value , to see the correlation plot in following. We will use general ploting diagram to visualize it ,where genres is alone X axes and ratings is along Y axes."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x2013b7b9d68>"
      ]
     },
     "execution_count": 19,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\nAxQZHujT0yZGAAAAAElFTkSuQmCC\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x2013b7b9278>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "join_datasets[-30:].plot(x='genres', y='rating', figsize=(10,5), grid=True , color ='g')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "    Fig : Ploting ratings VS genres . Drama genres tend to high than other movie genres\n",
    "    \n",
    "    "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<p style=\"font-family: Arial; font-size:1.55em;color:#382196; font-style:bold\"><br>\n",
    "Comments On Plot<br><hr></p>Here we can see , ploting **genres** and **ratings** values shows us that Drama type movies tends to rate more high than other movies genres.Other genres has average ratinsgs scale though comedy genres is following Drama genres."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### For making to visualize more convineint , let's use pie plot."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Drama                   4416\n",
       "Comedy                  2251\n",
       "Documentary             1877\n",
       "Comedy|Drama            1241\n",
       "Drama|Romance           1043\n",
       "Comedy|Romance           741\n",
       "Comedy|Drama|Romance     594\n",
       "Horror                   556\n",
       "Crime|Drama              435\n",
       "Drama|Thriller           421\n",
       "Name: genres, dtype: int64"
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# using value_counts() on our join_datasets , we can also see Drama movies are majority in numbers>\n",
    "gen_count = join_datasets['genres'].value_counts()\n",
    "gen_count[:10]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x201004849e8>"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAkAAAAGRCAYAAACNEAwhAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz\nAAALEgAACxIB0t1+/AAAIABJREFUeJzs3Xl4VNX5B/DvubPduTPJZE8IIYRMhrAGRGQ0ApHFukRw\nARcEZHGpVSu12ha7jrVVtFVbbWtrrbtttVVEpT83wB2HgCKIIiMSWbKvk8wkk5m55/fHnZiwJiF3\n5iaZ9/M885Bk5p55J5rknXPec17GOQchhBBCSDwRtA6AEEIIISTWKAEihBBCSNyhBIgQQgghcYcS\nIEIIIYTEHUqACCGEEBJ3KAEihBBCSNyhBIgQQgghcYcSIEIIIYTEHUqACCGEEBJ3KAEihBBCSNyh\nBIgQQgghcYcSIEIIIYTEHUqACCGEEBJ3KAEihBBCSNyhBIgQQgghcYcSIEIIIYTEHUqACCGEEBJ3\n9FoHQAhjLAxgJwADgBCApwA8wDmXNQ2MEELIkEUJEBkI2jjnkwGAMZYB4J8AEgH8qvuDGGN6znlI\ng/gIIYQMMbQERgYUznkNgOsA3MQUyxljLzPGNgLYwBizMsY2MMY+ZoztZIxdCACMsTzG2G7G2BOM\nsT2MsWcZY3MZYx8wxjyMsWmRx01jjG1mjH3CGPuQMVao4cslhBCiEcY51zoGEucYY62cc+sRX2sC\nUAjgPAC/AVDEOW9gjOkBSJxzL2MsDcBHABwARgL4CsApAHYBKAPwKYCrAcwHsIJzfhFjLBGAn3Me\nYozNBfA9zvmC2LxSQgghAwUtgZHB4E3OeUPkYwbgLsbYTAAygOEAMiP37eOc7wQAxtguABs455wx\nthNAXuQxNgBPMsYcADiUuiNCCCFxhpbAyIDDGMsHEAZQE/mSr9vdiwGkAzg1UjdUDUCM3Bfo9ji5\n2+cyupL9OwFs4pxPADCv27WEEELiCCVAZEBhjKUD+CuAP/Fjr8/aANRwzoOMsVlQlr76wgbgUOTj\n5ScdKCGEkEGNEiAyEJgZY9sjy1ZvAXgDwB3HeeyzAKZGlrWuArC7j891L4C7GWOfgJaACSEkblER\nNCGEEELiDs0AEUIIISTuUAJECCGEkLhDCRAhhBBC4g4lQIQQQgiJO5QAEUIIISTuUAJECCGEkLhD\n56AQEkN5q9czAKkAsqC08MiK3NIBJACQAJgj/0on+FwAEOp2Cx7xefdbG4BGAA29uDWWrymVo/cd\nIISQgYHOASJERXmr12cBGB255QEYhq4kJxNABgZ2/7EwgAoA5ce47QNwoHxNaUiTyAghREWUABHS\nR3mr1ydA6VQ/+oibA0CihqHFQhhKK5FyKAnRbgCfAthRvqb00AmuI4SQAYUSIEKOI7JcVQDgVABT\nAJwCYAKU2RxytDoAOyK3TyP/7ipfUxo44VWEEKIBSoAIichbvT4HgDNymwYl4RnqMzrRFgLwJZRk\naCuADwB8XL6mNKhpVISQuEcJEIlLkdmdSQDmADgTStKTrWlQ8aMNQBmUZOh9AO+Xryn1ahsSISTe\nUAJE4kbe6vV5AM6GkvTMhrLzimgvDGA7gLcjt3cpISKERBslQGTIylu9PhVKsjMHwFwA+dpGRHop\nDGALgFcBvFK+pnSnxvEQQoYgSoDIkJK3ev0pABYAOB/AZABM24iICsoRSYYAvF2+prRD23AIIUMB\nJUBkUIvU8kyDkvQsAM3yDHUtAN6EkgytL19TWqtxPISQQYoSIDLo5K1eL0ApXF4A4BIAI7SNiGhE\nBuAG8ByAf5WvKa3ROB5CyCBCCRAZFCJJz1kAFgK4GHQWDzlcCMAbAJ4B8FL5mtI2jeMhhAxwlACR\nAS1v9fqRAFZEbrkah0MGhxYALwB4GkrNEPU2I4QchRIgMuDkrV5vBHARgKs553MZY4LWMZFB6yCA\nZwE8Xb6mdJfWwRBCBg5KgMiAkbd6/XgoSc9Sxlia1vGQIWcrgD8B+De15yCEUAJENJW3er0FwCIA\nVwM4XeNwSHyoAfAIgIfL15RWaB0MIUQblAARTeStXp8J4Puc8+8xxlK0jofEpSCUWqGHyteUfqh1\nMISQ2KIEiMRU3ur1hQBu5ZxfxRgzaR0PIRFbATwE4DlaHiMkPlACRGIib/X6MznnPwIwnzFGpzOT\ngaoGwMMA/li+prRR62AIIdFDCRCJmsjZPRdyzn/EGDtD63gI6QMvgAcB3E+JECFDEyVARHV5q9fr\nACzlnP+UMebQOh5C+sELZWnsPkqECBlaKAEiqspbvf5izuW7GBPGaB0LISqiRIiQIYYSIKKKvNXr\nZ/Nw6HdMp5+idSyERBElQoQMEZQAkX7JW71+Kg+Hfs90+hKtYyEkhrwAHgBwb/maUr/WwRBC+o4S\nIHJS8lavL+Th0D1Mp79Q61gI0dBBAD8pX1P6T60DIYT0DSVApE/yVq/P5OHQPRB0S6lHFyHf2gxg\nVfma0jKtAyGE9A4lQKRX8lavF3g4eDOY8Bsm6Cxax0PIAMShdKBfXb6mtFLrYAghJ0YJEOlR7q0v\nngHgccFgKtQ6FkIGgVYAd0M5Q6hd62AIIcdGCRA5rtxbX0zh4eDDgslyKZ3eTEiflQO4rXxN6Qta\nB0IIORolQOQoeavXs3Bby42CUbyb6QxWreMhZJB7GcD1tCxGyMBCCRA5TO4P/3sKOH9KMEkTtI6F\nkCGkCcAt5WtKn9A6EEKIghIgAgDIW73eEPY3/0EwJ3yPMYGWuwiJjtcAXFe+pvSA1oEQEu8oASIY\nfu3fTtNZk/8jmCwjtY6FkDjgBfBjAI+UrymlX8CEaIQSoDiWfNYKwexwPmBIzr6RCTqd1vEQEmc2\nArimfE3pPq0DISQeUQIUp7KuXDNBnzL8Rb01hbq1E6IdH4DbAfyJZoMIiS1KgOKM5HCypOlLfmZI\nzfkF0xuNWsdDCAEAvApgWfma0gatAyEkXlACFEcyL/91jiFlxFq9LWOq1rEQQo5yAMDl5WtKN2sd\nCCHxgBKgOJG15N6lxoz8vwhGM53rQ8jAFQLwMwC/oyUxQqKLEqAhTnI4RVvxokeNmfYrmUDb2wkZ\nJNZDWRKr1zoQQoYqSoCGsOSSZeOlMdNfMCRnUw8vQgafAwCuKF9T+qHWgRAyFFECNARJDiczFziX\nS6OL/6AzJyRqHQ8h5KTRkhghUUIJ0BAjOZxmy8S590n2065lOoNe63gIIapYB2BJ+ZrSVq0DIWSo\noARoCJHGnDksceqFz5uGj5tOzdsJGXJ2AJhfvqb0G60DIWQooARoiEh0XlKcMOncfxpShlM7C0KG\nrhoAF1NdECH9RwnQICc5nDpDxqiliVPm3a+zJCVrHQ8hJOoCAE4vX1O6XetACBnMqEZkEJMcTsk4\nbPTtiafOu0UwWSxax0MIiToZwE8p+SGk/ygBGqQkhzPTlDP+noQpF1whGEwmreMhhESdD8Di8jWl\n67QOhJChgBKgQUhyOEeZ7ac9ZJ149jlMp6f/hoQMcXJHW1uw4dDFlU+selPrWAgZKuiP5yAjOZzj\nLePOelgaM306Y3SyMyFDXdjX2Ojdus4VrNv/NrBK63AIGTIoARpEJIfzjIRTSv9szj/1FK1jIYRE\nX7Dh4EHvlrU3hH2Nr/o9btqxQoiKaBfYICA5nAyC7jybc+H9puxCamtBSBxoP/TFZ96yl5b6d79P\nBc+ERAHNAA1wksOpAxMuTypedKcxMz9f63gIIdHFuczbvtryduuON1b4PW469JCQKKEEaACTHE4j\nwFbYiq+4jZIfQoY+HgoGWz/b8Hzb3i2r/B43dYInJIooARqgJIdTAtgNtuIrrjVlFRRoHQ8hJLrk\ngM/X8sn/Hgoc+uJOv8ft1zoeQoY6SoAGIMnhNANYZTvjsqWmYY7RWsdDCImuUEt9nXfrup+HGg4+\n6ve4w1rHQ0g8oARogJEcThHAzYnOhYtN2YVjtY6HEBJdHXXffOMte+m7sr/5DdrpRUjsUAI0gESS\nn5sSp12yWMwZN17reAgh0dV+4LPt3rKXlvj3bN6ldSyExBtB6wCIQnI4TQC+lzD1oqXiiAkTtY6H\nEBI9XJZl3+73X/dueXHeYEt+GGNhxth2xtguxtinjLFbGWMx/1vCGCuP/OuOxLOfMVYb+Xg7YyyP\nMdbay7HmM8ZWRz52McZui3z8BGNsYdReBNEUzQANAMpuL3w34ZTSJeaRRUVax0MIiR4e6uho2fHm\nM+37tt3m97gbtY7nJLRxzicDAGMsA8A/ASQC+FX3BzHG9JzzULSD4Zw7I8+3HMBUzvlN3WLo8fpI\nnC8DeLm/scTqNRN1UAKkMcnhNAC4Tio8c6E5/9QpWsdDDsdDHaj650/AQ0FAliEVnomkGYvRuOkx\n+L/aAqbTQ5+UhbTzfwBBtB51/cGHV0IwmgFBABN0GLbsDwCAxrcfR9vX22DMGIW0C24FALTu2gTZ\n70XiaRfG9DWS2Am3t7a0fPzq/R2Ve9b4Pe52tcbN2rR9EYBXqmZN7tWMh1o45zWMsesAlDHGXACW\nAbgEgBWAjjFWCmAdgGQABgA/55yvY4zlAXgNwEcAigGUAXgcwB0AMgAs5pxvYYxNA/BHACKANgAr\nOOdf9iVGxthvAVwQuf5Cznk1Y+wJAO0ATgHwAWNsB45Ino4xzqkA7o+8tjoAyznnlYyxtwFsBzAd\nwL8A3NeX+Ih2KAHSkORw6gFcYxo+7nzLuFnFWsdDjkFnQOYVd0EwmsHDIVQ9+2OY80+FmDcZSSXL\nwAQdGt9+HM0f/QfJZ6045hCZi+6CTrJ9+7kc8KGjai+yV/4J9f/3IDpqy6FPGgbfzjeRcemvY/XK\nSIyFvLU13rK1Pw41VT2j1k6vrE3b9QD+DOA6ANuzNm0vrZo1uUKNsXuLc/41Y0wHJXEBgCkAijjn\nDYwxPYCLOedexlgagI8YY50zLQUALgWwEkoCdCWUJGI+gJ8CuAjAbgAzOOchxthcAHcBWNCH8CwA\nPuKc/4wxdi+AawH8JnJfDoBiznk4Mnt0XIwxA4CHoCRQtYyxywH8NhI7ABg551P7EBcZACgB0ojk\ncAoAlupThn8nceqFZzFB0GkdEzkaYwzMaAYAcDkEyGGAMZhHdU3WmbIL4fvyg76MCi6HwDmHHAyA\nCTp4t7yIhCnzwHT0IzkUddR8/bV3y9qVcsD3rlo7vbI2bbcB+A+AsyNfmgzAHUmCdqjxHCfpTc55\nQ+RjBuAuxthMADKA4QAyI/ft45zvBADG2C4AGzjnnDG2E0Be5DE2AE8yxhwAOJRZpL7oAPBq5ONt\n6PpeAcB/OOe9TUQLAUwA8GZkWU0HoLLb/c/1MS4yANBvW+2cJ5gTz0kqXjST6Q1mrYMhx8flMCqf\n/AFCjZVImFIKU/bh7dhad7wJaezMY1/MGKqf+zkYE2CdfB4SJp8LwSTBbJ+KyiduhjhyEpjJgo7K\nPUg6c1EMXg2Jtbby7WUt216+yu9x71ZjPLG4xKgvKFwlXbr0VsGakHnE3TkA3svatP2CqlmT31Pj\n+XrCGMsHEAZQE/mSr9vdiwGkAziVcx6MFC6LkfsC3R4nd/tcRtffpjsBbOKcXxxZNnu7j+EFeVfD\nyzAO/5vnO8bjj4cB2MU5P+M49/dlLDJAUAKkAcnhnAadYVHSzKuKBZOUonU85MSYoEP2iocgt7ei\nZu1v0VFbDmN6HgCg+cPnAEEHy7izjnlt1uJ7oE9IQ9jXhOrnfg5Dag7EERNgcy6EzalsLqn/vwdh\nm74YLZ++jvZ9n8CQkYek4iti9OpItHA5HPbvfv//fF+8c53f467s+YqeicUlicYp09aYSy9ZwUSz\neJyHJQJ4PWvT9gVVsyb/nxrPezyMsXQAfwXwp8jszZEPsQGoiSQ/swCM7ONT2AAciny8vD+x9tOX\nANIZY2dwzjdHlsRGc84H1Q4+cjjaBh9jksPpAHB90owlp+itKSO0jof0niBaIeYWoe3rjwEArTvf\ngn/vFqTNu+24u030CWkAAJ0lCdLoMxCo2HPY/R3Ve8E5hyElB/7d7yP9otUINVYh2HDoWMORQUIO\nBgItH6//u++LdxarmPwMM531nWfMF11+3QmSn05mAOuyNm2/VI3nPnLszm3wAN4C8AaU4uVjeRbA\n1Miy1lVQanr64l4AdzPGPoGGb9g55x0AFgK4hzH2KZSiZ6rbHORY1+wgiTbJ4cwE8MvE0y6eIuZO\nPF3reEjPwv5mMEEHQbRCDgZQ8/wvkOhcqBQ/b3wUmVeuOazAuTu5ox3gMgSTBLmjHTXP/Ry2MxfB\nnH/qt4+p+e8dSDnnJggGE2pfuhuZV/wWdf/7IxKnzoMxg/rfDkbhNm9zy7ZX7umo3nuf3+PuUGNM\nsbik0HzxoqeMpzqn9WZrdzcygOuqZk3+hxpxDCSMsXLOeZ7WcZDBi5bAYkRyOBMA3CKNPrOAkp/B\nI9zagLr1DwBcBrgMacwMSAXTcOhv14KHg6h+7ucAlELo1HNuQqilHvWvPYjMS+9A2N+E2hcjG05k\nGZZxJYclP/49m2HMKoA+IRUAYMzIR8U/boQhI4+Sn0Eq2FRV5d360i3h5prn/R633N/xxOISxqwJ\nMywrbnjMUFBoP4khBAB/z9q0PbFq1uQH+hsPIUMJzQDFQOSgw1v0KcOnJM9cdhHT6Y1ax0QIUVeg\nyrPHu2Xtct/n72xWYzyxuETQDRu+WLp06e90mcOOLHY+Ga6qWZOPt1Q16DDGfsA5/4PWcZDBixKg\nKItsd1/J9MaSlO/cMFdnTszSOiZCiHo452jft21zyyf/u8rvcX+lxphicYlJXzjux9JFV9wmJNoS\n1Rgz4hdVsyb/pueHETL0URF09M0FMNN2xuVjKPkhZGjh4VDIt2vjiy2f/O9iFZOfJONpxX+2XL78\nZyonPwBwZ9am7T9ReUxCBiVKgKJIcjjtABZJY2cmGDNG0SmhhAwhckdbm3fbK3/2f/nBMr/HXa3G\nmGJxSY449/x/mectXMFMJpMaYx7DmqxN22+J0tiEDBqUAEVJpOj5Rn1KDiyF08/XOh5CiHrCvqbG\n5o/+87PAgZ0/8nvcqvTfEmfMHidduvRlcdY55zKdLtq/m+/P2rT92ig/ByEDGtUARUGk7ucG6AxT\nUs+58Txa+iJk6Ag2HDrk3frSzeGW+rVqtLUQi0sYsyWdbbl06d/0owryVAixt2QAS6pmTf5XDJ+T\nkAGDtsFHx2wA05Ko7oeQISVQsftzb9m6Zb4v3t2qxnhicYlON2LkCmnB4rt16ZlpaozZBwKAp7I2\nbW+K9onRhAxEtASmMsnhzAewWCo802LMzD9N63gIIf3Hucz9Hvc7zZufv0DF5MdsGDvx15Yl1z6g\nQfLTSQ/g+axN20/R6PkJ0QwlQCqSHE4rgBsFc2JAKpx+jtbxEEL6j4eDwdadbz3XuuP1hX6Pe58a\nY4rFJSnG02c8Il121W2CNcGqxpj9YAWwPmvT9lyN4yAkpigBUkmk7mc5AFuic8HpgsFk0TgkQkg/\nyQG/z1u27oE2z0dX+z3uOjXGFItLRornzv+PufSSK5nROFAORR0G4H9Zm7Yfu68LIUMQJUDqmQFg\nmtk+TTSmjpikdTCEkP4JtTbUN29+7seBQ5//zO9x+9UYUyw5e5K0aMUr4ow5s5kgDLTfv+MBvJi1\nabtB60AIiQUqglaB5HCmAVjMTFKtZVzJ1VrHQwjpn476A/u9ZS9dL/saX1Nrp5eQknaBdeUNf9bn\njhqhRoxRMhvAowCWaR0IIdFGCVA/SQ4nA7AEAE887eIzBaOZppAJGcTaD+za4S1bu8S/Z/NONcYT\ni0v0urz870qXLP61LjUtRY0xo+yqrE3bPdQygwx1A20KdjA6DcAUU+5EvTEjf5rWwRBCTg7nsuz7\n8oO3vFtemKdi8mMxTDzlbsvia+4dJMlPpzuyNm0v1ToIQqKJEqB+kBxOG4DlTG+sTZh49nzGGNM6\nJkJI3/FQR0fr9tef8X224XK/x71fjTHF4pJ005mz/iEtWLxKkCySGmPGkADg2axN2x1aB0JItFAC\ndJIiS19XADAknDp/qiBatTrHgxDSD3J7a2vzlrX3tn1ddr3f425QY0yxuCTffMGCF8Tz5l/GDIZB\nWVTMuBy6jD/72w0b7bSjlQxJVAN08iYCKDakjmgyZY85U+tgCCF9F2qpq/WWvXR7qLHiCb/HHVZj\nTHHWOadZllzzpGHsxLFqjBdznAfHY+eHq/D7yRb4LgUQAnCl1mERojbqBXYSJIfTAuAuAKHk2dec\nY0jOHq91TISQvumoLd/nLXvpOrnNu0G1nV4ZWZdICxf/UT88d7gaMcZaYv2emtttfw7k6g4euVPt\n5jmz9z4UzedmjGUB+AOUusomANUAfsA533PE4z7knBer8Hx5AJ7gnJ8V+TwMYCcAA5Sk7ykAD3DO\n5f4+FxmYaAbo5FwMwGoaMZFT8kPI4NP2zacft2x7dYl/z4dfqDGeWFxi0NtHr5IuWfQzISklSY0x\nY0nva2i4ou0RnJdalnGch9y3YaPdPWf23i3ReP5I/eRaAE9yzq+IfG0SgEwAeyKf6znnITWSn+No\n45xPjjxXBoB/AkgE8KsjYtVzzkNRioHEENUA9ZHkcOYCmAPgkHXcWd/ROh5CSO9xOSz7vnj3/1q2\nrpuvYvKTYJh82v2WRSvvHHTJT0egbUbNs5WPit9NOS+17ES71AwAno1iPdAsAEHO+V87v8A5/xSA\njjH2HmPsZQCfAwBjrDXy71mMsXcYY+sYY18zxtYwxhYzxrYwxnYyxuyRx6Uzxl5gjJVFbj2WLHDO\nawBcB+AmpljOGHuZMbYRwAbGmJUxtoEx9nHkuS6MPFceY2w3Y+wJxtgextizjLG5jLEPGGMexti0\nyOOmMcY2M8Y+YYx9yBgrVPfbSXqDZoD6IFL4fBmAdmnMjEKdNXkgH2hGCOlGDgYCrTveeKq9/JMf\n+T3uZjXGFItLskwlZz8szj53HtPrdWqMGQtclmV7/QeHfpDw92Gp6b5hvbysAMoS1bVRCGkCgG3H\nuW8KgAmc82P1YZsEYCyABgBfA3iUcz6NMbYKwPcB/ADAH6EsZb3PGMsF8HrkmhPinH/NGNMB6JwV\nmwKgiHPewBjTA7iYc+5ljKUB+CiSpAHK9+lSACsBlEGpn5oOYD6AnwK4CMBuADM45yHG2FwoJRUL\neoqJqIsSoL4ZB2ACdPr9UsG0y7QOhhDSO+G2Fm/Lx6/c21H11e/9HndAjTHF4hKH+aLLnzZOPcM5\nmE7ASGz86tDNugeTx6YdOpk3cNds2Gh/dc7svetUD+z4thwn+QGAMs55JQAwxvYCeCPy9Z1QZpUA\nYC6Acd3+GyUyxk6mAe2bnPPOXYIMwF2MsZkAZADDoSzXAcA+zvnOSEy7AGzgnHPG2E4AeZHH2AA8\nyRhzAOBQZthIjFEC1EuSw6mHksk3JRR9Z6pgsgymQ80IiVuh5upqb9lLt4aaq//l97hVKWg1n116\npmXZ9Y8bRo8dNOfkdKvz6W+B9qOReqAqVQJT7AKw8Dj3+U5wXfdkVu72uYyuv28CgNM55+3dL4zM\n3BwXYywfQBhAzTHiWAwgHcCpnPMgY6wcgNiHmO4EsIlzfnGkGPvtE8VCooMSoN6bBiBHEBMqxNyi\nEq2DIYT0LFC99yvvlrUrfLs2va/GeGJxiSBkDb/CuvKG+3RZw7PUGDPqOgJtM5r+23R16kvDDJIq\n+V8agMcAnK/GYBEbocyoXMc5fwQAGGNFUJpM99cbUJbDfhcZdzLnfPuJLmCMpQP4K4A/RWZvjnyI\nDUBNJPmZBWBkH2OyATgU+Xh5H68lKqEi6F6QHE4zlEMPaxJOOW860xsH26muhMQVzjna9n3sbn7/\n2VIVkx+T3jH2duuy6x4eDMkPl2U5v/a9Aw/K1xquT39xmEFQdTf3eRs22m9UazCunMdyMYC5jLG9\nkaWjuwGoMct0M4CpjLEdjLHPAVx/nMeZGWPbI8/9FpTE6Y7jPPbZyJg7AVwFpaanL+4FcDdj7BPQ\nRIRm6BygXpAczlIACwXJVp36nRtvYTq9UeuYCCHHxuVw2Pf5O6/6v3z/er/HrcoyjVhcYjNOPf1e\n8/kXL2Mm0aTGmNH0bZ1PwqFovlnzA5g4Z/ber6P4HFFz5DlAJP5Q5tkDyeFMhlK1X2kdP9tJyQ8h\nA5fc0d7e+ulr/2jfv+N2v8fdosaYYnFJtjjnvEdMJWefy3S6Ab3TS8U6n96QoCwT0XEgZFCiBKhn\npQAEZjDJxuxCp9bBEEKOLexvbvJuffmuYO2+P/o97g41xhSLS8ZKCxY/bZwy7VQ1xosa9et8euvs\nDRvtV82ZvfepWD6pSpoAPKF1EEQ7tAR2ApLDmQKlcK7COvm8UyT7aaVax0QIOVqwsbLCW7Z2Vbil\n7gW12lqwBNts6dIljxjso/PViDEaDjvPx+TT6g1tPYAxc2bvrdPo+Qk5KTQDdGLKORJMkMWc8dE6\nfp0Q0g+Byj27vVvXLfftetutxnhicYlOlzNymbTgyrt1GVnHaw2huX6e56OmVChFvSs1joOQPqEZ\noOOQHE4rgPsB1FnGljgs40qOd0YFIUQDnHPe9nXZB63bX1vu97j3qjGmWFwi6sdOuF268PIfCgmJ\nJ3NYXtR1q/MZSGeRcQAz58zeq8qOO0JigWaAju8MKN+fDjHvlB57xxBCYoeHQyHfrk1r/Z7NN/o9\n7lo1xhSLS5KN0858wHzehYuY0TTwNjtoV+fTGwzAwxs22k+ZM3svNQolgwIlQMcgOZwmKH1bas35\nU/N1UmJve+UQQqJM7mjzt3zyv78GDu76pd/jPtEpwb0mFpeMEM+Z95hp+qzZTNANqPPRTrJvlxYm\nQGkg+hetAyGkNygBOrZTAVgB1Jvt02j2h5ABItza2ODdtu6OYN3+h/0ed1CNMcXpsydKly972lg0\nZZIa46lpANX59NavNmy0Pz1n9l5VjiAgJJooATqC5HDqoJxI2mBIz0vVJ6YN2B0ghMSTYP3BA96y\ntTeGfY2vqrbTKyn5HOs1N/1VPzK/r60MoirG5/moKQPATwD8XOtACOkJJUBHmwil1803kuP0s7UO\nhhACtB/J8z9OAAAgAElEQVT8/DPv1nVL/bvfP2EPp94Si0v0uty8a6UFS+7UpaWnqjGmKgZ2nU9v\n/XDDRvvDc2bvPdTzQwnRDiVA3UgOJwNwIQAvdHrBkJ434KbECYknnMtym8f9duvON1f6Pe5v1BhT\nLC6RDBMm/8o8/9IbBYvVosaY/cVlWS6of+/QqoR/DPQ6n94wA/gNgBVaB0LIiVACdLhcAHkAvpEc\nZ4wV9MYB8cuRkHjEQ8Fg62cbnm/bu2WV3+OuV2NMsbgkzVRc8qD4nXkLmcFgUGPM/kps/KriZt2D\nSYOozqc3rtqw0f7AnNl7d2gdCCHHM6B2OwwAZwIIAgDTG43htpZqjeMhJC7JAZ/PW7b2d217t1yr\nVvJjLJpSGPzqy6/9a/+9qP66KwytTzx81GNC+/eh4aarUH3ONPie6+ruIDc1oOHmFahbuRDt72/6\n9utNP/8BwnU1JxWP3tfQsLTu7oaHk36SHeWmpVoQoJyiT8iARQchRkgOpwjgjwDqEEmCAECXmG4V\nc4vsxrSRdp0tI59mhQiJrlBLXZ1368s/DzUcfNTvcYfVGFOcdc5U84IrnzTkO8YJZgk8FETDzSuR\ncNOPYBxX9O3j5MYGhKsrEfhgE5g1EZbLrwIA+F/8J1iCDeKM2Wi8/ftIeeBRBD58B8E9X8C6/Pq+\nBdO9zkcYtHU+vTWDDkckAxUtgXUpAmBEt+QHAMLe2lbfZxs+9QGfAoApe0yWMbvQbkjJKdBZkkcw\nQRjQ3aEJGUw66r4p95at+67sb3pTrZ1eQlr6fOvKG/6kzxmZ8+0doRAQCoExdtjjheQUCMkpCHz0\n3uED6fTggXbwYBBM0IGHQ/C/8E8k/fYPvY6lq87n0WGp6f7BXufTW78EdYsnAxTNAEVIDucVAM6H\nkgA1A2iBcrz7cTGjZBBHTsozZubbDbasAkG0DJzdJIQMMu37d273bl23xL9n8y41xhOLSwz6fMdN\n5ksW/UKXnJoMADwcRsP1VyJ86ADMF12OhOtWHfPa1if+CmaWvp0Bkltb0Pzbn0JurIf1ulUIl+8F\nk6wwnzu/V7F8W+cz9Ja6euOMObP3fqR1EIQciWaAuvwXwBYAhQCmAhgV+XoQQCOA9iMv4B3+YJtn\ns6fNs9kDAPrkbJs4YoLdkJZr1yek5zO9QYxR7IQMWlyWZf+eD9707dp0jd/jPqjGmGJxidUw6dQ7\nzfMWflcwS+bOrzOdDql/fw5yawuafvlDhPZ9Bf2ogh7HE6wJSL77IQCA3OKF/1+Pw/br++H9/a8h\nt3ohXboUxvFHbxrV+xoaFrX9Deembs1W43UNJpyjvb094ZP93xQtnzMblACRAYdmgI4j0gzVDuVc\noKkAEiN3+QA0AThxbQITmCln/HDTsNF2Q0q2XZCSctiR8+2ExDke6uho2fHmM+37tt3q97ib1BhT\nLC7JMM2Y8xdx7vkXMr3+uG/yWp/6G5jJ/O0sz2H3HTED1F3LX34PU/FZCB3cD2bQQ5x5Npp+dSuS\n7+3WASK+6ny+JcucNzWZ9nubxx2oqBgzKRw2JECZSS9yuVyfaR0fId3RDNBx+D3uVih1P59KDuez\nADIBFEBJhsYB0EH5we5cLjscl3ngwM6DgQM7DwJ4RzAnmMSRk/ON6Xl2fVKWXTCak2L1WggZiMLt\nLS0t2169r6PKc4/f4z5qhvVkiMUlBeb5lz5pnFZ8BmPCYW845KYGQG+AYE0AD7SjY5sbliuW92n8\n0MFvEK6tgXHyVIT27gGMiQADeEAJPx7rfDjnaGrS11RUjGhrbJiUznniSADdT9ZmUE6HXqpNhIQc\nG80AnQTJ4TRC+QEfC+A0AJ3H1XcAaIj8e0KGtJEpppzxdmPaiAKdNTWP6fQDr/s0IVES8tbUeMte\n+nGoqeoZtXZ6meecd4Z06ZLHDYXjC491f3DvHnjv+SUgy+CyDPGss2G96rvwv/wfAIA0/1KEG+rQ\ncP1icL8PYAzMLCH18RcgWKwAgKY7fgzr1TdCnzMScmMDmn5xC2RfK6wrvoeMiXlxVefj9bL6yoph\nLfX1k1PC4dTEHh4eAlDgcrlUOcySEDVQAqQCyeG0QVkumwRgCgALlNmhVigzRCeeA9fpBXHExBGm\nLIddnzysQDAnDqPVMjJUdVR/vddbtvZqOeB7V6WdXoKQOWyhtHDJH/TZOTGfdelW55MS6+eONb8f\nzRWH0hvr6ooSg8Hsvr7eh1wu181RCYyQk0AJkMokh1MAkA3AAWW5bEzkLhlK7ZCvpzF01hRJzC3K\nN6Tn2fW2DLtgEBOiFjAhMcI5R/s328tatr1yld/j3q3GmGJxiVFfUPhD6ZJFqwVbsk2NMXstTup8\nAgHuq6hIrqutGS8FAvnp/RiqBcAwl8vV4+9AQmKBEqAoixywOApK3dBUAFlQZofaoewuCx7/aoUx\nqyDDNHys3ZCSY9dZU0YyQUe1W2RQ4XI47Pvivf/5d7/7Xb/HXanGmGJxSaJxyrR7zKULljNRjNmO\ny8PqfEz+IfmzGAzyQFVVQnV19ViD3zc668h6qn642uVyPabSWIT0CyVAMRRptpoMpZj6FACToRy+\nCCjvjprR09lDBpNezC3KNWYWFOiTsuw6c0JGNGMmpL/kYKC99dPXn2j/ZvtP/B63V40xxeKSYaZZ\n5/xNnPWd85lOH7PDSIfyeT7hMA/V1JirKitHM1/ruCzAEI3v60cul+uMKIxLSJ9RAqQhyeHUAcgB\nMBrANAD5kbtkKMXUbT2NoUvMUFp1pI8s0Cem5zO9ccj9YiaDV9jvbW7Z9vKajpqv7/d73D1uDugN\nsbik0HzJoqeNU5ynxapWbqjW+cgyl+vqjFVVlflhr3diJufmWGzGKHK5XDtj8DyEnBAlQAOI5HBK\nUJKg8VASouTIXX4o9UOhnsYwDR87zJRdaNen5BToLEkjGBOo4S3RRLCpqtJbtvaWsLf2P36Pu99F\nMmJxCWPWhJnSpUv/YSgotKsRY4+GYJ0P5xyNjfrqyorc9samonQuJ8b6TRMVQ5MBgRKgASqyXJYO\nZXfZqVAOZOysN+hdqw6TxWgeWZRnzMhXzh4yUasOEhuBKs8e75a1y32fv7NZjfHE4hJBl52zVFq4\n5F5d5rCoL/sOxTofr5fVVVRkt9bXT0qVw6labqxoBJDtcrlUOfuJkJNFCVBvuWyroBzo9TpczV/E\n+uklh9MAIBdKq47T0HXQWBDKclmgpzH0KTlJ4ojxdkNqrl2fmDaK6ahVB1EX55y379u2ueWT/y3z\ne9xfqTGmWFwi6gvH/0S6+PJbhQRb1P9wd9b52E0HpFt+UIlgkCMc5pg504Jlyw9fAdvwVgv+/e9m\ncHBIZgGrfpAGu92EpqYwfvWrKvhaZaxYkYIzp1sAAL/4RRVWrUpDWlpsciqfD00VFRlNdbVFtlBo\nWHLPV8TMUpfL9YyaAzLGWjnn1m6fLwcwlXN+k5rPQ4YOSoB6w2UTAVQB6NxmewDAG5HbW3A1N8Q6\nJMnhTEBXq45TcRKtOsQRE3KMw0bbDcnD7IKUNJxadZD+4OFQyPf52y/793x4g9/jrlZjTLG4JMk4\n7cz7zOdduIQZTVGtTzmyzodzjvZ2DrNZQCjE8YNVFbjhxlSMG9f1vmHXrnbk5hqQkKDDFrcfTz3V\niD/9eTjWvtiMhAQB02dY8NOfVuH++7Ox+UMf9ngCWLYsumVE7e28tbIypb6meoLU0ZHXn23r0fSu\ny+UqUXPA/iZAjDE95zx0vM97ex0ZPIbE1G40zC806ADoX/4yGAAwH13JDwCMAHB15CbDZdsKJRl6\nHcBHcDVH/YfB73G3ANgOYLvkcD4DZXt959lDYwEIUJbImqAcyHg4LvP2/TsOtO/fcQDA24I5URRH\nThplzBhVoLdl2gWjObZnqpBBTe5oa2vZ/tojgQM7fx5pI9NvYnFJjnh26aOmmXPOZoIuerVs3et8\npK46H8YYzGblPUEoxBEKcRz5FmH8+K5kaOw4E2prlR99nZ6hPcARDHLoBCAc5njxxWbc+ZusqLyE\nYJC3V1YmVtdUjzH5/aMzGROsPV+lqZkul6vQ5XJ9GYsnY4zlAXgMQBqAWgArOOf7GWNPQDmS5BQA\nHzDGvFDeWOYD2M8YWwHgYSi/V0MAfsg53xRJri4BYIXSFknVZI7EBs0AHcf8QsPVAM4E8PkTF5kv\nTjGz4l5e6gWwEZ0Jkav562jFeDyRVh15UA5hdALoPB03AGX9vedWHemjUsWccXZD6ogCXUJKHhP0\nhmjFSwa3sK+p0bvt5TuDteV/8nvcPZ5r1RvijNnjpQVXPm2cNPUUNcY7lt7U+YTDHDd87xAOHQri\nwgsTce11xy+je/75JhzYH8Stt6WjtVXGXXdVo6kxjGuuTcU35R2QJAHnnKveCl44zIPV1VJVVdVo\nwdc6Nlrb1qPpLpfL9TO1BmOMhQF0312WAuBlzvlNjLFXAPyXc/4kY2wlgPmc84siCVAagAs552HG\nmAvAPADTOedtjLFbAYznnK9kjI2B8nt9NIArAPwGQBHnPOYrAEQdlAAdw/xCgwXAHwHUZFlZ+sOl\n4tU64aSXh/aia3ZoI1zNRzdOjTLJ4UyC8q5mMpRWHebIXZ1nD51wewvTGXSm3EirjqRhdsGcQK06\nCAAg2HDokLds7ffDrQ0vqdTWgjFb0tmWy676mz7PnqdCiMfU1/N8WlvD+NUvq3HT99MwatTRK3Hb\nP2nDgw/W4YE/ZMNmOzwPaWkJ485f1+COX2fiL3+pR2uLjEsvtWHc+L6X4Cnb1k2VlZV22ds8MQsw\nDeY3Jl+6XK4xPT+sd060BMYYqwMwjHMeZIwZAFRyztMiCdAmzvmTkWtcUErZ7oh8vhbAQ5zzjZHP\n3wNwI5TfoyWc8xVqxU9ij5bAjm0ClCWkjgtG6zP7kfwASuLxvcgtBJdtM7oSom1wNUd9b63f424C\nsA3ANsnhfBxK89bO5bLRUIq7ZSizQ/4jr+fhYLh938fl7fs+LgewQWdNlcSRRXZDep5dn5hhFwym\ngT7dTqIgcGj3596t65b5vnh3qxrjicUlOl3OyJXSwiV36dIz0tQY80jd6nyy+3Kd1arD5MlmlJX5\nj0qAvt4bwH331eLuu7OOSn4A4Jmnm3Dl4iRs3NiKiRNEzJhpgctVjXvu6V3bMs45b2zU11RUjGxv\napyUwbl1eM9XDQqFLpdrgsvl+kzjOI5szdHbVh3U0mOQowTo2GYhUjczMUM3WsVx9QBmRG53AqiH\ny/YWupbLDqn4XMcUOY/lQOS2MdKqIx9Kq47ToOw0A07QqiPcWu/37dq0E5HpZmOWI8M0fGyB0qoj\nOZdadQxtnMu87ast77bueGOF3+Pep8aYYnGJ2TCu6OfmCy+7WbAmqJ9QH6fO50SamsLQ65XkJxCQ\nsW1bG6644vDSuOrqEFyuaqy+PQM5I46eGTp4MIjauhAmTzbj670dMCYyMAZ0BHqeLGtuZnWVFcN9\n9fWTU2U5ObN3L3TQWQAgFgnQh1CWrZ4GsBjAe7287r3I4zcyxkZD+f34JZQZIDLI0R+qI8wvNKRB\n2Wq+XzJAn5PI8nu6ph9SAVweuQEu2+fomh16B67mHk+C7i+/x90O4HMAn0sO5wtQ1s3tUH7AJ0Fp\n1cGgLJV5cYyzhzqqPDUdVZ4aAB8yg6gXRxaNNGbaC/RJw+w60TpQd6GQk8DDwWDrZxtfaPvK/X2/\nx12nxphicUmq8fQZfzCfO/9yZjCquqRzWJ1Pur9PneIb6kO4595ayGFlR1hJiRWnn2HBK68o3Tzm\nzUvEM083wuuV8eAflW+FTgf85eGcb8d47LEGrFyp7PqaNduKX/2yCv/+VxOWLT/2jnSfD40VhzKb\n6+qKbKFQVhqU+pShbAGAO2LwPN8H8Dhj7EeIFEH38rq/AHiYMbYTShH0cs55gEoAhgaqATrC/ELD\nTADLAeyfX6gvuGaKcbFGoQSgvPtQttu7mj+NdQCRVh0j0NWqY1TkrjCU2aEeEzS9LStBzJ1oN6Tl\n2vWJ6XamN5p7uoYMTHLA72v55H9/Dhz6/A6/x33UUunJEItLRornXviY6cyzzmKCuqeWD5a+Xe3t\nvLWiIrW+tmaCpaNj5FBPeI4l3+VyqTKTSEhfUAJ0hPmFhp8AyAbQ+OtZpvMnZ+lO0zqmiCoAb0KZ\nHXoTruaaWAcgOZwWKMtlE6DUD/WtVQdjzDR87DDTsEK7PmW4nVp1DB6h1ob6lrKXfhFsOPh3v8et\nyjEPYsncydLCJU8bJ0yeoMZ4nQZD366ODt5WVZVYU1M9zuT3F2QxFtc/BqtcLteDWgdB4g8lQN3M\nLzRIAB4CcAiA/Owl5lUJJpakcVjHwqGcAdS5XPYBXM2qNJrsrUirjgwc3qqjswK08+yhE/7PJYhW\no5hbNKqrVYc0YP9gxbOOuv3feLeu+57sa3xNrZ1eQkraBdKlS/+sz80boUaMAAZ8365QiAdrqi1V\nVVWjdT7f2CxAH9dZTzdvuVyus7UOgsQfSoC6mV9omARgFYD9U7OFjF+WiN/TOqZe8gF4B0oy9AZc\nzbtjHUCkVcdIKGcPTY18zNGHVh2GlJwk04gJBYa0EXZ9QvooptObohkz6Vn7gV2fesvWLvXv2axK\n926xuESvy7PfIC248le6lDRVEt6B3LdLlnm4ttZUVVVp517vxMxBvm09WjoApLlcrpgfEULi24D6\nZTEATEHkkMDpuXqHxrH0hQXA+ZEb4LJ9g67lsrfgam6KdgCRA/C+itxelRzORCjLZZOgzBBlQCmm\nboVSUH1Uq45gw8GmYMPBrQC2QtAJ4ogJw41ZjgJDcrZdkGzZ1KojdjiXZf+ezRt9n2242u9x71dj\nTLG4xGIomnKHed7C7wmSRZW6nG/rfNIOqTeT1E+cc97QYKiurBzZ0dRYNJS2rUeLEcB3ALygdSAk\nvtAMUESk9cWDUP44d/ztAnHFsAQht4fLBoMwgDJ09S77CK7mE/cJU1lkuWwYgAIoW+3HQkmGjt+q\n4wiCZBPFkZPyjemj7HpbZoFgFBN7uoacHB7q6Gjd+da/2r7e+kO/x63KKbdicUm6afrsP4tnn38x\n0xv6/cZrINb5NDcLtRUVw/0NDZNS5XAynY3VNw+6XK5VWgdB4gslQBHzCw15AH4JYH+GhYmPzBN/\nLAzNGYdmKK06Xody9lB5rAOQHE4TlFYdY6EkRH1v1ZGRnybmjLMbUnLsuoTUPCboaGlBBXJ7a6v3\n41f/0FG55y6/x63KMQxicUm+ed6CJ43O6WcyJvTvZ2qA1fm0tqKxoiKzub5uUlIolDkQ6wUHi49d\nLtepWgdB4gslQBHzCw2lUJrbHdB4+3usedBVTL0JrmZVGln2heRwJqOrVccp6GrV4Y3cemzVIY4s\nyjVmFtj1ycPsgpiQNTRz1+gKeWtrvVvX3R5qrHjC73GrMktonnOeU1qw+AnD2An9ankwkOp82tp4\nS2VlakNtzURLR0duPG5bj4YwgCSXyxXz3z8kflECFDG/0PAbKH94W358pvGs6bn6eOzuGwSwGZ3F\n1Eqrjpj+DyI5nAKAHCitOk6L/MvQdfZQj+fP6BLSLGJukd2YPtKuU1p1WKIZ81DQUVO+z1u29lq5\nvWWjaju9MrIukRYueVA/fESf2k4caSCc59PRwdsqK201NdXjxba2/Mw437YeLWe7XK63tA6CxA9K\ngADMLzQkA7gfwDcA8KfzxSW5NsGubVQDQh2At9C1u6wi1gFIDqcZygGMnWcPdb7jboOSEPV4Jo1x\nWGGmafiYAkPKcLvOkpLLBGGwdc2OqrZvPt3WsnXdUr/H/YUa44nFJUa9ffQq6ZJFPxWSUk56WUjr\nOp9QiHdUV1uqq6sKda2tY7IYo23rUXaHy+VyaR0EiR+0C0yRi8gyCwOQaWG0a0ORBqV/zhUAAJft\nM3Qtl70LV3N7tAOI1KF0tur4D5T2IZ1nDxUB6Kz96VwuO7pVR+WX1R2VX1YD+IAZzQYxt2ikMdNu\nNyRlFQiiNW6XMLgclv1fvv+a7/N3rvN73Kr0oROLSxIMp0y7Syq95GpmNp/cqd8n0bdLLeEwD9fV\nilWVlQW8pWV8FmAaAQC0ohoT07UOgMQXmgECML/QcBGAeQAOFGUKqb+ZLd6kdUyDQDuUVh2ds0Oq\nnBPTF5LDqcexW3WEoJw91GOCpk8alvhtq46E9HymN8RFqw45GAi07njjqfbyT37k97ib1RhTLC7J\nMp31nYfFWefMY3p9n2fZtKrzkWXOGxoMVZWVecGmxkmZgNTn86dkWcbf//53JCQk4Morrzzsvrq6\nOqxbtw6VlZWYPXs2iouLAQA+nw/PPfcc2tvbMXv2bIwZo5RJ/fvf/0ZpaSkSEhJUeHWDSiuUOqCY\n7lIl8YtmgBTjocweYHKWjmZ/ekcEcHbkBrhsFTi8VYcqjTJPJNKSYV/k9rrkcFqhnD00EcpyWefZ\nQz4oy2VH/WINNVV6W5sqPwHwidKqY1y2KbvQbkjOtguWpJyh2Koj3Ob1tmx75d6O6r2/93vcPR5Q\n2Rticclo80WXP2WceobzZArQtTjPp6lJqK2oyPE3NkxKk+WkPjVKPZLb7UZaWhoCgaO/nWazGeee\ney527z78fNLPPvsMU6dOxdixY/Hss89izJgx+PLLL5GVlRWPyQ8AWKFshNimdSAkPsR9AjS/0GCA\nMnNQAQAFKULOia8gx5ENYFnkxuGyfYKuYuoP4GoORjsAv8fdCmAHgB2Sw/lPAJlQlsumQklyT9yq\ng3MeOLjrUODgrkMA3hXEBJM4ctIoY8You96WaRdM0rFbeA8ioebqKm/ZS7eFmqv/5fe4VVlfMs89\nf7pl+fceMzjG9Pnw0G51Pv0qlO6t1lY0VhzKaq6rm5wcDqenqzGm1+uFx+PBjBkzsHnz5qPut1gs\nsFgs8Hg8h31dEAQEg0GEQiEIggBZluF2u7Fo0SI1whqspoMSIBIjcZ8AAciCMksgA8DwBEYJUP8x\nKKdqTwFwO4BWuGxvo2u5bE+0A4jsZKqK3D7o1qqj8+yhzpmGDiizQ0e9dZfbWwL+L9/f7f/y/d0A\nYEjNTTaNGF9gSB1h1yek5Q22Vh2Bqq883rKXVvp2bXpfjfHE4hJByMpeZL36pvt0WdmZfbo4hnU+\nbW3wVlSkNtTWFCUEgzmp6Griq4rXXnsNc+fORUdH39rxTZw4ES+++CK2bduGuXPnoqysDEVFRTAY\n4vpIq2laB0DiByVAypZrBgCSAfoUM+vbL3LSG1YAF0RugMtWjq6TqTdo0KrjFcnhtEFZLpsMJVHr\n3qqjCcc4eyhYv78xWL+/DECZ0qpjYo5xmMNuSM4uEMyJwwZqqw7OOdr3ffxRyyfrl/k9blWST7G4\nxKQfPe426eIrfiwk2np9KvdhdT7p/n4tO51IIMD9VZVJtdXV48T29vxMxoSonBy+Z88eWCwWZGdn\no7y8vE/XiqL4bb1QW1sbPvjgA1x++eV4+eWX0d7ejjPOOAMjRgyYDh+xMl7rAEj8iPsi6PmFhuUA\nTgdQNXOkbvhtxaZrNA4p3oQBbEHXctkWDVp1CDi8VccYdLXqaIRSQ3RCOkuyWRxZlG9Iz1OWywwD\no1UHl0Nh3+fvvur/8v3r/R53lRpjisUlNuPUM+41n3/RMmYSez0LFu3zfEIhHqiqslZXV43R+3yF\nwxjTRT0hfeutt7Bjxw4IgoBQKIRAIICxY8fikksuOeqxb7/9NoxG47dF0N29/vrrKCwsRH19PXQ6\nHcaNG4fnn38eS5YsifZLGGgCACxUCE1igWaAlCURLwDkJQmpGscSj3QAzojcXACa4LJtQOd2e1fz\nN9EOIFILcyhyeyfSqmMUgHFQEqLOzvbtUBKio+qZwr7GNt/n7+wC3tkFAMZMe7pp+Fi7IXWEXWdN\nGalFqw65o7299dPXHm3fv+Onfo9blU7bYnHJcHHu+Y+YZs49l+l0vSoQ1/sa6he1/Y1Fo84nHOah\n2lqxqqrSAWXbujEXiN229blz52Lu3LkAgPLycnz44YfHTH5OpL6+Hl6vF3l5eaiqqoJerwdjDMFg\n1MvmBiITlLq9qC+TExLXCdD8QoMFytLHNwCQZWWDvsh1CEgCsCByA1y2PeiaHdoEV3OPszH9FdkZ\ntTtye1FyOFNweKsOE5QZIi+U3mpHnz1Uvbe2o3pvLYCPmN6oE3OLRhqzCuz6pGF2nTkh6susYX9z\nk3fry3cFa/f90e9x96045TjE4pKx0sLFzxhPmTalVxd0tPtnNv23aWXqumw163xkmfP6emNVVWVe\nqKmpKAOQBlzd3tatWwEAU6dORWtrKx555BEEAgEwxvDRRx/hxhtvhMmkTJ5t3LgRs2fPBqDUBf37\n3//GBx98gLPOOkur8LU2HpQAkRiI6yWw+YUGB4DVAA4AwD1zTRePTdcVaRsVOYEOAB+iKyH6RINW\nHToAw6GcPXQalGWzvrXqSEy3irlFdmPaSLvOlpEv6I2qtuoINlZUeMvW3RxuqX1RrbYWLME2W7ps\n6d8N+Y5RPT0+Wuf5NDYKNZWVI9oaGyaly7JNs7YYpH/CoVAbD3GfLsQCprBetsgm5rCO+CaJW6w2\nLqVK3PTQqDVn3at1nGToi/cEyAnguwD2A8Aj88SVWVYh7qoOB7FaKGcPKQXVrubKWAcgOZwSulp1\nnAags21Dr1t1mLLHZBmzC+2GlJwCnSV5RH9adQQqvtztLVu7zPfFe1tOdozuxOISnS4nd7m0YPHd\nuoysHreN2xo9h76veyhZrTqflhZWX1GR1VJfNyklHE4fEHVV5PjC4XCAB+VWIYSASdaHLLIoJ0ES\nUliCIV2wmdN1NqsomHpKih/PWTNjZUwCJnEt3hOg+QDmAzgIAM8tNN9mNjBqnDl47UTX7NB7sWjV\n0Z3kcDIo7UM6W3VMRFerjmYALTjGcll3zCgZxJGT8oyZ+XaDLatAEC29qkvjnPO2vWXvt3762nK/\nxxHc/IQAACAASURBVP31yb+KLmJxidkwduLt5gsvu0VISLSe6LHd6nz63bfL74e3oiKtoa52Yue2\ndTIAyGE5KIfCrUII7cawPmiRjbINFiEZVn26YDNn6JIskk40qvBU7+WsmTFThXEIOaF4T4BuhFIE\nXWczwfj0JdLtWsdEVNMG4F10FVPvinUAkVYduQAKocwO5UXu6n2rjuRsmzhiQvdWHeKRj+HhUKh1\n16YX2zybb/J73LVqxC4WlyQbndMfMJ87fxEzmo7/R617nY9w8nU+gQD3V1Ym19bUjDcH2vMzTnog\nclJkWQ7JwbCPhdBmDOuCkmwMJ8LMUpBgSBVspgydzZKosxz1/16UVOWsmRG1IxII6RTvCdBvoBS0\n+pzDdZk/m2m6XuuYSNQcQtfZQ2/C1Vwf6wAirTrs6GrVkYjDzx468dZfJjBTzvjhpmGj7YaUbLsg\n2XJ4MNDW8sn//ho4uOuXfo9blQJxsbgkVzxn3j9M02fPZsKxW4GoUecTDPJAdZW1uqp6jMHvK8yK\nxbb1eMQ5l8PBUCsLoc0QFjrMsjGcwM0sBVZ9mpBoStfZpGRd4kCrqbLmrJkR9Q0PJL7FbQI0v9Ag\nAPgbgEoA8mXj9WOXFBkv0zgsEhsygI/RtVy2ORatOrqLLJdlAnBAWS4bD0CAskTWuVx2IkZmsozS\nidZ3Q83Vf4/0Res3cfrsidJlS58xTjzluJsB+lPnEw7zUE2NuaqqyoEW7/hhjBlOut6JKEuf4VDY\nhxD3G0KsQ5SN4QQuIhlWXaqQYEoXkswpukSLjgmDLbkcn7NmxudaB0GGtl69c2OMrQLwOJRfyo9C\n2Qq8mnP+RhRji7YEKH9wZAAYZhVoC3z8EKDMwEwF8DMALXDZNqFrueyraAdwRKuO9ySH04jDW3V0\nnj3UAWW5rPtWdguATB7wPRYK+N5Sa6eXkJJ6rvWa7/9VP3JU7rEe063Op08Ng2WZy/X1xqrKylFh\nb3NRJufmHCB2Z/UMVpxzhMNhP4KyXx8WAmLYELJykSfBoktlicZ0wWZO0yda9UxvBYMVQ6uDBtV+\nkajr7dT1Ss75Hxlj50Dpo7MUwNNQ/mAMVinoVpCaYmY2DWMh2kqAUgw/HwDgsn2Nw1t1eKMdQOSs\nHk/k9nKkVYcdwCQorTo6i/NDUJbN7vN73J+q8dxicYleNzL/OmnBlb/WpaYf/YfnJM7z4ZyjqUlf\nU1GhbFvnPDEmzU4Hk3Ao3M5Dsk8XYu0mWR+yyiJPgqRLYQmGNKWo2GoUDBIYJOgRb6e2UQJEoq63\nP1Kd79XOB/A053zXQO171AcpUGYCAABmA2JV4EcGvnwA10duIbhsbnTODgFlcDVHt3snAL/H3Qxl\nme5jyeF8EkA2lOWyMfh/9s47Oo7yXOPPO7O9qhdLtuVOtx2DE4oLxgkYiCEQWoCEACHkOgQSB9Iv\nDoGEQHKBkAChl1BMMxYOxbgbbMA2LsJFuEkukiWr7q62TfnuHzOSV7JsSfbuzpbvd86es5qZnXln\nJc0881bgveD2z+LSIdt21hSH+ZRxd9tnXjFLcLq6VUD2mNvVLwHj81FzfV2pv7l5XJ6i5GdtMrOi\nKFEmqR2CgpBVMclO1ap64RTyyGUuELz2QjHH6RCsNgC2LBM2/YULIE7C6e+/3joiWgit38lviMiN\nXoZFphnd/sFsJuICiNMbJgBn668/AmjpMapjb6IN0Ed17NNfS+O1X9tZUwqsZ0191Patiy+nHiPI\nu/J8Cvb32RcrGER73f7C1qam0zySNCgfGX7z0iumAiQjZFVEyaFaVQ8cQh5cpnzBYy0Sc1xu0WEF\nYIGIXPAsp2Mho/+GOKlBfwXQTdDGAOxijAWJKB/ADxNnVlIohTZ4DwBgFbkHiNMv8gBcob+AOd5t\nOOQdWoY57X12gk4FbGdNGWa/6DvPWb4xeTIJhxJk+5vnE4mwjvq63KbGxpPtkcjwIgAZEUJWVVVR\nZa0c3KwIUYdiUTxwUG6nuBFynDkmlx1ADkTkcHGTMLgA4iSc/gogBm0w5MUA7oGWj5DugsGFmC69\nVhP6PdWaw4nhBP31MwARzPF+gkOCaGOyR3X0B9u555/uvPamF8wnnXZS18J+5PlIEoscOOBuaGg4\n0RzsGF1CJAxNls3xgDHGFEkJQGYhsyJE7KpF1SumTPmCx1IkeB25otspkOCBAA8EIMMSi9MJLoA4\nCae/AugxaCGvadAEkB/AW9CqVdKVbgLIIvIQGOe4sUL7H5kG4H4ADZjjjR3V0WCkcbazppBQWHyp\n68ZZj5rKh5QBfef5dJWt14+mQOCkEsCc1Gnr/YUxhs5ycJNMEZtqVtzMjhw4hXzyWAtFrz1f9LhM\nJLohwI1+zbHnGAgXQJyE018B9HXG2NeIaD0AMMZaiSgeLc+NxIluAijtPVqc1KMYwHX6i2GOdxMO\neYc+xpz2yNE+HE9sZ00xm4aP+qnjsmv+IOTm5wJHzvNRVaY2NVkOHKgfrvh8p3aVrRtJ7ABNm2Lq\nKgfPI4+lUPDYC0Sv0yKYnSA4udcmI+ACiJNw+iuAJCISoZeNE1Eh0j8J2gm9t4pAILPAQ2CchELQ\nStrHArgTQBBzvMtxKJl6a6IObDtriss89vR77d++/BbB7rD3lufDGENrq6mhvm5IuLXttEKmJq9s\nXR+g2SHICB9lgKYdgD0Ly8GzFS6AOAmnv5eSfwCYB6CIiO4D8F0Av0+YVcnBCSAIALk2sqR/VT8n\nzXAAmKG/gDnevTjUe2gR5rS3xOMgtrOmFFknT3/Mdt6MS0iVo5Mb/1MXm+fj81FTXd2gQHPz2HxV\nyS+OxzFj6WuAZqHodTpFuxWAlQsbTgzHPVSXw+mLfl1yGGMvE9E6AOdBe5K9lDGWsCfWRKOPwbBC\nn72U7+D5PxzDGQyt2vImACrmeNfiULjsU8xpH/CoC9tZU0baL7nyRcuEb0wc2fJxXWeeT7uPgo0N\nRQebmsZ6ZamkANoE+wGjV0wFSEbIIotRh2pRjzBAUysFz5KKKUVVcNELt6DEXYDnv/vXXrfZUL8V\nl770P/jXzLtx0QlT0Rxsw4/e/h3aIwHcOelmXDB6EgDgxrd+gz9/azZK3Mf0K0pn0j3FgpMG9CmA\n9NDXZsbYCQC2Jd6kpGBFTBdom4k/e3JSCgHARP31ewA+zPEuwaFw2a6+dmA/b8aZzu//+Pn8QpP3\nZx0/jwyy1ZXuq8nzb2+doErRinxoozaOSF8DNAtEryNHcDkEErwQ4OW3q0M8s/ZNjMwfikC091me\niqrgL8uewORhp3ctm79lEa4bfwlmjJ6M779xFy4YPQkf7fgEpxSPykbxAyC+aepEVALgYWiFO20A\nGgDcwRj7Kp7HOcKxawCczhhrOto2jLEK/f0yHGrTYgGwCMDvGWNtiba1h03LANzAGKshoucBTIE2\np5AA/IIxtjiZ9iSCPm/8jDGFiKqJaAhjbE8yjEoCNsQIIFlN+3wmTmbjAXCp/gLmeHfikHdoCea0\ndw1OtZ01RRBKBl1ZevWl913sfNc77OAOW1PzSHYwOlUk0ubdMaZCikZlyGrIrJg7HMwadjMb9TJA\n81A5OKdf1PsasWTXatx25vV4as3rvW7z3Lq3MGPMFGysP/Q8aRJNCElhRBQJoiBAVmU8s/YNPHf5\n/ckyPdWIW06CPrVgHoAXGGNX68vGQitSSLgAOkauZYyt1YuN/gJgPjQB0oV+XsQYS9b9607G2JtE\ndC6AJ6F1pk9r+uv5yAWwmYg+B9D1WMMYm5kQqxIPF0CcdGYEgJ/oLxlzvKsBLDwYFReXl0+efNL4\nolmn7V/skXxDTB2sIpSrWsil2pEveMUSsZCKzflmM5lMEOGGCLexp5JZzFn8KH479SfoiPbeD7Pe\nfxAfbF+J1695BLPrD4mbS0+ajtsq78HLG9/Fb6fcihe/eAeXnXw+7Oasjc7HU3afC0BijD3RuYAx\ntpE0HoSWh8cA3MsYm0tEU6F1fW8DcCqA1wFUAbgdgB1aCshOvRjoCQCdw4PvYIx9ojcKfhVAGYDV\n0MUcEd0DoIUx9rD+830AGhljjxzJcMZYlIjuArBDF23t0B58PgMwAcCFRPRraJ4tO4A3GWN36/uv\n0e2YAa3i+RZoYmokgAcZY08QkQuauMqF1vXq94yx+X18n6v1c4N+nPMA/A2anlgD4CeMscjxHJ+I\nKgC8D+BjAGcB2A/gEsZYiIhG6t97IbQ0liv038edAK6EFuGZ1/k9HI3+CqA/9HO7dKHbeUtK0hQ0\nhxNvTAAmAZj0ns156yVyyOHeaDbnC7lwm8Acot3utRTKeZYCyWv2ksNkdxhtcKayaMcq5DtzcVrJ\nGKzes77Xbf64+FH8dsqtEKj7/d1jdeGFKx4AALSF/Xjs05fx1GX34q73H0B72I9bJl6FCWWnJPwc\nUoh4CqBTAKzrZfll0CYcjIWWB7eGiFbo68YCOBFAC4BdAJ5mjE0kotsB3AbgDgCPAHiIMfYxEQ2B\nJkxOBHA3gI8ZY/cQ0UXQ8voA4FkAbwN4mIgEAFdDC3MfFT0KsxFaw9XPoHlefsAY+xQAiOh3jLEW\nPV1lMRGdxhjbpH98D2NsHBE9BOB5aCN9bAC+hCYiwgC+wxjzEVEBgE+JqJIxdrQGrhcAeEc/tk3f\n73mMsa+I6EVoD2YPH8/x9c+OAnANY+xHRPQ6gMsB/AfAywDuZ4zN048vENG39O0nQhOclUQ0mTHW\n+fvslf4mQS/vz3ZpRDfBwz1AnHRGZlB+aCluXl9mLbtheU3YIQ5VI0Musu5sW9hmY1vtNhMdGlPB\nBFWASzaTh9lFj+Iy5agecy7LseYKXqvX5LI4LAIJvCTyGFi7vwofbf8ES3d+iogShT/SgZ+9+yf8\n49uHnh83HdiGWZV/BAC0hNqxdNenEAWxK+kZAB755AXcdtb1mL9lMc4oPxUXjZmKH837PV6+6u9J\nPycDUZJwjHMAvMoYUwA0ENFyaJ4UH4A1jLF6ACCizpAzoHmCztXfTwdwUkwFsUf3aEyGJq7AGPsv\nEbXq72uIqJmIxkMLv61njDX309bY/8naTvGjcyUR3QLtfl4KbWpDpwDqFBNVAFyMMT8APxFFiCgH\nWkTnz0Q0Gdp9sUy37UAvNjxIRH8GUA7gTH3ZGAC7Y3KpXgAwC4cE0LEeH/p+N+jv1wGo0OeQljHG\n5gEAYywMALoA+haAzicPFzRBdPwCiIguA/BXAEXQfhGkHZt5+vP5FKSb4JG4AOKkKbWqELzSXWoJ\nFolFBEAhYufuWemodIwIlZRcnq+oMlpbV7STvEl0WlQXSBVU+CwR+BBRgDYFWqplQNsfMVIsgifg\nEHKCDlOu5DLlqW5zjuCyeCwus9tpN9ucAgk8K6gXfj3lx/j1lB8DAFbvWY9/f/5aN/EDAKtuPZQX\n9PP//hnTR5zVTfzsbtmLA/6DOHPIeGxp3AGryQMiQlhOWs/MVEGK4742Q2vdMhBiv3A15mcVh+6b\nAoBvdN6EO+mjpcrTAG4AUALNI9QnumfnVACdldcdMeuGAfglgDP0BsXPo/uYqli7e56TCcC10EJJ\nExhjkh62OlLctTMH6Dbd9gn9MP94jh+7vQItxHckCMBfGGP/7odNXfQ3BPYAgG+nc+l7D7oLIIUL\nIE768UbUEvhTWaGTucSuK64iiABUXLDtP7aPnGUddvcgZ0H+NC8wDQF/1UEp9EnUZuoYREe4SjNi\nYoS1eyNKu7dVqe1+CQIABmYht88u5oQcYm7UbcpVXOYcwWXxWlxmt91hdrhEQciSgvf+8dJ6LaXi\n+vGX9LntAyuexl2TbwYAXHLidNz89m/x2KcvY/akGxNqYwoSTwG0BJqX4RbG2JMAQESnQcvxuYqI\nXoDWd2gytCalJ/RzvwuhhcMe1Pc5TvdYrADwPQD3EtEMaPktncyDNk7KrG9zVIjIDOA+AHsZY5v0\n3JhYPNAEUTsRFUPLt1nWT/sBbYhxoy4+zkUf1aE6/wRwIxGdD2A5NM/MSMbYDgDX68sScnzGmJ+I\n9hHRpYyxd4jICq3BxocA/kRELzPGAkRUBi3vq/Fo++uvAGrIIPEDHOYB4jlAnPRBZQw/ZR7/ilE5\n7p7RqrBJVgABFsj0jU2PimvO+F3UYnFZAMDlPrUQ7lPR0bFbCviWhFyWNpfYMxmlLwgUhd8TVfye\ndmUv6qPdVzPGYCFXh03wdjhNeRFXp0Aye00us9vutDhcJsGU8cMqzhwyHmcOGQ/gyMLnoYt+e9iy\nxy/9Y9f7Amcu3rn+8cQYmPpE+96kfzDGGBF9B1ruza+g5Z3UQMvjcQHYCC0J+i7G2AEi6q8A+hmA\nfxHRJmj30hUAboWWQP0qEW0GsApAV/W0ntS8FECbHno7Ei8TUQRaQu8iAL3+EenJ3OuhtajZC+CT\nftredRwA7xJRFYC16EerG/37vBfa9/UhEf0QwBtE1JkE/cTR93B8x4cmsv6tJ5VL0JKgFxLRiQBW\n6892AWgjiI4qgOjouU76RkSPQHPZvYOYZ0LG2Nv9MDblmDnGnA8tpLcPAOwmiHOvcKR7Z2tOFtCg\nUvQKR77SWuro1R18yTtqw7Vb1a6Ozjs9ww/uHndHniCIh3llItHWaGvL+wGHWOe2mISkiRIR9qBd\nyOlwiDkRlylPcZlz4DZ7TS6Lx+Y0O1xm0czH0nB2lt8/aaTRRsQbPfn5C2g37e0xy7v6AKUKsX2A\nDDYlYfTXA+SBNjbiWzHLGLSM9nSkm8cnwkNgnDTgQ9kUuLO0yMpcpiPGwqPm7h6hEb5dhXVfvd4m\nnXBNTs9trZZcS0nJ9/IUJaK0tS3eIypb3TYz5fbcLt4oCDkCasgRUOvRKAEIdV8vwhq2kTfgMOVG\nnKZc2W3KhcviFV1mj81pdrqsJkvW1oZnEb13kUxjiOgkAAuglWhv72t7TuLpbxXYDxNtSJJhiMmq\nVxmYrDLJJFDGu+Y56cmvFKfvv8Pz3CQePcMyJLDD+vpMOvBxzruuIUFn+dm9lsCLolXMz79wiKpe\nAJ//s/1K+DPRaVFL4mX7QFEQsXWwRluH1IiDvWSCCMwUtYk5AbuQE3aa8iS3OYe5zDkml9ljdVmc\nTpvJxkv905+jhi7SEcbYFgDDj7D64SMsN5LnoeVJZSz9rQIbDeBxAMWMsVP0BLKZjLF7E2pd4jjM\n4xOS0OG24rCnZA7HSNpUSFfY8qUDZU5Pf2rTFasSAegwAXDBjtdsH7iH+JzewUes3BQEATneM8vg\nPROBjq+awoHFIac5WKa77VMGlWRLUG3KC6pNaJahZXTEQBBlK3kCDiE36DTlSi5zLrQ8JI/FZXE5\n7Sab80hJ4JyUocFoA5JJZ3PEVIIx9rzRNiSa/obAnoKWHf9vANCz0V8BkM4CqNsFMCixgNtKXABx\nUoaPZbHjp8VFFsVj7rdHQ7GxEHB4GMsMVZhS9S/T6q//b8Bsdrj62o/LObrA5RyNcKTB72//oNkh\nHiwVBSEtcnMYFFOYteaEldacls4y/24bkGoVPL7eS/1dDrvZ7uKl/oaTcR4gTurRXwHkYIx93uOh\nacDTqVOICHoIoA6psxMKh2M898l236vD8l1kGtiNOGo5srfGI/sdJ2x67OD28T+3CYLYr/99m7XY\nbSv6gVuWO6JtbR/WWtiuXItJSNf+XxrEhGMs9Te7zG4HL/VPClwAcRJOfwVQExGNgD4/i4i+C6A+\nYVYlmMpqSZo5xhyGdv4yAASijAsgjuF0MKZcbcoL1wxz9yvk1ZOw5ehDJIf6dxc2bX9rb/uYKwcP\nZL8mk9NSUHDZUFWVWXv7ir2QNtjsZhQeg4mpz7GU+ptySBdIWVPqn2CyKgTGMYb+CqBZ0Ka/nkBE\n+wHshtbBMZ1pA2CBLoB8EZZxVQec9GK9InbclF9olnItzmPdR9RCfXomJtQvH7zEM7wWpaf3p+lZ\nNwTBRLm50wYD0+Dzb2iIBlfKTnO0LJtSaogIEjqcktrh9Efreu1Yc5RSf7vT7HDyUv8+4R4gTsLp\nrwC6FMB7AJZCa//dAWA6Ea2LmdWRbrRCm5sCAGgLcw8QxzgelWy+f1cUuMhyfLknEUv/hkhO2fb8\nkIWuQfVW96DSvrfuHY97XDHc4xAK7Wn1+z70O02+QYJA/b2mZDS81P+44QKIk3D6e7E6XX9VQsud\nuQ7asLVbiegNxtgDCbIvkbQgpu12a4gLIE7yCatM/YGYG9wy2nNMIa+eRKzoV26KSIwmbXw45+OJ\nd/ssFudx5fTY7UNy7fYf5UajrUFf+wf7rLS/yCwKvBT9KPBS/z7hITBOwumvACoH8DXGNJFARHcD\n+C+02SnroM0KSzeaoYXAAAAHg9kjgG6cH8KCr2QUOQlf/s+hgqBHP4viX2uiEAXgolEmPPDNwx9C\n28IMN1eG8GWjCiLg2Zk2nDnYhF99FMb7O2SMKxHx4ne0Pn3/2RRFU5Dhjm9wb39vVCtC6LqcQiFc\nYO2zKqu/RC1k0lP1+sQld9hP2fhocOuEX0piHHJWLJZcR0HhNRWKEpHb2hbtManb3FZT4hsrZiID\nL/XPYS5zrphBpf7cA8RJOP0VQEXoXishQesJFNLnlaQjLYg5/wOB7BFAN4wz46cTLfj+vEN++aW7\nZcyvlrDxViesJkJjR+/NsW//IIwLRprw5pUWRBWGoAS0hxm+OKBg009cuLkyhKoGBSPzBDy3QcIH\n12b6g+qx8YJk9f1tSIETtsNHVBwPUUv/PECdlHfszW+unru3+cRrB5QUfTRE0WrKz79oiKrOgM//\nWZ0a/kxwGNhYMRM5llJ/lzlHcFs8VpfZZU/xUv/28vsnhfvejMM5PvorgF4G8BkRzdd//jaAV4jI\nCWBLQixLPAHENETc2aL6FJUpotB3Emm6M3moCTVt3QXO42uj+PU5VlhN2kNjkfPwa2N7mGFFrYzn\nL9E8QxaRYBEBf4RBUrTqmKDEYBaBv62K4raJFpjFdH4IjT8yY+xH8AbWjPR6eg4yjQdRa/89QJ2M\nbVg1eKlneA0rO7MinrbojRUHaY0VtzWFA0tTsrFiRjLAUn+XKVdxW3IElzklSv35mAhOUujvKIw/\nEdH7AM7WF93KGFurv0/XarAAYu4Ukgq1PYLmPDuKDLTJML5qVrGyVsbvloRhMxH+9k0bzijrfv3b\n3aai0EH44fwwNjYomFAq4pELbHBbCReOMmH8vztw3jATvFbCZ/sV/GEKD33Fskeh8NXuQviL7e5E\nycKopd8PNd2Y/NXLQz9ylddZvIMHxdsmAHA5TyhwOU9AOHJAb6zYlDaNFTOSHqX+iEKb9qjTvdQ/\nN+I05ap6onYySv37MxGcwzlu+n2x1AXP2j43TB8OC3k1BdXGPLuYlQJIVoGWEMOnNzmxpk7FlW8G\nsetnLsSmEcgq8EW9ikdn2PD1cjtufz+M+z+O4E/TbLjrbCvuOlu7n91cGcI951rx9BdRLNwp47Ri\nEb+fnN33unmy2f+/ZYV2OEyJrZISBChMUUQamCdTJEaTNz2St2Li3W0WqzthHdFt1hK3regGtyT7\nI+1tC2stbHeexSQcNr+MYywDLfV3mnIVtzk3XqX+XABxkkI2l6y2At1Lhg8E2MHR+QZZYzDlHsJl\nJ5pBRJhYJkIgoCnIUOikbtuUewhfL9f+bL57kgn3f9L9yri+XgFjwJh8Ab9ZHMaH1znxw/khbG9W\nMCo/46OLh6EyhtuZ2790RK6LhOQkpaqALGJguUAA4FBCtrEbHw1+OeGuqCiaLH1/4tgxm9zWgoLL\nhyqqrLa3L99L0ka73YyCRB6TE19iS/1xlFJ/u5gTcZnzZJcph7ktOWaX2WPto9S/OtG2czhAFgug\nymopOHOMuR2AFXqEvKZNbZw84NZwmcGlJ5ixtEbGucNM+KpZQVQBChzd79clLgGDvQKqmxSMKRCx\neLeMkwq6p3P8YWkET37bBkkFFD3NSAAQ7KXUN9NpVBG9wlGotJQ6Ehby6g0ZTDEfvSH0ESkN7s9r\n3vqf/Q0n/yApzQ1FwSTk5Z43GDgPPv/6Bin4sezIssaKmUpXqb/ciKZeBid1lvpbyavk24oaB7nK\nm1zmHAvSN6+Uk2ZkrQDS2QNgGHQBtK1JzYrSy2veCmJZjYKmIEP5//nxx6lW3DjejBvnh3HKYwFY\nROCFS+0gItT5VdxcGcZ7ejXXozNsuPbtEKIKMDxXwHOX2Lv2+842CacPEjDIrYmicSUiTn08gNOK\nBYwtyS7vz0eSKfDLQUVW1WWy9711fFEIyvF8/pSmNWXN+4bXKoOT+zjgcY8vhns8gqGa1oDvI95Y\nMcPpKvVHE1o7dhbu0HrxRwBsPxGXGGscJysgxgZWMZJJzBxjnglgJoB9ACAQ6M0r7b818Ysu5zj4\njeL0vTssz02iMW6MJ++PtuUw4bjyeFQGLBz3y/2W3GFl8bJroESjLUFf+weNNqorMvHGitnC+tlz\nF3zNaCM42UG23+j3I2YqvMrA2sKsqcBBvGcJZ8C0q5CvsOZF64e54tLV+ViRiSkDrIQ/DIGAKVWP\nFi6feHerxeY1pJmhxZLnKCj8XmdjxVqTus2TSo0V71uwBFazCQIRBCLc8c1zuq3f0diM5z9Zizyn\npt1OKSvBt04ehUA4gudXrUMoKmHGqWNwSpl2uXnu47W4bMIp8NqzegrGRqMN4GQP2S6ADvZc0BRk\njQUOcAHEGRCrZVPHT4oKzYrXbLinQj7OEFgndjViGb/xkeDG038TMRk4vFNvrDhUVWfA51u9X42s\nMTksarFR9sTyk6nfgNN65HzxYQV5uGnSGd2Wrd9ThzNHDMGpZaV4euXnOKWsBJvrGjAox5Pt4gcA\n0nW2JCcNyfaGZI3o8R3U+VlW5AFx4sdfZLvvRxUldsVrTmjlVH+RBfTexvsYKA415Aze/HwzS4FY\nuSAIyMk5uyyv+I5i2TLjYCBq28sYi9u5JgtRECDJKmRVhUAERVWx8qvdOPeEEUablgpwAcRJm5+F\nwgAAIABJREFUGlktgCqrpTC0kRhdj11bDir7jLOIk04EVabMFHM7XhlV6CFz6owVkOIogADgxJYN\ng6y1S/bEc5/Hi8t5YmFB8f8MJue1Ab+UV6uoai+dahIMAf9e/hke+mglPt3Z+9dT09yKv3+4Ak+t\n+BwH2v0AgPFDBuHLugN4cvlnOO/EkVi1oxYThpbBYsquQoEjwENgnKSR1UnQADBzjPlnAEZBG44K\nhxmmly+z/zobRmJwjp1Nshj8YUGhKZprSQmvTyz3PhLeNzpoKo/3fj887Y595rxRcd9vPNAaK35Y\nb0FNgUUU4jZc9mi0B8PwOmzwhyN4cvlnuPRrJ2NE4aFGYmFJAoFgNZuwtb4R89dvxq8vPLfbPoJR\nCS+t/gI3nDUBlRu2IChJmDJ6OCoKUibVKZlUz5674ASjjeBkDynz1GogOwF05W0EJchNQVZvoD2c\nFOcx2eb73tBSWyqKHwCIisebAt07U6v+VRwJtTYnYt/Hi9ZY8bsVzrzbHUGctjckoSnRx/Q6NMex\n22bFKWUl2Nvc1m29zWyG1aylWZ5YWgRFZeiIdHdULdqyHeedOBLr99ShojAPV08ci4Wbv0q06anK\nR0YbwMkuuAACag9b0M5Syt3PSQ0ijKlXkzfw+KgiD1lSJ+TVEylBAsjKJPMZGx42y3I01PfWxiAK\nZiEvd/rg3KJfFETFKQc6oqa6RHi5I7KMsCR3vf+q4SBKvN0nevhCYXQee09zGxgYHJZD47MO+jvQ\nFgxjZFE+JEWBAIBAkJS0S2uKFwuNNoCTXRxTFRgRlQB4GMAZANoANAC4gzGW8EcXIqoBcDpjLF5P\neHuA7m1ztxxUaieWiWfFaf+cDGC7IoSvzSmgUIEtKeGV4yFRHiAAKIg0eSq+fKZ+79gf2ygR4+zj\niMczoQSeCQiGdmuNFc3+MmGAM9KORCAcxfOfaKMRVcYwfsggnFBahFU7tOeps0YOxaZ9B7B6Zy0E\nIphFEdd9Y3y32XrvV1VjxqljAADjhgzC85+sxZJtO3H+KaPjYWK6IQFYarQRnOxiwDlApP0HrwLw\nAmPsCX3ZWAAextjK+Jt42PFrEF8BhJljzH+FJoKCAJBvJ+szl9h+JfB+/BwAL0lW/wNDChywiWmR\nF3bbs+HaSQ2mhHZxXjXk4prw8BkViTxGvIlEm4O+tg8a7UJ9sUkUkt6hm3NUVsyeu2CK0UZwsotj\nceOfC0DqFD8AwBjbCOBjInqQiL4koioiugoAiGgqES0novlEtIuI7ieia4noc327Efp2hUT0FhGt\n0V9n68vziWghEW0moqehe2uI6B4iuqPTBiK6j4huP8bvoQqAt/OH5hCLNAVZ3THui5MhyIyxG5nH\n/9eRRe50ET8AEDUlzgPUyVl7FlTITVvTKlRsteQ7CouurbDl/tTcoY6ujcisre9PcZIED39xks6x\nCKBTAKzrZfllAMYBGAtgOoAHiahUXzcWwK0ATgRwPYDRjLGJAJ4GcJu+zSMAHmKMnQHgcn0dANwN\n4GPG2MkA5gEYoi9/FsD3AYCIBABXA/jPMZwPAGwFYI5dsLNF3XWM++JkAPtUCk9xFoXXDM9xp3ik\n5zCi5r63iQdTNz8xKBJsPqyZaKpjEm2m/PyLh7rzf+4N08T9wSg1GG0ThydAc5JPPBM5zwHwKmNM\nYYw1AFgOLUcIANYwxuoZYxFoVVedar8KQIX+fjqAfxLRBgCVADxE5AIwGbqwYYz9F0Cr/r4GQDMR\njQfwLQDrGWPHWqFS03PB+gPq7mPcFyfNeUcy+y8sLTX5iu1pGSaJmJMj2CxMNn19w8M2SQ4Hk3LA\nOCMIAuXknFOWV/zzYtl8QWMgat2XCg0fs5AWAGuNNoKTfRyLANoMYMIAPxOJea/G/KziUCK2AOAb\njLFx+quMMRboY79PA7gBwA+heYSOlRZofYC6yuGX18h7JIVJx7FPThpyu+Ly/35kiYs5TGk7JiZq\nRtJcVnnRFvfIqif9KlPTunTJ5TqpqKB4Vjk5rvH7o7nGNFbMXhbPnrsgrf9+OOnJsQigJQCsRHRL\n5wIiOg1aNdhVRCQSUSE0z83nA9jvQhwKh4GIxulvVwD4nr5sBoDYDmHzAFwAzdP04cBPRaOyWmLQ\nwnpdE7RDMpSaNjVrG3JkGwdVRKdaC0JLRua5SUjv5PdIEgUQAIxory5271ywN5nHTBQ22yBPYfEP\nh1q8P1YD8uAaSVH7egjjHD88/4djCAMWQLqL+DsAphPRTiLaDOAvAF4BsAlaK/MlAO5ijB0YwK5/\nBuB0ItpERFug5QwBwB8BTNaPcxm0svVOW6LQSidfZ4wd7wDILejRFmBNnbLlOPfJSQMWyabA9KJS\nah7kSMuQV0+SLYAA4Ov7PhyqNFYd1lMrXTGb3LaCwisqHHm3O4Ls1D0hCSnZADJD4AKIYwhpPQpD\nT37+AsAVjLHtx7OvmWPMbmiJ2HsBrYrGbYH5he/Y7zQJlKS0Uk6y+Z3s9M0fnucmMb29PrFMWR7d\nN2uVkPSRFRJEZdEZv2+2OouKkn3sZNDuW1svh1Yxp0UeZLQtGQQff8ExjJTtZtsXRHQSgB0AFh+v\n+AGAymrJD6AaMSE2fxRSbRvbcbz75qQe7Srk8835wcpR+Z5MEj8AEDUb839thiKeteEhpySFMjJs\n5PWcXppf/LNBqvXSFn/UuUc9fq8zh3t/OAaStgKIMbaFMTacMTY7jrtdAaBbP/u1PAyWcXwqmzqm\nFpSodeVOR99bpx8Ri3GCziv5nGOqHg+qqpKx4sDhGJ5XWPzjIaLrhkhAKq6VFTVstE1pzJtGG8DJ\nXtJWACWIrdDCX103kAVfSV/JKpONM4kTTx6Q7L6bK0rssjc1B5nGg4gVhjZtrPDtLMrZMW+/kTYk\nA6sl31FQdO1QW+4sMaCMrI3IarvRNqUZtQASPj2AwzkSXADFUFkttQHYjphqsPYIonvaeRgs3Qmq\nTLlUyO14aXShh8ypO8g0HkTNZPj5nV63dIh64IuMSYo+GibRbi4omDnUnf8LT5hO38cbK/ab/8ye\nuyB9k1A5aY/hF8oUZCUAT+wCHgZLb6pkMTgpt0TeOdTtNNqWZGC0B6iTqdueGxzx1w+kEjSt0Ror\nTi7PK/55sWQ+/yBvrNgnLxltACe74QLocDajRxjsv19J1YrKEx7Tkcclm++aIaW2aJ7VarQtySJq\nSQ0BZIIqnLPxYU802uEz2pZk43adXNjVWFHK4Y0VD2fN7LkLqo02gpPdcAHUg8pqqRXauI6u4ait\nYUR3tqpbjbOKM1AijKnXwBt4bHSRh6yZHfLqSdRKKSGAAMAtBxwnb/pXVFWVrMyjs9kGeQqLbuxs\nrFjLGyt2wb0/HMPJqhvDAFiBHmGwD3bIawyyhTNAdipCeLK7WPpymNdltC1GEEkRD1AngwO1BfnV\nr9cbbYeR6I0Vh2qNFU/ZE5aOeW5hJhAB8KrRRnA4XAD1zmZoIbCuMNiiXcqelhBrNM4kTn94Wbb4\nLi0rNQcLbVkT8upJ1EopN8dsfMPHg1H3WVYkRR8NUTALeXnfGpJTNDs/IpxT3xEV64y2yQDenj13\nQVO8dkZEJUT0mj6ZYB0RvUdEo+O1/z6OXUNEBX1tE/N+GRFVE9FGIloTM/KJYwBcAPVCZbXUAmAb\ngLzY5av3ci9QqiIzxm5mHv9fRhR7YBdTygOSbCRL6gkgAJhS/dKQiG9fVnuCYvF6J5bmF98+SLFe\n0hzIrsaKT8ZrR0RE0GZCLmOMjWCMTQDwGwDF8TpGAriWMTYWwGMAHjTamGyGC6Aj8yGAbiGU176U\nNkUVxpMZU4x9KkWmOosinw3PcZOQUU2djw0iKCl4MxWJ0aSNj+RGIwHeLycGp2NEfkHxj4eIzh+E\n/VJRraxmdGPF6tlzFyyL4/7OBSAxxp7oXMAY2wjgYyJ6kIi+JKIqIroKAIhoKhEtJ6L5RLSLiO4n\nomuJ6HN9uxH6doVE9JbupVlDRGfry/OJaCERbSaip6FHCYjoHiK6o9MGIrqPiG7vw/bVAMpiPnON\nbsOXRPTXmOUB/Vw2E9EiIpqoe5J2EdFMfZsKIlpJRF/or7NizncZEb1JRNuI6GVdNIKIziCiVbo3\n6nMicuvDzB/Uz3kTEf34OH43KQ8XQEdmM4AAgK4Bme0RRLccVDcaZxKnJ5WS2X9hSanYXmy3GW1L\nKqEAKZl07FKCtlM3PSorqswfJHpgtRY4C4uuG2rLmSV2KCMytbHiU3He3ykA1vWy/DIA4wCMBTAd\nwINEVKqvGwtt2PaJAK4HMJoxNhHA0wBu07d5BMBDjLEzAFyurwOAuwF8zBg7GZrnaYi+/FkA3we6\nZlReDeA/fdh+AYB39M8MAvBXANN0u88gokv17ZwAlujH9AO4F8A3oQ0lv0ffphHANxljXwNwFYB/\nxBxnPIA7AJwEYDiAs4nIAmAugNt1b9R0ACEANwFo18/7DAA/IqJhfZxH2pKSrvJUoLJakmaOMX8A\n7Y+/awL9/G3SmnEl4hnGWcbp5A7V5V80IteVabO84oECJgOUknlQZR378lu2vrKv8aTry4n/6g7D\nJNrN+QWXDFVVlbX7Vu5j0S8sDjPLhAGzEQAvJOlY5wB4lWme0AYiWg7thu4DsIYxVg8ARLQTh+aR\nVUHzKAGaIDgp5u/TQ0QuAJOhiSswxv5LRK36+xoiaiai8dDCb+sZO2Ki+8u6AHFBEzvQbVvGGDuo\n2/Wyfqx3AEQBfBBjY4QxJhFRFYAKfbkZwD/1nCIFQGwO1OeMsX36fjfon2kHUM8YW6Pb79PXfwvA\naUT0Xf2zXgCjAOw+wrmkNVwAHZ3V0ASQAEAFgHX16sF6v1pb6haGGmpZFnNQRfRKe77cNMjp5rfP\n3lEIKRcCi+XUg5+VL9s/vEYtP6fCaFtSFUEQKDdnSjkwBf5AVWOkY0XUaQ6XUfqqxtfimfyssxnA\nd/vcqjuRmPdqzM8qDt0TBQDfYIx1C0f28dU/DeAGACXQPEJH4lpoXqsHATwKXVAdBSmmoWaXvYwx\nlagr3+/nABqgebcEALF2x56vgqPf9wnAbYyxD/uwKSPgIbCjoCdDrwXQ7elrRa2y1hiLOEtlU2B6\nUSk1DcrMQabxQk5xAQQAk7e/WhFtq834mWHxwO06taigeFY5HFf5/FFvraIyyWibBogC4L4E7HcJ\nACsR3dK5gIhOA9AG4Co9p6UQmjfl8wHsdyEOhcMQU621AsD39GUzAOTGfGYetLDWGdBySI+ILmj+\nAOAbRHSCbtsUIiogIhHANQCWD8BeLzSPjgotrNdXIUg1gFIiOkM/F7cupj4E8BMiMuvLRxNRxnbQ\n5wKobxYD6JZf8sYWaUsgyrKuu63R/EF2+G4bVupU3Waz0bakOjKlXhJ0TwQCJm/6R0E04msz2pZ0\nwW4r9xYW3zTU4rlZCcjlNZKidhhtUz95dfbcBdvjvVNdSHwHwHS9DH4zgL8AeAXAJgAboYmkuxhj\nAxnL8jMAp+uJwFug5QwBwB8BTNaPcxli0iMYY1EASwG8zvpRhMAYCwH4O4A79ZDcr/XPbwSwjjE2\nfwD2PgbgB0S0EcAJAI76d6HbehWAR/XPfATtPvc0gC0AviCiLwH8GxkcKSI+qubozBxjFgDcD01R\n+zuX/3iC+fSLRpsvMsywLMKnQr7KkhfZN9iVsU8i8eaRByONpbKYFnkjB+ylbVWn/8ouiuaUzFlK\nZRQlqrS3L90vyF+6bGbK6/sThqACOCnTR1/oyc9fALiCMbY9ZnkNY6zCMMM4RyRjlV28qKyW1Jlj\nzP8F8APECKAXNkrrp1SYJrks5DnypznHy+eKqePHBQVmOcfCxc8AkEnLWUsHSkL1OS1bXqyrP+XG\n0kTktzS07cWzi/7U9XOzrx4XnX4Dzj3t8q5lizbMxZodiwEAqqrgQNse3P/9t6AyFU8tvBuhSAAX\nn/FDjB12DgDg3x/8AVdNuh05zqP2wEs4omgR8/LOHwKcj/b2z+vk8GpyWpTSvj+ZVF7LAvFzEoAF\nAObFih9OasMFUP9YCy3ua4GWkY+wDGVZjbzyYu4FShh/k+2+5yvyXWTOrlle8UASoSKNskROav5i\nUNOe4TXy0HMr4r3v4pzB+M13td57qqrgd/+5qkvIdDJ93FWYPu4qAEBVzSosrXoLTpsHy6rexjkn\nXoxxwybhsfd/i7HDzkFVzSqUF4w0XPz0xOudOAjeiegI7mgO+Rd1OMwd5YLmlTASFcCf+twqzWGM\nbYFWYt4bDyfTFk7/MfqfIy2orJY6oKn7bt1FX9worQ9EWSb26jCUkMrU7wi5gRdGFXq4+Dk2JIGl\njQeok8m736yQWnbuS+QxqvevR6FnEPLcR24UvHbnUkwYOQ0AIAomROUIZFWCQAIUVcHSqrfxzbFX\nJdLM48LpGJlfUHzrENF5fdAvFdYY3Fjx9dlzF2wz8PiGwxjjAihF4TeX/rMMWnM5S+eCTi+QYRZl\nIF8qYnBSTom0Y6g7KweZxgtJRFom902p+mdxJNyWsEGh62LETW9EpTC27l2DccMmAQBOHzkNVbWr\n8OiCu3D++O9h5eb5mDh6Oizm1O+7abUWuQqLrq+w5cwSA8rw2qisJrtwIyu8P5z0hQugflJZLfmh\neYFKYpc/v4F7geLFk5LNd83gUmsk38qTYY+TaJoKIBuLmk/f8LBJVqJx91rIioSq2lUYP3zyEbep\nql2N4cUnw2nTUvvsVhd+MuPP+NXlj2Nw4ShU1a7G+OFT8Mryv+PphXOw68DmeJsZd0yi3VxQcOlQ\nV/4d7hC+ti8kIVlDnd+cPXfBliQdi8MZMFwADYxlACTEeIGiCtSlu7kX6HiQGGPXwRv4x6hCD6xC\nVg8yjRdRU3oKIAAoDB/0Dv3yuVbG1Liew5a9n2NwwSh4HEculjqah+j9dS/h/K9di7U7lmB4ySm4\n/txf4b11L8bTxIQiCCbKzZ1anlv0i6Ko6byGQNSyjyWuDJjh0JgGDicl4QJoABzJC/TCRmm9P8J4\nL5NjYJcihM5xF0c2DvO60rfBbeoRTfPyhjGtm0ptNR/t6XvL/rN2xxJMGHHk8FcoEsCO+k04reKs\nw9Y1tu9DW0cTRg8ah6gchkACCARJjvSyp9TH4x5bXFD803I4rmxPUGPFN2fPXZD67jFOVsMF0MBZ\nil68QIt2yQPp2skB8Kpk8V1SVmoJFtpSP6EizUh3AQQAZ9dWDpWaq/fGY18RKYRt+9ZhXEz118ot\n72Lllne7ft5Y8zFOKJ8Aq9l+2Off/fxZfHvijQC0vKCVWyrxwLz/wdRT+5pikNrYbYNzCotvGmp2\n3yQH5LJ4NVbk3h9OWsAbIR4DM8eYL0aPLqAE4KmZtpuLnEKZYYalCSpj+Ak8/k8qctwkcK9PIrjh\n1XDNhTWmCqPtOF4iZJaXnPG/bVZHXmrVnGcoihJR2tqW7BeVLcfTWPG12XMXXBNXwzicBMA9QMfG\nMmj9gLqSdRmA5zdI76lcUR6VOoUiUxxFoVXDc7n4SSARc2bEE61MMn1948MWWY4EjbYlGxBFq5if\nP2OIp+DneRHh7LqOqDiQ8REAEADwy0TYxuHEGy6AjoHKaikA4F30yAX6eI9St7lRXW+MVanPAtns\nv6C0VGwrsR8eY+DElWgGTUvLizR7hlU95WNMTbveRumKIAjwer8+KL/49hLFenFzIOrYo7J+9Za6\nZ/bcBXzALSct4ALo2FkMbeKwO3bho59HF0VkFjLGpNRltuLy/Xp4iYs5TRmQnZL6RMzICA9QJ6Pa\nt5Y4d70Xl3wgzsBwOkbnFxTfOkRwXh/0SwU1sqoeKfN7K3jXY04awQXQMVJZLYUBvAigW27CgQAL\nLd4tLzXGqtSjWYU0zZIfXDgyz0NiZoRl0oGoJfO+62/sfX+ofPDLuFaGcfqPzVrkKiz6foXN+xMK\nKMN6a6x42+y5C9JoAAsn2+EC6PjYAKAKPUZkPLlOWtsUVAcaO884lsmmwLTCUhwsczqMtiXbiJgz\n83/73M1PlUU6DiarkR+nF0wmp6Wg4DtDXfl3uAPqaQclRayBNvJisdG2cTgDISMvksmislpiAF6B\nlgzdFdpRGdhLG6X3sjkfeo7s9P10WKlT9ZgzKBslfYhYMisE1okZsnjmhocckhSOR7k25zgQBBMV\n5E8vdOX/LM/ivuoOo+3hcAYKF0DHSWW1VAfgvwAGxS5fWqPs3dakbjTGKuPwq5AvNOUF3xqV7yFT\n5oVh0oWI1fAp4AkjR2p3ja56okNVVcVoWzgAEf3mtqevrzfaDg5noGTsRTLJvA+t/NMZu/DRz6Mf\nhWWWNeW7a2WxY3J+ibp3sIuHvAwmasns/+1hvu1F3p3zEzo5ntMvVgF43GgjOJxjIaMvksmisloK\nAvgPgKLY5ft8rOONzdK7vX8qs/g/2e67oaLULudYLH1vzUk0EUvmeoA6OWP/oqFqw4Zao+3IVhhj\nUQC3zHpiWvbG+jlpTcZfJJPIWmhloN1E0Btb5G1bDiobjDEp8YRVpl4u5ASeG1XoIbPA/55ShIgF\nWTFUdsrWZwZHAg0NRtuRjRDRn2Y9MY3P++KkLfyGFScqqyUVmhfIBqBb4u8Dn0Q/yMRhqVsUIXRO\nTon01VCPy2hbON2JWpEV/ZbMUIWzNzzklqSg32hbsgnG2EoAfzbaDg7neOACKI5UVkv7ALwBoNs8\nsJYQizy/IfpOJo3JeFqy+q4aXGqJ5FutfW/NSTYRM2WFBwgAPLLfceKmxyKqqshG25INMMZ8RHT9\nrCem8c7cnLSGC6D48xGAavToDfTRLqV2XZ262hiT4ofEGLse3sDDo4o8sIpZc5NNN6LW7AiBdTLE\nv7sgd/tbvBIpCRDRj2c9MY3nXnHSHi6A4kxltSQDeAaACC0c1sXfVkWWtIRY2jZx260I4Umu4siG\nYV4X8Qr3lCZqoawIgcUyoX75YNSvqTHajkyGMfWlWU9Me81oOziceJB1F8lkUFktNc4cY34RwC0A\ndkMbFo+QDOWxNdG3f3OO5UeikF4hitcli/9PgwvtsItp+zez75l98G/ww+QxYdR9owAADW81wLfe\nByKC6BFRfnM5zLmH925s+rAJrctbAQJs5TaU3VQGwSLgwOsH4N/kh32IHeW3lAMA2la1QfbLKDi/\n4LD9JAvZKoiMKcg2oTpl2wtDF7rK6q3uQaVG25JpqEytFUiYZbQdHE684B6gxPEJgDUAul2IP9+v\nNCyrUZYYY9LAURnDrarbf8/IYnc6ix8AyD0nFxWzK7otK7iwAKPuHYWRfxoJzzgPGucf7qCTWiU0\nf9SMEXNGYNR9o8BUhvbP2qEEFYRqQxh17yiQiRDeG4YaVdG6shX55+Un6ayOjApkXU6MSIwmbXw4\nJxrt6DmninMcMMYUgYSrZz0xjSebczIGLoAShD4m4yUAUQDdqqT+8Vl01a5WdZshhg2AeoUiUxyF\noU9G5LpJSH9PgnOME6Kzu+NNtB/6WY2oR/SYMJVBjapgCgOLMphyTQABTGZgTFtHIqHp/SbkT88H\nmYz/vpQsFEAA4JI77KdsfFRSVJkP5owff5z1xLRPjTaCw4knXAAlkMpqqQ3AU9B6A3V91wzAH5eF\n57WFWZNRtvXF+7LZf35pqdhW4rAbbUuiaXizAdt+sQ1tq9tQ9J2iw9abc80ouKAAX83+Ctvu2AbB\nLsB9ihuiXYR7rBs7/3cnTF4TBIeA0K4QPBM8BpzF4cjE4joq4qXWFszcvQvf3r0LL7a0HLZ+VySC\na2prMParajzb0ty1vEWWcd2eWszcvQuL/IccCLP270NjgjRKecfe/KJtr/H+QHFAVZVFRHSf0XZw\nOPGGC6DEswnAYgDlsQtbw4j+bVXktajCIsaYdWTuVJy+O4eXuJjTlNYhr/5S/N1inPB/JyDnzBw0\nL24+bL3SocC/3o/RD47GCQ+dADWiom2V1tap8MJCjPzTSJReU4rGtxtR9J0itCxvwZ5/7UFjpbH5\n7goQNwG0PRLBG21tmDu0AvMqhmFZRwC10Wi3bbyiiN8WFeOHuXndlv/X78OV3hzMHVqBl1o14bQ0\n4MeJViuKTImblTu2cXU57V9dk7ADZAGKKu8WBPEKXvLOyUS4AEoweijsdQD1AApj121qUJtf2ii9\nlSr9gVpUSNMt+cEPRuZ7SMyy7FkA3jO98K09PHUksDkAc4EZJo8JZCJ4TvcguKP7iLdQbQiMMVhL\nrfCt8WHIrCGINkYROWCcvlUofgJoZzSC0+x22AUBJiKcYXd08+YAQL7JhFPtdvSM/plBCDOGKGMQ\niCAzhhdbW3FTXuLzpCZ/9fLQaPueuoQfKANRVSUoCqYLZz0xLeOauHI4ABdASaGyWgoB+Ae077tb\nPtD8ann7ylplqSGGxbBSFgPTCkvRUObMqkGmsQLF/4Uf1tLD+zqa880I7QxBjahgjKFjS8dh2zW+\n3Yjiy4q1nCBV17MEqFHjHpylOIbARlmsWBcMok1REFJVrOgIoL6f4auLPB4sCfhx8969uCUvH6+2\ntWKmxwN7EianiMRo8sZH8qMRP7+JDwDGGFOZevWsJ6alfK4ih3OsZEWIIxWorJYaZo4x/xPAXQAi\nALruHv+3Orqy3COUjsgTTjTCtntkh+/1YXluMmVApvNR2Pv4XnRs64AckLHt59tQdGkRApsCmggi\nwJJvwaAbBgHQKr/2P7cfFb+ogGOEA54zPNhx9w6QSLANsSF3am7Xfn3rfLBV2LrK521DbNj+++2w\nldtgH2JcCpUsQEWc9NcIqxU35+Xj5r17YBcEnGC1ob9OQrco4onywQCAdkXB0y3N+EdZOf73QD18\nioob8vIwzp6478mhhq1jN/4j+OWEX0VF0cSH9faDqBy+5xfPXJQVg5w52QulSPQla5g5xjwDwDWI\n6Q8EAF4rLP+YYb85106FR/xwnPGrkK+25EX2DHY5k3VMTvL4+98jBwZHxZJE7PuhgweveJqHAAAg\nAElEQVRRYjLhmtzcw9b9s+kgHIKAG3sJcf21sQHnulyojUowE+Fbbjdu378fTw0enAgzu/Flwen7\nG06+oSzbeiMNlIgUrvzFMxdeYrQdHE6i4SGw5PMhgFXokRTdHkH0gU8ir0VkFk6GEV/IYseUvBKV\ni5/MJSrELwcIAJplraq+TpKwKODHRZ6BVbvVRKM4IMuY6HAizFQIAAhAmCUnTHhK09oy074VNUk5\nWJoiyZFqq9l2jdF2cDjJgAugJKNPjX8BQB208vguNh9UW55cF31NVllC+7c8Itl93x9aapdyLTwc\nkMFIYnzdu7fX7cfFu3dh1v59+H1RMTyiiNfaWvFaWysA4KAs49ydO/BCayv+3dyMc3fuQEA5pMEe\naTqI2ws0B+eFbg9ea2vDlbU1uL4XL1KimLTj9Ypo6+79STtgGiErUqvZZP3WrCemBfvemsNJf3gI\nzCBmjjEXA5gDoANAIHbd5Seaxlw/1nyVEGdffVhl6nVibrC6wuPqe2tOuvOHf4X3nuozJT62lGaE\nBGt0+cS7Oyw2b/KUV4ojK3JIZcqZP396xkajbeFwkgX3ABlEZbXUAOCfAAoAdPPEvLVVrp6/Ta6M\npzjdKguhSTklEhc/2UNUBH+66QW7GrF8bcMjJCtSyvXgMgJFlaVgxP9tLn442QYXQAZSWS1thjYu\noxza9PguntsgbViyW/koHsd5Vrb6rhxcagnnWw+v8eZkLJKJC6AjURRuyBm8+flmluUucFVV1dZA\n4w2/efHyxUbbwuEkGy6AjGcJgHkAhqLH7+ORz6KrPt8vf3KsO5YYY99n3sD/jSzywCam1fR5zvET\n5b/xo3Jiy4ZB1trFtUbbYRSMMXbQt/+Xd79y3StG28LhGAEXQAajd4qeD+AjaCKoW97PvSuiizY3\nKusHut9ahcKTXcWR9cO9Ll72m51EzdwD1Bfn1MyrkFq27zXaDiNo8tX/5Z7XfvCQ0XZwOEbBBVAK\noFeGvQLgUwBDeq7/w9LIuwOZHv+mZPFfPGiQKVBks8XRTE6aEeFtTvvF1Kp/lURCrYcPgctgmnz1\nT8159brfGW0Hh2MkXAClCJXVkgLgGQCb0aNHkKyC/XZx+K06v1pztH2ojOF/VLd/zshiNxwiv/1l\nOREzd/31ByuTzGdseNgsy5GQ0bYkgxZ/w7y7X7n2FqPt4HCMhgugFKKyWooCeAzAHgClseuCEuQ7\nF4Zf2e9Td/f22QaVolPthaGVI3LdlNkTLTj9JJq4QesZR0GkyVPx5bNtjKkZPfX8oK9uweufPHq5\n0XZwOKkAF0ApRmW1FATwCIBWAMWx6/xRSHd+FH5lT7u6M3b5B7LJ/83iUmotdRg3eIqTckTM4Ep4\nAIxu+7LUsfvDjM0HOtBa+95bqx6bWVWziueGcTjgAiglqayW2gH8DUAYWp+gLgJRyHcuDL9a06Z+\nBQC/Upy+Xw4vdTGXiT/vc7oRtfAQ2EA5c8+CoXLT1j1G2xFv9jXv/OCdz57i4ofDiYELoBSlslpq\nAvAAABk9RFBIhnLrwsiKb7c4mt4bme+h/o7l5mQV3AN0bEzd/MSgSLDpoNF2xIvaxm3/XbDmuZlV\nNaviOhuOw0l3uABKYSqrpXoAfwEQhT43jAFoFIXxW0zms1av9H8Y3h/eYKSNnNQlauH/38eChcmm\nr294xCbJ4bSeicUYw476TXPf/+I/l1bVrJKMtofDSTX4BTLF0Udm/AVAUAbKa03i9L0mU7lPEBZG\nIexoeKNhfqgm9KnRdnJSj7CF+P/3MZIXbXGPrHrSr6ZpUrTKVLZ139rnFm18/bqqmlUJHa7M4aQr\n/AKZBlRWSwcB/GW/SXQeMJnILwjvqUTtnesb32n8sKO6Y6mBJnJSkKiFeC/o42BEe3Wxe8e7+4y2\nY6AoqqJU1a7+14rN83/ExQ+Hc2S4AEoTKqul5t0Wy/+EBWEJiEp6rm96v2lF+5r2eUxlPM7PAcBD\nYPHg6/sXDlEaN6VNUnRECoc//+qjOau3vX87z/nhcI4Ov0CmEb71vlZoidG1AAb3XN/2Sdum5sXN\nL6qSmhUN3ThHJ2wF9wDFgalbni6LdDQ2Gm1HX/hDbW3Lqt6+bWPNx/dV1axKy9Adh5NMuABKM3zr\nfX4AfwewBUAFeswO69jcsafxncanlaCSVa39OYfDPUDxwQxFPGvDQ05JCgWMtuVIHGzfX/f+updu\n2N245Rle6s7h9A9+gUxDfOt9IQCPAlgJYBiAbmMvIvsjLQdeO/CM1CZl7aRrDhCxEh+HEie8ks85\npurxoKoqKRdWqmnYurXy82cvX/7lvPnxFj9EpBDRBiLaTEQbiWg2UfKT64moJvY9EVUR0SYiWk5E\nQ5NtDycz4AIoTfGt90UBPAfgdWjhsG5doGWfHKp/uf6lcF14oxH2cYyHJ0HHlwrfzqKcHfP2G21H\nJ4yprKpm1YoP1r/87S92Lk1UJWiIMTaOMXYygG8CmAHg7p4bESVdbJ/LGDsNwDIAv0/ysTkZAhdA\naYxvvU/1rfctAPAvAIUAvLHrmcSUhtcb3glsDSxmjHG3eJYhWcG7g8eZ0+uWDmEH1hnuWZUVSVq9\n7YM3Ptn23neralbt7PsTxw9jrBHALQB+Sho3EFElES0BsJiIXES0mIi+0D00lwAAEVUQ0TYiep6I\nviKil4loOhF9QkTbiWiivt1EIlpNROuJaBURjemHWasBlHX+QES/IKIv9dcd8Ti+fp5vE9EH+vYP\nxBzvAv18NxLRYn2Zk4ieJaLP9X1dEpdfACfuEL8vZgae8Z6RAO6AlhN0WBdb16muYbmTci8XLIIz\n6cZxDGPunyVGxDuFxxMZgvrRhN82Wt2lh1VjJoNAuL394y0L/l3TuPWeqppVHYk8FhEFGGOuHsva\nAIyB5g26F8BpjLEW3QvkYIz5iKgAwKcARgEYCmAHgPEANgNYA2AjgJuA/2/v3oPjrO97j7+/e9Gu\n1vKjiyUwvtsEwsWAhR0gYG6tkylpeiGcHpikk5LTM2k6adqcToeTmZ6THMoEcmtxSShwyimXhFBS\nAoRCSwxYXE2wjYUtG2zwRTaWZNmWbO/qttrd53v++D2LZVuSJVvalbTf18wzerT77D6/Xa/1fPZ3\n5feBr6jqH4qIB/SoalZEVgB/rqo3BedsVtUF+X1gmaoeFJGVwHuq+n9FZCnwMHAF7u/g28Af49ZV\nPOXzi8itwLeDx6eBbcBy3FJFG4BrVHWXiNQE78OdQZl+JiJVwFqgXlXH9d/KjJ7VAE0RycbkduAO\nIMmAb0R5XU1du/b9Yt8DmcOZSTOk15y+HEy4PiuTXQQ/tHzjSq+/vztZ6HPvPbh959O/eeCvm/e/\n/7fjHX5G6EVV7Qz2BbhTRDYBL+H+DuUXdN6lqk2q6uNCSL5Wugk3mANcDfa/ichm4G7gwmHO2yAi\nLbgQ9nhw23LgaVXtVtUu4Cng6jE6/8uqekRV+3ADUObjgtZrqroLYMD78FngWyLyLq6JLg7MG+a1\nmCKxADSFJBuT7cB3cd9QFsKxw6AzBzOp1p+2PtKzq+etYpTPFF7OrSVnxtj0bFdi8aZ7+30/V5D3\nN+fnsuu3r17z3PqHv9rdl3yoWBMcisgiXKjOTwswMIR9CdcUv1RVlwDtuIs/uJqTPH/A7z5HB3Hc\nATSo6mLg9wY8djDX40LIu8DtIyj66Z5/4ONzHDfw5DgC3BT0nVqiqvNU9f0RlNEUmAWgKSbZmOwC\nVgLP4r51HNvklcM/8KsDqw69eegJzWp6kKcwU0hO1ALQOJnTtbu2dtsTbeN9nu6+5OHn1z/y1Prt\nq7/W1Lzm5WINcxeROuB+4CdD9CmsBParakZE8gFlNCqBfCfzW092sKpmcc3+XxaRGtyo2D8UkYSI\nTANuDG4bl/PjmviuEZGFAEEZAH4NfCPf9Cwi9aMogykgC0BTULIxmU02Jn8J/AMwnWAh1WOOWZfc\n2v5U+wPZruy+ghfQFIw1gY2vJe1vzpXWt8etU3RLx46dT665997Wzp3faGpe0zRe5xlGeX4YPK5Z\naxVD17g8BiwTkSbgy8DWUZ7rB8BdItLI8DUsH1PVNlwT2NdVdQOuD9BaXP+fB1W1cbzOr6oHcJ3C\nnxKRjcATwV13AFFgU/C+3TGKMpgCsk7QU5xX750BfB1XG/QRrsr3YxKVcO0Ntb9VvrD809ZZdup5\n4HvpzmoN15z8SHOqciq6aum32mLenFlj9px+Ltu489V167evvgd4qql5Tf9YPfdkNLATtDFjxQJQ\nCfDqvRhwM7ACaMWNXjjGtAunzau+uvrGcDxcVejymfFz7/fTB+v8cG2xyzHVdYUTfW9c9p10Wayi\n8uRHDy/Z03nglc3PvNLaufPOpuY1745F+SY7C0BmPFgTWAlINibTwE+B+4DaYDtG95buPa2Ptt7X\nt7dvQ6HLZ8ZPJoStCVUAFbme+MUb78nl/Owp19T4vp9776O1G5544577Wjt3/oWFn2OsLHYBzNRj\nNUAlxqv35gB/hps9ei+DjBKafun0c6quqPr9UFmo4vj7zOTyo79P75vXHy7KfDWlqKnusr37L/jy\nnNG2Jqd6D7ev3vTk2rZDzY8Dvyz1Ji9jCsECUAny6r0y4PO4ScCO4CYKO0akMlJe+7naz8fOjF1Q\n6PKZsXPX3X0tZ/dFTpgXyoyfV86+pdmfe/WCkRzr+7nc1pZ3Nrzx3vPv+Jp7ENhgi5kaUxgWgEpY\nMHv0V3FNYnvhxOaSyssqz/eWejeEYqHphS6fOX1/d0/f3vO6I3OKXY5S4iusqr+tpaxq/rDBM9lz\naF9D05Nr2w7tfhF4rKl5zQlfRIwx48cCUInz6r1y4Cbc7KUHgNTxx4QSobLaz9ReH18Qv9xGik0u\n//vevo8uSkbmFrscpaYnFE+/dvl3espiXvXx9/l+Lvf+3nfeefP95zb46j8ErLNaH2MKzwKQAcCr\n9y7E1QZV4CYDO6E2qHxR+Zk119Z8PlJpNQqTxW339+1edigy2gnpzBjYVz7zUNOybyXC4Wgsf9vB\nZNuOVzY/velgsnU18LOm5jWHi1hEY0qaBSDzMa/em44bLn81rl/QoH+cq6+tvrRiccWKUDRUXsjy\nmdH75oN9u688YAGoWN6bUd/StvhPZ6UzvUfWbX/57S173t4JPASst1ofY4rLApA5hlfvCW6l56/g\nFjJsBU4YkRKpiiRmfGbGZ2KzYkusVWzi+vrDfbuvbbMAVCxZJfPYjKteX9W+vS2T638L19fHan2M\nmQAsAJlBBSPFVgBfwA2VbwdO+LAkzk3Mqrqy6rPRqqhdZCeg//6zdPNnPwovKHY5So0qfKDhzQ9k\npr23V8P7gEeARqv1MWbisABkhhUspfFFoB7XSbpr0OOWeud6l3orwtPCdYUsnxnel59IN39+pwWg\nQtqdk65fZMtfWqexQ8DzwH80Na/pLXa5jDHHsgBkTipoFlsC/AngAW1A5oQDQ0j18ur6igsrrrNh\n8xPDLU+ld39hW9hq5wqgK5c71NDd9ZsnM/GadLz6ZT8cu7epeU1rsctljBmcBSAzYl69lwB+B/gc\nrjmsjUFGi4XioWjNdTVXJD6RuEoiEjv+flM4X3g2vfuWLRaAxlNXLnfozZ7uNc8lkx052A/8DNjU\nkErZH1djJjALQGbUvHqvFjeL9NW4hVX3M0j/oEhVJFFzbc3y+Lz4MglLtMDFNMDnXkjvubUxPK/Y\n5ZiKunK5zjU93W88m0we9F0/uX8DXmtIpWwZC2MmAQtA5pR59d5c4I+AS3BLanQOdlykKpKoXl59\nRfmC8susRqiwVqzu3/vVt0M2b9MYcsGn5/Vnk0f2+xAFXgb+vSGVOlLsshljRs4CkDktA4bNfxGY\nzzAdpcMV4Vj11dWXly8qv8LmECqMq1/vb/nGGyFbC2wMDBJ81gDPN6RS1s/HmEnIApAZE169F8aN\nFPsiUAN0MMiyGgCh8lC0enn1ssQ5iSttxfnxddnb/a1/szo0q9jlmMws+BgzNVkAMmPKq/eiwFLc\n+mJ1uBmlB20akDKJVF9VvSRxTuLycCJcW8BiloxLGjP7/vYFmVnsckxG7ZnMrrd7etav6kodHhB8\nnmtIpdqKXTZjzOmzAGTGhVfvRXB9g24CZuFC0JCrXU+/ZPqiisUVl0Vro+fagqtj5/wt2QO3P4vN\nzTRCGdX+Hen0xhe7UuvfT6fDQBnwJq7Gx4KPMVOIBSAzrrx6LwQsxgWh+bhmsY6hji+bWVZVeVnl\np+Jz4/XWT+j0nf1htuOuJ5lR7HJMdMlc7uDGvt51zyeTTUnfr8bV+FjwMWYKswBkCiLoLH0+cCPw\nCdz6YvuB3GDHh2KhSOXllRclzk1cHqmInFm4kk4ts3dnD939c6qLXY6JyFfVlkxm25s93Wtf6+5u\nB2px81q9CbxgwceYqc0CkCmoIAgtAK4HrgRCuJFjQy4VMO28aXMqFlfUx2bGLrRh9KNTty+Xuvch\ntVm5B0j7fs/WdHrDC6nk+t2ZTBSYBhzGLVuxtiGVSha3hMaYQrAAZIrGq/cqgStwM0t7uOHzQzaP\nhWKhiLfUOz/xicSSSHVkofUVOrnKzlzPPz+giWKXo9gyquk9/f1bN/T2bn69u2tPFs4AwsAW4NfA\n+w2pVLa4pTTGFJIFIFN0QYfpxcANwLm4dcYOMNh6Y4FoXXS6t8S7KD4/frE1kQ0t3uX3P/pjv6zY\n5SiGnGq2JZP54N2+3s2vdnV92KtaDlTjPlercbM2WzOXMSXKApCZMILmsdnAtbhlNmK4WqFOBllq\nIy++IF5XcWHF4vis+Pm2Gv2xwhnff/xHfqjY5SgUX9Xfl83ubOrrbWro6tqa9H3FTcdQhlu77jmg\nsSGV6ilqQY0xRWcByExIXr0XBy4EfhvXedrHDaMfdJbpvNjsWE3FhRXnxWbHzot4kTnWTAb/emdG\nQ1P4fVBVDuRyu9/r69vc0NX13oFcNo3r0BzHdbZ/CzeHz/aGVOqExXuNMaXJApCZ8ILFVy8Ffgs4\nEzdy7CBuIdYhRWui0youqvhkfG78vGhNdJGEJDz+pZ14fn5nJhORqbUYbUY13ZrJ7Pggnf7wrZ7u\nD/dls724Gcin4RYmfQcXerY1pFLpYpbVGDMxWQAyk0bQRDYX+BSumWwarmmsExi2SSOUCJVNXzz9\n7Nic2KKyurJF4fJwzbgXeIL46Z39vTGZ3HMqqSpHfL99T3//9k19vR+u7en5KOv+7auB6bj9jcAb\nuA7N1sRljBmWBSAzKQVrj80HLgaW4779gxvOfNJhzGVnlHmJTyYWxWfFF0ZnRBdN5TXJHr6rvyvB\n5Ht9Pb5/pDWT2flhOr1zbW/PrvZsths3bUIlbtSgAh8ArwBbGlKpQdeeM8aYwVgAMpNeUDN0Fq7P\n0FW4YKS4/kKHcf2HhhWfF69NfCKxKDYztjBSFZkzlQLRg3f1H/EIVRa7HMNRVU35/sH92WzL3kxm\nb2Nv764P+9Odwd0xXMCNcjT0/AZoakilOod4SmOMGZYFIDPlePXeDOA83ESL5wU3K249si6GGVGW\nV3ZGmVe+oHx22cyyOdGa6OzI9MhZEpZJOZz8/u+lO2t0YjX59fh+8mA229KWzbTsSPe3bOrrbU36\nfn9wdwioAvIhtAtYi2vi2mHNW8aYsWAByExpwWiy+bj5hZYC83ABKD+qbGQXU0HKF5TXxefGZ5fV\nlc2OVEZmhhPhOolM/FD0kx+kD5yRK970ABnVdGc229qWze5t7u9v2dzX29KazQ4czSe4sFMZ7Cuw\nFdeReTvQYqO3jDFjzQKQKSlevVcBLMQNrV+KmyNGgy0VbCO+2JadUebFZsXqorXRumhVtC48PVwX\nToTrQtFQfByKf0pW/jDdPisbHtfJIn1Vv8f3Dyd9v+NQLtdxMJvtaMtmOnb393fuyWSOHPdXJo7r\nuFyOe98F2AOsB7YBuxtSqX6MMWYcWQCaYEQkBzTh+jtkgUeBu1V1wn8DFpElwCxV/Y9il2WkvHqv\nGlcrtBDXh2gBrglGcDMGJ3G1RKP6jxKdEa2InRWrjVRHqiIVkcrwtLAXLg9XhspDlaFYqFLChRuW\n/sO/T7fN7w+fdbrPk1PNpVW7Urlc52E/19mRzXXsy2Y69vRnOnZl+g9lBv+MRnAdlqcFvwuuKXIb\n8D7wEdDakEoNO6WBMcaMtUixC2BO0KuqSwBE5Azg57gLyHeKWqqRWQIsA0YcgEQkoqpFW4Mp2Zg8\nhGsK2wg8EyzLMRM3I/U5uJqiebhaIcHNQdSNC0VD1lJkOjJdmY7MkJM2RrxIebQuWhmtinrhivD0\nUDxUHoqFykNlofJQWSguUSmXqJSHoqFyiUj56QSmTHjw8Oyr+v2qvWnV7j7f7+5V7e7x/e5u3+/u\n8nM9yZzffTiX6+7IZbsPZnPdh/3ccPPpCK5mJxFsIVxo7Mc1Y23B1fK0AMmGVMq+eRljispqgCYY\nEelS1YoBvy8C1uFmto0B9+FCRhb4a1VtEJEw8H3gd3AX6n9W1R+LSDOwTFUPisgy4Eeqep2I/B9c\njcci3MX9f+AWJb0Bd4H6PVXNiMhS4B9w/TMOAreqapuIvAK8jVvRvQr40+D37bhmjRbgLmAX8I+4\nC2Mv8BVV3SYitwJfCJ43DOwGnlLVZ4LX/BjwC1X91Zi9safBq/fKgVm45rLZuPduPq5Ww8dd7H1c\nKOoF0oyiGW0kJCrhUCwUkYiEJSphCUs4FAmFJSJHt7CECRGasSd7ZUJCG0PCYcmqf/YeP5tIaa5P\n/Uyvr9k+9bM9vp/JjbJWK1CGCzjlwX7+dQpuIdsWXNDZFewftP47xpiJyGqAJjhV3RkEnDOAP3Y3\n6UUich6wSkTOBb6Ca7pZoqpZERnJiJ+zcQHmAtxSATep6m0i8jTwuyLyPPBj4A9U9YCI3Ax8F/hv\nweMjqnqZiHwO+I6qrhCRb+MC118AiIgHXB2UaQVwJ3BT8PhLgYtVtVNErsWFsGdEpBI3eutPTv1d\nG1vJxmQvsCPYgI+H3idwoWhgMDoLF5byoUiC/Rxu5up0sGUYRQDRjOZymVxuJMfOaNfF0W4ORH3a\nAfaO7BQhXLNrFBds8j/zr0NxYTXJ0ZCzFxd6OoBDDanUkIvXGmPMRGMBaHJZjgslqOpWEdmNG920\nArg/35SkqiOZG+U/g1qeJtyF7YXg9iZcmPokboX2F4NlpMK4xSTzngp+vhMcP5hK4BEROQd3AR3Y\njPNivpyq+qqI/JOI1OEC0i+L2Sw2EsnGpOKawrqBZlwtHQBevRfC1W55uPegEleDdxYuyNYG9+dH\nPOWDkAzYfFxoyoeP438O3D/msb6AKDUcrZ06fss/luPOl8LNm3QY1yzYieuvcxgXcjqtr44xZqqw\nADTBBU1gOWD/KTw8i7vggWuGGigNoKq+iGT0aFuoj/tcCLBFVT89xHPn+4PkGPpzdAfQoKo3isgC\n3Iy9ed3HHfsorobrFlyN1qSVbEz6uJqSJENUwAQ1SGW4pqTjtzguIE3Hvbf5mpnIED/B/TvkgFxf\nGQ0IrSgpjtY49eOa53o5GtwGbunJ3i9HRGYCK3FLpRwG2oFvquoHBTh3M0Fz83DHqOqCYP8VXCBO\n4z4HLwH/S1UPj3dZjTGOBaAJLKgRuR/4iaqqiLwOfAlYHTR9zcONpnkR+DMRacg3gQW1K824od7/\nydGmp5HaBtSJyKdV9S1xi2meq6pbhnlMCnfRzqvENZcA3HqS8z2Mm+xun6q+N8qyTjpBDVI+nNhF\n7zSJq6Z8GnhEVW8JbrsEt3juuAegU/QlVV0vImW4PnO/wq1x97HgdclkGAVqzGQTOvkhpsDKReRd\nEdmC+1a4Crg9uO+fgFDQbPUErlNyGngQ1ydjk4hsBL4YHH878I8ish5XOzBiqtoP/Bfg+8Fzvovr\nmzOcBuCCoPw3Az8A7hKRRk4StlW1HTcs+qHRlNOYwPVARlXvz9+gqhuBN0TkhyKyWUSags8lInKd\niLwqIr8SkZ0i8j0R+ZKIrA2OOzs4rk5Efiki64LtquD2GSKySkS2iMiDuBpTROTvROSb+TKIyHdF\n5K+GK3jwf+02YJ6IXCIiC0Rkm4g8CmwG5orIfSKyPjhf/u8BItIsIncF/+fWi8ilIvJrEdkhIl8L\njqkQkZdFZEPw2v5gTN5xYyY7VbXNtqJvuA7FO4DKYpfFtsm3AX+Jmy/r+NtvwtWQhnG1QXtwTU/X\n4WrezsKNrmwBbg8e81fAymD/58DyYH8e8H6wfw/w7WD/d3H9qmpx/eE2BLeHgs/0jOD35gHlegXX\nZDawrM8ANwfP4QNXDLivJvgZDh57cf45gT8P9u8GNuFqYeuA9uD2COAF+7W40ZpS7H8z22wr9mZN\nYKboghFi/w93ATtS7PKYKWU58Liq5oB2EXkV10coCaxT1TYAEdmBq20FNxDg+mB/Ba5WM/98nohU\nANfgpnJAVZ8XkUPBfrOIdIhIPS5wNapqxwjLKgP2d6vqbwb8/l9F5Ku4MHMWbvTmpuC+ZweUu0JV\nU0BKRNIiUoXr43WniFyDC1azg7LtG2G5jJmSLACZolPVl3Dz6hhzqrbgmmxHY+DEjv6A3/MDAcDV\n4lyhqseMfhsQiAbzIK7P20zgX0ZSkGCqi4twzcAwYJCAiCwE/gb4lKoeEpGHOXZQw8ByH/+aIrh+\ng3XAUnUjP5s5cVCEMSXH+gAZY6aC1UAsqCUBQEQuxjVz3Swi4WBQwTW4zvYjtQr4xoDnXBLsvkbQ\n105EbgCqBzzmadykpJ8Cfn2yEwQDDO4CPlLVTYMc4uEC0RERORM3YeloVAL7g/BzPfZlwxjAaoCM\nMVOAqqqI3AisFJH/iZt0shn4Jm5KgY24fjq3qeq+YCLRkfhL4F4R2YT7e/ka8DXcAIPHg8EKa3B9\ni/Jl6ReRBuBw0PQ2lMdEJI3rg/QSMGjnZFXdGAwk2IpbO+3NEZb94/MA/x4MnokH2X0AAAFtSURB\nVFgfPI8xJc+WwjDGmDEkIiFgA/BHqvrhgNubNZgHyBhTfNYEZowxY0RELsCNsnp5YPgxxkw81gRm\njDFjRN0knouGuHtlIctijBmeNYEZY4wxpuRYE5gxxhhjSo4FIGOMMcaUHAtAxhhjjCk5FoCMMcYY\nU3IsABljjDGm5FgAMsYYY0zJsQBkjDHGmJJjAcgYY4wxJccCkDHGGGNKjgUgY4wxxpQcC0DGGGOM\nKTkWgIwxxhhTciwAGWOMMabkWAAyxhhjTMmxAGSMMcaYkmMByBhjjDElxwKQMcYYY0qOBSBjjDHG\nlBwLQMYYY4wpORaAjDHGGFNyLAAZY4wxpuRYADLGGGNMybEAZIwxxpiSYwHIGGOMMSXHApAxxhhj\nSo4FIGOMMcaUHAtAxhhjjCk5FoCMMcYYU3IsABljjDGm5FgAMsYYY0zJsQBkjDHGmJJjAcgYY4wx\nJccCkDHGGGNKjgUgY4wxxpSc/w+0mhKWwcn3JgAAAABJRU5ErkJggg==\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x201000be828>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "# plot the most frequent genres\n",
    "gen_count[:10].plot(\n",
    "                    kind = 'pie', figsize=(8,7) , shadow = True,\n",
    "                    explode =(0.1,0,0,0,0,0,0,0,0,0), \n",
    "                    autopct = '%1.1f%%' , startangle = 45\n",
    "                   )"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "       Fig : Ploting the most frequent genres , here which is Drama   "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### We can also find is movie ratings are related of its concern launch year"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x201004bf860>"
      ]
     },
     "execution_count": 22,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\nJCT/H9xtHx9/m1sfAAAAAElFTkSuQmCC\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x201006b5048>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "# takings our whole data set\n",
    "join_datasets[-20:].plot(x='year', y='rating', figsize=(10,5), grid=True , color = 'r')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {
    "collapsed": false
   },
   "outputs": [],
   "source": [
    "# taking average of the year\n",
    "average_year = join_datasets[['year','rating']].groupby('year', as_index=False).mean()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {
    "collapsed": false
   },
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<matplotlib.axes._subplots.AxesSubplot at 0x2010060aef0>"
      ]
     },
     "execution_count": 24,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAlYAAAFACAYAAAB+wjIEAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz\nAAALEgAACxIB0t1+/AAAIABJREFUeJzt3Xl8VPW9//HXNwsEkpBhCZBAWJJBoFABQdlqZSlKFTfc\nl16trdZW29r78Npa7/V2edjaX9vfVX9a11rt5lIvLojSIjXuoICKIlgmC5CwBZLJvuf7+2NmQoBA\nJuTMnJnk/Xw88mAyc+ac73w5hHe+3+/5HGOtRURERER6LsHtBoiIiIj0FgpWIiIiIg5RsBIRERFx\niIKViIiIiEMUrEREREQcomAlIiIi4hAFKxERERGHKFiJiIiIOETBSkRERMQhSW4d2OPxWK/X69bh\n40ZtbS2pqaluNyOmqY+6pj4Kj/qpa+qj8KifuhZvfbRx48YD1trMrrZzLViNGDGCDRs2uHX4uJGf\nn8+CBQvcbkZMUx91TX0UHvVT19RH4VE/dS3e+sgYsyOc7TQVKCIiIuIQBSsRERERhyhYiYiIiDjE\ntTVWIiIiEluam5spKSmhoaEh4sfKyMhg69atET9Od6WkpDB69GiSk5NP6P0KViIiIgJASUkJ6enp\njBs3DmNMRI9VXV1Nenp6RI/RXdZaDh48SElJCePHjz+hfWgqUERERABoaGhg6NChEQ9VscoYw9Ch\nQ3s0YqdgJSIiIu36aqgK6ennDytYGWOKjTGfGGM+MsYcVXzKBNxnjPEZYzYbY07pUatERERE4lB3\nRqwWWmunW2tndfLaV4EJwa8bgAedaJyIiIhIZ+655x7q6uravz/77LPx+/0utijAqanA84E/2oB1\ngMcYk+XQvkVEeqWKigbee2+3280QiVnWWtra2jp97chg9corr+DxeKLVtGMK96pAC7xmjGkFHrbW\nPnLE66OAXR2+Lwk+t6fjRsaYGwiMaJGZmUl+fv6JtLlPqampUT91QX3UNfVReKLdT48/XspTT+1l\n5crppKQkRu24PaFzKTzx2k8ZGRlUV1dH5Vitra2dHmvHjh1ceOGFzJo1i48++oiZM2fy2WefUV9f\nz/nnn88dd9zBgw8+yO7duznjjDMYOnQoq1atYurUqbzxxhvU1NRw0UUXMXfuXNavX09WVhZPP/00\nAwYMYOPGjdx8880kJCSwcOFC1qxZw/r1649qQ0NDwwn//YUbrL5krS01xgwH1hhjtllr3+zuwYKB\n7BGAiRMn2ni6R5Bb4u1eSm5QH3VNfRSeaPfT7373Ei0te8jJmcaUKcOidtye0LkUnnjtp61bt7aX\nQLjlln/y0Uf7Hd3/9OnDueeeRcCxyy2kpaVRUFDAn/70J+bMmUN5eTlDhgyhtbWVxYsXU1RUxG23\n3cbvfvc73njjDYYNC/zbMcaQlpYGQEFBAc888wzTp0/n0ksv5R//+AdXX301N998M48++ihz587l\nRz/6EQkJCZ22ISUlhRkzZpzQZwxrKtBaWxr8cz/wPHDaEZuUAjkdvh8dfE5ERI7B5/Mf9qeIBIwd\nO5Y5c+YA8Oyzz3LKKacwY8YMtmzZwmeffdbl+8ePH8/06dMBmDlzJsXFxfj9fqqrq5k7dy4AV155\nZUTa3uWIlTEmFUiw1lYHH58J/OyIzV4CbjbGPA3MBiqttXsQEZFOWWvbA1VBgYKVxJ7QyJIbUlNT\nASgqKuI3v/kNH3zwAYMHD+baa68Nq8ZU//792x8nJiZSX18fsbYeKZwRqxHA28aYj4H3gVXW2tXG\nmBuNMTcGt3kFKAR8wKPAdyLSWhGRXqKsrI7q6iYAfL4Kl1sjEpuqqqpITU0lIyODffv28eqrr7a/\nlp6e3q31YB6Ph/T09PY1VU8//bTj7YUwRqystYXAtE6ef6jDYwvc5GzTRER6r47Tf5oKFOnctGnT\nmDFjBpMmTSInJ4f58+e3v3bDDTewdOlSsrOzef3118Pa3+9//3uuv/56EhISOOOMM8jIyHC8zbpX\noIiIC0JhaubMEZoKFOlg3LhxfPrpp+3fP/HEE51u993vfpfvfve77d8XFxcDMGzYsMPef+utt7Y/\nnjJlCps3bwbg7rvvZtaszkpz9oxuaSMi4gKfr4LERMPixWMoLq6iqanV7SaJ9HqrVq1i+vTpTJ06\nlbfeeov//M//dPwYGrESEXGBz+dnzJhBTJ48lLY2y44dVUyYMNjtZon0apdddhmXXXZZRI+hESsR\nERf4fH68Xg9eb6BStKYDJVYElk33XT39/ApWIiIuOBSsBge/15WB4r6UlBQOHjzYZ8OVtZaDBw+S\nkpJywvvQVKCISJSVl9dTUdGA1zuYESMGkpqaTEFBpdvNEmH06NGUlJRQVlYW8WM1NDT0KMBESkpK\nCqNHjz7h9ytYiYhEWeiKQK/XgzGGvDyPRqwkJiQnJzN+/PioHCs/P/+EbxsTyzQVKCISZR2DVehP\n1bIS6R0UrEREosznq8AYyM0NBKu8PA+FhZW0tra53DIR6SkFKxGRKPP5/IwenU5KSmA1htfroamp\nldLSGpdbJiI9pWAlIhJloSsCQ/LyVHJBpLdQsBIRibKCAn97mQU4tNZK66xE4p+ClYhIFFVVNbJ/\nf91hI1ajR6fTr1+irgwU6QUUrEREoig03dcxWCUmJjB+fIamAkV6AQUrEZEoOlRq4fD7Aqrkgkjv\noGAlIhJFofCUl5dx2POBIqH+PnsrEZHeQsFKRCSKfL4KsrJSSU3td9jzXq+H2tpm9u+vc6llIuIE\nBSsRkSgKlFoYfNTzujJQpHdQsBIRiSKfz3/UNCColpVIb6FgJSISJbW1TezeXdPpiNW4cRkkJBiV\nXBCJcwpWIiJRUlhYCRxeaiGkX79Exo4dpKlAkTinYCUiEiWHSi0cHawgMB2oqUCR+KZgJSISJaFp\nvtB6qiOplpVI/FOwEhGJEp/Pz7BhA/B4Ujp9PS/PQ3l5AxUVDVFumYg4RcFKRCRKAqUWOh+tgkNT\nhJoOFIlfClYiIlHi81V0ekVgiGpZicQ/BSsRkShobGxh167q445Y5eZqxEok3ilYiYhEQVFRJdYe\n+4pAgIEDk8nOTlMtK5E4pmAlIhIFh0otHHsqMPC6rgwUiWcKViIiUdBVDasQ1bISiW8KViIiUeDz\nVeDx9GfIkM5LLYR4vR727KmltrYpSi0TEScpWImIREGo1IIx5rjbhYqHhm5/IyLxRcFKRCQKAsHq\n+OurQCUXROKdgpWISIQ1N7dSXFx5zFvZdBTaRlcGisQnBSsRkQjbsaOK1lbb5cJ1AI8nhaFDB1BQ\noKlAkXikYCUiEmHhXhEYEii5oBErkXikYCUiEmGhkBTOGitQyQWReKZgJSISYT6fn9TUZEaMGBjW\n9l6vh507q2lsbIlwy0TEaQpWIiIRFm6phRCv10Nbm6W4uCrCLRMRpylYiYhEWChYhSt0ZaCmA0Xi\nj4KViEgEtba2UVgYXg2rENWyEolfClYiIhG0a1c1zc1t3RqxyswcSHp6P10ZKBKHFKxERCIoNJ3X\nnWBljNGVgSJxSsFKRCSCDtWwCn8qMLC9R1OBInFIwUpEJIJ8vgpSUpLIzk7r1vvy8jwUFVXS2toW\noZaJSCQoWImIRJDP5ycvL4OEhPBKLYR4vR6am9vYtas6Qi0TkUhQsBIRiaBAqYXuTQOCrgwUiVcK\nViIiEdLWZiko6F4NqxDVshKJT2EHK2NMojHmQ2PMy528tsAYU2mM+Sj4daezzRQRiT979tRQX99y\nQsFq1Kh0+vdPVMkFkTiT1I1tvw9sBQYd4/W3rLXLet4kEZHeITSNFxp96o6EhEDJBU0FisSXsEas\njDGjgXOAxyLbHBGR3uNQqYXuBytAtaxE4lC4I1b3ALcB6cfZZp4xZjNQCtxqrd1y5AbGmBuAGwAy\nMzPJz8/vXmv7oJqaGvVTF9RHXVMfhcfpfvrnP0tISjIUFn7Ijh3duyoQoH//GrZvL+f1118P+wbO\nkaZzKTzqp6711j7qMlgZY5YB+621G40xC46x2SZgjLW2xhhzNvACMOHIjay1jwCPAEycONEuWHCs\n3UlIfn4+6qfjUx91TX0UHqf76YEHXiI3t5HFixee0Pu3bPmQ555by6RJp5KV1b06WJGicyk86qeu\n9dY+CmcqcD5wnjGmGHgaWGSM+XPHDay1VdbamuDjV4BkY8wwpxsrIhJPAqUWTmwaEFRyQSQedRms\nrLW3W2tHW2vHAZcD/7TWXt1xG2PMSBMcpzbGnBbc78EItFdEJC5Ya/H5Kk6ohlVI6L26MlAkfnTn\nqsDDGGNuBLDWPgRcDHzbGNMC1AOXW2utM00UEYk/+/fXUVPT3KMRqzFj0klMNBQUVDrYMhGJpG4F\nK2ttPpAffPxQh+fvB+53smEiIvGsp1cEAiQnJzJuXIZGrETiiCqvi4hEQCgM9WQqEFRyQSTeKFiJ\niERAQYGfxETD2LHHqqkcHq/Xw/btfrS6QiQ+KFiJiESAz+dn7NhB9OuX2KP9eL0eKisbKS9vcKhl\nIhJJClYiIhEQKLXQs2lA0M2YReKNgpWISAT0tIZViGpZicQXBSsREYeVl9dTUdHgSLDKzfVgjGpZ\nicQLBSsREYcdKrXQ86nAlJQkRo1K11SgSJxQsBIRcZgTNaw68no9mgoUiRMKViIiDvP5KjAGxo/P\ncGR/qmUlEj8UrEREHObz+Rk9Op2UlBO+a9hhvF4P+/bVUV3d5Mj+RCRyFKxERBzm1BWBIaF9adRK\nJPYpWImIOMznq3Bk4XqIalmJxA8FKxERB1VWNlJWVu/oiFUoWKnkgkjsU7ASEXFQaFTJyWA1aFB/\nhg8fSEFBpWP7FJHIULASEXFQaFTJyalACIxaacRKJPYpWImIOChUbyovz5lSCyGqZSUSHxSsREQc\n5PP5ycpKJTW1n6P7zcvzUFJSTUNDi6P7FRFnKViJiDiooMDv+DQgBEasrIWiIq2zEollClYiIg5y\nuoZVSCisaTpQJLYpWImIOKS2tondu2siEqxCa7ZUy0oktilYiYg4pLAwME0XiWA1dOgAMjL668pA\nkRinYCUi4pDQNF0k1lgZY3QzZpE4oGAlIuKQ0GhSqFK601RyQST2KViJiDjE5/OTmRmYsosEr9dD\ncXEVLS1tEdm/iPScgpWIiEN8Pn/ERqsgMBLW0tLGzp1VETuGiPSMgpWIiEN8voqIrK8KCS2K13Sg\nSOxSsBIRcUBDQwu7dlVH5IrAkFBo0wJ2kdilYCUi4oCiokqsjUyphZCsrFQGDEhSyQWRGKZgJSLi\ngEiWWggJlVzQVKBI7FKwEhFxQGgUKZIjVoBqWYnEOAUrEREH+Hx+PJ7+DBmSEtHjeL0eCgoqaWuz\nET2OiJwYBSsREQeEbr5sjInocbxeDw0NLezeXRPR44jIiVGwEhFxQKRLLYSE6mRpOlAkNilYiYj0\nUHNzKzt2VEV8fRWolpVIrFOwEhHpoR07qmhttVEJVjk5g0hOTtCIlUiMUrASEemhaJRaCElKSmDc\nuAzVshKJUQpWIiI9FK1SCyFer2pZicQqBSsRkR7y+fykpSUzfPjAqBwvVMvKWpVcEIk1ClYiIj0U\nKLUwOOKlFkK8Xg9VVU0cOFAfleOJSPgUrEREeihUwypaQsfSAnaR2KNgJSLSA62tbRQW+tvrS0VD\n6FhaZyUSexSsRER6YNeuapqb26I6YjV+fAbGoCsDRWKQgpWISA8cKrUQvWDVv38SOTnpFBRURu2Y\nIhIeBSsRkR44VGoh8jWsOvJ6B2vESiQGKViJiPSAz+cnJSWJ7Oy0qB5XtaxEYpOClYhID/h8fvLy\nMkhIiE6phZC8PA8HDtRTWdkY1eOKyPEpWImI9IDPVxH1aUBQyQWRWBV2sDLGJBpjPjTGvNzJa8YY\nc58xxmeM2WyMOcXZZoqIxJ62NktBQWVUF66HhMKcgpVIbOnOiNX3ga3HeO2rwITg1w3Agz1sl4hI\nzNu9u4aGhhZXglVubgagWlYisSasYGWMGQ2cAzx2jE3OB/5oA9YBHmNMlkNtFBGJSaHRIjemAtPS\n+jFyZKquDBSJMUlhbncPcBuQfozXRwG7OnxfEnxuT8eNjDE3EBjRIjMzk/z8/O60tU+qqalRP3VB\nfdQ19VF4uttPq1aVAXDgwDby84si1KpjGzbMsHFjcVT/bnUuhUf91LXe2kddBitjzDJgv7V2ozFm\nQU8OZq19BHgEYOLEiXbBgh7trk/Iz89H/XR86qOuqY/C091++vvf3yQ5eReXXLKExMToXws0c2Y9\nr722I6p/tzqXwqN+6lpv7aNwfhLMB84zxhQDTwOLjDF/PmKbUiCnw/ejg8+JiPRaPp+f3FyPK6EK\nAlcGlpbWUF/f7MrxReRoXf40sNbebq0dba0dB1wO/NNae/URm70E/Fvw6sA5QKW1ds+R+xIR6U18\nPr8rC9dDQjdjLizUrW1EYsUJ/5pljLnRGHNj8NtXgELABzwKfMeBtomIxCxrbbCGlXvBKnRsXRko\nEjvCXbwOgLU2H8gPPn6ow/MWuMnJhomIxLL9++uoqWluHzVyg2pZicQeVV4XETkBoVEiN0esBg9O\nYfDgFJVcEIkhClYiIicgFGbcqGHVkW7GLBJbFKxERE6Az+cnMdEwduwgV9uRl+fRVKBIDFGwEhE5\nAT6fn7FjB9GvX6Kr7fB6PezYUUVzc6ur7RCRAAUrEZETELgi0N1pQAgEq9ZWy44dVW43RURQsBIR\n6TZrLdu3u1vDKiR0VaLWWYnEBgUrEZFuKi9voLKyMSaCVWjUTFcGisQGBSsRkW46VGrB/anAESMG\nkpqaTEGBqq+LxAIFKxGRbjpUasH9EStjDHl5Ho1YicQIBSsRkW4qKPBjDIwfn+F2UwDVshKJJQpW\nIiLd5PP5yclJJyWlW3cFi5i8PA+FhZW0tra53RSRPk/BSkSkm3w+f0ysrwrxej00NbVSWlrjdlNE\n+jwFKxGRbgrUsHJ/fVWIbsYsEjsUrEREuqGyspGysvqYClZ5eYG1XlpnJeI+BSsRkW4IjQrF0lTg\n6NHp9OuXqCsDRWKAgpWISDeEwkuo4nksSExMYPz4DE0FisQABSsRkW4ITbeFpt9ihUouiMQGBSsR\nkW7w+fxkZaWSmtrP7aYcxuv1UFDgx1rrdlNE+jQFKxGRboi1UgsheXkeamqa2b+/zu2miPRpClYi\nIt0Qa6UWQkJt0nSgiLsUrEREwlRb28SePbUxGaxCi+m1gF3EXQpWIiJhKiioBGLj5stHGjcug4QE\no5ILIi5TsBIRCVMotMTiGqt+/RIZO3aQpgJFXKZgJSISpkOlFmJvxAoC7dJUoIi7FKxERMLk8/nJ\nzBxARkZ/t5vSKdWyEnGfgpWISJgKCmKz1EKI1+uhvLyBiooGt5si0mcpWImIhClWSy2E6MpAEfcp\nWImIhKGhoYVdu6pjOliplpWI+xSsRETCUFRUibWxeUVgSG6uRqxE3KZgJSIShtAoUCyPWA0cmEx2\ndppqWYm4SMFKRCQMh2pYxW6wgtDNmCvdboZIn6VgJSISBp/Pj8fTnyFDBrjdlOPKy/NoxErERQpW\nIiJh8Pn8MT9aBYERqz17aqmtbXK7KSJ9koKViEgYAqUWYnfhekgo/BUWajpQxA0KViIiXWhqaqW4\nuCouRqxCtaxUckHEHQpWIiJd2LGjirY2G2fBSuusRNygYCUi0oVDVwTG/lSgx5PC0KEDdGWgiEsU\nrEREuhAPNaw6CtyMWSNWIm5QsBIR6YLP5yctLZnhwwe63ZSwBGpZaY2ViBsUrEREuhC6ItAY43ZT\nwpKX52HnzmoaG1vcbopIn6NgJSLShXipYRXi9Xpoa7MUF1e53RSRPkfBSkTkOFpb2ygqqoyrYBW6\nMlDTgSLRp2AlInIcu3ZV09zcFhdXBIaEQqBqWYlEn4KViMhxxNsVgQCZmQNJT++nESsRFyhYiYgc\nx6EaVvETrIwxuhmziEsUrEREjsPn8zNgQBJZWWluN6VbArWsNGIlEm0KViIix+Hz+cnL85CQEB+l\nFkK8Xg9FRZW0tra53RSRPkXBSkTkOHy+ivar7OJJXp6H5uY2du2qdrspIn1Kl8HKGJNijHnfGPOx\nMWaLMeannWyzwBhTaYz5KPh1Z2SaKyISPW1tloKC+Cq1EKIrA0XcEc6IVSOwyFo7DZgOLDXGzOlk\nu7estdODXz9ztJUiIi7YvbuGhoaWuAxWqmUl4o6krjaw1lqgJvhtcvDLRrJRIiKx4NAVgfFTwypk\n1Kh0+vdP1JWBIlHWZbACMMYkAhsBL/CAtXZ9J5vNM8ZsBkqBW621WzrZzw3ADQCZmZnk5+efaLv7\njJqaGvVTF9RHXVMfhefIflq1qgyAAwe2kZ9f5FKrTtzIkcmsX+/Dyb96nUvhUT91rbf2UVjBylrb\nCkw3xniA540xU621n3bYZBMwxlpbY4w5G3gBmNDJfh4BHgGYOHGiXbBgQU/b3+vl5+ejfjo+9VHX\n1EfhObKfVq9+k+TkXVxyyRISE+PvWp+TT66guLjS0b97nUvhUT91rbf2Ubd+Ulhr/cDrwNIjnq+y\n1tYEH78CJBtjhjnWShERF/h8FeTmeuIyVEFgAXtBgZ/Aig4RiYZwrgrMDI5UYYwZACwBth2xzUhj\njAk+Pi2434PON1dEJHp8Pn9cLlwP8Xo91NW1sHdvrdtNEekzwvk1LAt4Pbh+6gNgjbX2ZWPMjcaY\nG4PbXAx8aoz5GLgPuNzqVyQRiWPW2rgPVqErA1VyQSR6wrkqcDMwo5PnH+rw+H7gfmebJiLinn37\n6qitbY7rYBW6mrGgwM/pp492uTUifUN8LhwQEYmwUP2neCy1EDJmTDqJiUYjViJRpGAlIsdkre2z\n95o7VMMqfkeskpMTGTcuQ7WsRKJIwUpEOtXa2sZll61kwoTfU1jY90Y8fD4/iYmGsWMHud2UHgld\nGSgi0aFgJSJHsdby3e+u5W9/+xf79tWycOEzFBdXut2sqPL5/Iwbl0FycqLbTemRvDwP27er5IJI\ntChYichRfvnL9Tz44MfcdtupvP32FVRVNbFw4TPs3FnldtOixueriOtpwBCv10NlZSPl5Q1uN0Wk\nT1CwEpHDPPHEp9xxx9tcddVkfvnLLzNjxgjWrLmEiopGFi58hpKSarebGHHWWrZvj+9SCyG6GbNI\ndClYiUi71auL+OY3/87ixWN4/PGlJCQYAGbNGsnf/34xZWX1LFz4DLt313Sxp/hWXt5AZWVjeyiJ\nZ6FwqCsDRaJDwUpEANi4cS8XX/wSU6cOY8WK8+nX7/C1RbNnZ7F69UXs3RtYc9Wbq3mHQkg8l1oI\nyc31YIxGrESiRcFKRCgs9HP22SsYNmwAr7xyEYMG9e90u3nzRvHqqxdRWlrDokXPsH9/7wxXvaHU\nQkhKShKjRqWr5IJIlChYifRxZWV1nHXWc7S0tLF69UVkZ6cdd/svfWk0q1Ytp7i4isWL/0ZZWV2U\nWho9Pp8fY2D8+Ay3m+IIr9ejqUCRKFGwEunDamubWLZsBSUlNaxceSGTJg0N631nnJHDyy8vx+fz\n85Wv/I2DB+sj3NLo8vn85OSkk5LS5V2/4oJqWYlEj4KVSB/V0tLGZZe9zIYN+3jqqXOYN29Ut96/\naNEYXnrpAj7/vJyvfOVvlJf3nnAVKLUQ/+urQvLyPOzbV0d1dZPbTRHp9RSsRPogay3f/vYaVq0q\n5IEHFnPBBRNOaD9LlozjhRcu4LPPDnLmmc/h9/eOWkk+X+8otRAS+iwatRKJPAUrkT7oZz97j8ce\n+4Q77pjDjTdO79G+li4dz4oV57F5cxlnnfUclZWNDrXSHX5/AwcO1PeqYKVaViLRo2Al0sc89thm\nfvKTd7nmmin8/OfzHdnnOefk8dxz57Fp036WLn2Oqqr4DVeh8NHbpgIBXRkoEgUKViJ9yMsvF3Dj\njWs466xxPPromRhjHNv3eed5eeaZZXzwwV7OPnsFNTXxuZ7nUA2r3jNiNWhQf4YPH0hBQd+636OI\nGxSsRPqI9ev3cOmlK5k+fTjPPXdeRG4uvHz5STz11DLWrdvNOeesoLY2/sJVaMQqN7d3lFoIycvz\naMRKJAoUrET6gJKSBpYtW0FWViqrVi0nLa1fxI51ySUT+dOfzubtt0s599znqatrjtixIsHn85Od\nnUZqauT6yA2qZSUSHQpWIr3cvn213HbbvwBYvfpiRoxIjfgxr7hiMk8++VXy83dx/vkvUF8fP+Gq\nt10RGOL1eigpqaahocXtpoj0agpWIr1YdXUTZ5+9goqKFlatWs6ECdFbkH311V/gD39Yytq1O1i+\n/MW4+Q89UMOq9wWrvDwP1kJRkdZZiUSSgpVIL9Xc3Moll7zExx/v5847cznttKyot+Gaa6by6KNn\nsXp1MRdf/BKNjbEdrurrW9mzp7ZXXREYEvpMKrkgElkKViK9kLWW66//B3//ezEPPbSEuXPdG4H5\nxje+yMMPL2HVqkIuvXQlTU2trrWlK7t3B8pE5OX1roXrcOgzaZ2VSGQpWIn0Qv/1X+/w5JNb+MlP\n5vHNb57sdnO44YZpPPDAYl56qYDLL3+Z5ubYDFelpYFg1RtHrIYOHUBGRn9dGSgSYQpWIr3Mgw9+\nxF13reP660/mzjvnut2cdt/5zgzuvXcRzz+/nSuvXEVLS5vbTTpKaWngljyhgpq9iTFGN2MWiYLe\ncet2EQHghRe2c/PNa1m2LJff/e4rjhYAdcL3vncKra1t/Pu/55OU9Ap/+tPZJCXFzu93paWNZGYG\nRnZ6o7w8D5s27XO7GSK9moKVSC/x7rulXHHFKk49dSRPP70spgJLRz/4wSyam9v44Q/fJCkpgSee\nWEpiYmy0dffuxl45DRji9XpYsWI7LS1tMXt+iMQ7BSuRXmDbtoOce+7z5OSks3LlhTFf3PK2206j\npaWNO+54m8REw+OPLyUhwf3RtdLSRs46K8ftZkRMXp6HlpY2du6sIje39013isQCBSuROLd7dw1L\nl/4vSUkJrF59EZmZA91uUlh+/OM5tLS08d///S5JSQk88siZroar+vpm9u9v6pU1rEJCn83n8ytY\niUSIgpXT+YFYAAAaH0lEQVRIHKuqauTss/+XAwfqeeONy+LuP8s775xHS0sbP//5OhITDQ8+uMS1\ncBUqnNm7pwJVy0ok0hSsROJUU1Mry5e/yJYtB1m58kJmzhzpdpNOyE9/Op+WFssvf7mepKQE7r9/\nsSuL7kP1nXrziFVWVioDBiSp5IJIBClYyQlpaWmjoMDPp58eYMuWA2zZcpB//auCk04azOLFY1i8\neCy5uRkxd1Vab9HWZrnuutWsXbuTJ55YytKl491u0gkzxnDXXV+ipaWNX//6A5KSErjnnoVRP3f6\nQrAyxpCXp5sxi0SSgpUcV1ubpaiosj08hYLUtm3lNDYGijwaA7m5HrxeD2+/Xcqzz34OwNixg9pD\n1qJFYxg5MvI3/42U6uom1q/fw7vvlvLOO7vZtu0gWVlpjB+fwfjxGeTmZrQ/zslJJzk5MaLtuf32\nN/nLX7byi1+czjXXTI3osaLBGMOvfvVlWlra+J//2QjA178+lQEDkhgwIImBA5OCj5MjNlXo81WQ\nnp7IkCEDIrL/WOH1eti+PXIjVg0NLezaVc2OHVXs3Bn6qmbnzirS0voxd24Wc+dmM2vWSAYOTI5Y\nO0TcomAlQOAWKLt2VbNly4FgeAqEqK1bD1JXd+j+bmPGpDN16jDOPHMcU6cOY8qUoUyePLT9B6S1\nls8/L2ft2p2sXbuTFSu28/jjnwIwZcpQFi8ey+LFYzjjjJyYrhW0c2cV7767m3feKeWdd0r5+OMy\n2tosxsDUqcP40pdGs3dvLevX7+Fvf/uc1lbb/t7ERMPo0elHBa7Q18iRqT0ajbnvvk38n//zAd/5\nznR+9KPTnPi4McEYw29/u4CWljbuu28T9923qdPt+vVL7CRwBULXocdHvnbo9WM9//HHZYwaFbvn\npFPy8jysXl1MW5vtdki11uL3N7Nx495gcKpuD0+h7/fvrzvsPcZAdnYaOTnplJTU8OKLPgCSkhKY\nPj2TefNGMXduNvPmZZOTk65Rbol7ClZ9jLWWvXtrDwtPodGo6uqm9u2ys9OYMmUo3/rWNKZMCQSo\nL3xhKIMGHf8/HmMMkyYNZdKkodx00wxaW9v48MP9rF27g7Vrd/Loo5u5775NJCQYTj11ZPuI1rx5\n2aSkuHM6trS0sXlzWXuIeued3ZSUVAOQmprM7NlZ3HHHbObPH8Xs2Vl4PClHvb+kpJqiokoKCysp\nKjr09corRezdW3vY9ikpSYwfP+iowBUIYp7jBs7nnvucW275Jxdc4OW++xb1uv+EjDHce+8iLr10\nImVl9dTXt1BX10x9fUunX0e+VlnZyN69tZ2+JxxLlgyN8Cd0n9froaGhhT17ahg1Kv2w1xobWygp\nqel0tCkUnBoaWoCP298zcGASY8YMYuzYQcyYMYIxY9Lbvx8zJp1Ro9Lp1+/QCO7Bg/WsW7ebd98N\nfD322Ob2EJ2dnca8edntQWvGjOH07x/b/001N7dSWFjJtm3lbN16kG3bytm+vYK6umpOOqma4cMH\ndvoVKkTb2/4NCxhrbddbRcDEiRPt559/7sqx40l+fj4LFiw4ofeWldUdNQK1ZctBKioa2rfJzBwQ\nHHkKhKfQ48GDU46z5xPX2NjCe+/tbh/Rev/9PbS2WlJSkpg/P7t9RGvmzBFhF43sbh9VVjaybt3u\n9hC1fv0eamubARg9Op3587OZN28U8+dnM23a8B4XUqyra2bHjioKC/0dQldV++PKysbDth88OCUY\ntA4PX/X1LVx55SpmzhzBa69dwoAB4U+j9OQ86g2stTQ2th4zpNXVNdPQ0Iq1xSxfvsTt5kbUmjXF\nnHnmc3zve6eQnJxwWGg68pcAgJEjUxkzJj0YlAbR2LiPxYtPaf9+yJCUHoWD0C82770XCFrvvbe7\n/QrN/v0TmTlzRHvQmjs3m6ystBM+Vk9UVTWybVv5YV9btx7E5/Mfdnum7Ow0TjppMAcPVtDYmMz+\n/XX4/Y2d7jM5OeGYwauzINadf/PxIN5+LhljNlprZ3W5nYJVbAvnxLPWUlpaw4YNe9mwYR8bNuzl\nww/3HzYk7/H0bw9NU6cObQ9Sw4e7u+6pqqqRN98sCQatHXzyyQEAMjL6s2BBTnBEawyTJw895g/v\n4/WRtZbi4kreeScQpN59dzeffFKGtZCQYJg2LZN587KZP38U8+ePYsyYQZH6qMdUUdFwROg6FL6K\niyvb17IBTJo0hLffvoKhQ7u3DijefoC5pS/00+7dNYwZ83D7LzShEaaO4Sn0fU5O+lEjRtHoo717\na4NBq5T33tvDhg172/8djBs3KDh9mMW8eaM4+eRMx6rIh36WBoLTQbZuPRSidu+uad8uKSkBr9fD\n5MlDmTRpyGFfoVH9jv3U1NTKgQP17N9fd9yvsrI69u2rO+YIa3p6PzIzBxwzfM2Zk8X48fFz8UW8\n/Huz1vLqq0Wcc05eWMEqtsdYpVN79tSwceO+w4LUvn2BEJWYaPjiFzNZtiyXqVOHtYeprKyereuJ\nlEGD+rNsWR7LluUBsH9/Lf/85672qcPQeoysrFQWLRrTPnV4rADU3NzKhx/uP2x91J49gd/C09P7\nMWdOFsuXz2uf1ktPd79C+eDBKcycObLTcgltbZY9e2ooKqqktLSGxYvHdDtUiXSUnZ3Gjh03kJyc\nQGbmwJj8uTByZCoXXjiBCy+cAARGuj/6qCwYtHbzxhu7+OtftwKBqcjTTstqH9WaMyeLYcOOXyS3\nqakVn68iOOpU3h6ktm0rp6amuX27QYP6MXnyUJYsGcukSUPag1Rubka3LlDp1y+R7Ow0srPDG22r\nrW0Khq2jw1hZWeDPHTuq+OCDvezfX9e+xjM9vR/vvXclU6YMC7ttcmytrW2sWLGdX/xiPR99tD/s\n9ylYxbiKimZefbWwPUBt2LCv/TenhATDF74wlK9+dTyzZo1k1qyRnHzysLgeLh4+PJXLL5/E5ZdP\nAqCoyN8+bbhmzQ7+8pfAD1Ov19M+bVhQ4GfNmrd4551S3n9/b/tve2PHDmLhwjHMnx8YkZo6dVjM\n3JMuXAkJhlGj0o9aCyPSE/F2PvXvn8Ts2VnMnp3FD34QeG7Xrqr2qcN3393Nr3/9QfuU3EknDWbu\n3MDU4cSJgykqqjxsCq+gwH/YBSc5OelMmjSEr3996mGjUD290OREpab2Y/z4fmGNPrW1Wfz+BgoL\nKzn33Oc599znWb/+qri5A0Msam5u5amntvHLX65n27ZyTjppMH/4w1K+/vX/COv9mgqMIeXl9cGR\nqFCI2svOnYFF1MbAxIlDggFqBLNmjWT69MyYvyeck6y1bNlygNdeC0wbvvFGSfuC+8REw4wZw9un\n9ObNy467/zwiKV6G3N2mfuparPZRfX0zGzbsO2ytVsflEP36JTJhwtHTdxMnDiEtzfmfo2700wcf\n7OHLX36GWbMC6zBjfeF/rJ1LDQ0tPPHEp/zqV+9TXFzFySdn8uMfz+bii08iMTEh7DVWsd3rDrLW\n0tzcRnJyQkwMffv9DWzatL89QG3cuI/Cwsr2171eD/PmjeKcc2q47LL5zJgxvMsr8no7YwxTp2Yy\ndWomt9wyk5aWNjZs2Mu6dRu4/vqlfSpkisjhBgxI5vTTR3P66aOBwM/8wsJKfL4K8vI8jBuX4dha\nrFh16qlZPPnkUi677GW+9a01/OEPS2Pi/7tYV1vbxMMPb+Y3v/mAPXtqmT07i/vuW8yyZbkn1H8x\nEaxCoaeurpna2mbq6lrCeBz4vuPj472nrq6FtrbA6Fyglk0yAwce+vPI50L1bo5+7vjv66yQYXV1\nEx9+uO+w6byOBfrGj89g1qwRfOtb05g1aySnnDK8/ZL+/Px8zjgjJ/p/KXEgKSmBOXOyaWgYpFAl\nIocJVZnPy4ufxdxOuPTSSWzdWs5PfvIukycP4Yc/nO12k2KW39/AAw98xD33bOTAgXoWLszhT386\nm0WLxvQokLoWrIqK6snKerA9AHWc7w6HMRwWaFJTDz0eNmwAAwemH/V8SkoSTU2HLrnuGLoCfzZz\n4ED9Ec+1BOu2dF9KSiBk+f0NhGZcc3LSmTVrJNdeO4VZs0Yyc+YILUYWERHH3HnnXLZtK+f2299i\n4sQhXHDBBLebFFPKyuq4556N3H//h1RVNXHOObnccccc5s7NdmT/rgWrlJQEzjsvrz0cBQJQ+I9T\nUpKiNsTZ1mZpaDg8hHUezFqor28+6vnMzIGcemogRI0YEb+3dRERkdhnjOHxx8+iqKiSq65axdtv\nX8GMGSPcbpbrSkur+c1vNvDIIx9TX9/CxRefxO23z3a8b1wLVllZ/Xn44TPdOny3JCSYYKCL36vt\nRESk7xgwIJkXXriA0077M+ed9wLvv3+Va8VV3VZY6OdXv3qfJ57YQmtrG1ddNZnbb5/NpEmRudNC\n717JJyIi0keNHJnKypUXUlHRwPnnv0B9fXPXb+pFPvvsAF/72iucdNLveeKJLVx33VS2b/8GTz55\ndsRCFShYiYiI9FrTpg3nr389hw0b9nLttavbL+LqzT78cB8XX/wiU6c+wYoV/+L73z+FoqLrefDB\nJVGpTB8TVwWKiIhIZJx3npdf/erL3Hbbm0yePISf/GS+202KiHfeKeWuu9bx6qtFZGT058c/nsMt\nt5zSZSV+p3UZrIwxKcCbQP/g9s9Za//7iG0McC9wNlAHXGut3eR8c0VERKS7br31VLZuLeenP32P\nSZOGtt/dIt5Za3nttR3cddc63nijhGHDBnDXXV/ipptmkJHhTu3HcEasGoFF1toaY0wy8LYx5lVr\n7boO23wVmBD8mg08GPxTREREXGaM4aGHllBQ4Ofaa19l/PgMZs/OcrtZJ6ytzfLyywXcddc63n9/\nL9nZafzP/yzk+uu/6Hpdwy7XWNmA0G29k4NfR07Sng/8MbjtOsBjjInfvzEREZFepl+/RP73f89j\n1Kg0zj//eXburHK7SSdkxYp/MX36k5x//guUldXz8MNLKCz8JrfcMtP1UAVh3ivQGJMIbAS8wAPW\n2h8e8frLwN3W2reD368Ffmit3XDEdjcANwBkZmbOfPbZZx35EL1ZTU0NaWl98xLZcKmPuqY+Co/6\nqWvqo/DEcj/t2FHPTTdtY+TIfvy//zeJAQMSXWlHd/uotraVe+/dwZo15Ywdm8JVV2WxaNEQEhOj\nU9Ny4cKFzt0r0FrbCkw3xniA540xU621n3a3UdbaR4BHIHAT5li6+WKsirWbVMYi9VHX1EfhUT91\nTX0Unljvp5EjJ3H22St46KEqVqw4n8TE6BcJ6E4frVu3m+uuW8XOnVX89Kfz+PGP58TsvR+71Spr\nrR94HVh6xEulQMcb2o0OPiciIiIx5qyzxnPvvQt56aUCbr/9Lbebc0ytrW3cddc6vvSlp7DW8uab\nl3PnnfNiNlRBeFcFZgLN1lq/MWYAsAT41RGbvQTcbIx5msCi9Upr7R7HWysiIiKOuPnmU9i6tZxf\n//oDJk8ewte//kW3m3SYXbuquPrqV3jzzRIuv3wSDz20xLUr/bojnKnALODJ4DqrBOBZa+3Lxpgb\nAay1DwGvECi14CNQbuHrEWqviIiIOOTeexexfXsF3/rWGnJzPZxxRk7Xb4qC5577nOuv/wctLW08\n+eRX+drXvhC1+wP3VJfBylq7GZjRyfMPdXhsgZucbZqIiIhEUlJSAs8+ey5z5/6V5ctf5P33ryYv\nL/LVyY+ltraJW255ncce+4RTTx3JX/96Dl7vYNfacyJid5JSREREIs7jSWHlygsBWLZsBZWVja60\nY9OmfZxyyp/4/e8/4fbbZ/POO1fEXagCBSsREZE+z+sdzIoV51NQ4OfSS1fS0tIWtWO3tVl++9sP\nmDPnL9TWNrN27aX84henk5zsThmInlKwEhEREc44I4eHHlrCP/5RzA9+8HpUjrlnTw1Llz7Hrbe+\nwTnn5PLxx9ewcOGYqBw7UnQTZhEREQHguuu+yNatB/nNbzYwefIQvvOdo5ZYO+a99/xccsmT1NY2\n8/DDS7j++pPjZoH68ShYiYiISLu77/4yn39ewfe+908mTBjMkiXjHN1/Q0ML//Efb3D//T6mTcvk\nqaeWMXnyUEeP4SZNBYqIiEi7xMQE/vKXc5gyZRiXXLKSbdsOOrbvTz8t49RT/8z993/IxRcPZ926\nq3pVqAIFKxERETlCeno/XnrpAvr3T2TZsuc5eLC+R/uz1vLAAx8ya9af2b+/jldeWc5NN40hJaX3\nTZwpWImIiMhRxo7N4MUXL6CkpJrly1+kqan1hPZTVlbHeec9z803r2Xhwhw2b76Gr3411+HWxg4F\nKxEREenUnDnZPP74Ut58s4Rvf3sNgXrg4VuzppiTT36Sf/xjB/fcs5BVqy5ixIjUCLU2NvS+MTgR\nERFxzJVXTmbbtoP8/OfrmDx5KLfeemqX72lqauWOO95qv7pw9eqLmDZteBRa6z4FKxERETmun/xk\nPtu2lXPbbW8wceIQzj0375jb/utf5VxxxSo2bdrHjTdO47e/XcDAgclRbK27NBUoIiIix5WQYHji\nia8yc+YIrrzyZTZvLjtqG2stjz/+CTNm/JHi4kqef/58HnxwSZ8KVaBgJSIiImEYODCZl166kIyM\n/px77gr27attf62iooHLLlvJN77xd2bPzmLz5mu44IIJLrbWPQpWIiIiEpasrDRWrryQAwfqueCC\nF2hoaOGtt0qYNu1Jnn/ex913n86aNZcwalS62011jdZYiYiISNhmzBjBn/98DsuXv8jcuX9l8+Yy\ncnMzePfdKzj11Cy3m+c6jViJiIhIt1x44QTuvvt0PvpoP//2b19g06Z/U6gK0oiViIiIdNsPfzib\nr31tCtnZaW43JaZoxEpEREROiELV0RSsRERERByiYCUiIiLiEAUrEREREYcoWImIiIg4RMFKRERE\nxCEKViIiIiIOUbASERERcYiClYiIiIhDFKxEREREHKJgJSIiIuIQY61158DGVAOfu3Lw+DIMOOB2\nI2Kc+qhr6qPwqJ+6pj4Kj/qpa/HWR2OttZldbeTmTZg/t9bOcvH4ccEYs0H9dHzqo66pj8Kjfuqa\n+ig86qeu9dY+0lSgiIiIiEMUrEREREQc4mawesTFY8cT9VPX1EddUx+FR/3UNfVReNRPXeuVfeTa\n4nURERGR3kZTgSIiIiIOUbASERERcYhjwcoYk2OMed0Y85kxZosx5vvB54cYY9YYY7YH/xzc4T23\nG2N8xpjPjTFndXh+pjHmk+Br9xljjFPtlNjn8LmUH3zuo+DXcDc+k7jD4XPpMmPM5uB+fuXG5xH3\ndPdcMsYMDW5fY4y5/4h9rTbGfBzcz0PGmEQ3PpNEhmNrrIwxWUCWtXaTMSYd2AhcAFwLlFtr7zbG\n/AgYbK39oTHmC8BTwGlANvAacJK1ttUY8z7wPWA98Apwn7X2VUcaKjHP4XMpH7jVWrvBjc8i7nLq\nXAI8wIfATGttmTHmSeCP1tq10f9U4oYTOJdSgRnAVGCqtfbmDvsaZK2tCg4aPAf8zVr7dLQ/k0SG\nYyNW1to91tpNwcfVwFZgFHA+8GRwsycJnIgEn3/aWttorS0CfMBpwZN3kLV2nQ2kvj92eI/0AU6d\nS9FttcQiB8+lXGC7tbYsuN1rwEXR+RQSC7p7Lllra621bwMNneyrKvgwCegH6CqyXiQia6yMMeMI\nJPX1wAhr7Z7gS3uBEcHHo4BdHd5WEnxuVPDxkc9LH9TDcynkyeA04H9pWrnv6uG55AMmGmPGGWOS\nCPznmROFZksMCvNc6moffwf2A9UERq2kl3A8WBlj0oD/BW7pkMoBCI5AKZlLWBw6l66y1k4BTg9+\nfc3xhkrM6+m5ZK2tAL4NPAO8BRQDrRFprMQ0p/6Ps9aeBWQB/YFFTrdT3ONosDLGJBM44f5irV0R\nfHpfcHovNEe9P/h8KYf/xjc6+Fxp8PGRz0sf4tC5hLU29Gc18Fc0RdjnOHgurbTWzrbWziVwA/l/\nRaP9Eju6eS51yVrbALxIYDpRegknrwo0wO+Brdba/9vhpZeAa4KPryFwEoWev9wY098YMx6YALwf\nHFKtMsbMCe7z3zq8R/oAp84lY0ySMWZYcJ/JwDLg02h8BokNTp1LwX0ND/45GPgO8FjkP4HEihM4\nl461n7QOQSwJOAfY5nyLxS1OXhX4JQJD5J8AbcGnf0xgDvpZYAywA7jUWlsefM8dwHVAC4Fh1VeD\nz88CngAGAK8C37UqEd9nOHUuBa/KeRNIBhIJLDj+d2utpnD6CId/Lj0FTAvu42e6iqtvOcFzqRgY\nRGCBuh84EzgIvExgCjABeB34gbW2JVqfRSJLt7QRERERcYgqr4uIiIg4RMFKRERExCEKViIiIiIO\nUbASERERcYiClYiIiIhDFKxEREREHKJgJSJ9kjEm0e02iEjvo2AlIjHPGPMzY8wtHb6/yxjzfWPM\nfxhjPjDGbDbG/LTD6y8YYzYaY7YYY27o8HyNMea3xpiPgblR/hgi0gcoWIlIPHicwO2tMMYkAJcD\newnccuY0YDow0xjz5eD211lrZwKzgO8ZY4YGn08F1ltrp1lr347mBxCRviHJ7QaIiHTFWltsjDlo\njJkBjAA+BE4lcIuQD4ObpREIWm8SCFMXBp/PCT5/EGglcBNdEZGIULASkXjxGHAtMJLACNZi4JfW\n2oc7bmSMWQB8BZhrra0zxuQDKcGXG3SvSBGJJE0Fiki8eB5YSmCk6u/Br+uMMWkAxphRxpjhQAZQ\nEQxVk4A5bjVYRPoejViJSFyw1jYZY14H/MFRp38YYyYD7xljAGqAq4HVwI3GmK3A58A6t9osIn2P\nsda63QYRkS4FF61vAi6x1m53uz0iIp3RVKCIxDxjzBcAH7BWoUpEYplGrEREREQcohErEREREYco\nWImIiIg4RMFKRERExCEKViIiIiIOUbASERERccj/B13JDo6CMse1AAAAAElFTkSuQmCC\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x20100872f98>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "average_year[-20:].plot(x='year', y='rating', figsize=(10,5), grid=True , color='DarkBlue')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "                           Fig : Average Movie Ratings over Time "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.6.0"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
