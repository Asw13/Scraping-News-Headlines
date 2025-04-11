## *📰 News Archive Scraper (Times of India)*
This project is a robust web scraping pipeline that collects daily news headlines from Times of India archives, extracts metadata including publish and update timestamps, and stores the structured data into a MySQL database.

## *📌 Features*
✅ Scrapes news headlines and links from archive pages (2013–2025)

🕒 Extracts Last Updated timestamps from each article

⚡ Supports multi-threaded scraping for speed and efficiency

💾 Saves data to a MySQL database

📁 Optionally exports data to CSV for local storage

# *🔧 Project Structure*
1. get_news_data()
Scrapes headlines and URLs from a given archive page based on:

python
Copy
Edit
get_news_data(year, month, day, starttime)
Constructs the archive URL using date parameters

Parses and extracts headline text and article links

Returns a Pandas DataFrame: Date, Headline, Link

2. Date Range Scraper with ThreadPoolExecutor
Efficiently fetches news data from a date range:

python
Copy
Edit
start_date = date(2013, 1, 1)
end_date = date(2025, 1, 31)
Computes starttime for each day

Uses ThreadPoolExecutor to scrape multiple days in parallel

Stores valid news data into a list of DataFrames

3. get_last_updated_time()
Fetches Last Updated Date & Time from each news article link:

python
Copy
Edit
df_all_news["Last_Updated"] = df_all_news["Link"].apply(get_last_updated_time)
Looks for <time class="jsdtTime"> in each article

Appends timestamp as a new column

4. insert_into_mysql()
Saves the final DataFrame into a MySQL table:

python
Copy
Edit
insert_into_mysql(df_all_news)
Connects to MySQL using mysql.connector

Inserts records into a table News with:

Date, Headline, Link, Last_Updated

Uses executemany() for bulk insertion

# *🛠️ Requirements*
Python 3.x

Libraries:

requests

beautifulsoup4

pandas

mysql-connector-python

Install via:

bash
Copy
Edit
pip install requests beautifulsoup4 pandas mysql-connector-python
# *🗃️ Sample Output (CSV or MySQL Table)*
Date	Headline	Link	Last_Updated
2018-07-02	India to boost EV production	https://timesofindia.../article12345.cms	Jan 02, 2018, 11:45 PM IST
# *📌 To-Do / Enhancements*
 Add support for retrying failed dates

 Automatically create MySQL table if not exists

 Add command-line or UI interface

 Dockerize the scraper
