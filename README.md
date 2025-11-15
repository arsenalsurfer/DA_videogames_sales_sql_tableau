# Video Game Sales Analysis

![1_Dashboard_1.png](/images/2_Dashboard_1.png)
![1_Dashboard_2.png](/images/2_Dashboard_2.png)

## Introduction

The video game industry is a rapidly growing market with diverse genres and platforms. Analyzing sales data helps identify top-performing games, regional trends, and consumer preferences. This analysis aims to uncover patterns in sales across genres, platforms, and regions, providing insights to guide development, marketing, and investment decisions.

### Dashboard Link

My final dashboard is in [Videogames_sales_url](https://public.tableau.com/views/videogame_BI/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link).

### Skills Used

The following skills and tools are used for analysis:

- **Extract**: CSV file type
  - ![0_CSV.png](/images/0_CSV.png)
- **Transform**: postgreSQL, Dvbeaver

  - Created Staging and Datawarehouse Schema
    - ![1_schema_creation.jpg](/images/1_schema_creation.jpg)
  - Data cleaning, one example:
    ```sql
    SELECT DISTINCT(platform) FROM sales;
    ```
  - Removal of Duplicates

    ```sql
    WITH duplicate_check AS (
    SELECT
    *,
    ROW_NUMBER() OVER(PARTITION BY ranking, game_name, platform, "year", genre, publisher, na_sales, eu_sales, jp_sales, other_sales, global_sales ORDER BY game_name) AS rn
    FROM sales
    )
    SELECT \* FROM duplicate_check WHERE rn > 1;
    ```

- **Load**: postgreSQL, Dvbeaver

  - Loaded the cleaned data to the videogames_dw (Data Warehouse)
    - ![3_upload_schema.png](/images/3_upload_schema.png)
    - ![4_upload_schema_view_data.png](/images/4_upload_schema_view_data.png)

- **Load Visualization BI**: Tableau
  - Performed Business Intelligence using Tableau
    - ![5_BI.png](/images/5_BI.png)

## Dashboard Build

### 📉 Charts

#### 📊 Top 10 Games Global by Total Revenue

![6_sheet_top10_global.png)](/images/6_sheet_top10_global.png)

### 💡Insights

- Wii Sports leads by a large margin due to being bundled with the Wii console.

- GTA V ranks second, showing strong long-term sales from multi-platform releases and GTA Online.

- Nintendo dominates the top 10 with 7 titles, proving strong franchise loyalty and evergreen game appeal.

- Classic games like Super Mario Bros. and Tetris still sell globally even decades later.

- Sales drop sharply after the top 3, showing a few breakout hits followed by steady performers.

#### 📊 Top 10 Games in Other Regions (Australia, Asia, South America) by Total Revenue

![7_sheet_top10_others.png)](/images/7_sheet_top10_others.png)

### 💡Insights

- GTA: San Andreas ranks #1 with $10.72M, showing very strong popularity in emerging markets.

- Wii Sports and GTA V also perform well, proving these titles have broad global appeal beyond major Western regions.

- Racing games (Gran Turismo 4) and soccer games (FIFA, Pro Evolution) appear in the top spots, highlighting strong interest in sports and racing genres in these regions.

- Multiple Call of Duty titles appear but at lower sales levels, suggesting shooters are popular but not dominant in these markets.

#### 📊 Top 10 Games in North America by Total Revenue

![8_sheet_top10_NA.png)](/images/8_sheet_top10_NA.png)

### 💡Insights

- Wii Sports leads strongly with $41.49M, showing the huge impact of Wii’s popularity in North America.

- Classic Nintendo titles like Super Mario Bros., Duck Hunt, and Tetris dominate the top ranks, reflecting strong nostalgia and long-term franchise loyalty.

- GTA V also performs well, highlighting widespread appeal across different console generations.

- Shooter titles like Call of Duty appear in the top 10 but lower in ranking, showing popularity but not top dominance.

- Overall, North America shows a strong preference for Nintendo classics, family-friendly titles, and long-lasting franchises.

#### 📊 Top 10 Games in Europe by Total Revenue

![9_sheet_top10_EU.png](/images/9_sheet_top10_EU.png)

### 💡Insights

- Dominance of Top 2: Wii Sports and Grand Theft Auto V (GTA V) hold a significant lead, with sales of $29.02M and $23.04M respectively. Their combined sales far surpass the rest of the list.

- Nintendo's Strong Presence: Two of the top ten games are Nintendo's console-specific titles: Wii Sports (No. 1) and Wii Sports Resort (No. 9).

- Sports/Racing Popularity: The list is heavily dominated by Sports and Racing genre titles, including three FIFA games (FIFA 15, FIFA 16, FIFA 14), Wii Sports, Wii Sports Resort, and Mario Kart Wii.

- Call of Duty Consistency: The Call of Duty franchise has two titles in the top ten (Modern Warfare 3 and Black Ops II), demonstrating consistent shooter genre popularity in the European market.

- Mid-to-Lower Tier Closeness: The games ranked 3rd through 10th have relatively close sales figures, all clustering between $11.00M and $12.88M.

#### 📊 Top 10 Games in Japan by Total Revenue

![10_sheet_top10_JP.png](/images/10_sheet_top10_JP.png)

### 💡Insights

- Pokemon Domination: The chart shows an overwhelming preference for the Pokémon franchise. Six out of the top ten best-selling games are Pokémon titles.

- Top Title Lead: Pokemon Red/Pokémon Blue is the clear leader with $10.22M in sales, maintaining a substantial gap of over $3M from the second-place title.

- Nintendo's Strong Hold: Every single game on the list is either a Nintendo-published title (like Mario and Animal Crossing) or a title closely associated with Nintendo platforms (like Dragon Quest VII and Tetris), highlighting Nintendo's historic significance in the Japanese market.

- Enduring Classics: The list is composed primarily of older, well-established franchises and titles (Pokemon, Super Mario Bros., Tetris, Dragon Quest), suggesting a strong loyalty to classic games in Japan.

- Genre Variety (Within Limits): While Pokémon (RPG) dominates, the list includes successful titles from different genres: Platformer (Super Mario Bros.), Puzzle (Tetris), and Life Simulation (Animal Crossing).

#### 📊 Global Total Revenue Every 5 Years

![11_sheet_recenue_5years.png](/images/11_sheet_recenue_5years.png)

### 💡Insights

- Explosive Growth to Peak (1980–2005): Revenue shows a rapid, accelerating growth phase, starting at $143M in 1980 and peaking at a high of $2.99B (Billion) in 2005. This 25-year period represents the zenith of the market as defined by this sales category.

- Catastrophic Decline (2005–2020): Following the 2005 peak, the revenue plummeted sharply and persistently:

  - By 2010, revenue fell to $2.18B.

  - The sharpest drop occurred between 2010 and 2015, plunging to just $335M.

  - The line ends at a minimal $0M (or near-zero) by 2020.

- Implied Market Shift: The near-total collapse of the revenue category by 2020 strongly suggests that the market segment being measured—likely explicit sales (one-time purchases, particularly physical media)—became largely obsolete due to the industry's mass migration to digital distribution, subscription services (like Game Pass), and free-to-play models.

#### 📊 Sales By Year (Trend KPI) with Year Over Year Growth

![12_sheet_yoy.png](/images/12_sheet_yoy.png)

### 💡Insights

- Peak Period: The market experienced its highest sales, peaking in 2008 at 678.9M.

- The Crash (2009–2020): Following 2008, sales entered a steep, continuous decline, falling to a near-zero low of 0.1M by 2020.

- YoY Confirms Collapse: Year-Over-Year (YoY) growth figures confirm the decline with consistent negative numbers, culminating in a -100% YoY crash in 2020.

- Market Shift: The collapse aligns with the industry's shift from physical/explicit purchases to digital distribution, subscriptions, and microtransactions, which are not captured by this traditional sales metric.

- 2022 Anomaly: A sudden, massive sales spike to 48.0M occurred in 2022 (with +4800% YoY growth), which is highly unusual after the revenue stream's apparent demise, suggesting a potential change in data definition or a specific, massive one-off event.

#### 📊 Which Gaming Console Do Most Customers Use?

![13_sheet_console.png](/images/13_sheet_console.png)

### 💡Insights

- Legacy Dominance: The top three consoles are older generations: DS (13.03%), PS2 (13.02%), and PS3 (8.01%). Their combined usage accounts for over one-third of the total.

- Widespread Usage: The market is very fragmented, but consoles from Nintendo and Sony account for the vast majority of the top slices.

- Top 5 Platforms: The top five consoles by usage share are:
  1. DS (13.03%)
  2. PS2 (13.02%)
  3. PS3 (8.01%)
  4. Wii (7.98%)
  5. X360 (7.62%)

#### 📊 Number of Purchase By Genre

![14_sheet_pcg_genre.png](/images/14_sheet_pcg_genre.png)

### 💡Insights

- Top Genres: Action (19.63%), Sports (14.92%), and Shooter (11.63%) historically drove the majority of explicit sales revenue (over 46% combined).

- RPG/Platforming: These genres also hold significant shares, reinforcing their importance before the market shift.

- Europe: Highly dominated by Action/Adventure (GTA V), Sports (FIFA), and Shooters (Call of Duty).

- Japan: Overwhelmingly dominated by RPGs (Pokémon holds 6 of the Top 10 spots) and Nintendo-associated classics.

#### 📊 Top 10 Publisher by Total Global Sales

![16_sheet_top_publisher.png](/images/16_sheet_top_publisher.png)

### 💡Insights

- Nintendo's Huge Lead: Nintendo is the dominant publisher by Total Global Sales, recording $1,786M in explicit sales. This figure is significantly higher than its competitors, confirming its power in the physical/explicit sales era.

- Strong Runner-up: Electronic Arts (EA) is a distant, but strong, second with $1,110M. EA's focus on annualized sports titles (like FIFA) and multi-platform blockbusters likely drove this high figure.

- Console Manufacturer Presence: Both major console manufacturers appear high on the list: Sony Computer Entertainment ($687M) and Nintendo ($1,786M), indicating a massive advantage in publishing for their own hardware.

- Action/Adventure Focus: Activision ($727M) and Take-Two Interactive ($600M) hold high positions, reflecting the high explicit sales volume of their key franchises like Call of Duty and Grand Theft Auto, which dominate the European Top 10 list.

## Conclusion

I created this dashboard to showcase insights into total sales globally across various regions. Utilizing data from my SQL and Tableau skills, this dashboard allows us to show the sales of the video game industry. Exploring what games are in demand in different region, showing what console are most gamers using, and top publishers who release successful games.
