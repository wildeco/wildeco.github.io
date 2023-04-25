---
title: "Evaluating spatio-temporal trends of leopard-human conflict in Kathmandu"
date: 2019-02-18T15:34:30-04:00
categories:
  - blog
tags:
  - human-wildlife conflict
  - leopard urban
  - biodiversity
---

![](https://images.pexels.com/photos/1319504/pexels-photo-1319504.jpeg)
[Photo](https://images.pexels.com/photos/1319504/pexels-photo-1319504.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1) by [Magda Ehlers](https://www.pexels.com/@magda-ehlers-pexels/) from Pexels

## Introduction ##

Human-wildlife conflict has become an increasingly pressing issue in today's world as the human population continues to expand and encroach on natural habitats. The conflicts that arise from this interaction between humans and wildlife can have detrimental effects on both parties involved. Leopard-human conflict is a specific type of human-wildlife conflict that has become a significant issue in many parts of the world. Leopards are highly adaptable animals that can thrive in a variety of habitats, including forests, grasslands, and even urban areas. As such, they often come into contact with humans, which can lead to conflict. It is crucial to understand the nature of these conflicts, their causes, and their impact on both humans and wildlife in different contexts and over time. 

Understanding the spatio-temporal patterns of leopord-human conflict helps to: 

* Determine which areas are most at risk and help develop effective mitigation strategies. 
* Gain insight into the underlying causes of these conflicts (e.g., habitat loss, land use change, agricultural practices, prey abundance).

Spatio-temporal statistics provide useful tools for understanding the conflict patterns, and there are a range of tools such as point pattern analysis, kernel density estimation, among others. One quick and easy tool is provided by ArcGIS, which is a tool for [emerging hotspot analysis](https://pro.arcgis.com/en/pro-app/latest/tool-reference/space-time-pattern-mining/emerginghotspots.htm).  One advantage of this method is that it doesn't require data on the underlying drivers of conflict (e.g., habitat loss, land use change, agricultural practices, prey abundance), so it will be useful as a tool where such data is not available, and where the interest is to only identify areas where conflicts are most likely to occur. Here I use a sample of 345 records of conflicts recorded by household survey conducted in 2019 in Kathmandu valley, Nepal. Further, I also explore how the conflict trend and human population trend (Sen's slope) overlap. 


## Workflow ## 

Step 1: Aggregate the conflict points into a [space-time bins](https://pro.arcgis.com/en/pro-app/latest/tool-reference/space-time-pattern-mining/learnmorecreatecube.htm)

Step 2: Convert to a netCDF data cube format 

Step 3: For each bin a Getis-Ord Gi statistic is calculated, and the Mann-Kendall trend test is calculated for each bin's time series - the Getis-Ord Gi statistic measure the intensity of clustering of high or loss values of conflict in a bin relative to it's neighboring bins in the data cube. The sum of the bin and its neighbors is compared to the sum of all bins in the data cube. The Getis-Ord Gi statistic generates Z scores (standard deviations) and P values (statistical probabilities) for each bin that indicate whether forest loss in a given bin is statistically clustered compared to loss in neighboring bins, as well as loss across the entire
analysis domain.


The results show that the south-western region of the valley has detected high risk of conflict. Further, there are random conflicts in north region, with no detectable patterns. There appears to be some positive correlation between conflict hotspots and increasing population density (we need to conduct a statistical test to confirm this). Also, the results are sensitive to the neighborhood size and time step used in the analysis (as neighborhood size increases, the number/intensity of hotspots decreases) so sensitivity analysis should be performed when using this method.

In any case, you will get the output as something like this, which shows which areas are the emerging hotspots for conflict, and which areas have some random conflict without any apparent trend. 

![Conflict map!](/assets/images/conflict_leo_ktm/conflict.jpg "Conflict map")

### This work is in progress !!!!!!! ###

## References

Sharma, P., Chettri, N., & Wangchuk, K. (2021). Human–wildlife conflict in the roof of the world: Understanding multidimensional perspectives through a systematic review. Ecology and Evolution, 11(17), 11569-11586. 
