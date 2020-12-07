---
marp: true
---

# Faster R-CNN

<div style="text-align: center;margin-top: 0%;">
<img width="50%" src="/assets/images/faster_r_cnn/faster_rcnn.png">
<div/>

------

## Region Proposal Network (RPN)
![alt text](/assets/images/faster_r_cnn/rpn.jpeg "RPN model")

------

## Region Proposal Network (RPN)

* Anchors are labelised as **positive** if :
    * it has the highest IoU with a groundtruth box
    * it has an IoU greater than 0.7 with any groundtruth box.
* Anchors are labelised as **negative** if :
    * its IoU with all groundtruth boxes is less than 0.3
* Other aren't used in training

------

## Compare
![alt text](/assets/images/faster_r_cnn/faster_rcnn_comparaison.png "Compare Faster R-CNN with R-CNN and Fast R-CNN")

------

## Result
![alt text](/assets/images/faster_r_cnn/faster_result.png "Result of Faster R-CNN")
