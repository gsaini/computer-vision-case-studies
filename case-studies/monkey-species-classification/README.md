# Problem Statement: Monkey Species Classification

## Business Context

In recent years, habitat destruction, climate change, and poaching have led to the extinction of several monkey species, with many more now endangered. To support conservation efforts, a U.S.-based wildlife sanctuary is gathering a vast collection of images of endangered monkey species from different parts of the world. This initiative aims to improve research and protection strategies for these animals.

However, sorting and identifying species within this extensive collection is a major challenge, as many look similar and the volume of data is overwhelming. Without an efficient way to categorize these images, it becomes difficult to track populations, analyze trends, and make informed conservation decisions.

To address this, the sanctuary is working on ways to refine how these images are processed and analyzed. By improving how species are identified and classified, conservationists will be able to gain better insights, making it easier to monitor wildlife and strengthen protection efforts.

## Objective

Develop an image classification model using an Artificial Neural Network (ANN) to categorize endangered monkey species efficiently. By leveraging image preprocessing techniques, the model aims to improve classification accuracy while operating within the sanctuary’s resource constraints, ultimately enhancing conservation efforts.

## Data Description

Due to the large volume of data, the images were converted to the `images.npy` file and the labels are also placed in `Labels.csv`, allowing you to work on the data without being concerned about the large data volume.

The dataset comprises 10 monkey species.

### List of Species

* Mantled Howler
* Patas Monkey
* Bald Monkey
* Japanese Macaque
* Pygmy Marmoset
* White Headed Capuchin
* Silver Marmoset
* Common Squirrel Monkey
* Black Headed Night Monkey
* Nilgiri Langur
