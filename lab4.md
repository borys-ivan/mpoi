```r
> download.file(url="https://dcc.ligo.org/public/0146/P1700337/001/H-H1_LOSC_C00_4_V1-1187006834-4096.hdf5", destfile = "data.hdf5", mode="wb")
пробую URL 'https://dcc.ligo.org/public/0146/P1700337/001/H-H1_LOSC_C00_4_V1-1187006834-4096.hdf5'
Content type 'text/plain; charset=UTF-8' length 125217658 bytes (119.4 MB)
downloaded 119.4 MB
```
```r
> source("http://bioconductor.org/biocLite.R")
Предупреждение в install.packages("BiocInstaller", repos = a["BioCsoft", "URL"]) :
  'lib = "C:/Program Files/R/R-3.4.3/library"' is not writable
пробую URL 'https://bioconductor.org/packages/3.6/bioc/bin/windows/contrib/3.4/BiocInstaller_1.28.0.zip'
Content type 'application/zip' length 130329 bytes (127 KB)
downloaded 127 KB
```
```r
package ‘BiocInstaller’ successfully unpacked and MD5 sums checked

The downloaded binary packages are in
        C:\Users\borys\AppData\Local\Temp\RtmpCqs5ig\downloaded_packages
Bioconductor version 3.6 (BiocInstaller 1.28.0), ?biocLite for help
> biocLite("rhdf5")
BioC_mirror: https://bioconductor.org
Using Bioconductor 3.6 (BiocInstaller 1.28.0), R 3.4.3 (2017-11-30).
Installing package(s) ‘rhdf5’
also installing the dependency ‘zlibbioc’

пробую URL 'https://bioconductor.org/packages/3.6/bioc/bin/windows/contrib/3.4/zlibbioc_1.24.0.zip'
Content type 'application/zip' length 751310 bytes (733 KB)
downloaded 733 KB

пробую URL 'https://bioconductor.org/packages/3.6/bioc/bin/windows/contrib/3.4/rhdf5_2.22.0.zip'
Content type 'application/zip' length 5819220 bytes (5.5 MB)
downloaded 5.5 MB

package ‘zlibbioc’ successfully unpacked and MD5 sums checked
package ‘rhdf5’ successfully unpacked and MD5 sums checked

The downloaded binary packages are in
        C:\Users\borys\AppData\Local\Temp\RtmpCqs5ig\downloaded_packages
installation path not writeable, unable to update packages: MASS, mgcv, nlme, rpart
```
```r
> library(rhdf5)
> h5ls("data.hdf5")
                 group            name       otype  dclass      dim
0                    /            meta   H5I_GROUP                 
1                /meta     Description H5I_DATASET  STRING    ( 0 )
2                /meta  DescriptionURL H5I_DATASET  STRING    ( 0 )
3                /meta        Detector H5I_DATASET  STRING    ( 0 )
4                /meta        Duration H5I_DATASET INTEGER    ( 0 )
5                /meta        GPSstart H5I_DATASET INTEGER    ( 0 )
6                /meta     Observatory H5I_DATASET  STRING    ( 0 )
7                /meta            Type H5I_DATASET  STRING    ( 0 )
8                /meta        UTCstart H5I_DATASET  STRING    ( 0 )
9                    /         quality   H5I_GROUP                 
10            /quality          detail   H5I_GROUP                 
11            /quality      injections   H5I_GROUP                 
12 /quality/injections InjDescriptions H5I_DATASET  STRING        5
13 /quality/injections   InjShortnames H5I_DATASET  STRING        5
14 /quality/injections         Injmask H5I_DATASET INTEGER     4096
15            /quality          simple   H5I_GROUP                 
16     /quality/simple  DQDescriptions H5I_DATASET  STRING        7
17     /quality/simple    DQShortnames H5I_DATASET  STRING        7
18     /quality/simple          DQmask H5I_DATASET INTEGER     4096
19                   /          strain   H5I_GROUP                 
20             /strain          Strain H5I_DATASET   FLOAT 16777216
```
```r
> strain <- h5read("data.hdf5", "strain/Strain")
> H5close()
```
```r
> st <- h5readAttributes("data.hdf5", "/strain/Strain")$Xspacing
> st
```
```r
[1] 0.0002441406
> gpsStart <- h5read("data.hdf5", "meta/GPSstart")
```
```r
> duration <- h5read("data.hdf5", "meta/Duration")
```
```r
> gpsEnd <- gpsStart + duration
```
```r
> myTime <- seq(gpsStart, gpsEnd, st)

```r
> numSamples <- 1000000
```
```r
> plot(myTime[0:numSamples], strain[0:numSamples], type = "l", xlab = "GPS Time (s)", ylab = "H1 Strain")
> 
```


