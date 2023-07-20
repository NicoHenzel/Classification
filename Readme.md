### Project description
Winter semester 2022 at Hochschule der Medien in Stuttgart, Germany
The motivation is to demonstrate the low-code open source software [Rapid Miner Studio](https://rapidminer.com/) and apply various classification algorithms.

The goal for this is to use the spotify charts dataset to see if features can be identified that make for a top hit song.
Ideally this would lead to an algorithm that can predict whether a song will be a top song or not, given specific features.

* In the [presentation](https://github.com/NicoHenzel/Classification-with-Rapid-Miner/blob/main/HDM%20Data%20Science_Final.pptx), you can find the final conclusion as well as a breakdown of the results.
* [GitHub Link](https://github.com/NicoHenzel/Classification)
* [RapidMiner Studio](https://docs.rapidminer.com/9.4/studio/installation/)
---

### Data
[Artists and Tracks](https://www.kaggle.com/datasets/yamaerenay/spotify-dataset-19212020-600k-tracks)
* artists.csv --> Artist Features like Popularity, Followers etc.
* dict_artists.json --> The artists recommended for fans of artists. Each recommendation is sorted in descending order (The first one is the most favorite one). The number of recommendations are limited to 20.
* tracks.csv --> The audio features of tracks.


[Chart Position](https://www.kaggle.com/datasets/jfreyberg/spotify-chart-data)
* charts.csv: This dataset is comprised of weekly Spotify track chart data from 2014 to 2022. Used to get the chart position of the song in various countries.

### License
This project is licensed with LGPL. For more information checkl the "License" file.

---
### Project structure


```nohighlight
├── README.txt                   <- The top-level README for people using this project.
├── Data Eploration              <- Inspection of datasets in different preprocessing and clean states. Contains RapidMinerFiles that were used in the exploration
│   └── DataEplorationResults    <- Results of the exploration for every original dataset and the final combination
│       ├── ArtistsRecommended   <- Combined Dataset, contains artists and which artists are recommended by spotify for a specific artist
│       ├── Cleanset             <- Tidy Dataset used for first iteration of modelling.
│       ├── FinTable             <- The final dataset for the final iteration of modelling.
│       ├── Presentation         <- Exploration Results shown in the presentation.
│       └── RawData              <- The original, immutable data dump.
│
├── Data                         <- Contains different states of the datasets used in our iterations.
│   ├── Datasets Rapidminer      <- Data that was transformed using Rapid Miner Studio.
│   ├── Other                    <- Data that was transformed using SQL.
│   ├── Python                   <- Python Code to for the first look, data engineering and quick-and-dirty modelling.
│       └── Engineering          <- Result of the Data engineering to generate the ArtistsRecommended dataset.
│   └── Raw                      <- Copy of the RawData for the artists.csv.
│
├── First Iteration              <- Results from modelling in Rapid Miner Studio for the first iteration, using the Cleanset data.
│
└── Second Iteration             <- Results from modelling in Rapid Miner Studio for the first iteration, using the FinTable data.
    ├── Engineering              <- Engineering in Rapid Miner Studio.
    ├── Final Model              <- Comparison of Models and Ensembles to find the best performing algorithm.
    ├── Optimize Parameters      <- Hyperparamater Tuning of all used algorithms.
    └── Results                  <- Results of Final Model and Optimize Parameters Runs.
        ├── Models               <- Dump of Model obtained from Final Model run.
        ├── Parameters           <- Comparison of hyperparameter tuning.
        └── Performances         <- Coparison of Ensemble, Voting and Stacking models.

```    
### Steps for Dataengineering 
(needed to generate Rapid Miner Studio Datasets in order to run processes)

1. Download datasets
Datasource: https://www.kaggle.com/datasets/yamaerenay/spotify-dataset-19212020-600k-tracks
artists.csv --> Artist Features like Popularity, Followers etc.
dict_artists.json --> The artists recommended for fans of artists. Each recommendation is sorted in descending order (The first one is the most favorite one). The number of recommendations are limited to 20.
tracks.csv --> The audio features of tracks.


https://www.kaggle.com/datasets/jfreyberg/spotify-chart-data
charts.csv: This dataset is comprised of weekly Spotify track chart data from 2014 to 2022.
Used to get the chart position of the song in various countries.

Store them in Classification\Data\Raw

Use Table in Classification\Data\Other:
FinTable.csv

2. Run JsonReads.ipynb in python (adjust file paths if needed)

3. Import Datasets into RapidMinerStudio with these settings:
Header Row - 1
Start Row - 1
Column Separator - Comma ","
Encoding - UTF-8
Escape Character - \
Decimal Character - .
Use Quotes - "
Skip Comments - #


4. Run Processes in Engineering Folder in Rapid Miner 
ArtistsRecommendedBy Dataset generated by Rapid Miner Process "0. Generate Recommended Artists Dataset" from "artists.csv" and result of "JsonReads.ipynb"
Final Dataset Generated after running "1. Join Data" and "2. Step Data Engineering"
