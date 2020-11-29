---
marp: true
---

## YOLO (You Only Look Once)
- Real time object detection algorithm
- Requires only one forward propagation to make predictions
- Outperforms other detection methods
![alt text](/assets/images/yoloExample.jpg "YOLO Example")

---

### Workflow
- Resolves object detection as a regression problem
- Splits input image to NxN grid and gives confidence score for each cell
- Neural Network : 24 convolution layers followed by 2 fully connected layers
![alt text](/assets/images/yoloNN.png "YOLO Neural Network")

---

### Performance
- Adjustements and improvements in v2 (v3 and v4 also exist)
- Better and faster overall
- Trained on VOC 2012 on following comparaison
![alt text](/assets/images/yoloPerformance.png "YOLO Performance")