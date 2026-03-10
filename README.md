# 🎬 Movie Genres Data Analysis Project
## 📊 Overview

![Movie Genre Analysis](https://raw.githubusercontent.com/iyanusol/Movie-Data-Analysis/main/download.png)

This project explores a dataset of movies to uncover patterns between movie genres, budgets, revenues, popularity, and profitability. Using Python and Pandas, the analysis focuses on how different genres perform financially and how genre combinations influence movie success.

The goal of this project is to demonstrate data cleaning, transformation, and exploratory data analysis techniques commonly used in real-world data analytics workflows.

## 📁 Dataset
| Column         | Description                                  |    |
| -------------- | -------------------------------------------- | -- |
| popularity     | Popularity score of the movie                |    |
| budget         | Production budget                            |    |
| revenue        | Total revenue generated                      |    |
| original_title | Movie title                                  |    |
| runtime        | Length of movie (minutes)                    |    |
| release_date   | Date movie was released                      |    |
| vote_count     | Number of votes received                     |    |
| vote_average   | Average rating                               |    |
| genres         | Movie genres (multiple genres separated by ` | `) |

Example genre format:

Action|Adventure|Science Fiction
Comedy|Drama
Thriller|Crime

![Movie Genre Analysis](https://raw.githubusercontent.com/iyanusol/Movie-Data-Analysis/main/movie%20project%20images/movies4.png)

Because movies can belong to multiple genres, the dataset required transformation before analysis.

## 🧹 Data Cleaning and Preprocessing
The first step involved preparing the data for analysis.

**Steps performed:**
- Selected relevant columns for analysis
- Created a profit column
- Split the genres column into individual rows
- Removed missing values
- Converted data types where necessary
- Creating the Profit Column

```
movies['profit'] = movies['revenue'] - movies['budget']
```

## 🔀 Splitting the Genre Column
The dataset originally stored multiple genres in a single column separated by |.
Example:

![Movie Genre Analysis](https://raw.githubusercontent.com/iyanusol/Movie-Data-Analysis/main/movie%20project%20images/movies7.png)

```
Action|Adventure|Science Fiction
```
To analyze each genre independently, the column was split and exploded into separate rows.

```
from pandas import Series, DataFrame

split = movie_genre['genres'].str.split('|').apply(Series, 1).stack()
split.index = split.index.droplevel(-1)
split.name = 'genres_split'

del movie_genre['genres']

movie_genre = movie_genre.join(split)
```
**After transformation:**

| title          | genres_split    |
| -------------- | --------------- |
| Jurassic World | Action          |
| Jurassic World | Adventure       |
| Jurassic World | Science Fiction |

**This allows analysis by individual genres.**

```
genres_avg = movie_genre.groupby('genres_split').mean(numeric_only=True)

genres_avg
```

## Example Insights

The analysis revealed interesting trends:

• Adventure and Action movies tend to have higher production budgets.
• Science Fiction and Fantasy movies often generate higher revenues.
• Comedy movies generally have lower budgets but can still achieve strong profitability.
• Some niche genres such as Documentary or Foreign films have lower average revenue but often require smaller budgets.

![Movie Genre Analysis](https://raw.githubusercontent.com/iyanusol/Movie-Data-Analysis/main/movie%20project%20images/movies2.png)

##📊 Visualization Example
Visualizing genre popularity helps identify which genres appear most frequently in the dataset.

```
genre_counts = movie_genre['genres_split'].value_counts()

genre_counts.plot(kind='barh', figsize=(10,6))
```

## 📌 Key Questions Answered

This project explores several important questions:

1️⃣ Which movie genres have the highest average budgets?
2️⃣ Which genres generate the highest revenues?
3️⃣ Which genres appear most frequently in the dataset?
4️⃣ Are higher budgets associated with higher profits?
5️⃣ Which genres have the highest average ratings?

![Movie Genre Analysis](https://raw.githubusercontent.com/iyanusol/Movie-Data-Analysis/main/movie%20project%20images/movies3.png)

## 🧠 Skills Demonstrated

This project highlights practical data analytics skills, including:

- Data cleaning
- Data transformation
- Feature engineering
- Exploratory Data Analysis (EDA)
- GroupBy aggregation
- Data visualization
- Working with real-world datasets

Tools used:

- Python
- Pandas
- Matplotlib
- Jupyter Notebook


### 📂 Project Structure

```
movie-genre-data-analysis
│
├── imdb_movies.csv
├── Movie_Data_Analysis.ipynb
└── README.md
```

### 🚀 How to Run the Project

1️⃣ Clone the repository

```
git clone https://github.com/yourusername/movie-genre-analysis.git
```
2️⃣ Install dependencies

```
pip install pandas matplotlib
```

3️⃣ Open the notebook
```
jupyter notebook
```

4️⃣ Run all cells in Movie_Data_Analysis.ipynb

## 📊 Example Code Snippets
**Load Dataset**

```
import pandas as pd

movies = pd.read_csv("imdb_movies.csv")
movies.head()
```

**Select Relevant Columns**
```
movie_genre = movies[['popularity','budget','revenue','original_title',
                      'runtime','release_date','vote_count',
                      'vote_average','profit','genres']]
```

**Group Analysis by Genre**

```
genres_avg = movie_genre.groupby('genres_split')[['budget','revenue']].mean()

genres_avg
```

##👨‍💻 Author
**Iyanu Adebara**
Data Analyst | Python | SQL | Data Visualization

**🔗 Connect with me on LinkedIn**
https://www.linkedin.com/in/iyanu-adebara-5a62a0103/
