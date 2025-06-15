🎧 Spotifyzer: Music Insights through Data Warehousing
A data-driven solution that converts raw Spotify interaction data into meaningful insights for artists, marketers, and labels by leveraging modern cloud infrastructure and analytics tools.
________________________________________
🔍 Overview
Spotifyzer is a cloud-native data warehouse and analytics project designed to examine patterns in Spotify user behavior, track characteristics, and engagement metrics. By aggregating and analyzing music data, it provides strategic insights to empower decision-makers in the music industry.
________________________________________
❗ Challenge
Although Spotify generates vast amounts of listening and audio feature data, most artists and stakeholders lack a comprehensive system to harness this data effectively. Spotifyzer solves this by integrating an end-to-end ETL pipeline with interactive dashboards that surface impactful trends.
________________________________________
✨ Key Features
•	🎯 Automated Data Ingestion: Pulls streaming metadata, user engagement signals, and audio characteristics.
•	🧹 ETL Pipeline: Cleans, enriches, and transforms raw data into a warehouse-ready format.
•	🧠 Intelligent Categorization: Adds mood-based tagging using audio feature engineering.
•	💾 Scalable Warehousing: Stores optimized analytical data in Snowflake for real-time queries.
•	📊 Dynamic Dashboards: Provides deep insights into listener activity, artist popularity, and playback trends via Power BI.
•	🔎 Granular Metrics: Track plays, skips, engagement windows, and more.
________________________________________
🛠️ System Architecture
Spotify API → AWS S3 → AWS Glue (ETL in Python) → Snowflake → Power BI Dashboards
•	API Source: Spotify Web API streams track & user interaction data
•	Staging: Raw JSON data stored temporarily in Amazon S3
•	ETL: AWS Glue Jobs written in Python clean, enrich, and normalize the data
•	Warehouse: Processed data loaded into Snowflake
•	Analytics: Dashboards and visualizations built using Power BI
________________________________________
🔄 ETL Workflow
🧪 Extract
•	Tool: spotipy (Spotify’s Python client)
•	Data collected:
o	Track metadata: title, artist, album, release date
o	Listening behavior: popularity, play counts, device types
o	User content: saved tracks, playlists, and recently played history
bash
CopyEdit
pip install spotipy
python spotify_etl_extract.py
Sample output:
yaml
CopyEdit
✅ Auth complete
✅ Tracks fetched: 295
✅ Playlists fetched: 9
✅ Recently played: 50 tracks
________________________________________
🔧 Transform
•	Platform: AWS Glue + Python (Pandas)
•	Actions:
o	Handle nulls, standardize schema, and convert data types
o	Add sentiment-based mood categorization
o	Enrich with genre labels via external datasets
o	Normalize and audit consistency
________________________________________
📥 Load
•	Destination: Snowflake
•	Schema Design:
o	Fact Table: fact_streaming_events
o	Dimensions: dim_track, dim_artist, dim_user, dim_audio_features, dim_date
•	Optimization: Data partitioned by genre, year, and mood category
sql
CopyEdit
CREATE OR REPLACE TABLE dim_track (
  track_id     STRING,
  track_name   STRING,
  artist_name  STRING,
  album_name   STRING,
  genre        STRING,
  release_date DATE
);
________________________________________
🧮 Data Model
lua
CopyEdit
              +----------------+
              |  dim_artist    |
              +----------------+
                      ↑
                      |
+------------+   +------------+   +------------------+
| dim_track  |<--| fact_stream |-->| dim_audio_feat   |
+------------+   +------------+   +------------------+
                      |
                      ↓
                +-------------+
                |  dim_user   |
                +-------------+
Follows a classic star schema for optimized querying and BI integration.
________________________________________
📊 Dashboard Walkthrough
Built using Power BI, the dashboard delivers insights across:
•	Albums, Artists, and Tracks
•	Listening time heatmaps (peak: 6 PM – 2 AM)
•	Device-based filters (e.g., Android vs. Mac)
•	Frequency vs. Duration Scatterplots
•	Skips, shuffles, and daily/hourly breakdowns
________________________________________
📈 Sample Insights
Metric	Value / Observation
Weekend Activity	~59% of plays happen on weekends
Peak Listening	6 PM – 2 AM
Most Played Artist	The Beatles
Avg Track Length	2–4 minutes; 10–25 replays per listener
Year-over-Year	Artists ↓ 26.39%, Albums ↓ 21.82%, Tracks ↓ 11.49%
________________________________________
🧰 Tech Stack
Layer	Technology
Language	Python
Libraries	Spotipy, Pandas, Requests
Cloud	AWS (S3, Glue, CloudWatch)
Warehousing	Snowflake
Visualization	Power BI
Versioning	Git
________________________________________
🚀 Getting Started
✅ Prerequisites
•	Python 3.x + pip
•	AWS account (S3, Glue)
•	Snowflake account
•	Power BI Desktop
🔐 Spotify API Setup
•	Create a developer account at Spotify Developer
•	Create an app and collect:
o	CLIENT_ID
o	CLIENT_SECRET
•	Set environment variables:
bash
CopyEdit
export SPOTIPY_CLIENT_ID='your_id_here'
export SPOTIPY_CLIENT_SECRET='your_secret_here'
export SPOTIPY_REDIRECT_URI='http://127.0.0.1:8000/callback'
________________________________________
🧪 Running the Pipeline
bash
CopyEdit
# Install dependencies
pip install spotipy pandas

# Clone the repo
git clone https://github.com/yourusername/Spotifyzer.git
cd Spotifyzer

# Run extraction
python spotify_etl_extract.py
Set up AWS Glue Jobs to transform and push to Snowflake. Connect Power BI to Snowflake for analytics.
________________________________________
🌟 Future Roadmap
•	Add real-time streaming via Kafka/Kinesis
•	Deploy ML models for hit-song prediction
•	Expand to multi-platform: YouTube, Apple Music
•	Launch web UI for interactive exploration
________________________________________
🤝 Contributions
We welcome feedback and collaboration! Fork the repo, make your changes in a branch, and open a PR 🚀
________________________________________
👨‍👩‍👧‍👦 Team
•	Shibin Biji Thomas
•	Jenil Savalia
•	Vrushabh Bodarya
•	Sarvesh Waghmare
________________________________________
🙏 Acknowledgements
•	Spotify Developer API
•	AWS Docs
•	Snowflake Docs

