# MovieLens
MovieLens data sets were collected by the GroupLens Research Project at the University of Minnesota.
## Context:
The GroupLens Research Project is a research group in the Department of Computer Science and Engineering at the University of Minnesota. The data is widely used for collaborative filtering and other filtering solutions.

There is need to import 3 files from the folder as data frames into your Jupyter notebook
* u.data 
* u.item
* u.user
## Task
* Display univariate plots of the attributes: 'rating', 'age', 'release date', 'gender' and 'occupation', from their respective data frames
* Visualize how popularity of Genres has changed over the years. From the graph one should be able to see for any given year, movies of which genre got released the most.
* Display the top 25 movies by average rating, as a list/series/dataframe.
Note:- Consider only the movies which received atleast a 100 ratings
* Verify the following statements (no need of doing a statistical test. Compare absolute numbers):
* Men watch more drama than women
* Men watch more Romance than women
* Women watch more Sci-Fi than men
## References:
 https://movielens.org/
---------------------
## Data importation
After getting the data the next thing to do is to get the data in it can be challenging because it was not just the normal csv file now it was in another form entirely.

``` 
item = pd.read_csv('u.item', names=['movie id','movie title' , 'release date' , 'video release date' , 'IMDb URL' , 'unknown' , 'Action' , 'Adventure' , 'Animation' ,  "Children's" , 'Comedy' , 'Crime' , 'Documentary' , 'Drama' , 'Fantasy' ,  'Film-Noir' , 'Horror' , 'Musical' , 'Mystery' , 'Romance' , 'Sci-Fi' , 'Thriller' , 'War' , 'Western' ], sep='|', encoding='latin-1', header=None)
```
![item table raw](https://github.com/iamasprout/MovieLens/assets/114030254/f8745c3e-c987-470e-95d1-e0446c28a5a2)

```
data=pd.read_table('u.data',names=['user id',  'item id',  'rating', 'timestamp'])
```
![data table](https://github.com/iamasprout/MovieLens/assets/114030254/7a932395-e700-42fb-829b-769ad836068f)
``` 
user = pd.read_csv('u.user',names=['user id' , 'age' , 'gender' , 'occupation' , 'zip code'], sep='|', encoding='latin-1', header=None)
```
![user table](https://github.com/iamasprout/MovieLens/assets/114030254/2e1e12b3-b4ca-4a88-aaa9-6bb6bf4035d4)
## Data Cleaning
After importing the data, I needed to clean it up so that it was usable for our analysis. I made the following changes and created the following variables:

* the datatype of each columns need to be corrected for example the columns that has to do with date has to be updated 
* a new column has to be created or you can choose to rename a column that already exist but useless i went for option two
* The movie title looks awkward do i need to remove the year behind every title
* and the table need to be merged. i needed to normalize my data and to get that the item id is same as movie id in two tables so i changed it from item id to movie id
* and the univarate anylysis was done on a cleaned data
so after clening the item table i have this 
![item table cleaned](https://github.com/iamasprout/MovieLens/assets/114030254/90c9a3e5-ff0b-4b0f-9216-ba6b64b9aa5c)
  ###### the users table

![user table](https://github.com/iamasprout/MovieLens/assets/114030254/d6f24b65-690d-4cf9-99a7-ee9d28dcda82)
  ###### the data table

![cleaned data table](https://github.com/iamasprout/MovieLens/assets/114030254/f86cccf1-d9ad-4ceb-aac8-0bd2c7285a82)

i then need to merge the tables together
```
userdata=pd.merge(data,user, how="right")
userdata=pd.merge(userdata,item,how='right')
```
then we have userdata columns as

![merged columns](https://github.com/iamasprout/MovieLens/assets/114030254/8315d026-08ea-49a7-b8ed-3bf2244005a1)

## univariate plots of the attributes
#### Ratings
```
rating=userdata['rating'].value_counts().sort_values(ascending=False)
rating.values
plt.figure(figsize=(10,5))
sns.barplot(x=rating.index,y=rating.values)
plt.xlabel('Ratings', fontsize=12)
plt.ylabel('Counts', fontsize=12)
plt.title('Univarate Analysis of Ratings')
plt.show()
```
![Univarate Analysis of Ratings](https://github.com/iamasprout/MovieLens/assets/114030254/9b002a3a-77c0-42d1-b06e-dbbb2cfd2681)

#### age
```
age=userdata['age'].value_counts().sort_values(ascending=False)
age.values
plt.figure(figsize=(12,6))
sns.barplot(x=age.index,y=age.values)
plt.xlabel('age', fontsize=12)
plt.xticks(rotation=90)
plt.ylabel('Counts', fontsize=12)
plt.title('Univarate Analysis of age')
plt.show()
```
![Univarate Analysis of age](https://github.com/iamasprout/MovieLens/assets/114030254/181b8285-01eb-493c-acd2-7f6176de9e6b)

#### Release Date
```
release_date=item['release year'].value_counts().sort_values(ascending=False).head(20)
plt.figure(figsize=(12,6))
sns.barplot(x=release_date.index,y=release_date.values)
plt.xlabel('Years', fontsize=12)
plt.xticks(rotation=90)
plt.ylabel('Counts', fontsize=12)
plt.title('Univarate Analysis of Movies Released per year')
```
![nivarate Analysis of Movies Released per year](https://github.com/iamasprout/MovieLens/assets/114030254/3b6eb7b7-a1ee-4129-8fc8-85aa24d361bc)

#### gender
```
gender=userdata['gender'].value_counts().sort_values(ascending=False)
plt.figure(figsize=(8,4))
sns.barplot(x=gender.index,y=gender.values)
plt.xlabel('Gender', fontsize=12)
plt.xticks(rotation=90)
plt.ylabel('Counts', fontsize=12)
plt.title('Univarate Analysis of Users by Gender')
plt.show()
```
![Univarate Analysis of Users by Gender](https://github.com/iamasprout/MovieLens/assets/114030254/40de2ae7-48fb-459c-95ee-2c240b302d62)

#### occupation
```
occupation=userdata['occupation'].value_counts().sort_values(ascending=False)
plt.figure(figsize=(12,6))
sns.barplot(x=occupation.index,y=occupation.values)
plt.xlabel('occupations', fontsize=12)
plt.xticks(rotation=90)
plt.ylabel('Counts', fontsize=12)
plt.title('Univarate Analysis of Users by occupation')
```
![Univarate Analysis of Users by occupation](https://github.com/iamasprout/MovieLens/assets/114030254/2b8595d0-408f-4e1d-bada-3b6a42940068)

#### Visualize how popularity of Genres has changed over the years. From the graph one should be able to see for any given year, movies of which genre got released the most.
```
genre_counts = userdata.groupby('release year').sum().loc[:, 'Action':'Western'].head(30)
genre_counts
genre_counts.plot(kind='bar', stacked=True, figsize=(12, 6))
plt.xlabel('Release Year')
plt.ylabel('Number of Movies')
plt.title('Popularity of Genres Across Years')
```
![Popularity of Genres Across Years](https://github.com/iamasprout/MovieLens/assets/114030254/6034f4fc-3cef-43a3-8432-a0d7276c875b)

#### Display the top 25 movies by average rating, as a list/series/dataframe. Note:- Consider only the movies which received atleast a 100 ratings
```
ratings = userdata.groupby('movie id')['rating'].agg(['count', 'mean'])
ratingabove100 = ratings[ratings['count'] >= 100]
top_movies = ratingabove100.sort_values('mean', ascending=False).head(25)
top_movies
```
![ratings](https://github.com/iamasprout/MovieLens/assets/114030254/5273c3c9-9f93-4406-ae42-7fb4c397cb45)
#### Verify the following statements (no need of doing a statistical test. Compare absolute numbers):
#### Men watch more drama than women
```
drama = userdata.groupby(['gender', 'Drama'])['rating'].count()
drama
# when o is considered to be false 1 is true
f_drama=drama.loc['F',1]
m_drama=drama.loc['M',1]
print(f'The total number of female that watch drama {f_drama}, and for male {m_drama}, from our finding men watch drama genre than women')
```
![drama men](https://github.com/iamasprout/MovieLens/assets/114030254/9f62d401-5215-43dc-b029-8a8818134b30)

#### Men watch more Romance than women
```
romance = userdata.groupby(['gender', 'Romance'])['rating'].count()
romance
f_romance=romance.loc['F',1]
m_romance=romance.loc['M',1]
print(f'The total number of female that watch drama {f_romance}, and for male {m_romance}, from our finding men watch romance genre than women')
```
![romance](https://github.com/iamasprout/MovieLens/assets/114030254/cf58808e-a234-4704-bdd5-d6bb9189ef3a)

#### Women watch more Sci-Fi than men
```
sci_fi = userdata.groupby(['gender', 'Sci-Fi'])['rating'].count()
sci_fi
f_sci_fi=sci_fi.loc['F',1]
m_sci_fi=sci_fi.loc['M',1]
print(f'The total number of female that watch drama {f_sci_fi}, and for male {m_sci_fi}, from our finding men watch Science Fictional genre than women')
```
![sci-fi](https://github.com/iamasprout/MovieLens/assets/114030254/4e883b83-bd30-4724-9b50-6ebcc2d1412d)
 ##### lastly i wanted to have a collation of all the genre of each film
 ```
 genre_columns = ['Action', 'Adventure', 'Animation', "Children's", 'Comedy', 'Crime', 'Documentary', 'Drama', 'Fantasy', 'Film-Noir', 'Horror', 'Musical', 'Mystery', 'Romance', 'Sci-Fi', 'Thriller', 'War', 'Western']
userdata['genre'] =userdata[genre_columns].apply(lambda x: '|'.join(x.index[x == 1]), axis=1)
userdata
 ```
 ![all genre](https://github.com/iamasprout/MovieLens/assets/114030254/e2436905-e39a-42aa-ade4-474ac5cf8493)

