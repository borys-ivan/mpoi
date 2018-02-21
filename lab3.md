1.	За допомогою download.file() завантажте любий excel файл з порталу http://data.gov.ua та зчитайте його (xls, xlsx – бінарні формати, тому встановить mode = “wb”. Виведіть перші 6 строк отриманого фрейму даних.

```r
>install.packages("rJava")

>library(rJava)

>install.packages("xlsx", dep = T)

>library("xlsx")

> download.file("http://data.gov.ua/file/181885/download?token=P84xWbWs", destfile = "doc.xls", mode = "wb")
пробую URL 'http://data.gov.ua/file/181885/download?token=P84xWbWs'
Content type 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet' length 27671 bytes (27 KB)
downloaded 27 KB

> doc <- read.xlsx("doc.xls", sheetIndex = 1, startRow=6, as.data.frame=TRUE, encoding = "UTF-8")
> 

> head(doc)
  X2.              поточний.ремонт.та.заправка.картріджів
1  3.      консультації з питань програмного забезпечення
2  4. за теплопостачання, електроененргію, водопостачання
3  5.                                          канцтовари
4  6.                                               папір
5  7.                                           стат.дані
6  8.                                         БМП, нетбук
                          ФОП.Пігович.Григорій.Йосипович
1                             ФОП Малий Дмитро Борисович
2 КП "Управління будинками Кіровоградської міської ради"
3                                        ПП Дорошко Г.Ф.
4                          ФОП Лелека Людмила Григорівна
5                                          Облстатистика
6                                     ФОП "Кадигроб Я.С.
      дог..4.від.25.01.2017   X2510
1    дог.928 від 22.02.2017  2300.0
2      дог.6/к від 01.02.17 43900.0
3      дог.1 від 01.02.2017  6708.5
4  дог.19 від 01.02.2017 р.  3700.0
5    дог. 10 від 16.02.2017  5460.0
6 фоп-000012 від 01.02.2017 20000.0
> 
```


2.	За допомогою download.file() завантажте файл getdata_data_ss06hid.csv за посиланням https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv та завантажте дані в R. Code book, що пояснює значення змінних знаходиться за посиланням https://www.dropbox.com/s/dijv0rlwo4mryv5/PUMSDataDict06.pdf?dl=0  Необхідно знайти, скільки property мають value $1000000+

```r
> download.file("https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv", destfile = "doc.csv")
trying URL 'https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv'
Content type 'text/csv' length 4246554 bytes (4.0 MB)
downloaded 4.0 MB
> data <- read.csv("doc.csv")
> values <- doc$VAL
> res <- lapply(values, function(x) if (!is.na(x) && x==24) TRUE else NA)
> length(res[!is.na(res)])
[1] 53
```

3.	Зчитайте xml файл за посиланням http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml Скільки ресторанів мають zipcode 21231?
```r
> install.packages("XML")
Устанавливаю пакет в ‘C:/Users/borys/OneDrive/Документи/R/win-library/3.4’
(потому что ‘lib’ не определено)
пробую URL 'https://cran.cnr.berkeley.edu/bin/windows/contrib/3.4/XML_3.98-1.10.zip'
Content type 'application/zip' length 4325149 bytes (4.1 MB)
downloaded 4.1 MB

пакет ‘XML’ успешно распакован, MD5-суммы проверены

Скачанные бинарные пакеты находятся в
        C:\Users\borys\AppData\Local\Temp\Rtmpi8L6U9\downloaded_packages
> library("XML")
> 
> library("XML")
> url <- "http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml"
> doc <- xmlTreeParse(url,useInternal=TRUE)
> rootNode <- xmlRoot(doc)
> length(xpathApply(rootNode, '//row/row/zipcode[text()="21231"]'))
[1] 127
```
