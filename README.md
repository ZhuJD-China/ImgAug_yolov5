# ImgAug_yolov5
## This approach uses Data Augmentation to generate new samples given a training/validation dataset without the Keras Augmentation.

Prerequisites
They are the same as YOLOv5, but make sure you have already installed them.

Recall: YOLOv5 requires the dataset to be in the darknet format. Here’s an outline of what it looks like:
- One txt with labels file per image
- One row per object
- Each row is class x_center y_center width height format.
- Box coordinates must be in normalized xywh format (from 0 - 1). If your boxes are in pixels, divide x_center and width by image width, and y_center and height by image height.

Class numbers are zero-indexed (start from 0).
    Example:
    
    Image properties: width=1156 pix, height=1144 pix.
    bounding box properties: xmin=1032, ymin=20, xmax=1122, ymax=54, object_name="Ring".
    Let objects_list="bracelet","Earring","Ring","Necklace"
    YOLOv5 format: f"{category_idx} {x1 + bbox_width / 2} {y1 + bbox_height / 2} {bbox_width} {bbox_height}\n"

    𝑏𝑏𝑜𝑥𝑤𝑖𝑑𝑡ℎ=𝑥𝑚𝑎𝑥/𝑤𝑖𝑑𝑡ℎ−𝑥𝑚𝑖𝑛/𝑤𝑖𝑑𝑡ℎ=(1122−1032)/1156=0.07785467128027679 
    𝑏𝑏𝑜𝑥ℎ𝑒𝑖𝑔ℎ𝑡=𝑦𝑚𝑎𝑥/ℎ𝑒𝑖𝑔ℎ𝑡−𝑦𝑚𝑖𝑛/ℎ𝑒𝑖𝑔ℎ𝑡=(54−20)/1144=0.029720279720279717 
    𝑥𝑐𝑒𝑛𝑡𝑒𝑟=𝑥𝑚𝑖𝑛/𝑤𝑖𝑑𝑡ℎ+𝑏𝑏𝑜𝑥𝑤𝑖𝑑𝑡ℎ/2=0.9316608996539792 
    𝑦𝑐𝑒𝑛𝑡𝑒𝑟=𝑦𝑚𝑖𝑛/ℎ𝑒𝑖𝑔ℎ𝑡+𝑏𝑏𝑜𝑥ℎ𝑒𝑖𝑔ℎ𝑡/2=0.032342657342657344 
    category_idx=2
    Final result: 2 0.9316608996539792 0.032342657342657344 0.07785467128027679 0.029720279720279717

## some functions:
* Data Reading and Storage Functions
* Photometric Transformations
* Geometric Transformations¶
* Random Occlusion
* Deep Learning based Approaches (experimental)
        
        Suggested Labeling for TTA
        gaussian noise: _GN
        localvar noise: _LN
        poisson noise: _PN
        salt noise: _SN
        pepper noise: _PP
        salt&pepper: _SP
        speckle noise:_SE
        gray: _GR
        Histogram Equalization: _HE
        shear x: _SX
        shear y: _SY
        flip lr: _LR
        flip ud: _UD
        rotation 90: _R90
        rotation 180: _R180
        rotation 270: _R270
        random erasing: img _RE
