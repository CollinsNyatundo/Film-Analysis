# Film-Analysis

## Project Overview  
A new film studio wants data-driven guidance on what types of movies to make. This analysis combines box-office and movie metadata to identify which film genres yield the strongest box-office returns. We merge data from major sources (Box Office Mojo, TheMovieDB, The Numbers) to profile genres, budgets, and release patterns. Our goal is to highlight opportunities for high-revenue films (e.g. top grossing genres, seasonal timing) to inform the studio’s production strategy ([Genres Movie Breakdown 1995-2025](https://www.the-numbers.com/market/genres#:~:text=1%20Adventure%201%2C202%20%2467%2C192%2C872%2C334%209%2C235%2C222%2C219,17)).

## Business Problem  
The core question is: **Which genres and release strategies will maximize box-office success?**  
In other words, we aim to identify the film genres with the highest returns and optimal release windows. Key factors include total gross vs. budget (ROI), domestic vs. foreign performance, seasonal trends, and audience ratings. Understanding these will help the studio prioritize film projects (genres, budgets, release dates) that historically perform best at the box office.

## Data Sources  
We use the following primary datasets (CSV files):  
- **Box Office Mojo** (`bom.movie_gross.csv`): Domestic and foreign gross for movies from 1977–2016.  
- **The Movie Database (TMDB)** (`tmdb.movies.csv`): Metadata on movies (genres, release dates, popularity, etc.).  
- **The Numbers** (`tn.movie_budgets.csv`): Production budgets and gross (domestic and worldwide).  
- **Merged Dataset** (`merged_df.csv`): Cleaned and merged master table (budget, gross, genre, etc., by movie).  

Each CSV is described in the analysis notebook. Together they allow computation of total grosses, genre breakdowns, ROI, and time trends for films.

## Methodology  
- **Data Cleaning & Merging:** We load and clean each CSV (parse dates, handle missing values, parse genre lists) and merge on movie titles.  
- **Exploding Genres:** Each movie can belong to multiple genres. We “explode” the genres column so each movie-genre pair is a row, enabling per-genre aggregation.  
- **Feature Engineering:** We compute new fields such as *worldwide_gross* (domestic+foreign), *ROI* = (gross–budget)/budget, and *release_month*. We also compute the number of movies produced per genre each year.  
- **Visualization & Statistics:** Using Python (pandas, matplotlib, seaborn), we generate charts to explore: total gross by genre, domestic vs. foreign gross by genre, gross by release month, average audience rating by genre, ROI by genre, and production trends over time. Basic stats (sums, means, counts) and sorting highlight top genres and patterns.

## Key Insights  
- **High-Grossing Genres:** Adventure, Action, and Animation dominate worldwide revenue ([Genres Movie Breakdown 1995-2025](https://www.the-numbers.com/market/genres#:~:text=1%20Adventure%201%2C202%20%2467%2C192%2C872%2C334%209%2C235%2C222%2C219,17)). The bar chart below shows *total worldwide gross by genre*. Adventure films (e.g. *Avatar*, *Incredibles 2*) lead with the highest lifetime grosses. This aligns with industry data (The Numbers reports Adventure with ~$67B worldwide) ([Genres Movie Breakdown 1995-2025](https://www.the-numbers.com/market/genres#:~:text=1%20Adventure%201%2C202%20%2467%2C192%2C872%2C334%209%2C235%2C222%2C219,17)). Studios may focus on blockbuster franchises in these genres.  

  ![Worldwide Gross by Genre](images/worldwide_gross.png) *Figure: Total worldwide box-office gross by genre (2010–2016). Adventure and Action films gross far more than other genres.*  

- **Domestic vs. Foreign Splits:** Many genres earn much more overseas than domestically. The chart below compares domestic and international gross by genre. For example, Action and Adventure have large foreign markets, while genres like Documentary earn a higher share domestically. Notably, Adventure’s domestic gross (~ $9.2B) is dwarfed by its foreign gross (~ $57.9B) ([Genres Movie Breakdown 1995-2025](https://www.the-numbers.com/market/genres#:~:text=1%20Adventure%201%2C202%20%2467%2C192%2C872%2C334%209%2C235%2C222%2C219,17)). This suggests focus on international appeal for high-grossing genres.  

  ![Domestic vs International Gross by Genre](images/domestic_vs_foreign.png) *Figure: Box office gross by genre, split into domestic (blue) and international (green) markets. High-grossing genres (Action, Adventure) rely heavily on foreign box-office.*  

- **Seasonal Release Effects:** Summer and holiday seasons see higher grosses. Our analysis of gross by release month (below) shows peaks in June–August and in December. This matches historical trends: summer releases often capture summer vacation audiences, and holiday blockbusters drive year-end revenue (e.g. *Incredibles 2* grossed $602M in summer 2018 ([Summer Box Office - Box Office Mojo](https://www.boxofficemojo.com/season/summer/?grossesOption=calendarGrosses#:~:text=2019%20%244%2C320%2C749%2C661,482%2C853%2C070%2010.8))). The studio should time big releases for peak seasons.  

  ![Worldwide Gross by Release Month](images/gross_by_month.png) *Figure: Total worldwide gross by release month. Blockbusters released in summer (June–August) and December generally earn higher grosses.*  

- **Audience Ratings by Genre:** Some genres consistently earn higher audience ratings. The chart below shows average TMDB viewer rating by genre. Family and Animation films tend to have higher average ratings (often G/PG content), while genres like Horror and Action have more mixed reviews. High ratings can indicate strong audience satisfaction; combining high-gross potential with higher ratings (e.g. Animation, Fantasy) may be a sweet spot.  

  ![Average Viewer Rating by Genre](images/average_rating.png) *Figure: Average audience rating (TMDB) by genre. Family-oriented genres (e.g. Animation) have higher average scores, which may support strong word-of-mouth.*  

- **Genre Trends Over Time:** The production volume of certain genres has changed over time. The line chart below shows the count of films released per genre by year. Drama and Comedy have the most titles overall, but their production grew more slowly. Notably, genres like Documentary and Animation have ramped up production in recent years. Understanding supply trends helps gauge competition and audience interest over time.  

  ![Movies Produced per Genre Over Time](images/genres_over_years.png) *Figure: Number of movies released per genre by year. Drama and Comedy have the most releases, while Documentary and Animation show growth in recent years.*  

Each insight above is supported by the chart shown. (Sources: Our analysis of combined industry datasets; The Numbers box-office data ([Genres Movie Breakdown 1995-2025](https://www.the-numbers.com/market/genres#:~:text=1%20Adventure%201%2C202%20%2467%2C192%2C872%2C334%209%2C235%2C222%2C219,17)); Box Office Mojo seasonal records ([Summer Box Office - Box Office Mojo](https://www.boxofficemojo.com/season/summer/?grossesOption=calendarGrosses#:~:text=2019%20%244%2C320%2C749%2C661,482%2C853%2C070%2010.8)).)

## Getting Started  
To run this project locally:  
1. **Clone the repository:** `git clone https://github.com/CollinsNyatundo/Film-Analysis.git && cd Film-Analysis`  
2. **Install dependencies:** Run `pip install -r requirements.txt` (or manually install common libraries: `pandas, numpy, matplotlib, seaborn`, etc.).  
3. **Open the notebook:** Launch `index.ipynb` in Jupyter Notebook or JupyterLab to reproduce the analysis and charts.  
4. **View output:** The pre-generated charts are saved in the `images/` folder for embedding; you can re-run the notebook to regenerate them.  

## Project Structure  
- **README.md:** This file (project overview and documentation).  
- **index.ipynb:** Jupyter notebook containing data analysis code and visualizations.  
- **bom.movie_gross.csv:** Box Office Mojo domestic/foreign gross data.  
- **tmdb.movies.csv:** TMDB movie metadata (genre lists, release dates, ratings).  
- **tn.movie_budgets.csv:** The Numbers production budgets and grosses.  
- **merged_df.csv:** Combined, cleaned master dataset (result of merging the above).  
- **images/**: Folder (added) containing `.png` charts extracted from the notebook, referenced above.  
- **LICENSE:** Open-source license file.  

## Contributing  
Contributions are welcome. If you find issues or have ideas (new analyses, updated data), please open an issue or submit a pull request. For major changes, please discuss via GitHub issues first. We follow standard [Contributor Covenant](https://www.contributor-covenant.org/) guidelines: be respectful and include tests or notebooks that validate your additions.

## License  
This project is open-source under the MIT License. See `LICENSE` for full terms.

