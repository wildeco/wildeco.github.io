---
title: "Research areas"
layout: categories
permalink: /research/
author_profile: true
---

My research interests are in the intersection of ecology, conservation science, data science, and machine learning.

## Causal Inference and Impact Evaluation ##

<img align="right" width="350" height="150" src="https://imgs.xkcd.com/comics/correlation.png">

Causal inference is the process of inferring the causal effect of an intervention on an outcome. It is a fundamental component of science and is used in many fields, including medicine, economics, and social sciences, and conservation. Causal inference is hot topic in the field of data science, including in AI. Impact evaluation is a discpline that uses causal inference and 'counterfactual' thinking to evaluate the impact of interventions on outcomes. My research interests are developing novel impact evaluation frameworks in conservation, and to apply them to real-world conservation problems. As an interdiscplinary researcher, I integrate methods from remote sensing, statistics, machine learning, and data science to develop novel evaluation frameworks. I am particularly interested in developing methods that can be used to evaluate the impact of conservation programs and policies, and to predict future impact. I am currently working on a project to evaluate the impact of conservation programs and policies in Australia they are: 

* Evaluating impact of private protected areas: Typically, conservation programs are evaluated by estimating the average impact at the program level, which allows for comparisons between programs or regions but masks the variation in impact across individual program units. In this research, we develop a reliable and clear methodology that includes synthetic control design, statistical matching, and time series data on woody vegetation cover to estimate the impact of individual protected areas over time. We also demonstrate how the impact at the individual level can be combined to estimate program-level impact using a meta-analytic approach. The framework was utilised to evaluate the impact of conservation agreements in Victoria, Australia. The research paper is currently in a peer review in *Conservation Biology*. 
  
* Predicting future impact of conservation agreements: Impact evaluation in conservation are typically done after the programs have been implemented, which limits their usefulness in predicting future performance due to changes in ecosystems and policies. Additionally, the long time lags between implementation and response make it difficult to capture the true impact of newly implemented programs using conventional evaluation methods. To address this issue, predictive models should be used to evaluate future impact. Despite the extensive work that has been done on ex-post evaluations, there has been little emphasis on utilising forecasting and predictive methods to estimate impact in conservation. In this research project, we develop predictive framework to estimate the impact of conservation interventions on biodiversity. 

---

## Spatial conservation prioritisation ##

<img align="right" width="350" height="300" src="https://dmpublisher.s3.us-west-2.amazonaws.com/2022/February/17/6/3d0bb6c7-5db6-4701-be61-b254d0f2a791-sized">

Systematic conservation planning is a well-established discipline which has been used to inform reserve design in many parts of the world. Most of these approaches, however, have focused on the representation of ecosystem units at various scales and the loss of ecosystems if they are not reserved. The importance of achieving impact in conservation is growing in recent decades – where the outcomes of already implemented programs is compared to a counterfactual scenario where the program is not implemented. However, much of the research has focused on evaluating past conservation programs – and not much to conduct an ex-ante evaluation which are evaluations done before the program is implemented. In the context of achieving impact - rather than preserving ‘residual areas’ which would be intact regardless of protection, it is increasingly important to focus on the protection and conservation of areas which help deliver higher impact alongside maintaining and enhancing the integrity and viability of ecosystems and species. These kinds of ex-ante evaluations would be extremely useful in conservation planning such that reserves are established on areas to maximizing impact. We are developing a framework to conducting ex-ante conservation impact to develop a conservation plan for private land conservation in Victoria. The planning is done in two steps; first is the identification of high value biodiversity private land and second, within these private lands to identify and prioritize land parcels that will deliver conservation impact over the years. 

---
## Predictive modelling deforestation, species distribution, and land-use change ##

<img align="right" width="350" height="300" src="https://www.iucn.org/sites/default/files/2022-12/deforestation-in-surinam-britta-jaschinski-iucn-nl.jpg">

Predictive modelling can be used to associate outcome with a set of predictors. For example, a predictive model can be used to predict the probability of a species occurrence based on environmental variables such as climate, land cover, and topography or to predict the probability of deforestation based on land use and socioeconomic variables. Predictive models can be used to identify areas where a particular outcome is most likely to occur, and can be used to inform conservation and land-use planning efforts. For example, a predictive model can be used to identify areas where conservation efforts are most needed, or where land-use policies and regulations may need to be strengthened to prevent further deforestation. 

Currently, I am working in a project to develop a predictive model to predict the risk of woody vegetation clearing in the NSW state, Australia. The model is based on a XGBoost algorithm and uses a combination of satellite imagery, land use, and socioeconomic variables. The model was developed through comprehensive experiments on hyperparameters, feature engineering, and model selection. Amazon's AWS cloud computing resources were utilised to develop the model. The model outputs are currently being used to identify areas where conservation efforts are most needed, and to identify areas where land-use policies and regulations may need to be strengthened to prevent further clearing. 

I like model based Bayesian methods and probabilistic machine learning, and working on utilising them in several other projects e.g., species distribution models, and human-leopard conflict in India and Nepal.  

---