# myurlsutil
a utility to parse and process the iPad-generated MyUrls note

On my iPad I have created a note named MyUrls.  I have written a shortcut to save the URL of a page I am viewing into that MyUrls note -- appended with the date and time the URL is added to the MyUrls note.  This creates new lines the MyUrls note like the following:

```
https://www.digitalocean.com/community/tutorials/how-to-install-ruby-on-rails-with-rbenv-on-ubuntu-20-04 20220520.061533 
https://code.visualstudio.com/docs/remote/wsl-tutorial 20220520.061546 
https://www.jetbrains.com/help/ruby/how-to-use-wsl-development-environment-in-product.html 20220520.061600
```

When needed, I rename the MyUrls note (to something like "MyUrls - yyyymmdd") and create a new MyUrls note.

Then I create a new file in directory /Users/davidho/myurls/myurls/myurls-yyyymmdd-raw.txt and copy the text from note "MyUrls - yyyymmdd" to that new file.

```
dphmm2:myurls davidho$ pwd -P
/Users/davidho/myurls
dphmm2:myurls davidho$ ls
ant-research-20211129.txt	myurls-20210823-sortu.txt	myurls50b.txt
ant-research-20211129b.txt	myurls-20210823-sortuk2.txt	myurls51.txt
ant-research-20211129c.txt	myurls-20210922-nbl.txt		myurls51b.txt
ant-research-20211129d.txt	myurls-20210922-raw.txt		myurls52.txt
ant-research-20211129e.txt	myurls-20210922-sortk2.txt	myurls52b.txt
homeurls4.txt				myurls-20210922-sortu.txt	myurls53.txt
homeurls5.txt				myurls-20211128-raw.txt		myurls53b.txt
homeurls6.txt				myurls-20211128-sortuk2.txt	myurls54.txt
myurls-20210328.txt			myurls-20211207-raw.txt		myurls54b.txt
myurls-20210427.txt			myurls-20211207-sortuk2.txt	recenturls.txt
myurls-20210706.txt			myurls-20211214-raw.txt		recenturls2.txt
myurls-20210805-raw.txt		myurls-20211214-sortuk2.txt	recenturls3.txt
myurls-20210805-sortu.txt	myurls20200507.txt		recenturls4.txt
myurls-20210805-sortuk2.txt	myurls20200507b.txt		research-log4j2.txt
myurls-20210805.txt			myurls20200507c.txt		tomcat-20211124-sort.txt
myurls-20210819-raw.txt		myurls20200507d.txt		tomcat-20211124.txt
myurls-20210819-sortu.txt		myurls20200612.txt		tomcat-windows-account.txt
myurls-20210819-sortuk2.txt	myurls20200919.txt
myurls-20210823-raw.txt		myurls50.txt
dphmm2:myurls davidho$
```

Sometime I capture the same URL in the MyUrls note more than once.  Because the strings end with the date and time, each of the strings is unique, and running the command line "sort -u" will not eliminate the duplicates.  Also, there are blank lines between the URLs in the "raw" version of the file.  I want to leave all the lines in the "raw" version of the file, if only because they capture the time I spent researching a technical topic (even if I revisit the same URL more than once).  But I want to write a utility (in groovy) that can eliminate the duplicate entries.  

```
https://rubydoc.info/gems/elasticsearch-api/Elasticsearch/API/Actions 20220520.002514 
https://rubydoc.info/gems/elasticsearch-api/Elasticsearch/API/Actions 20220520.002645
```

But the following will at least get rid of the duplicate blank lines.  The first sort results in a list of URLs sorted by the name of the URL.  The second sort results in a list of URLs sorted by the date and time the URL was captured to the "MyUrls" note.

```
dphmm2:~ davidho$ sort -u      < myurls-20220520-raw.txt > myurls-20220520-sortu.txt
dphmm2:~ davidho$ sort -u -k 2 < myurls-20220520-raw.txt > myurls-20220520-sortuk2.txt
dphmm2:~ davidho$ ls -latr myurls*.txt | tail
-rw-r--r--@ 1 davidho  staff    4546 Jun 10  2019 myurls.txt
-rw-r--r--@ 1 davidho  staff    9572 Jun 11  2019 myurls2.txt
-rw-r--r--  1 davidho  staff    4677 Jun 11  2019 myurls3.txt
-rw-r--r--@ 1 davidho  staff  206926 Aug 15  2020 myurls4.txt
-rw-r--r--@ 1 davidho  staff  156404 May  9 06:37 myurls-20220509-raw.txt
-rw-r--r--@ 1 davidho  staff   33538 May 20 06:23 myurls-20220520-raw.txt
-rw-r--r--  1 davidho  staff   33189 May 20 06:36 myurls-20220520-sortu.txt
-rw-r--r--  1 davidho  staff   33189 May 20 06:36 myurls-20220520-sortuk2.txt
dphmm2:~ davidho$ 
```

```
sort -u      < myurls-20220509-raw.txt > myurls-20220509-sortu.txt
sort -u -k 2 < myurls-20220509-raw.txt > myurls-20220509-sortuk2.txt

sort -u      < myurls-20220520-raw.txt > myurls-20220520-sortu.txt
sort -u -k 2 < myurls-20220520-raw.txt > myurls-20220520-sortuk2.txt

dphmm2:~ davidho$ sort -u      < myurls-20220509-raw.txt > myurls-20220509-sortu.txt
dphmm2:~ davidho$ sort -u -k 2 < myurls-20220509-raw.txt > myurls-20220509-sortuk2.txt
dphmm2:~ davidho$ 
dphmm2:~ davidho$ sort -u      < myurls-20220520-raw.txt > myurls-20220520-sortu.txt
dphmm2:~ davidho$ sort -u -k 2 < myurls-20220520-raw.txt > myurls-20220520-sortuk2.txt
dphmm2:~ davidho$ 
dphmm2:~ davidho$ ls -latr myruls*.txt | tail
ls: myruls*.txt: No such file or directory
dphmm2:~ davidho$ 
dphmm2:~ davidho$ ls -latr myurls*.txt | tail
-rw-r--r--@ 1 davidho  staff    4546 Jun 10  2019 myurls.txt
-rw-r--r--@ 1 davidho  staff    9572 Jun 11  2019 myurls2.txt
-rw-r--r--  1 davidho  staff    4677 Jun 11  2019 myurls3.txt
-rw-r--r--@ 1 davidho  staff  206926 Aug 15  2020 myurls4.txt
-rw-r--r--@ 1 davidho  staff  156404 May  9 06:37 myurls-20220509-raw.txt
-rw-r--r--@ 1 davidho  staff   33538 May 20 06:23 myurls-20220520-raw.txt
-rw-r--r--  1 davidho  staff  154782 May 20 06:42 myurls-20220509-sortu.txt
-rw-r--r--  1 davidho  staff  154004 May 20 06:42 myurls-20220509-sortuk2.txt
-rw-r--r--  1 davidho  staff   33189 May 20 06:44 myurls-20220520-sortu.txt
-rw-r--r--  1 davidho  staff   33189 May 20 06:44 myurls-20220520-sortuk2.txt
dphmm2:~ davidho$
```



