# YOLOv5_DOTA_OBB
YOLOv5 in DOTA_OBB dataset with CSL_label.(Oriented Object Detection)


## Datasets and pretrained checkpoint
* `Datasets` : [DOTA](https://captain-whu.github.io/DOTA/dataset.html)
* `How to set the DOTA dataset for training and testing` : [DOTA_devkit](https://github.com/CAPTAIN-WHU/DOTA_devkit)


## Fuction
* `train.py`.  Train.

* `detect.py`. Detect and visualize the detection result. Get the detection result txt.

* `evaluation.py`.  Merge the detection result and visualize it. Finally evaluate the detector



## Installation  (Linux Recommend, Windows not Recommend)
`1.` Python 3.8 or later with all requirements.txt dependencies installed, including torch>=1.7. To install run:
```
$   pip install -r requirements.txt
```
`2.` Install swig
```
$   cd  \.....\yolov5_DOTA_OBB\utils
$   sudo apt-get install swig
```
`3.` Create the c++ extension for python
```
$   swig -c++ -python polyiou.i
$   python setup.py build_ext --inplace
```

## Usage Example
`1.` `'Get Dataset' `
 
* Split the DOTA_OBB image and labels. Trans DOTA format to YOLO longside format.

* You can refer to  [hukaixuan19970627/DOTA_devkit_YOLO](https://github.com/hukaixuan19970627/DOTA_devkit_YOLO).

* The Oriented YOLO Longside Format is:

```
$  classid    x_c   y_c   longside   shortside    Θ    Θ∈[0, 180)


* longside: The longest side of the oriented rectangle.

* shortside: The other side of the oriented rectangle.

* Θ: The angle between the longside and the x-axis(The x-axis rotates clockwise).x轴顺时针旋转遇到最长边所经过的角度
```
`WARNING: IMAGE SIZE MUST MEETS 'HEIGHT = WIDTH'`

![label_format_demo](./label_format_demo.png)

`2.` `'train.py'` 

* All same as [ultralytics/yolov5](https://github.com/ultralytics/yolov5).
* Single GPU training:
```
$ python train.py  --batch-size 4 --device 0
```


`3.` `'detect.py'` 
    

```
$  python detect.py
```


`4.` `'evaluation.py'` 

* Run the detect.py demo first. Then change the path with yours:
```
evaluation
(
        detoutput=r'/....../DOTA_demo_view/detection',
        imageset=r'/....../DOTA_demo_view/row_images',
        annopath=r'/....../DOTA_demo_view/row_DOTA_labels/{:s}.txt'
)
draw_DOTA_image
(
        imgsrcpath=r'/...../DOTA_demo_view/row_images',
        imglabelspath=r'/....../DOTA_demo_view/detection/result_txt/result_merged',
        dstpath=r'/....../DOTA_demo_view/detection/merged_drawed'
)
```

* Run the evaluation.py demo. Get the evaluation result and visualize the detection result which after merged.
```
$  python evaluation.py
```