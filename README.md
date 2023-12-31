# DSC-Phase1Project

## Overview
Microsoft, is a multinational corporation that was founded in 1975 and serves as the world’s leading software developer. As an ambitious entity that seeks to offer solutions to global challenges, the company has identified a gap in movie production and it seeks to fill the gap by opening a subsidiary movie studio. It is worth highlighting that Microsoft's business domain is broad and encompasses a wide range of products, services, and initiatives in the technology industry hence venturing into movie production is an added avenue for business. It is primarily known for its software products, cloud services, and hardware devices hence delving into the film industry will not only promote diversification but also promote economic growth while creating employment opportunities. Most importantly, the new venture will generate income for the entity thus improving its performance and while surpassing the set financial goals.  

###Business Understanding

Microsoft is embarking on a strategic venture to establish its own movie studio, marking a significant expansion into the entertainment industry. The aim of this project is to create a thriving movie production entity that produces high-quality, diverse content for various distribution channels, including theaters, streaming platforms, and television networks. The project is pivotal in leveraging data-driven insights to optimize various aspects of movie production, distribution, and audience engagement. This is because the global entertainment industry is valued at $2 trillion and continues to expand (Guttmann, 2023). Streaming platforms, international markets, and diverse content preferences offer substantial growth prospects. The Microsoft brand, and technological prowess of the company can create a competitive advantage that can set the new movie studio venture apart in the industry. Additionally, integration with Microsoft's existing ecosystem can enhance user engagement and content delivery. The following objectives will play a role in shaping the new investment;
i.	To determine the most popular genres among viewers, aiding in strategic genre selection for future movie projects.
ii.	To understand how movie titles influence user engagement and voting behavior, enabling the creation of impactful titles.
iii.	To identify directors whose movies consistently receive a high number of votes and positive ratings.
iv.	To explore viewer preferences regarding movie runtime and identify the ideal runtime for maximizing engagement.
v.	To uncover which director-genre combinations yield the most favorable results in terms of audience engagement.
vi.	To investigate the correlation between movie runtime and genre preferences among viewers.
vii.	To develop a quality assessment metric considering both user ratings and votes, facilitating content quality evaluation.

####Data Understanding and Analysis

Sources of data
Source 1 : 'im.db.zip'
Source 2 : 'bom.movie_gross.csv.gz'

Because of the wealth of data available that can help understand the film production industry, began with the selection of the most ideal datasets to work with. The process of data cleaning began with the exploration of the available datasets. After an in-depth comparison, I decided to work with the ‘im.db’ database where I analyzing a database that contains several tables. The most important tables in the database were; 'Movie basics' and 'Movie ratings'.  Each table has various fields which anchor critical information necessary for analysis. I later conducted visualization that played a critical role in drawing my conclusions, insights, and recommendations necessary for Microsoft movie studios. The fields for the 'Movie basics' table include; Movie_id, Primary title, Original title, Start_year, Runntime_minutes, and most importantly, the ‘Genres’ field. The second table contains three major fields; the Movie _id column, Average rating column, and the Number_of_votes column. Here, I was able to gain a deep understanding of the dataset's characteristics. I completed the data cleaning process where I addressed the issue of missing values, dropped unnecessary columns, edited the field titles, and shaped the tables in a more attractive manner for analysis.
After settling on the ‘im.db’, the first step was to access the data in a pandas DataFrame format where I generated the ‘Movie_basics’ and the ‘Movie_ratings’ tables.
''' python
# To access the data in a pandas dataframe format
df1 = pd.read_sql("""SELECT * FROM movie_basics;""", conn)
df1.head()
# use value count to check categorical variable distribution
df1['genres'].value_counts().head()
# Use a one line code to open the 'movie_ratings' table
df2 = pd.read_sql("""SELECT * FROM movie_ratings;""", conn)
df2
# To identify non-null values in a runtime_minutes column:
null_column = pd.isna(df1['runtime_minutes'])
null_column
# Replace null values in 'genres' column with 'Horror, Thriller' where 'runtime_minutes' is < 100
df1.loc[df1['runtime_minutes'] < 100, 'genres'] = df1.loc[df1['runtime_minutes'] < 100, 'genres'].fillna('Horror, Thriller')
df1.loc[df1['runtime_minutes'] >= 100, 'genres'] = 'Documentary'
# Instead of changing the columns one by one, i decided to change all the column names to uppercase
df1.columns = [column.upper() for column in df1.columns]
df1.head()
# Specify the collumn and in this case is the 'PRIMARY_TITLE'
column_names = 'PRIMARY_TITLE'

# Remove duplicates in the column
df1 = df1.drop_duplicates(subset=[column_names])
df1
# merge the 2 tables(DataFrames)
df4 = df1.merge(df2, on='MOVIE_ID', how='inner')
df4.head()
# Calculate the mean of the AVERAGERATING for all documentaries
# Filter the DataFrame to select only movies with the "Documentary" genre
documentary_movies = df4[df4['GENRES'] == 'Documentary']

# Calculate the mean of the AVERAGERATING column for Documentary movies
mean_rating_documentary = documentary_movies['AVERAGERATING'].mean()

print("Mean rating for Documentary movies:", mean_rating_documentary)
'''
'''python
# Visualizing 
import seaborn as sns
# Assuming your DataFrame is named 'df5'
# Sort 'df5' by 'AVERAGERATING' in descending order and select the top 40
top_40_movies = df5.sort_values(by='AVERAGERATING', ascending=False).head(40)

# Create a vertical bar graph using Seaborn
plt.figure(figsize=(12, 10))
sns.barplot(data=top_40_movies, x='MOVIE_ID', y='AVERAGERATING', hue='GENRES', palette='viridis')
plt.xlabel('Movie ID')
plt.ylabel('Average Rating')
plt.title('Top 40 Movies by Average Rating')

plt.xticks(rotation=90)  # Rotate x-axis labels for better readability

plt.grid(axis='y')  # Add horizontal grid lines for y-axis

plt.legend(loc='upper right', bbox_to_anchor=(1.4, 1))

plt.show()
# Create a histogram of average ratings
# Set the figure size
plt.figure(figsize=(12, 8))  
sns.histplot(data=df5, x='Average_Rating', bins=20, kde=True)
plt.xlabel('Average Rating')
plt.ylabel('Frequency')
plt.title('Distribution of Average Ratings')
plt.show()
# Create a scatter plot of average ratings vs. number of votes
plt.figure(figsize=(12, 8))
sns.scatterplot(data=df5, x='Average_Rating', y='NUM_VOTES')
plt.xlabel('Average Rating')
plt.ylabel('Number of Votes')
plt.title('Average Ratings vs. Number of Votes')
plt.show()
# Create a countplot of movie production by year
plt.figure(figsize=(12, 6))
sns.countplot(data=df5, x='START_YEAR', palette='viridis')
plt.xticks(rotation=90)
plt.xlabel('Year')
plt.ylabel('Number of Movies (Based on the List of Genres)')
plt.title('Yearly Movie Production Trends')
plt.show()
import matplotlib.pyplot as plt

# reducing the sample to 20 for clarity
director_ratings = finaldf.groupby('DIRECTOR_ID')['AVERAGERATING'].mean()
top_20_directors = director_ratings.sort_values(ascending=False).head(20)

# Plotting the top 20 directors and their average ratings
plt.figure(figsize=(12, 6))
plt.plot(top_20_directors.index, top_20_directors.values, marker='o', linestyle='-', color='b')

plt.title('Top 20 Directors by Average Movie Rating')
plt.xlabel('Director ID')
plt.ylabel('Average Rating')
plt.xticks(rotation=90)
plt.grid(True)
plt.tight_layout()

plt.show()
'''
This was followed by calculating the value count to check the categorical variable distribution of various genres in the ‘Genre’ field.  After cleaning the tables, I joined them and the process of data visualization kicked in.  The first graph was generated using the seaborn module where I created a vertical bar graph.  Because of the length of the data in each field, a sample population of 40 variables was selected based on average ratings and genres.  The goal was to select the top 40 movies in the merged DataFrame. From the graph, all the top for movies and their corresponding genres have a rating of more than 9 in a scale of 10. The most preferred genres according to the generated barplot and in the order of preference include;
 	Documentary
 	Drama
 	Adventure, Comedy
 	Documentary, History
 	Comedy, Documentary 
 	Biography, Documentary Drama
 	Biography, Music
 	Action
![Alt Text]![image](https://github.com/TitusKilonzoMutuku/DSC-Phase1Project/assets/142430151/c772e512-03f0-4a1e-87cd-e2d0fe66e673)
 
Therefore, inasmuch as the new Microsoft movie studio will diversify to produce as many genres as possible, the best performing genres according to the analysis are the one’s listed above. 

The second visualization generated a histogram of average ratings whereby the analysis sought to establish how skewed the ratings were for the purpose of confirming how biased the audience could have been in order to make sound decisions as far as the new movie studio is concerned. The symmetrical distribution typically suggests that the ratings for the movies are evenly distributed around a central value. Therefore, the studio should use this information as a starting point for further analysis and decision-making and for understanding the nature of the target audience. 
![Alt Text]![image](https://github.com/TitusKilonzoMutuku/DSC-Phase1Project/assets/142430151/2b977238-4053-41ba-84c1-2dd022920943)

The third visualization sought to establish whether there is correlation between the average rating and the number of votes for each movie on the basis of their respective genres. Analyzing the relationship between average ratings and the number of votes provided valuable insights into audience engagement and the impact of audience size on perceived content quality. From the scatter graph, it is evident that the top rated movies and their respective genres tend to receive the most votes. It is therefore advisable for the manager of the new Microsoft movie studio to put more focus on the highly regarded genres when planning for production to attract positive responses and establish the studio is the go-to studio for contemporary movie consumers. 

![Alt Text]![image](https://github.com/TitusKilonzoMutuku/DSC-Phase1Project/assets/142430151/60de87a1-6e38-4893-830b-843f3690aa9a)

Finally, the analysis sought to establish the trend of movie production per year. To establish this line of thought, a count plot of movie production by year was created.  This visualization established the number of movies produced each year. It was established that movie production was on the rise up until 2019 whereby the industry witnessed a sudden decline. For justifiable conclusion, there needs to be done for the year 2020, 2021, and 2022 to determine whether the decline was subjective. The countplot allows the studio to visualize how the number of movies produced has evolved over time. This provides insights into trends and patterns in the studio's production history. This understanding can inform strategic decisions related to resource allocation, content strategy, and audience engagement, ultimately helping Microsoft Movie Studios succeed in the film industry. The decline signifies the need for huge resource allocation to outdo competitors and the probable decline. 
![Alt Text]![image](https://github.com/TitusKilonzoMutuku/DSC-Phase1Project/assets/142430151/17f650f0-0194-4da3-8417-28f0b164ba22)


#####Conclusion

The project confirms that there is a strong correlation between genres, user ratings, and number of votes. The three can be effectively used to identify genres associated with high-quality content. By developing a content quality assessment metric, Microsoft Movie Studio can make data-driven decisions to improve the quality of its productions. Engaging top-notch directors and writers should be prioritized too. Investing resources tom spearhead growth is also imperative to avoid the impacts of the imminent decline in the industry.
Engaging top-notch directors and writers should be prioritized too. Investing resources tom spearhead growth is also imperative to avoid the impacts of the imminent decline in the industry.
It is imperative to put more emphasis on the highly regarded genres when planning for production to attract positive responses and establish the studio is the go-to studio for contemporary movie consumers. 
By observing production trends, the studio can make informed decisions regarding resource allocation for future projects. For example, during periods of increased production, more resources may be needed for casting, marketing, and distribution.
Invest in technology to engage the target audience continuously

###### Recommendations
 	Put more emphasis on the highly regarded genres when planning for production to attract positive responses and establish the studio is the go-to studio for contemporary movie consumers. 
 	By observing production trends, the studio can make informed decisions regarding resource allocation for future projects. For example, during periods of increased production, more resources may be needed for casting, marketing, and distribution.
 	Invest in technology to engage the target audience continuously

####### NextSteps

	Consider more analysis to establish the poorly performing genres and establish the reason to their poor performance.

	Establish the role of technology in improving the performance of contemporary movie studios.

	Predict the undesirable trends in movie production for the contemporary audience. 

