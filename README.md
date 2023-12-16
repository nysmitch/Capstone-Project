# Capstone-Project

## Introduction

Academy Xi not only teaches the up and coming Data scientists it also supports and mentors some of Australia's best musicians under it's second company Xi Records.
Xi Records have tasked me to find if it is possible to predict if a song with certain characteristics would be popular ie. succesful.
To do this I have found some data from one of the top Music software used today. Spotify of course.

![image](https://github.com/nysmitch/Capstone-Project/assets/147038854/f5051294-3093-4404-9029-a4c189e51679)


## The Data

The Dataset is entitled "Most Streamed Spotify Songs 2023" it has 943 rows with 24 columns. In spotify terms the no. of streams indicates the number of plays ie. how popular a particular is and therefore how succesful it is. This is the dependent variable we will be predicting.
The Dataset includes the columns:
 - track_name: Name of the song
- artist(s)_name: Name of the artist(s) of the song
- artist_count: Number of artists contributing to the song
- released_year: Year when the song was released
- released_month: Month when the song was released
- released_day: Day of the month when the song was released
- in_spotify_playlists: Number of Spotify playlists the song is included in
- in_spotify_charts: Presence and rank of the song on Spotify charts
- streams: Total number of streams on Spotify
- in_apple_playlists: Number of Apple Music playlists the song is included in
- in_apple_charts: Presence and rank of the song on Apple Music charts
- in_deezer_playlists: Number of Deezer playlists the song is included in
- in_deezer_charts: Presence and rank of the song on Deezer charts
- in_shazam_charts: Presence and rank of the song on Shazam charts
- bpm: Beats per minute, a measure of song tempo
- key: Key of the song
- mode: Mode of the song (major or minor)
- danceability_%: Percentage indicating how suitable the song is for dancing
- valence_%: Positivity of the song's musical content
- energy_%: Perceived energy level of the song
- acousticness_%: Amount of acoustic sound in the song
- instrumentalness_%: Amount of instrumental content in the song
- liveness_%: Presence of live performance elements
- speechiness_%: Amount of spoken words in the song

## Modeling

After cleaning the data I created an initial visualisation to understand how normalised our data was.
![download](https://github.com/nysmitch/Capstone-Project/assets/147038854/364db2c2-3209-4d12-bf87-59253d5fe444)
This clearly showed the categorical vairables which were then removed from the dataframe.Next was a correlation test which cleary showed the highest correlations were the in spotify charts and playlists vairables.
![download](https://github.com/nysmitch/Capstone-Project/assets/147038854/95977b64-71f5-4600-b5fb-bb87e8810931)
But returning to the inital problem we wanted to know what about a song made it a hit so I again removed the unneded variables and focused on the characteristics of a song. Namely the bpm, danceability, valence, energy, acousticness, instrumentalness, liveness and speachiness.
After running an initial OLES test it created a model with the following Q-Q plot.
![download](https://github.com/nysmitch/Capstone-Project/assets/147038854/f6cd6ebe-54b7-47dc-8120-4b47a95ec3b5)

I then attempted to create a log transformation of the variables but this returned an even worse r-squared result.

I then went further through a stepwise selection process to select the variables to create the best result.
This resulted in the two categories with the p-values lower than 0.05 being speechiness and danceability.
![image](https://github.com/nysmitch/Capstone-Project/assets/147038854/13cbdbf9-087b-4c02-ab1d-49b2ee53af87)

but unfortunately the resulting Q-Q plot was if possible even worse
![download](https://github.com/nysmitch/Capstone-Project/assets/147038854/21f9b8ed-e3a7-433a-8b55-60191859c640)

## Insights
These results have led me to the conclusion that what makes a song popular or successful in this particular dataset is not able to be predicted accurately with a linear regression model.
But an earlier insight did show me that there was a fairly high collinearity with another variable. This led me to create model plotting streams vs in_spotify_playlists

![image](https://github.com/nysmitch/Capstone-Project/assets/147038854/8bda413b-6396-4ca4-805d-8a00d401afc2)

which after log transformations had the following Q-Q Plot.
![download](https://github.com/nysmitch/Capstone-Project/assets/147038854/a3893ca6-fc43-47d8-bc2c-4b83e74fbf86)

Which I was able to train and split test to arrive at thes results.

Train Mean Squared Error: 1.1530396750430474e+17
Test Mean Squared Error:  1.1945768783483576e+17


## Final Conclusions
Although we are unable to infer what in a song makes it a hit with a linear regression model. I have been able to create a model to predict the no. of streams a song may have if it appears in a certain no of playlists to an acceptable level of accuracy.


