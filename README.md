### Table of Contents

1. [Installation](#installation)
2. [Project Motivation](#motivation)
3. [File Descriptions](#files)
4. [Results](#results)
5. [Licensing, Authors, and Acknowledgements](#licensing)

## Installation <a name="installation"></a>
Libraries used in the notebooks are as follows:

* sklearn  
* pandas  
* numpy  
* matplotlib.pyplot  
* seaborn
* plotly.express
* pandas.plotting
* lightgbm
* Tensorflow
* Datetime
* Beautifulsoup4
* requests


## Project Motivation <a name="motivation"></a>

>"In 2019, the football transfer market reached unprecedented levels both in terms of the number of transfers and the amount spent on fees.."

*James Kitching,Director of Football Regulator*


Growing football industry can cause clubs spend higher than what they possibly win. UEFA brought out Financial Fair Play Regulations to audit the expenses of clubs and prevent them to collapse financially.UEFA explained those regulations as improving the overall financial health of European club football.To follow the rules in the regulation, valuation of a player becomes crucial either to sell or to buy.

Fifa published a [report](https://resources.fifa.com/image/upload/global-transfer-market-report-2019-men.pdf?cloudid=x2wrqjstwjoailnncnod#:~:text=Of%20the%20total%20amount%20spent,USD%202.7%20million%20in%202019.) in 2019, showing the statistics about transfers in 2019. In the report, it is highlighted many times that football teams can give lots of money to be in the competition with others.

<figure>
  <img src="Medium Post/Year_vs_Transfers.JPG" alt="Spending on transfer fees by year (USD billion)" title="Spending on transfer fees by year (USD billion)" />
  <figcaption><center>Spending on transfer fees by year (USD billion)</center></figcaption>
</figure>


Above chart shows how fast the football transfer industry is growing.It reached ~7.5 billion USD in 2019.  

<figure>
  <img src="Medium Post/NOF_Transfers_Avg_Fee.JPG" alt=": Number of transfers with fees and average transfer fee by year" title=": Number of transfers with fees and average transfer fee by year" />
  <figcaption><center>Number of transfers with fees and average transferfee by year (USD billion)</center></figcaption>
</figure>

\
Above table shows the numbers of transfers are increasing, average fees are increasing as well as years pass.

What makes a football player expensive? Can the fee be predicted? I decided to go on these questions and by using the world-wide known website "transfermarkt" I built two  models  on transfer fees. I tried lightgbm and keras to predict the values. 
I started firstly scraping transfer data from the [transfermarkt](https://wwww.transfermarkt.com)


## File Descriptions <a name="files"></a>
There are 3 folders in repository, and subfolders in each folder.

####  0.Web scraping

Here is the part where I scrape the tranfermarkt.com. In each subfolder, you can find related
scraping code, and if possible data.

  - ###### 0.Transfers

      Transfers are the main table in which there are all the transfer history of all leagues that transfermarkt has. I decided to scrape all the transfers from the [link](https://www.transfermarkt.com/transfers/transfertagedetail/statistik/top/plus/0/galerie/0?land_id_ab=&land_id_zu=&leihe=&datum=2016-01-01).

      I looped from  all the pages and dates from 2016 to 2020. Finally i eliminated loans & Free transfers to get paid transfers

  - ###### 1.Transfer Details

      Transfer details are the source of the transfer history of a player. Also in each transfer, specific info is provided such as age at the time of transfer, market value at the time of transfer, remaining contract .The transfer detail website for a player can be reached from [here](https://www.transfermarkt.com/jonas-hofmann/transfers/spieler/7161/transfer_id/1391587).

      I looped for all the players in paid transfer dataset.I also created some other features like Number of transfers in transfer history, Avg Market Value, Total Fee, Avg Fee etc. I also created flag features such as: Country_Change_Flag, League_Change_Flag,League_Tier_Up_Flag,League_Tier_Down_Flag.I also created another dataset which shows the team a player played in each date.

  - ###### 2.Player Profiler

      Player profile is providing the general information about the footballer such as citizenship, height,preferred foot, positions etc. You can reach a player's profile page from [here](https://www.transfermarkt.com/jonas-hofmann/profil/spieler/7161).

  - ###### 3.Stats Scraper

     In transfermarkt, stats are given in each season, however a  footballer can change his club during the season. Since I wanted to get the stats before the transfers, I could not use the stats of website, so i decided to create my own features by scraping all the matches a footballer played. The scraping code is available in github, however dataset is not available, since it's bigger than github's limit.The matches are available in the [link](https://www.transfermarkt.com/jonas-hofmann/leistungsdaten/spieler/7161/plus/1?saison=2016)

  - ###### 4.National Stats Scraper

  A football player can also play for his national team. National team stats can  also be  helpful to predict transfer fee. Here the difficult part of this dataset is to get the matches of players, since they can play multiple under levels also like Under 21, Under 19 etc. Here is the [link](https://www.transfermarkt.com/jonas-hofmann/nationalmannschaft/spieler/7161/verein_id/3817/hauptwettbewerb//wettbewerb_id//start/1999-10-07/ende/2020-11-17/nurEinsatz/0/plus/1) of national matches. I first scraped the clubs in "national_urls_scraper.ipynb" then I looped for different national level clubs and for all players to create dataset.

  - ###### 5.Achievements
  Finally, achievements are also very important for predicting transfer fee. The fee can increase if the player wins top goal scorer awards, or cups. I decided to scrape achievements from the [link](https://www.transfermarkt.com/jonashofmann/erfolge/spieler/7161)

####  1.Feature Engineering

In Feature engineering folders, i created features for stats, national stats and achievements.
In notebook
* **Stats_Features.ipynb** &#8594; Created features about club matches statistics.
  I created features like , how many times of a player played,avg minutes,  goals, assists, benched times, substituted games,injuries,suspensions,match points, etc in last 5,10,20,30 games before transfer date. I saved the features as *Stats_Features_All.pkl*

* **National_Stats_Feature.ipynb** &#8594; Created features about national club matches statistics.I created features like , how many times of a player played,avg minutes,  goals, assists, benched times, substituted games,injuries,suspensions,match points, etc in last 5,10,20,30 games before transfer date. I saved the features as *National_Stats_Features_All.pkl*


* **achievements_features.ipynb** &#8594; I created number of achievements and number of distinct achievements of a player as features to be used in the prediction model.I saved the features as *achievement_features.pkl*

####  2.Modelling

**Market_Value_Model.ipynb** is the notebook in this folder. In this notebook, i merged datasets, processed the data for modelling. I run lightgbm and keras for predicting transfer fees of football players.


## Results<a name="results"></a>
Main findings can be found in [this](https://medium.com/@yahyayavuz1/i-ve-never-seen-a-bag-of-money-score-a-goal-12cdc5cae4e1) medium post


## Licensing, Authors, Acknowledgements<a name="licensing"></a>
All the data is property of transfermarkt. Any use of the data and model should be notified to the author. All data are scraped from [Transfermarkt](https://wwww.transfermarkt.com)
 according to their [terms of use](https://www.transfermarkt.com/intern/anb).
