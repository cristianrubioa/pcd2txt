# pcd2txt

## Brief

[![C++: solutions](https://img.shields.io/badge/C++-Solutions-blue.svg?style=flat&logo=c%2B%2B)](https://es.wikipedia.org/wiki/C%2B%2B) [![support level: community](https://img.shields.io/badge/support%20level-community-lightgray.png)](http://wiki.ros.org/Industrial)

> C++ application to convert .pcd file (point cloud data) into txt format (xyzi).

## Input file structure

- .pcd

```
# .PCD v0.7 - Point Cloud Data file format
VERSION 0.7
FIELDS x y z intensity
SIZE 4 4 4 1 4 1
TYPE F F F U F U
COUNT 1 1 1 4 1 12
WIDTH 165333
HEIGHT 1
VIEWPOINT 0 0 0 1 0 0 0
POINTS 165333
...
```

Check your .pcd file with: `head <pcd file>`

## Output file structure

- txt_cloud.txt

```
  x      y      z    intensity       # position (not printable)
-0.1    0.1    0.1    0.0741
-0.2    0.2    0.2    0.0762
...     ...    ...    ...
```

Check with: `head txt_cloud.txt`

Visualize 3D point cloud with:
[CloudCompare](https://cloudcompare.org/)

## Dependency

- [pcl](https://pointclouds.org/downloads/) (Point Cloud Library)

You can install pcl using:

```
sudo apt install libpcl-dev
```


## Compile

You can use the following commands to compile the package:

```
git clone https://github.com/cristianrubioa/pcd2txt.git
cd /pcd2txt
mkdir build && cd build
cmake ../src/
make
```

## Run the package

Stand in the "build" folder and run:

```
cd ~/pcd2txt/build
./pcd2txt <pcd file> -o <output dir>
```


