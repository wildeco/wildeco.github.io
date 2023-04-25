---
title: "Learning notes on Earth Engine + CNN + TensorFlow + Google Cloud"
date: 2023-03-14T15:34:12-05:00
categories:
  - blog
tags:
  - earth engine
  - geospatial
  - deep learning
---

**I have created these notes to document my own learning in integrating GEE + TensorFlow + Vertex AI**.

Over the years, I have worked across a range of GIS and remote sensing application environments. During my undergraduate and later at work I primarily used ArcGIS, IDRISI, and QGIS. Since my masters, I transitioned completely to using open-source softwares like R and Python and while doing a PhD in the year 2018 started to use Google Earth Engine (GEE). GEE started with a big bang in the geospatial community and has been growing ever since. It is a cloud-based platform for planetary-scale geospatial analysis, and provides a large collection of satellite imagery, geospatial datasets, and geospatial analysis tools. 

However, what I learnt over the last three years is that GEE is suitable only for small to medium scale geospatial analysis. I frequently encountered "Computation time out", and the much dreaded "Error: User memory limit exceeded" errors. Moreover, GEE offers a wide range of ML tools for data analysis (e.g., custom models like RF, CART, NaiveBayes SVM etc) but some types of analysis may require additional processing that is not available within the platform e.g., tools for deep learning. I think the limited ML tools in GEE was a major drawback for many researchers and practitioners who wanted to use GEE for big data analytics. 

In early 2019, GEE started to integrate with TensorFlow by adding export and ingest of TFRecord files. This was a major step forward. However, the integration was limited to only exporting and ingesting TFRecord files. Later in the year GEE integrated to Google Cloud's AI Platform, which leveraged the capacity of GEE and the predictive power of TensorFlow. In the **Geo for Good 2022** conference, I got to see Google's announcement of the integration of TensorFlow with GEE and their suggested workflow. The YT video is [here](https://www.youtube.com/watch?v=aiqAN1Zlhdk&t=2114s). An example notebook of using TensorFlow and GEE for deep learning is available [here](https://colab.research.google.com/drive/1QuKj2U5ekiUMYTJC6qpEK3F1unOlCUej?usp=sharing). 

I am convinced that using cloud computing will be necessary in the near foreseable future, given the rapid availability of high resolution data and complex ML tools. While I have experience using AWS Cloud Resources, I have not had any experience using resources in the Google Cloud. So, this is a great opportunity for me to learn and implement some deep learning models using TensorFlow and GEE. 

When to build a custom model: 

* Import/build models in TensorFlow, Keras, PyTorch
* You have large training data (GEE limited to 1 mil rows of training points)
* Build real time models (e.g., Dynamic World)
* When you want to build a **Convolutional Model**. 

**Architecture of integrating GEE with G cloud**

<img src="https://drive.google.com/uc?id=1rqQ2rEWU2AVEcQCJhD6SfDCoh3mIo8Io" alt="Google Drive Image" />
I borrowed (and slightly changed) this slide from the Geo for Good 2022 conference [presentation](https://www.youtube.com/watch?v=aiqAN1Zlhdk&t=2114s) by Google.

In theory, the workflow is quite simple. You will start with getting your data from GEE catalog, and then export it to DataFlow as a TFRecord file (a collection of input and label pairs). DataFlow reduces the time to pull the data and make TFRecord from hours to minutes. Save the record into a Cloud Storage bucket, and then train the model in TensorFlow/Keras using the Vertex AI (a predecessor of G Cloud's AI platform). You can host the model in Cloud Run or visualise the results in Colab notebook and Earth Engine. This is just a quick overview of the workflow. 

Here is another example [run](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/main/people-and-planet-ai/land-cover-classification) that shows the entire workflow. 

Resources: 

You Tube Videos: 

* [People and Planet AI](https://www.youtube.com/playlist?list=PLIivdWyY5sqI-llB35Dcb187ZG155Rs_7)

Slides: 

* [Deep Learning with Tensorflow and Earth Engine](https://docs.google.com/presentation/d/1HcbbEnC0wbGfp-d6qXbVkcBryP0acNlBKeMCsDCUXpw/edit) 


Notebooks: 

* [Land cover classification -- image segmentation](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/main/people-and-planet-ai/land-cover-classification) 
* [Earthengine_TensorFlow_FCNN_demo_2022](https://colab.research.google.com/drive/1QuKj2U5ekiUMYTJC6qpEK3F1unOlCUej?usp=sharing) 
* [Earthengine_TensorFlow_BigEarthnet_demo_2022](https://colab.research.google.com/drive/1pCCddw9gDs3GfoJHRYfriqomYY0O3CH8?usp=sharing)
 
I haven't yet started playing with this workflow, but I will be doing so in the coming weeks. I will update this post with my progress.




