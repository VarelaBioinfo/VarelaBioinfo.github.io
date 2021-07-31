---
title: "Visualización Enfermedad Vascular"
layout: default
output:
  md_document:
    variant: gfm
    preserve_yaml: TRUE
knit: (function(inputFile, encoding) {
  rmarkdown::render(inputFile, encoding = encoding, output_dir = "../_portfolio") })
author: "Alfredo Varela"
image:
  path: /assets/images/portfolio/hungary-2020-2015-f1/redbull-mercedes-rvest.png
---

## 1\. Abre el archivo “cardiovascular\_disease.csv” encontrado en cursos en R (todos los descriptores del dataset se encuentran en el archivo llamado “attributes.txt”).

``` r
library(ggplot2)
cardio_data<- read.csv("data/cardiovascular_disease.csv", header= TRUE)
head(cardio_data)
```

    ##   id age_days age_year gender height weight ap_hi ap_lo cholesterol gluc smoke
    ## 1  0    18393 50.39178      2    168     62   110    80           1    1     0
    ## 2  1    20228 55.41918      1    156     85   140    90           3    1     0
    ## 3  2    18857 51.66301      1    165     64   130    70           3    1     0
    ## 4  3    17623 48.28219      2    169     82   150   100           1    1     0
    ## 5  4    17474 47.87397      1    156     56   100    60           1    1     0
    ## 6  8    21914 60.03836      1    151     67   120    80           2    2     0
    ##   alco active cardio
    ## 1    0      1      0
    ## 2    0      1      1
    ## 3    0      0      1
    ## 4    0      1      1
    ## 5    0      0      0
    ## 6    0      0      0

## 2\. Realiza una gráfica de barras con el número de pacientes que se encuentran en cada grupo discreto de la variable colesterol.

``` r
chol_counts<-table(cardio_data$cholesterol)
chol_counts_df<-as.data.frame(chol_counts)
print(chol_counts_df)
```

    ##   Var1  Freq
    ## 1    1 52385
    ## 2    2  9549
    ## 3    3  8066

``` r
colnames(chol_counts_df) <-c("cholesterol_group","individuals")

ggplot(chol_counts_df,aes(x=cholesterol_group,y=individuals,fill=cholesterol_group)) + 
  geom_bar(stat = "identity") +
  coord_flip()+theme(legend.position = "none") + 
  labs(title="Pacientes agrupados por niveles de colesterol en sangre",x="Nivel de colesterol",y="Número de pacientes") +
  scale_x_discrete(labels=c("Nomal","Alto","Muy alto")) +
  scale_fill_brewer(palette = "Reds") + theme_minimal() +
  theme(legend.position="none")
```

![](/assets/images/portfolio/CardiovascualarDiseaseViz/unnamed-chunk-3-1.png)<!-- -->

## 3\. Realiza una gráfica de barras con el número de pacientes que se encuentran en cada grupo discreto de la variable colesterol agrupada por ausencia o presencia de una enfermedad cardiovascular. ¿Encuentras alguna asociación entre ambas variables?

**El colesterol alto se asocia a un mayor número de casos de cardiopatía
vascular**

``` r
chol_cardio_counts<-tapply(cardio_data$cholesterol,list(cardio_data$cholesterol, cardio_data$cardio), table)
chol_cardio_counts<-as.data.frame(chol_cardio_counts)
print(chol_cardio_counts)
```

    ##       0     1
    ## 1 29330 23055
    ## 2  3799  5750
    ## 3  1892  6174

``` r
colnames(chol_cardio_counts)<-c("No","Sí")
rownames(chol_cardio_counts)<-c("Normal","Alto","Muy alto")
chol_cardio_counts$colesterol<-rownames(chol_cardio_counts)
chol_cardio_counts
```

    ##             No    Sí colesterol
    ## Normal   29330 23055     Normal
    ## Alto      3799  5750       Alto
    ## Muy alto  1892  6174   Muy alto

``` r
chol_cardio_counts<-reshape(chol_cardio_counts, 
                            direction = "long", 
                            varying =list(names(chol_cardio_counts)[1:2]), 
                            v.names = "counts",
                            idvar= "colesterol",
                            timevar = "Cardiopatía",
                            times=c("No","Sí"))


ggplot(chol_cardio_counts, aes(x=colesterol, y=counts, fill=Cardiopatía))+
  geom_bar(stat="identity") +
  coord_flip() +
  labs(title="Niveles de colesterol asociados a Cardiopatía vascular",y="Número de pacientes",x="Colesterol") +
  scale_fill_brewer(palette="RdYIGn") + 
  theme_minimal() + 
  theme(legend.position = "bottom")
```

![](/assets/images/portfolio/CardiovascualarDiseaseViz/unnamed-chunk-4-1.png)<!-- -->

``` r
ggplot(chol_cardio_counts, aes(x = colesterol, y = counts, fill = Cardiopatía)) +
  geom_bar(stat = "identity", position=position_dodge()) +
  coord_flip() +
  labs(title="Niveles de colesterol agrupados por Cardiopatía vascular",x="Colesterol",y="Número de pacientes") +
  scale_fill_brewer(palette = "RdYiGn") +
  theme_minimal()
```

![](/assets/images/portfolio/CardiovascualarDiseaseViz/unnamed-chunk-5-1.png)<!-- -->
**El único grupo en donde es menos frecuente tener cardiopatía es el de
colesterol normal. Entre mayor es el valor de colesterol, más casos de
cardiopatía vascular se encuentra.**

## 4\. Realiza un histograma de la variable estatura y coloca una gráfica de densidad encima.

``` r
ggplot(cardio_data,aes(x=height)) +
  geom_histogram(aes(y=..density..),fill="white", binwidth = 2,color= "black") +
  labs(title="Distribución de la estatura de los pacientes", x="Estatura en centímetros",y="Número de pacientes") +
  geom_density(fill="orange",alpha=0.2) + theme_minimal()
```

![](/assets/images/portfolio/CardiovascualarDiseaseViz/unnamed-chunk-6-1.png)<!-- -->

## 5\. Realiza un histograma de la variable estatura agrupada por género. ¿Encuentras alguna asociación entre ambas variables?

**La mediana de estatura es más baja en el grupo de mujeres. En general
el grupo de mujeres presenta una menor estatura.**

``` r
table(cardio_data$gender)
```

    ## 
    ##     1     2 
    ## 45530 24470

``` r
ggplot(cardio_data, aes(x= height, color= as.character(gender))) + 
  geom_histogram(binwidth=2.5) + 
  labs(title="Estatura agrupada por género", x="Estatura en centímetros", y="Número de pacientes") +
  scale_color_discrete(name="Género",labels=c("Mujer","Hombre")) +
  theme_minimal()+ 
  theme(legend.position = "bottom") + 
  scale_color_brewer(palette ="Dark2",name="Género", labels= c("Mujeres","Hombres")) 
```

![](/assets/images/portfolio/CardiovascualarDiseaseViz/unnamed-chunk-7-1.png)<!-- -->

## 6\. Realiza una gráfica de dispersión con las variables tensión arterial sistólica y tensión arterial diastólica (limita el eje x a 250 y el eje y a 200). Coloca una línea de regresión encima. ¿Encuentras alguna asociación entre las variables?

``` r
summary(cardio_data$ap_hi)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##  -150.0   120.0   120.0   128.8   140.0 16020.0

``` r
ggplot(cardio_data, aes(x=ap_hi, y=ap_lo)) + 
  geom_point(shape=1, color="firebrick4") + 
  geom_smooth(method = lm, linetype="longdash", color="black") +  
  labs(title="Dispersión Tensión arterial sistólica vs diastólica", x="Presión sistólica (mmHg)", y="Presión diastólica (mmHg)") + 
  xlim(50,250) +
  ylim(30,200) +
  theme_minimal()
```

![](/assets/images/portfolio/CardiovascualarDiseaseViz/unnamed-chunk-8-1.png)<!-- -->
**La presión sistólica baja generelamente se relaciona con una presión
diastólica baja. Cuando la presión sistólica es elevada también la
presión diastólica suele superar los **

## 7\. Realiza una gráfica de dispersión con las variables tensión arterial sistólica y tensión arterial diastólica (limita el eje x a 250 y el eje y a 200), agrupada por la presencia o ausencia de una enfermedad cardiovascular. ¿Qué relación crees que existe entre estas tres variables?

``` r
ggplot(cardio_data, aes(x=ap_hi, y=ap_lo, group=cardio))+
  geom_point(aes(color=as.character(cardio), shape = as.character(cardio)))+ 
  labs(title="Presión sistólica vs diastólica agrupada por cardiopatía", x="Presión sistólica (mmHg)", y="Presión diastólica (mmHg)") + 
  xlim(50,250) +
  ylim(30,200) +
  scale_color_manual(name="Cardiopatía vascular", labels=c("No","Sí"), values =c("blue","red")) +
  scale_shape_manual(name="Cardiopatía vascular", labels=c("No","Sí"), values=c(1,2)) +
  geom_smooth(method = lm, color="black") +
  theme_minimal()
```

![](/assets/images/portfolio/CardiovascualarDiseaseViz/unnamed-chunk-9-1.png)<!-- -->
**A medida que la presión sistólica incrementa, los valores de presión
diastólica también lo hacen. Una presión diastólica alta así como una
presión sistólica alta, se asocian mayormente a cardiopatía vascular.**

## 8\. Realiza un boxplot con la variable peso y la variable de enfermedad cardiovascular. ¿Qué puedes deducir sobre el peso de los pacientes con enfermedades cardiovasculares?

``` r
ggplot(cardio_data, aes(x=as.character(cardio),y=weight, fill= as.character(cardio)))+
  geom_boxplot() + 
  labs(title="Distribución de peso agrupado por enfermedad vascular", x="Enfermedad vascular", y="Peso (kg)") + 
  scale_x_discrete(labels=c("0"="No","1"="Sí")) +
  scale_fill_brewer(palette="Blues", name=element_blank(), labels=c("0"="No","1"="Sí")) + 
  theme_grey() + 
  theme(legend.position="bottom")
```

![](/assets/images/portfolio/CardiovascualarDiseaseViz/unnamed-chunk-10-1.png)<!-- -->
**El 50% de los datos de peso de los pacientes sin efermedad es en
general más bajo que el de los pacientes con enfermedad vascular.
Curiosamente el valor mínimo de peso se encuentra para una persona con
enfermedad vascular. Los valores máximos en ambos grupos son iguales.**

## 9\. Realiza un boxplot con la variable peso y la variable de enfermedad cardiovascular, agrupadas por la variable “fumar”. ¿Qué relación existe entre las tres variables?

``` r
ggplot(cardio_data, aes(x=as.character(cardio),y=weight, color=as.character(smoke))) +
  geom_boxplot() + 
  labs(title = "Distribución de peso agrupada por enfermedad vascular y hábito tabáquico",x="Enferemedad cardivoascular",y="Peso (kg)")+
  scale_color_brewer(name="Fuma",labels=c("no","sí"), palette="Reds") +
  scale_x_discrete(labels=c("0"="No","1"="Sí")) + 
  theme_dark()
```

![](/assets/images/portfolio/CardiovascualarDiseaseViz/unnamed-chunk-11-1.png)<!-- -->

**El peso de las personas independientemente si padecen enfermedad
vasular o no, es mayor si fuman. El valor máximo de peso en ambos grupos
se encontró en no fumadores.**

## 10\. Realiza un heatmap de la edad en años, la presión arterial sistólica, la presión arterial diastólica, la estatura y el peso, contra los grupos obtenidos de las combinaciones entre las variables colesterol y enfermedad cardiovascular (debes obtener un heatmap de 6x5).

``` r
chol_card_group<-list(cardio_data$cholesterol, cardio_data$cardio)
heat_data<-aggregate(cardio_data[,c("age_year","ap_hi","ap_lo","height","weight")],by= chol_card_group, mean, na.rm =T)
heat_data
```

    ##   Group.1 Group.2 age_year    ap_hi     ap_lo   height   weight
    ## 1       1       0 51.39339 119.7578  83.42472 164.6088 71.02496
    ## 2       2       0 52.58333 121.5620  87.07476 163.5288 73.72901
    ## 3       3       0 55.24356 128.6253  91.40433 163.8018 76.09413
    ## 4       1       1 54.65985 135.3242 106.84862 164.5668 75.63498
    ## 5       2       1 54.45769 143.5268 118.23496 164.1127 78.60723
    ## 6       3       1 56.49296 138.3805 108.56851 163.3102 79.59404

``` r
heat_data<- reshape(heat_data,
                    direction = "long",
                    varying = list(names(heat_data)[3:7]),
                    v.names="Value",
                    idvar=c("Group.1","Group.2"),
                    timevar="Variable",
                    times= colnames(heat_data)[3:7])

row.names(heat_data) <- NULL
heat_data
```

    ##    Group.1 Group.2 Variable     Value
    ## 1        1       0 age_year  51.39339
    ## 2        2       0 age_year  52.58333
    ## 3        3       0 age_year  55.24356
    ## 4        1       1 age_year  54.65985
    ## 5        2       1 age_year  54.45769
    ## 6        3       1 age_year  56.49296
    ## 7        1       0    ap_hi 119.75782
    ## 8        2       0    ap_hi 121.56199
    ## 9        3       0    ap_hi 128.62526
    ## 10       1       1    ap_hi 135.32422
    ## 11       2       1    ap_hi 143.52678
    ## 12       3       1    ap_hi 138.38047
    ## 13       1       0    ap_lo  83.42472
    ## 14       2       0    ap_lo  87.07476
    ## 15       3       0    ap_lo  91.40433
    ## 16       1       1    ap_lo 106.84862
    ## 17       2       1    ap_lo 118.23496
    ## 18       3       1    ap_lo 108.56851
    ## 19       1       0   height 164.60876
    ## 20       2       0   height 163.52882
    ## 21       3       0   height 163.80180
    ## 22       1       1   height 164.56678
    ## 23       2       1   height 164.11270
    ## 24       3       1   height 163.31017
    ## 25       1       0   weight  71.02496
    ## 26       2       0   weight  73.72901
    ## 27       3       0   weight  76.09413
    ## 28       1       1   weight  75.63498
    ## 29       2       1   weight  78.60723
    ## 30       3       1   weight  79.59404

``` r
library(plyr)
colnames(heat_data)<-c("Colesterol","Cardiovasc_dis","Variable","Value")
heat_data$Colesterol<-as.factor(heat_data$Colesterol)
heat_data$Colesterol<-revalue(heat_data$Colesterol,c("1"="normal","2"="alto","3"="muy alto"))

heat_data$Cardiovasc_dis<-as.factor(heat_data$Cardiovasc_dis)
heat_data$Cardiovasc_dis<-revalue(heat_data$Cardiovasc_dis,c("0"="No","1"="Sí"))
heat_data
```

    ##    Colesterol Cardiovasc_dis Variable     Value
    ## 1      normal             No age_year  51.39339
    ## 2        alto             No age_year  52.58333
    ## 3    muy alto             No age_year  55.24356
    ## 4      normal             Sí age_year  54.65985
    ## 5        alto             Sí age_year  54.45769
    ## 6    muy alto             Sí age_year  56.49296
    ## 7      normal             No    ap_hi 119.75782
    ## 8        alto             No    ap_hi 121.56199
    ## 9    muy alto             No    ap_hi 128.62526
    ## 10     normal             Sí    ap_hi 135.32422
    ## 11       alto             Sí    ap_hi 143.52678
    ## 12   muy alto             Sí    ap_hi 138.38047
    ## 13     normal             No    ap_lo  83.42472
    ## 14       alto             No    ap_lo  87.07476
    ## 15   muy alto             No    ap_lo  91.40433
    ## 16     normal             Sí    ap_lo 106.84862
    ## 17       alto             Sí    ap_lo 118.23496
    ## 18   muy alto             Sí    ap_lo 108.56851
    ## 19     normal             No   height 164.60876
    ## 20       alto             No   height 163.52882
    ## 21   muy alto             No   height 163.80180
    ## 22     normal             Sí   height 164.56678
    ## 23       alto             Sí   height 164.11270
    ## 24   muy alto             Sí   height 163.31017
    ## 25     normal             No   weight  71.02496
    ## 26       alto             No   weight  73.72901
    ## 27   muy alto             No   weight  76.09413
    ## 28     normal             Sí   weight  75.63498
    ## 29       alto             Sí   weight  78.60723
    ## 30   muy alto             Sí   weight  79.59404

``` r
library(wesanderson)
pal <- wes_palette("Zissou1", 100, type = "continuous")

ggplot(heat_data,aes(x=Variable,y=Colesterol,fill=Value,group=Cardiovasc_dis))+
  geom_tile() + scale_fill_gradientn(colours = pal) +
   labs(title="Heatmap por nivel de colesterol", y="Colesterol") +
  scale_x_discrete(labels=c("edad en años", "p. sistólica","p. diastólica","talla","peso"))
```

![](/assets/images/portfolio/CardiovascualarDiseaseViz/unnamed-chunk-15-1.png)<!-- -->

``` r
ggplot(heat_data)+
  geom_tile(aes(x=Variable, y=Cardiovasc_dis, fill=Value))+
  scale_fill_gradientn(colours = pal)+
  labs(title="Heatmap por enfermedad vascular", y="Enfermedad vascular")+ 
  scale_x_discrete(labels=c("edad en años", "p. sistólica","p. diastólica","talla","peso"))
```

![](/assets/images/portfolio/CardiovascualarDiseaseViz/unnamed-chunk-15-2.png)<!-- -->
