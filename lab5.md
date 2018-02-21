```r
> install.packages("rvest")
Устанавливаю пакет в ‘C:/Users/borys/OneDrive/Документи/R/win-library/3.4’
(потому что ‘lib’ не определено)
--- Пожалуйста, выберите зеркало CRAN для использования в этой сессии ---
устанавливаю также зависимости ‘glue’, ‘stringi’, ‘jsonlite’, ‘mime’, ‘curl’, ‘openssl’, ‘R6’, ‘stringr’, ‘httr’, ‘selectr’, ‘magrittr’


пакет ‘glue’ успешно распакован, MD5-суммы проверены
пакет ‘stringi’ успешно распакован, MD5-суммы проверены
пакет ‘jsonlite’ успешно распакован, MD5-суммы проверены
пакет ‘mime’ успешно распакован, MD5-суммы проверены
пакет ‘curl’ успешно распакован, MD5-суммы проверены
пакет ‘openssl’ успешно распакован, MD5-суммы проверены
пакет ‘R6’ успешно распакован, MD5-суммы проверены
пакет ‘stringr’ успешно распакован, MD5-суммы проверены
пакет ‘httr’ успешно распакован, MD5-суммы проверены
пакет ‘selectr’ успешно распакован, MD5-суммы проверены
пакет ‘magrittr’ успешно распакован, MD5-суммы проверены
пакет ‘rvest’ успешно распакован, MD5-суммы проверены

Скачанные бинарные пакеты находятся в
        C:\Users\borys\AppData\Local\Temp\RtmpWIe5Fb\downloaded_packages
> 

>library(rvest)

> movie <- read_html("http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature")
> rank_data <- html_nodes(movie,'.text-primary')
> rank <- html_text(rank_data)
> rank
  [1] "1."   "2."   "3."   "4."   "5."   "6."   "7."   "8."   "9."   "10." 
 [11] "11."  "12."  "13."  "14."  "15."  "16."  "17."  "18."  "19."  "20." 
 [21] "21."  "22."  "23."  "24."  "25."  "26."  "27."  "28."  "29."  "30." 
 [31] "31."  "32."  "33."  "34."  "35."  "36."  "37."  "38."  "39."  "40." 
 [41] "41."  "42."  "43."  "44."  "45."  "46."  "47."  "48."  "49."  "50." 
 [51] "51."  "52."  "53."  "54."  "55."  "56."  "57."  "58."  "59."  "60." 
 [61] "61."  "62."  "63."  "64."  "65."  "66."  "67."  "68."  "69."  "70." 
 [71] "71."  "72."  "73."  "74."  "75."  "76."  "77."  "78."  "79."  "80." 
 [81] "81."  "82."  "83."  "84."  "85."  "86."  "87."  "88."  "89."  "90." 
 [91] "91."  "92."  "93."  "94."  "95."  "96."  "97."  "98."  "99."  "100."
 
> rank_data
{xml_nodeset (100)}
 [1] <span class="lister-item-index unbold text-primary">1.</span>
 [2] <span class="lister-item-index unbold text-primary">2.</span>
 [3] <span class="lister-item-index unbold text-primary">3.</span>
 [4] <span class="lister-item-index unbold text-primary">4.</span>
 [5] <span class="lister-item-index unbold text-primary">5.</span>
...

> rank<-as.numeric(rank)
> rank
  [1]   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17  18
 [19]  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35  36
 [37]  37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53  54
 [55]  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  70  71  72
 [73]  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89  90
 [91]  91  92  93  94  95  96  97  98  99 100
 
> title_data_html <- html_nodes(movie,'.lister-item-header a')
> title_data_html 
{xml_nodeset (100)}
 [1] <a href="/title/tt5580390/?ref_=adv_li_tt">Форма води</a>
 [2] <a href="/title/tt5027774/?ref_=adv_li_tt">Three Billboards Outside Ebbi ...
 [3] <a href="/title/tt1485796/?ref_=adv_li_tt">Найвеличнiший шоумен</a>
 [4] <a href="/title/tt5638642/?ref_=adv_li_tt">The Ritual</a>
 [5] <a href="/title/tt0974015/?ref_=adv_li_tt">Лiга справедливостi</a>
 ...
 
> title_data <- html_text(title_data_html)
> title_data
  [1] "Форма води"                               
  [2] "Three Billboards Outside Ebbing, Missouri"
  [3] "Найвеличнiший шоумен"                     
  [4] "The Ritual"                               
  [5] "Лiга справедливостi"                      
 ...                   
> 

> runtime_data <- html_nodes(movie,'.text-muted .runtime')
> runtime_data 
{xml_nodeset (100)}
 [1] <span class="runtime">123 min</span>
 [2] <span class="runtime">115 min</span>
 [3] <span class="runtime">105 min</span>
 [4] <span class="runtime">94 min</span>
 [5] <span class="runtime">120 min</span>
...

> runtime <- html_text(runtime_data_html)

> runtime <- html_text(runtime_data)
> runtime
  [1] "123 min" "115 min" "105 min" "94 min"  "120 min" "114 min" "113 min"
  [8] "130 min" "94 min"  "125 min" "105 min" "130 min" "164 min" "141 min"
 [15] "119 min" "132 min" "120 min" "116 min" "104 min" "135 min" "116 min"
 [22] "100 min" "118 min" "152 min" "134 min" "106 min" "134 min" "86 min" 
 [29] "111 min" "133 min" "140 min" "110 min" "141 min" "104 min" "121 min"
 [36] "117 min" "136 min" "135 min" "104 min" "109 min" "107 min" "105 min"
 [43] "104 min" "112 min" "102 min" "93 min"  "121 min" "129 min" "95 min" 
 [50] "119 min" "91 min"  "122 min" "115 min" "132 min" "126 min" "137 min"
 [57] "113 min" "129 min" "118 min" "107 min" "142 min" "92 min"  "112 min"
 [64] "134 min" "112 min" "108 min" "120 min" "107 min" "110 min" "104 min"
 [71] "118 min" "93 min"  "96 min"  "83 min"  "96 min"  "108 min" "137 min"
 [78] "123 min" "112 min" "101 min" "71 min"  "115 min" "136 min" "154 min"
 [85] "87 min"  "122 min" "101 min" "118 min" "127 min" "121 min" "118 min"
 [92] "104 min" "122 min" "107 min" "114 min" "89 min"  "95 min"  "140 min"
 [99] "132 min" "116 min"
> 

> movies <- data.frame(Rank = rank_data, Title = title, Runtime = runtime, stringsAsFactors = FALSE )

> movies <- data.frame(Rank = rank, Title = title_data, Runtime = runtime, stringsAsFactors = FALSE )
> movies
    Rank                                     Title Runtime
1      1                                Форма води     123
2      2 Three Billboards Outside Ebbing, Missouri     115
3      3                      Найвеличнiший шоумен     105
4      4                                The Ritual      94
5      5                       Лiга справедливостi     120

> 


> head(movies$Title, 6)

[1] "Форма води"                               
[2] "Three Billboards Outside Ebbing, Missouri"
[3] "Найвеличнiший шоумен"                     
[4] "The Ritual"                               
[5] "Лiга справедливостi"                      
[6] "Вбивство в Схiдному експресi"


> movies[movies$Runtime > 120, ]$Title
 [1] "Форма води"                              
 [2] "Тор: Рагнарок"                           
 [3] "Темнi часи"                              
 [4] "Phantom Thread"                          
 [5] "Той, хто бiжить по лезу 2049"            
 [6] "Диво-Жiнка"                              
 [7] "Call Me by Your Name"                    
 [8] "Воно"                                    
 [9] "Зорянi вiйни: Останнi Джедаi"            
[10] "Only the Brave"                          
[11] "Hostiles"                                
[12] "Людина-павук: Повернення додому"         
[13] "Гра Моллi"                               
[14] "Kingsman: Золоте кiльце"                 
[15] "Mother!"                                 
[16] "Вартовi Галактики 2"                     
[17] "Зменшення"                               
[18] "Вбивство священного оленя"               
[19] "Пiрати Карибського моря: Помста Салазара"
[20] "Roman J. Israel, Esq."                   
[21] "All the Money in the World"              
[22] "Король Артур: Легенда меча"              
[23] "Логан: Росомаха"                         
[24] "Красуня i Чудовисько"                    
[25] "The Square"                              
[26] "Mudbound"                                
[27] "Валерiан i мiсто тисячi планет"          
[28] "Сiм сестер"                              
[29] "Форсаж 8"                                
[30] "Трансформери: Останнiй лицар"            
[31] "Джон Уiк 2"                              
[32] "Nelyubov"                                
[33] "Battle of the Sexes"                     
[34] "Чужий: Заповiт"                          
[35] "Вiйна за планету мавп"                   
[36] "Brawl in Cell Block 99"    


> length(movies[movies$Runtime < 100, ]$Title)
[1] 15
> 
```
