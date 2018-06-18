
### Lab Questions


1. [Link Scraping](#q1) Write a function to collect the links to each of the song pages from a given artist page.
2. [Text Scraping](#q2) Write a secondary function that scrapes the lyrics for each song page.
3. [Combining Parts](#q3) Create a script using your two functions above to scrape all of the song lyrics for a given artist.
4. [Visualizing](#q4) Generate two bar graphs to compare lyrical changes for the artist of your chose. For example, the two bar charts could compare the lyrics for two different songs or two different albums.

**Extension:**
Think about how you structured the data from your web scraper. Did you scrape the entire song lyrics verbatim? Did you simply store the words and their frequency counts, or did you do something else entirely? List out a few different options for how you could have stored this data. What are advantages and disadvantages of each? Be specific and think about what sort of analyses each representation would lend itself to.

### Question 1  <a id="q1"></a>
Write a function to collect the links to each of the song pages from a given artist page.


```
#Starter Code

from bs4 import BeautifulSoup
import requests


url = '' #Put the URL of your AZLyrics Artist Page here!

html_page = requests.get(url) #Make a get request to retrieve the page
soup = BeautifulSoup(html_page.content, 'html.parser') #Pass the page contents to beautiful soup for parsing


#The example from our lecture/reading
data = [] #Create a storage container
for album_n in range(len(albums)):
    #On the last album, we won't be able to look forward
    if album_n == len(albums)-1:
        cur_album = albums[album_n]
        album_songs = cur_album.findNextSiblings('a')
        for song in album_songs:
            page = song.get('href')
            title = song.text
            album = cur_album.text
            data.append((title, page, album))
    else:
        cur_album = albums[album_n]
        next_album = albums[album_n+1]
        saca = cur_album.findNextSiblings('a') #songs after current album
        sbna = next_album.findPreviousSiblings('a') #songs before next album
        album_songs = [song for song in saca if song in sbna] #album songs are those listed after the current album but before the next one!
        for song in album_songs:
            page = song.get('href')
            title = song.text
            album = cur_album.text
            data.append((title, page, album))
data[:2]
```




    1



### Question 2  <a id="q2"></a>
Write a secondary function that scrapes the lyrics for each song page.


```
#Remember to open up the webpage in a browser and control-click/right-click and go to inspect!
from bs4 import BeautifulSoup
import requests

#Example page
url = 'https://www.azlyrics.com/lyrics/lilyallen/sheezus.html'


html_page = requests.get(url)
soup = BeautifulSoup(html_page.content, 'html.parser')
soup.prettify()[:1000]
```




    '<!DOCTYPE html>\n<html lang="en">\n <head>\n  <meta charset="utf-8"/>\n  <meta content="IE=edge" http-equiv="X-UA-Compatible"/>\n  <meta content="width=device-width, initial-scale=1" name="viewport"/>\n  <meta content=\'Lyrics to "Sheezus" song by Lily Allen: Been here before, so I’m prepared Not gonna lie though, I’m kinda scared Lace up my gloves, I’m goin...\' name="description"/>\n  <meta content="Sheezus lyrics, Lily Allen Sheezus lyrics, Lily Allen lyrics" name="keywords"/>\n  <meta content="noarchive" name="robots"/>\n  <meta content="//www.azlyrics.com/az_logo_tr.png" property="og:image"/>\n  <title>\n   Lily Allen Lyrics - Sheezus\n  </title>\n  <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.4/css/bootstrap.min.css" rel="stylesheet"/>\n  <link href="//www.azlyrics.com/bsaz.css" rel="stylesheet"/>\n  <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->\n  <!--[if lt IE 9]>\r\n<script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script'



### Question 3 <a id="q3"></a>
Create a script using your two functions above to scrape all of the song lyrics for a given artist.



```
#Use this block for your code!
```

### Question 4 <a id="q4"></a>
Generate two bar graphs to compare lyrical changes for the artist of your chose. For example, the two bar charts could compare the lyrics for two different songs or two different albums.
