---
title: "Method Correction"
author: "Justin Baumann"
date: "1/21/2022"
output:
  html_document:
    df_print: kable
    toc: yes
    toc_float: yes
  pdf_document:
    toc: yes
  word_document:
    toc: yes
editor_options:
  chunk_output_type: console
---

```{r setup, include=FALSE, warning=FALSE}
knitr::opts_chunk$set(echo = TRUE, warning=FALSE, message=FALSE)

```

# **Summary** 
Thanks to feedback from colleagues, we have identified some errors in the SEDAC Global Human Influence Index dataset. Notably, there are some island areas that are heavily populated or otherwise obviously impacted by humans that return a false HII value of zero, indicating no human impacts. Here, we have removed these values from our dataset and reanalyzed the data. The results are almost identical to those in the main text of the paper, with no major interpretations changing. That said, we feel it important to point out the deficiency in this underlying dataset for future users. 

We advise that future work utilize other global human impact databases that are more appropriate for coral reefs, such as Andrello et al "Global Human Pressure on Reefs" metric (referred to here and in our manuscript as WCS score) and Cinner et al's Human Gravity. 

Details on HII and WCS Score are provided in the following tabs. 

# **HII details and error identification** {.tabset .tabset-pills}
The Global Human Influence Index (**HII**) is a globally gridded dataset with 1 km resolution grid cells. It was generated in 2005 by the NASA Socioeconomic Data and Applications Center (SEDAC) through a collaboration between the Wildlife Conservation Society (WCS) and the Columbia University Center for International Earth Science Information Network. 

[HII website and data download](https://sedac.ciesin.columbia.edu/data/set/wildareas-v2-human-influence-index-geographic)

Citation: Wildlife Conservation Society - WCS, and Center for International Earth Science Information Network - CIESIN - Columbia University. 2005. Last of the Wild Project, Version 2, 2005 (LWP-2): Global Human Influence Index (HII) Dataset (Geographic). Palisades, NY: NASA Socioeconomic Data and Applications Center (SEDAC). https://doi.org/10.7927/H4BP00QC. 

## **HII Metric Details**
HII is a composite metric of human influence that includes the following layers: </br>
-Human population pressure (via human population density/ sq. km). Values from 0-10 assigned based on population density per square km </br>
-	Human land use and infrastructure (via urban areas, nighttime lights and land use/land cover) </br>
-	Urban area: if inside an urban polygon = 10, if outside = 0 </br>
-	Light: ranked scores from 0-10 based on nighttime light values </br>
-	Land use: Urban areas = 10, irrigated ag = 8, rain-fed ag = 3, other cover = 0 </br>
-	Human access (via coastlines, roads, railroads, and navigable rivers) </br>
-	Influence of coastlines was given 0 influence if > 15km from a coastline and 4 influence if within 15 km of a coastline </br>
-	Roads were assigned an influence score based on proximity. If a site was within 2 km of a major road, it received the highest score (8), between 2 and 15 km received a 4, and > 15 km from a major road received a 0 </br>
- Railroads were scored as 0 if > 2 km from a railroad and 8 if within 2 km of a railroad
-	Navigable rivers received a 0 score if > 15 km from a river and 4 if within 15 km of a river </br>
The metric is calculated by assigning an influence score to various values in each layer (higher = more human influence). After values are assigned to each layer of the metric, they are summed to give an HII value. </br>

[HII metric calculation website](https://sedac.ciesin.columbia.edu/data/collection/wildareas-v2/methods)

## **Error Identification**

Through expert feedback and detailed exploration of the dataset, we have identified a number of location in which HII is falsely reported to by zero (HII=0). An HII value of zero suggests no human impact on that site. 

![](G:/My Drive/Research/UNC Research/Global coral cover and abundance/global_coral_recovery/HII_missing_data.png)

Figure 1: Map of HII data from the SEDAC webpage. Gray areas indicate missing data. In these locations, HII=0. 

As a result of this missing data in the underlying HII layer, we combed our dataset and assessed each site in which HII=0 using Google Earth. Since we calculated HII for the manuscript as the sum of all HII within 100km of each site, we created a 100km radius circle on Google Earth with the lat/long of the site at the center and assessed (visually) whether there was clearly human influence or not. Since HII was generated in 2009, we utilized modern satellite imagery (the most recent available images) and images from 2008 and/or 2009 at each site. In some cases, there was very clearly human influence (Fig 2). In these instance, we removed the point from our dataset and reanalyzed. In other cases, there was no visible human influence within 100km. These sites were retained (Fig 3). 


![](G:/My Drive/Research/UNC Research/Global coral cover and abundance/global_coral_recovery/Maduvvari clear human influence.png)

Fig 2: Maduvvari had clear human influence and was removed from the dataset. 

![](G:/My Drive/Research/UNC Research/Global coral cover and abundance/global_coral_recovery/Cocos Isl, CR. Very remote. 100km.png)

Figure 3: Cocos Island, Costa Rica had no visible human influence and was retained. 

## **Data Removal**
After exploring the data, we removed 41 sites from our Recovery database (out of an original 182) and 40 sites from our resistance database (out of an original 184).
Most of these removals were in the Indian Ocean. It seems that the missing data in the HII dataset are concentrated in small island states, specifically within the Indian Ocean. We urge caution in using this dataset for this region of the world in the future and note that such gaps do not appear to exist in the Andrello et al WCS score or the Cinner et al Human Gravity data. 

# **WCS Score Details** {.tabset .tabset-pills}
Explore these tabs for details on the WCS Score metric (along with links to download the data)

## **WCS Score Background**
WCS Score is derived from a pre-print written by Marco Andrello, Emily Darling, Amelia Wenger, Andres F. Suarez-Casto, Sharla Gelfand, and Gabby Ahmadia that is available on BiorXiv. The paper is a collaboration between The National Research Council (Italy), MARBEC (University of Montpelier, France), Wildlife Conservation Society (WCS), and a number of other institutions. 
[Link to paper](https://www.biorxiv.org/content/10.1101/2021.04.03.438313v1.full.pdf)

The Supplementary Info are very helpful and contain details of each component of the metric
[Download Supplementary Info](https://www.biorxiv.org/content/10.1101/2021.04.03.438313v1.supplementary-material)

[Data and Code](https://github.com/WCS-Marine/local-reef-pressures)

Citation: A global map of human pressures on tropical coral reefs
Marco Andrello, Emily Darling, Amelia Wenger, Andrés F. Suárez-Castro, Sharla Gelfand, Gabby N. Ahmadia
bioRxiv 2021.04.03.438313; doi: https://doi.org/10.1101/2021.04.03.438313

## **Metric Details**
‘WCS Score’ is a composite metric that utilizes the following layers: </br>
-	Tropical coral reef locations (from Beyer et al 2018, based on UNEP-WCMC dataset from 2010). Resolution is ~ 5km. </br>
-	Fishing (Market Gravity from Cinner et al 2016, 2018, resolution = 10km) </br>
-	Coastal Development (gridded population of the world from SEDAC, 2018 – an updated version of the same data used in HII. They used number of people living within a 5km buffer of each reef polygon as the actual metric here) </br>
-	Industrial Development (World port locations- ports were identified from a google data product, given a point location, and then all port points within 5 square km of a reef were summed) </br>
-	Tourism (This value is directly from Spalding et al 2017 – an estimate of the annual economic value of each reef) </br>
-	Sediment Pollution (Via a newly calculate metric for this paper- Sediment delivery from rivers was estimated in 2 ways based on land cover, management, rainfall, discharge, land use, and more. Sediment exposure to reefs was modelled using sediment plume models and estimated at tons of sediment per square km) </br>
-	Nitrogen Pollution (Using FAO data on catchment level crop cover and national nitrogen fertilizer use, they modeled nitrogen plumes from rivers to estimate nitrogen pollution) </br>

Each metric was assigned a weight (1-6 with 6 meaning most impactful) for each reef pixel using perceptions of risk from a study by Stephanie Wear (2016). A weighed average of the 6 metrics was used to generate a cumulative score, or as we are calling it, ‘WCS Score’ for each pixel. 

See supplementary methods from Andrello et al for more detail on all of these metrics and how they were calculated. 

# **Updated Tables and Figures** {.tabset .tabset-pills}

## **Tables**
**Updated Recovery Model Table** 
```{r, echo=FALSE, warning=FALSE, message=FALSE, error=FALSE}

#startup and REC model table

#load packages
library(tidyverse)
library(ggplot2)
library(lme4)
library(car) #For checking multicollinearity, using performance instead
library(performance) #for checking R2 or ICC, and comparing model performances
library(ggeffects)
#library(cowplot)
#library(egg)
#library(ggpubr)
library(patchwork)
library(ggrepel)
library(ggsci)
library(parameters) #get model params
library(effects)
library(broom)
#library(visibly)
library(rgdal)
library(raster)
library(spdep)
library(ggridges)
library(formattable)
library(RColorBrewer)

setwd("G:/My Drive/Research/UNC Research/Global coral cover and abundance/global_coral_recovery/data")
recov<-read.csv('recov_adjusted_zerohii.csv')
resist<-read.csv('resist_adjusted_zerohii.csv')


finr4.3<-lmer(calculated.recovery.rate ~ region+disturbance+hii100km2+MPA_during_recov+recovery_time2+distance_to_shore_m2+cml_scr2+pre.dist.cc + (1|study), data = recov, REML=TRUE)

#summary(finr4.3)

fins4.1<-lmer(resistance ~ region+disturbance+hii100km2+MPA_during_resist+resistance_time_2+cml_scr2+travel_time.tt_pop2+pre.dist.cc + (1|study), data = resist, REML=TRUE)

#summary(fins4.1)


#COEF PLOTS
#summary(finr4.3)#rec
#summary(fins4.1)#res

finr4.3mp<-parameters::model_parameters(finr4.3)
fmp=as.data.frame(finr4.3mp)
fmp

fmplot<-ggplot(fmp, aes(x=Coefficient, y= Parameter))+
  geom_vline(xintercept=0, linetype='dashed')+
  geom_point()+
  geom_errorbarh(aes(xmin=CI_low, xmax= CI_high, y=Parameter),height=0.5)+
  theme_bw()+  
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank(),
        panel.background = element_blank(), axis.line = element_line(colour = "black"))+
  ggtitle('Recovery Rate')
#fmplot
```

**Updated Resistance Model Table**
```{r, echo=FALSE, warning=FALSE, message=FALSE, error=FALSE}
#resistance model table
fmpres<-parameters::model_parameters(fins4.1)
fmpresmp<-as.data.frame(fmpres)
fmpresmp

fmplotres<-ggplot(fmpresmp, aes(x=Coefficient, y= Parameter))+
  geom_vline(xintercept=0, linetype='dashed')+
  geom_point()+
  geom_errorbarh(aes(xmin=CI_low, xmax= CI_high, y=Parameter),height=0.5)+
  theme_bw()+  
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank(),
        panel.background = element_blank(), axis.line = element_line(colour = "black"))+
  ggtitle('Resistance')
```

## **Figures**

**Updated Figure 1 (regional trends)**
```{r, echo=FALSE, warning=FALSE, message=FALSE, error=FALSE, fig.width=14, fig.height=7}

##Build the Recovery Histogram
recov$region<-factor(recov$region, levels= c("Caribbean","Indian Ocean", "W. Pacific", "E. Pacific"))

#overall recovery histo
recovr<-ggplot(recov, aes(x=calculated.recovery.rate))+
  geom_density(fill='gray')+
  theme_ridges()+
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank(),
        panel.background = element_blank(), axis.line = element_line(colour = "black"))+
  theme(legend.position = "none")+
  labs(x = "Recovery Rate", y='Frequency')+
  theme(axis.text = element_text(size=10))+
  theme(axis.title = element_text(size=12))+
  scale_y_continuous(breaks=scales::pretty_breaks(n=3))+
  theme(panel.border=element_blank())

#recovr

#by region

#calculate outliers for recovery rate and generate a new column (outlier)
recouts<-recov%>%
  group_by(region) #%>%
  #mutate(outlier = ifelse(is_outlier(calculated.recovery.rate), location, as.numeric(NA)))
#recouts
#write.csv(recouts, 'recouts.csv')


#calculate IQRs for each region (Q1 and Q3)
recouts1<-recov%>%
  group_by(region)%>%
  summarise_at(vars(calculated.recovery.rate),
               list(IQR=IQR, Q1=~quantile(.,probs=0.25), median=median, Q3=~quantile(.,probs=0.75)))
#recouts1
#add outlier lines (1.5*Q1 or Q3)
recouts1$outlierval=1.5*recouts1$IQR
recouts1$highout=recouts1$Q3+recouts1$outlierval
recouts1$lowout=recouts1$Q1-recouts1$outlierval
#head(recouts1)

#head(recouts)
#merge iqr info to recouts

recouts2<-merge(recouts, recouts1, by='region')
#head(recouts2)

#histo for recovery by region (can add outliers with commented out code)
rechist<-ggplot(recouts, aes(x=calculated.recovery.rate, y=region, fill=region))+
  geom_density_ridges(jittered_points=TRUE, position=position_points_jitter(width=0.1, height=0), point_shape='|',alpha=0.8, quantile_lines=TRUE)+
  geom_segment(data=recouts1, aes(x=lowout, xend=lowout, y=as.numeric(region), yend=as.numeric(region)+.9),color='red')+
  geom_segment(data=recouts1, aes(x=highout, xend=highout, y=as.numeric(region), yend=as.numeric(region)+.9),color='red')+
  theme_ridges()+
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank(),
        panel.background = element_blank(), axis.line = element_line(colour = "black"))+
  theme(legend.position = "none")+
  labs(x = "Recovery Rate", y='Region')+
  scale_color_jama()+
  scale_fill_jama()
#rechist

#+
#add place names to the outliers!
# geom_text(aes(color=region),na.rm=TRUE, size=2.5, vjust=2, position= position_jitter(width=0, height=0.2))



##Build the Resistance Histrogram
resist$region<-factor(resist$region, levels= c("Caribbean","Indian Ocean", "W. Pacific", "E. Pacific"))

#overall resistance
resovr<-ggplot(resist, aes(x=resistance))+
  geom_density(fill='gray')+
  theme_ridges()+
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank(),
        panel.background = element_blank(), axis.line = element_line(colour = "black"))+
  theme(legend.position = "none")+
  labs(x = "Resistance", y="Frequency")+
  theme(axis.text = element_text(size=10))+
  theme(axis.title = element_text(size=12))+
  scale_y_continuous(breaks=scales::pretty_breaks(n=3))+
  theme(panel.border = element_blank())
#resovr

###RES outliers
#calculate outliers for recovery rate and generate a new column (outlier)
 resouts<-resist%>%
   group_by(region) #%>%
#   mutate(outlier = ifelse(is_outlier(resistance), location, as.numeric(NA)))
#resouts
#write.csv(resouts, 'resouts.csv')


#calculate IQRs for each region (Q1 and Q3)
resouts1<-resist%>%
  group_by(region)%>%
  summarise_at(vars(resistance),
               list(IQR=IQR, Q1=~quantile(.,probs=0.25), median=median, Q3=~quantile(.,probs=0.75)))
#resouts1
#add outlier lines (1.5*Q1 or Q3)
resouts1$outlierval=1.5*resouts1$IQR
resouts1$highout=resouts1$Q3+resouts1$outlierval
resouts1$lowout=resouts1$Q1-resouts1$outlierval
#head(resouts1)

#head(resouts)
#merge iqr info to recouts

resouts2<-merge(resouts, resouts1, by='region')
#head(resouts2)

##by region
reshist<-ggplot(resist, aes(x=resistance, y=region, fill=region))+
  geom_density_ridges(jittered_points=TRUE, position=position_points_jitter(width=0.1, height=0), point_shape='|',alpha=0.8, quantile_lines=TRUE)+
  geom_segment(data=resouts1, aes(x=lowout, xend=lowout, y=as.numeric(region), yend=as.numeric(region)+.9),color='red')+
  geom_segment(data=resouts1, aes(x=highout, xend=highout, y=as.numeric(region), yend=as.numeric(region)+.9),color='red')+
  theme_ridges()+
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank(),
        panel.background = element_blank(), axis.line = element_line(colour = "black"))+
  theme(legend.position = "none")+
  labs(x = "Resistance", y='Region')+
  scale_color_jama()+
  scale_fill_jama()

#reshist

##Build global maps of Recov and Resist

###plotting them together in a panel plot

#histograms
#recovr
#resovr

#Inset of overall histos
layout<- c(
  patchwork::area(t=2, l=1, b=9, r=8),
  patchwork::area(t = 1, l = 6, b = 2, r=8),
  patchwork::area(t= 2, l=9, b=9, r=17),
  patchwork::area(t = 1, l = 15, b = 2, r =17))

#make final Fig 2
Fig2<-rechist + recovr + reshist + resovr+
  plot_layout(design=layout)
Fig2

```
Figure 1 is very similar to the published figure. The only noticeable difference is in the Indian Ocean histrogram in panel A (Recovery Rate), where the distribution is unimodal instead of bimodal. 

**Updated Manuscript Figure 2 (model coefficient plots)**
```{r, echo=FALSE, warning=FALSE, message=FALSE, error=FALSE, fig.width=6, fig.height=8}
#Final COEF plot

fmplot/fmplotres + plot_annotation(tag_levels = 'A')
```
Figure 2 has changed slightly. For this version, WCS SCORE is called 'cml_scr2'. There are slight changes to some of the model coefficients following the removal of false HII=0 sites. Namely, HII is no longer (significantly) positively correlated with Recovery Rate, though that trend still appears to be present in Figure 3. 

**Updated Manunscript Figure 3 (HII/WCS Score vs. Recovery/Resistance)**
```{r, echo=FALSE, warning=FALSE, message=FALSE, error=FALSE, fig.width=10, fig.height=10}
#To make this figure you must first run the final recovery and resistance linear models
#Then use ggeffects to extract the data we want

finalmodel2<-lmer(calculated.recovery.rate ~ region+disturbance+hii100km2+MPA_during_recov+recovery_time2+distance_to_shore_m2+cml_scr2+pre.dist.cc + (1|study), data = recov, REML=TRUE)

resfinalmodel2<-lmer(resistance ~ region+disturbance+hii100km2+MPA_during_resist+resistance_time_2+cml_scr2+travel_time.tt_pop2+pre.dist.cc + (1|study), data = resist, REML=TRUE)


##RECOVERY HII
#need the recov dataframe to run this

#run the linear model
# Extract the prediction data frame
pred.hii <- ggpredict(finalmodel2, terms = c("hii100km2"))  # this gives overall predictions for the model
#pred.hii

# Plot the predictions 
ggpredhii<-ggplot(pred.hii) + 
  geom_ribbon(aes(x = x, ymin = conf.low, ymax = conf.high), 
              fill = "lightgrey", alpha = 0.3) +  # error band
  geom_point(data = recov,                      # adding the raw data (scaled values)
             aes(x = hii100km2, y = calculated.recovery.rate),alpha=0.5) +
  geom_line(aes(x = x, y = predicted),size=1, color='black') +          # slope
  theme_bw()+
  labs(x = "Scaled Human Influence Index", y = "Recovery Rate")+
  #labs(color= "MPA Status", shape= "MPA Status")+
  #scale_shape_discrete(labels=c('Outside','Inside'))+
  #facet_grid(region~MPA_status)+
  #theme(axis.text.x  = element_text(angle=90, vjust=0.5, size=8))+
  geom_hline(aes(yintercept=0),linetype='dashed')+
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank(),
        panel.background = element_blank(), axis.line = element_line(colour = "black"))+
  scale_color_aaas(labels=c('Outside','Inside'))+
  scale_fill_aaas()

#ggpredhii

##RESISTANCE HII
#need the resist dataframe to run this
# Extract the prediction data frame
pred.hiires <- ggpredict(resfinalmodel2, terms = c("hii100km2"))  # this gives overall predictions for the model

# Plot the predictions 
ggpredhiires<-ggplot(pred.hiires) + 
  geom_ribbon(aes(x = x, ymin = conf.low, ymax = conf.high), 
              fill = "lightgrey", alpha = 0.5) +  # error band
  geom_point(data = resist,                      # adding the raw data (scaled values)
             aes(x = hii100km2, y = resistance),alpha=0.3) +
  geom_line(aes(x = x, y = predicted),size=1, color='black') +          # slope
  theme_bw()+
  labs(x = "Scaled Human Influence Index", y = "Resistance")+
  #labs(color= "MPA Status", shape= "MPA Status")+
  scale_color_discrete(labels=c('Outside','Inside'))+
  #facet_grid(region~MPA_status)+
  #theme(axis.text.x  = element_text(angle=90, vjust=0.5, size=8))+
  geom_hline(aes(yintercept=0),linetype='dashed')+
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank(),
        panel.background = element_blank(), axis.line = element_line(colour = "black"))+
  scale_color_aaas(labels=c('Outside','Inside'))+
  scale_fill_aaas()

#ggpredhiires


##just HII (recov + resist)
#ggpredhii
#ggpredhiires

Fig4hii<-(ggpredhii / ggpredhiires)+
  plot_layout(widths=c(1,1))+
  plot_annotation(tag_level='A')+
  plot_layout(guides='collect')
#Fig4hii


#### RECOVERY WCS CML SCORE
#run the linear model
# Extract the prediction data frame
pred.wcs <- ggpredict(finalmodel2, terms = c("cml_scr2"))  # this gives overall predictions for the model
#pred.wcs

ggpredwcs<-ggplot(pred.wcs) + 
  geom_ribbon(aes(x = x, ymin = conf.low, ymax = conf.high), 
              fill = "lightgrey", alpha = 0.3) +  # error band
  geom_point(data = recov,                      # adding the raw data (scaled values)
             aes(x = cml_scr2, y = calculated.recovery.rate),alpha=0.5) +
  geom_line(aes(x = x, y = predicted),size=1, color='black') +          # slope
  theme_bw()+
  labs(x = "Scaled WCS Cumulative Stress Score", y = "Recovery Rate")+
  #labs(color= "MPA Status", shape= "MPA Status")+
  #scale_shape_discrete(labels=c('Outside','Inside'))+
  #facet_grid(region~MPA_status)+
  #theme(axis.text.x  = element_text(angle=90, vjust=0.5, size=8))+
  geom_hline(aes(yintercept=0),linetype='dashed')+
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank(),
        panel.background = element_blank(), axis.line = element_line(colour = "black"))+
  scale_color_aaas(labels=c('Outside','Inside'))+
  scale_fill_aaas()

#ggpredwcs

##RESISTANCE WCS SCORE
# Extract the prediction data frame
pred.wcsres <- ggpredict(resfinalmodel2, terms = c("cml_scr2"))  # this gives overall predictions for the model

# Plot the predictions 
ggpredwcsres<-ggplot(pred.wcsres) + 
  geom_ribbon(aes(x = x, ymin = conf.low, ymax = conf.high), 
              fill = "lightgrey", alpha = 0.5) +  # error band
  geom_point(data = resist,                      # adding the raw data (scaled values)
             aes(x = cml_scr2, y = resistance),alpha=0.3) +
  geom_line(aes(x = x, y = predicted),size=1, color='black') +          # slope
  theme_bw()+
  labs(x = "Scaled WCS Cumulative Stress Score", y = "Resistance")+
  #labs(color= "MPA Status", shape= "MPA Status")+
  scale_color_discrete(labels=c('Outside','Inside'))+
  #facet_grid(region~MPA_status)+
  #theme(axis.text.x  = element_text(angle=90, vjust=0.5, size=8))+
  geom_hline(aes(yintercept=0),linetype='dashed')+
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank(),
        panel.background = element_blank(), axis.line = element_line(colour = "black"))+
  scale_color_aaas(labels=c('Outside','Inside'))+
  scale_fill_aaas()

#ggpredwcsres

###JUST WCS SCORE
#ggpredwcs
#ggpredwcsres

Fig4wcs<-(ggpredwcs / ggpredwcsres)+
  plot_layout(widths=c(1,1))+
  plot_annotation(tag_level='A')+
  plot_layout(guides='collect')
#Fig4wcs

#Patchwork Fig (final fig)
#ggpredhii
#ggpredhiires
#ggpredwcs
#ggpredwcsres

Fig4<-(ggpredhii | ggpredhiires) / (ggpredwcs | ggpredwcsres)+  
  plot_layout(widths=c(1,1,1,1))+
  plot_annotation(tag_level='A')+
  plot_layout(guides='collect')
Fig4
```
Figure 3 has changed slightly from the main text. Panels A and B there are fewer HII=0 points, as many of these were false zeros and have been removed in the re-analysis. There were no apparent trends in Panels B, C, and D in the orignal text and this remains true. In Panel A, though there is a hint of a positive correlation between HII and Recovery Rate, this is no longer statistically significant. In short, there are no clear relationships between either human influence metric and Recovery or Resistance. 





