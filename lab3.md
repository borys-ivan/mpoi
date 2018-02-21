1.За допомогою download.file() завантажте любий excel файл з порталу http://data.gov.ua та зчитайте його (xls, xlsx – бінарні формати, тому встановить mode = “wb”. Виведіть перші 6 строк отриманого фрейму даних.

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
