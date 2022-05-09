**dataset :** 

Imagenet, Coco and google open images datasets are 3 most popular image datasets for computer vision. these datasets provides millions of hand annotated images with classification labels, bounding boxes for object detections and image segmentation masks. Data collection is the most difficult part in any supervised machine learning problem and availability of such datasets makes training CNNs very easy.

* COCO ([Common Objects in Context](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjCuIWJyaT2AhUXilwKHdV5A4AQFnoECAQQAQ&url=https%3A%2F%2Fcocodataset.org%2F&usg=AOvVaw2uf7n84Wuno9qgkHK-zOGp)) 2017 train/val browser (123,287 images, 886,284 instances). Crowd labels not shown.

* ImageNet .As many as 1,034,908 images have been annotated with **bounding boxes**.
  publicly available dataset called ImageNet .This data includes more than 15 million images
  for nearly 22,000 categories.

*  Open Images V4, a dataset of 9.2M images with unified  annotations for image classification, object detection and visual  relationship detection

  the Open Images dataset includes 9M images annotated with 36M  image-level labels, 15.8M bounding boxes, 2.8M instance segmentations,  and 391k visual relationships.

* Open images is bigger than ImageNet and has more classes which might make the transfer learning work even better ,and ImageNet is not very diverse/inclusive, open images is supposed to be better

  

**[TensorFlow Hub](https://tfhub.dev/)** is a repository of pre-trained TensorFlow models. we can use models from TensorFlow Hub with [`tf.keras`](https://www.tensorflow.org/api_docs/python/tf/keras).

**TF-Hub** module  trained to perform object detection . this contains several models /modules (trained models ) we can use and load any of them .. the following are examples of tf object detection  :

Modules:

- **FasterRCNN+InceptionResNet V2**: high accuracy,

  Object detection model trained on Open Images V4 with ImageNet pre-trained Inception Resnet V2 as image feature extractor. 

  

  

- **ssd+mobilenet V2**: small and fast.

   SSD Mobilenet V2 Object detection model, trained on COCO 2017 dataset. 

  and more ...  in https://tfhub.dev/s?module-type=image-object-detection 

run from tf hub 

https://colab.research.google.com/github/tensorflow/hub/blob/master/examples/colab/object_detection.ipynb#scrollTo=vchaUW1XDodD



***************

###### **TRAIN AN OBJECT DETECTION MODEL FOR A CUSTOM DATASET (TensorFlow 1.x)**

- Collect the dataset of images and label them to get their xml files.

- Install the TensorFlow Object Detection API.

- Generate the TFRecord files required for training. (need generate_tfrecord.py script and csv files for this) the folder called customTF1

- Edit the model pipeline config file and download the pre-trained model checkpoint.

- Train and evaluate the model. ( get error on this )

  ref : 

  https://medium.com/geekculture/training-a-model-for-custom-object-detection-using-tensorflow-1-x-on-google-colab-564d3e62e9ef

  https://colab.research.google.com/drive/1zZVruXSuHZb6RSeBlWXniXQchrBQ4Vx-#scrollTo=ORo9oGPiA8k7

  https://github.com/techzizou/Train-Object-Detection-Model-TF-1.x/blob/main/ssd_mobilenet_v2_coco.config

  https://colab.research.google.com/drive/1qiHLly8oIP3Y3CMh4OJQMSGGvx0xuvn3#scrollTo=sgulgVLLdWeS

  https://medium.com/geekculture/training-a-model-for-custom-object-detection-using-tensorflow-1-x-on-google-colab-564d3e62e9ef#6cb9

  

**********



this solution was succssesful 

**using yolo pytorch : YOLOv5 Custom Object Detection using  google Colab** 

steps :

1. Annotate the images using LabelImg software (get xml file for each image as yolo format)
2. Environment Setup in colab (install the requirments+ amount to my drive)
3. Create training and data config files inside drive (folder is called yolov4)
4. Train our custom YOLOv5 object detector on the cloud (install it then train it based on config file) . config file contain the number of classes and layers  
5. Inferencing our trained YOLOv5 custom object detection model by testing . 

 ref :

 https://machinelearningknowledge.ai/tutorial-yolov5-custom-object-detection-in-colab/ 

https://colab.research.google.com/drive/1JHVWJlWwxAwd0__GViJ29FAZc-ZSbt3a#scrollTo=vi4fGrYBYr3T

https://medium.com/p/61a659d4868#4be1

