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

Because of the wealth of data available that can help understand the film production industry, began with the selection of the most ideal datasets to work with. The process of data cleaning began with the exploration of the available datasets. After an in-depth comparison, I decided to work with the ‘im.db’ database where I analyzing a database that contains several tables. The most important tables in the database were; 'Movie basics' and 'Movie ratings'.  Each table has various fields which anchor critical information necessary for analysis. I later conducted visualization that played a critical role in drawing my conclusions, insights, and recommendations necessary for Microsoft movie studios. The fields for the 'Movie basics' table include; Movie_id, Primary title, Original title, Start_year, Runntime_minutes, and most importantly, the ‘Genres’ field. The second table contains three major fields; the Movie _id column, Average rating column, and the Number_of_votes column. Here, I was able to gain a deep understanding of the dataset's characteristics. I completed the data cleaning process where I addressed the issue of missing values, dropped unnecessary columns, edited the field titles, and shaped the tables in a more attractive manner for analysis.
After settling on the ‘im.db’, the first step was to access the data in a pandas DataFrame format where I generated the ‘Movie_basics’ and the ‘Movie_ratings’ tables. This was followed by calculating the value count to check the categorical variable distribution of various genres in the ‘Genre’ field.  After cleaning the tables, I joined them and the process of data visualization kicked in.  The first graph was generated using the seaborn module where I created a vertical bar graph.  Because of the length of the data in each field, a sample population of 40 variables was selected based on average ratings and genres.  The goal was to select the top 40 movies in the merged DataFrame. From the graph, all the top for movies and their corresponding genres have a rating of more than 9 in a scale of 10. The most preferred genres according to the generated barplot and in the order of preference include;
 	Documentary
 	Drama
 	Adventure, Comedy
 	Documentary, History
 	Comedy, Documentary 
 	Biography, Documentary Drama
 	Biography, Music
 	Action
![Alt Text](C:\Users\HP\Pictures\40 movies)
Therefore, inasmuch as the new Microsoft movie studio will diversify to produce as many genres as possible, the best performing genres according to the analysis are the one’s listed above. 

#####Conclusion

The project confirms that there is a strong correlation between genres, user ratings, and number of votes. The three can be effectively used to identify genres associated with high-quality content. By developing a content quality assessment metric, Microsoft Movie Studio can make data-driven decisions to improve the quality of its productions. Engaging top-notch directors and writers should be prioritized too. Investing resources tom spearhead growth is also imperative to avoid the impacts of the imminent decline in the industry.
Engaging top-notch directors and writers should be prioritized too. Investing resources tom spearhead growth is also imperative to avoid the impacts of the imminent decline in the industry.
It is imperative to put more emphasis on the highly regarded genres when planning for production to attract positive responses and establish the studio is the go-to studio for contemporary movie consumers. 
By observing production trends, the studio can make informed decisions regarding resource allocation for future projects. For example, during periods of increased production, more resources may be needed for casting, marketing, and distribution.
Invest in technology to engage the target audience continuously
