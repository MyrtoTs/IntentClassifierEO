# IntentClassifier
an intent classifier for requests concerning Earth Observation archives.
| Input | Output |
| ----------- | ----------- |
| User's request | Labels |

Example:
| Input | Output |
| ----------- | ----------- |
| Show me all images with ships, within 100 km from the port of Genoa|image search by text,geospatial|

## Description
The intent classifier decides the category in which the user's request falls:
1. Search by image 
2. Search by text 
3. Binary visual QA 
4. Specific algorithms for image segmentation / counting objects / object extraction in images 

Additionally, the intent classifier decides whether the user's request requires geospatial information from Knowledge Graphs.

## Implementation Details
LLMs[^1] used for EO intent classifier implementation:
- **bert-base-nli-mean-tokens**, for sentence similarity (for search by image task)
- **dslim/bert-base-NER** , for geospatial entity recognition
- **myrtotsok/distilbert-base-uncased-EO-intent-classifier-6**, for classification between 3 categories
  created by :
    - fine-tuning **distilbert-base-uncased**
    - with synthetic dataset **myrtotsok/clf-6**

[^1]: All LLMs and our synthetic dataset are available on HuggingFace.

## Intent Classification Examples
|index|User request|Labels|
|---|---|---|
|1|Show me all images with ships, within 100 km from the port of Genoa|image search by text,geospatial|
|2|Does this image contain a rural area?|binary visual question answering|
|3|Are there any vessels in this image?|binary visual question answering|
|4|Count vessels in this image|count/extract/segment|
|5|Extract water bodies|count/extract/segment|
|6|Retrieve Sentinel-2 images containing marine litters\.|image search by text|
|7|Can you gather 20 Sentinel-1 images that bear a resemblance to this one?|search by image|
|8|Show me all images with ships near the port of Genoa|image search by text,geospatial|
|9|Find all the Sentinel 2 images of Rome from 2013|image search by text,geospatial|
|10|Retrieve Sentinel-2 and Sentinel-1 images containing oil-spills in Mexican Gulf\.|image search by text,geospatial|
|11|Retrieve 10 Sentinel-2 images containing marine litters in the Pacific oceans\.|image search by text,geospatial|
|12|Find cloud-free Sentinel-2 images over the ten cities in india with the highest building density|image search by text,geospatial|
|13|Find Sentinel-2 images of the 100km radius area in North America which has the most corn production|image search by text,geospatial|
|14|Retrieve images of Sentinel-2 of intense storms over Italy, on the Latium coast|image search by text,geospatial|
|15|Please locate all peaks over 2000m in central Italy\.|image search by text,geospatial|
|16|I'm requesting 100 patches that are comparable to this one\.|search by image|
|17|Find Sentinel-2 images during summer months of 2020 to be used for sea temperature monitoring|image search by text|
|18|Offer me images that are akin to this one\.|search by image|
|19|Please provide me with 1000 photos that are comparable to this image\.|search by image|
|20|Show me all images with ships near the port of Genoa|image search by text,geospatial|

