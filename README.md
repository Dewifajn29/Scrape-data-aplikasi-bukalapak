# Scrape-data-aplikasi-bukalapak
1). 1. Download and Install Google Play Scraper Package
pip install google-play-scraper
![Screenshot_2024-10-01-08-42-51-267_com android chrome](https://github.com/user-attachments/assets/871c90be-cf29-4e85-8d41-b0c7f87f96a2)
2). Import required packages
from google_play_scraper import app
import pandas as pd
import numpy as np
![IMG_20241001_131250](https://github.com/user-attachments/assets/d8837782-d8fc-4644-8121-9a7a203be96a)
3).3. Find the App Id in Google Play Store and scrape
Bisa dilihat dari URL yang akan di ambil datanya, karena saya akan ambil dari Bukalapak maka
'com.bukalapak.android' .
#Scrape desired number of reviews
#Run kode ini jika ingin scrape data dengan jumlah tertentu. Ganti (misal, ingin scrape sejumlah
1000, maka ganti kode , count = 1000 )
from google_play_scraper import Sort, reviews
result, continuation_token = reviews(
'com.bukalapak.android',
lang='id', # defaults to 'en'
country='id', # defaults to 'us'
sort=Sort.NEWEST, # defaults to Sort.MOST_RELEVANT you can use Sort.NEWEST to get
newst reviews
count=1000, # defaults to 1000
filter_score_with=None # defaults to None(means all score) Use 1 or 2 or 3 or 4 or 5 to select
certain score
)![IMG_20241001_131450](https://github.com/user-attachments/assets/ca951da5-524f-4fe3-8b89-03402eb88e2d)
4).Put the Reviews into Pandas DataFrame
# Assuming 'result' from previous cells contains the review data
df_busu = pd.DataFrame(np.array(result), columns=['ulasan'])
# Replace 'gabung', 'daftar', and 'kepala' with their correct Pandas equivalents
# Assuming you want to expand the 'ulasan' column into separate columns
df_busu = pd.concat([df_busu, pd.DataFrame(df_busu['ulasan'].tolist())], axis=1)
# Display the first few rows of the DataFrame
df_busu.head()
![IMG_20241001_131612](https://github.com/user-attachments/assets/a9b731c7-e60b-4739-84e9-50408c7b3fb2)
5). Jumlah data yang akan didapat
len(df_busu.index) #hitung jumlah data yang kita dapatkan
Output: 1000
![IMG_20241001_092122](https://github.com/user-attachments/assets/6b54116f-6d9f-4d89-b680-975438f7a854)
6. Filter variabel
df_busu[['userName', 'score','at', 'content']].head() #preview userName, rating, date-time, and
reviews only
![IMG_20241001_092452](https://github.com/user-attachments/assets/81e77d8c-2072-4a38-8e59-a46456cf2fea)
7) Simpan Variabel dan download data
my_df = sorted_df[['userName', 'score','at', 'content']] #get userName, rating, date-time, and
reviews only
my_df.to_csv ( "scrapped_bukalapak.csv" , index = False ) #Simpan file sebagai , untuk
mengunduh: klik ikon folder di sebelah kiri. file csv seharusnya ada di sana
![IMG_20241001_094913](https://github.com/user-attachments/assets/0351d5c8-eee5-4e47-8569-6fb99762e5b9)
![IMG_20241001_094953](https://github.com/user-attachments/assets/056fea67-4485-453b-bcf8-54909bb59f3d)
