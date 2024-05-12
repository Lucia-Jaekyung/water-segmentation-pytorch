# water-segmentation-pytorch

## Description

- Subject: stagnant water segmentation
- Priod: 2022.09.06 ~ 2022.10.19 
    
    | schedule | contents |
    | --- | --- |
    | 09.06 ~ 09.30 | Data Labeling, Data Preprocessing |
    | 10.01 ~ 10.11 | modeling, train, test (Faster RCNN, Mask RCNN (epoch = 12), UNet) |  
    | 10.13 ~ 10.17 | modeling, train, test (Mask RCNN (epoch = 24)) |
    | 10.19 | PT |

## Information

### Environment

> Colab Pro  
Python: 3.7.15  
GPU: K80, T4 or P100  
RAM: 24.45GB  
Pytorch: 1.12.1 cu113  
> 

### Prerequisite

> mmcv-full  
mmdetection  
pytorch  
> 

### Data Set
  ||description|
  |-|-|
  |source|https://www.youtube.com/watch?v=_e_bzlDej5U&list=WL&index=15&t=209s&ab_channel=물축꾸리|
  |length|Selected portion from original video (2 minutes 43 seconds out of 18 minutes 40 seconds)|
  |resolution|1280*720 pixels|
  |frames|Extracted from original 30fps to 10fps for labeling and training, utilizing a total of 1627 frames|

### Structure

```
├── data
│   ├── Annotations
│   │   ├── COCODataset          # JSON files optimized for MMDetection in COCODataset format
│   │   └── OnetoOne             # JSON files corresponding one-to-one with images
│   │       ├── test_json
│   │       ├── train_json
│   │       └── val_json
│   └── Images
│       ├── MaskImages           # Masking images created based on labeling
│       │   ├── pixel_accuracy   # Images for PA calculation
│       │   │   ├── mask         # Masking images created based on labeling
│       │   │   ├── origin       # Model predicted images (3-dimensional)
│       │   │   └── output       # Model predicted images (1-dimensional)
│       │   ├── test
│       │   ├── train
│       │   │   └── mask_256     # Masking images of size (256, 256)
│       │   └── validation
│       │       └── mask_256
│       ├── OriginalImages       # Original images used for model training
│       └── Remainder            # Remaining images not used for model training
├── notebooks                    # IPython notebooks used for model implementation
└── models                       # Mask RCNN model

```

## Performance
1. Result Images
- train set inference image  
  <img width='663' src='https://user-images.githubusercontent.com/105214855/196437313-de2d7965-0405-4e6d-aa60-ebfc1202c836.png'>

- validation set inference image  
  <img width='663' src='https://user-images.githubusercontent.com/105214855/196437383-5ef76bcb-0cbf-47dc-a1a5-d4fad0c44b9a.png'>

- test set inference image  
  <img width='663' src='https://user-images.githubusercontent.com/105214855/196437489-d7a04a90-755c-4ce0-801a-4b44f2479d2d.png'>

2. AP(Average Precision)
- Performance as per Mask RCNN paper: AP = 35.7
  <img width="663" alt="Untitled (1)" src="https://user-images.githubusercontent.com/65541236/197061374-44dc501c-d1b8-4d7d-a398-33895a0e6e1f.png">  
- Performance of the final model for the project: AP = 36.6
  <img width="663" alt="Untitled (2)" src="https://user-images.githubusercontent.com/65541236/197061477-b735e88b-41d8-4080-ab05-2a5a1a0d44bb.png">

3. PA(Pixel Accuracy)  
![그림1](https://user-images.githubusercontent.com/65541236/197062525-675c558c-03ed-4f29-b5a7-a2e9e5238d95.png)  
Showing 92%, 97%, and 76% accuracy from top to bottom.
