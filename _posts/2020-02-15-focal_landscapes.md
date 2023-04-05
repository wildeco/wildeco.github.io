---
title: "Identifying focal landscapes for private land conservation"
date: 2020-02-15T15:34:30-04:00
categories:
  - blog
tags:
  - conservation planning
  - private land conservation
  - ecological vegetation
---

![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1e/View_over_Wodonga%2C_Victoria_in_1988.jpg/800px-View_over_Wodonga%2C_Victoria_in_1988.jpg?20091125100921)

Woodonga, Victoria 1988 [Photo](https://commons.wikimedia.org/wiki/File:View_over_Wodonga,_Victoria_in_1988.jpg) by [Phillip Capper](https://www.flickr.com/photos/42033648@N00)

## Introduction
In the context of the global biodiversity crisis and accelerating climate change, it is increasingly important to focus on the protection and conservation of areas which help improve the ‘Adequacy’  of the reserve system. Maintaining and improving the viability and condition of biodiversity and ecosystems is also a key objective of [National Reserve System (NRS) of Australia](https://www.dcceew.gov.au/environment/land/nrs) and conservation planning (CMP 2007). The NRS is a network of protected areas that are managed by the Australian Government and the States and Territories. The NRS is designed to protect the most important areas for biodiversity conservation (e.g., threatened species and ecological communities) and to provide a network of protected areas that are representative of Australia’s biodiversity. 

In Victoria, Australia, this issue is complicated by the fact that many of its under-represented ecosystems and threatened species occur primarily on private land but often in small, isolated remnants across the two-thirds of Victoria which is freehold land (TFN 2013). The Victorian Government has committed to protecting 12% of Victoria’s land area by 2020, and 20% by 2030. However, the current protected area network is only 8.5% of Victoria’s land area (TFN 2013).

## Objectives
To identify a set of “focal landscapes” that provide the best opportunities for maintaining and improving viable ecosystems and species on private land in Victoria, Australia. 

## Method   
### Selection of biodiversity features
We selected 3 biodiversity features that are under-represented in the NRS and are also important for the maintenance of viable ecosystems and species on private land. These features are:

* Proportion of EVC remaining: EVC depletion level is the percentage of EVC remaining and provides an objective assesment of the quality of the vegetation. 
![Proportion of EVC remaining](/assets/images/fl/evc_remain.png)

* Proportion of EVC on private land: 
![Proportion of EVC remaining](/assets/images/fl/evc_proportion_on_pl.png)

* Habitat priority for threatened species: Higher ranking indicates areas that would best complement public land conservation values. The layer is created using Zonation with higher weightage to threatened species.
![Habitat priority](/assets/images/fl/habitat.png)   

* [Ecological Vegetation Classes (EVCs)](https://www.environment.gov.au/biodiversity/abrs/online-resources/fauna/evc) that are under-represented in the NRS. 

### Relative priority index
We calculated a relative priority index using the 3 biodiversity features, using the following formula:

* Relative priority index = EVC proportion on private land / EVC depletion level x Habitat priority

### Aggregation, connectivity, and thresholding
Focal landscapes are concerned with general and not species-specific movements, thus structural connectivity method was applied. Different methods to apply structural connectivity are available, we used the distribution/gaussian smoothing (a parametric single feature connectivity option) and used the [Google Earth Engine](https://earthengine.google.com/) to implement the method. We then thresholded the priority values to remove patches with low connectivity. We used a threshold of 5000 ha, which means only patches greater than 5000 ha were included in the focal landscapes. We tested different sigma parameters and used sigma 2 for this analysis.

![Impact of different sigma parameters](/assets/images/fl/gaussian.png)

## Final focal landscapes

We identified ~ 70 patches of private land that are important for maintaining and improving viable ecosystems and species on private land in Victoria, Australia. These patches are shown in the map below. Collectively the patches represent about 1.8 million ha of significant biodiversity value from the total of 14 million of private land in Victoria

![Focal landscapes](/assets/images/fl/result2.png)

## References 

CMP (2007). Open Standards for the Practice of Conservation. Version 2.0 Conservation Measures Partnership

Trust for Nature (2013). Trust for Nature’s Statewide Conservation Plan for Private Land in Victoria

Verboom, J., Foppen, R., Chardon, P., Opdam, P. & Luttikhuizen, P. (2001). Introducing the key patch approach for habitat networks with persistent populations; an example for marshland birds. Biological Conservation 100: 89-101.










