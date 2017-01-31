# KT001_cleanup_Apac_T3
cleanup time-point 3 data

```r
rm(list=ls())
setwd("C:\\Users\\helbd\\Documents\\Magic Briefcase\\LSHTM\\Kevin's array\\151118 data")
```

##########################################################################################
##Load array data:

```r
files <- sort(list.files(".\\Data\\Processed Data")[grep("import_data.RData", list.files(".\\Data\\Processed Data"))], decreasing=T)[1]
print(load(paste(".\\Data\\Processed Data\\", files, sep=""))) 
d1$spot[grep("std._", d1$spot)] <- gsub("std", "std0", d1$spot[grep("std._", d1$spot)])

temp.d1 <- d1[d1$study=="Apac_X3",]
```

##########################################################################################
##create matrix of raw MEAN intensity values

```r
temp <- matrix(NA, nrow=length(unique(d1$spot)), ncol=length(unique(temp.d1$sampleID)))
rownames(temp) <- sort(unique(temp.d1$spot))
colnames(temp) <- unique(temp.d1$sampleID)

for(id in colnames(temp)){
  for(ag in rownames(temp)){
    print(id)
    print(ag)
    temp[rownames(temp)==ag, colnames(temp)==id] <- temp.d1[temp.d1$spot==ag & temp.d1$sampleID==id, "Raw.Mean"]
  }
}
X3_raw_mean <- temp
```

##########################################################################################
##create matrix of raw Median intensity values

```r
temp <- matrix(NA, nrow=length(unique(d1$spot)), ncol=length(unique(temp.d1$sampleID)))
rownames(temp) <- sort(unique(temp.d1$spot))
colnames(temp) <- unique(temp.d1$sampleID)

for(id in colnames(temp)){
  for(ag in rownames(temp)){
    print(id)
    print(ag)
    temp[rownames(temp)==ag, colnames(temp)==id] <- temp.d1[temp.d1$spot==ag & temp.d1$sampleID==id, "Raw.Median"]
  }
}

X3_raw_median <- temp
```


##########################################################################################
##save data

```r
save(X3_raw_mean, X3_raw_median, file=".\\Data\\Processed Data\\0001.KTarray.Apac.cleaned_X3.RData")
```
