# EpicFlow

This repository is a modified version of Revaud's EpicFlow (Dec 2014: v1.00) algorithm. 

This code is mentioned only for scientific or personal use.
Please contact Revaud for any algorithm related questions.

### Compiling using CMake (The only part added by Zhaoyang):

Libraries libpng16, libjpg, libm and liblapack are required. 
To build epicflow:

```
mkdir build
cd build
cmake ..
make -j2
```

### Prerequisities

Given two images, you need first to compute edges and matches before running EpicFlow.
You can download the code from these links.
- for edges using SED:  http://research.microsoft.com/en-us/downloads/389109f6-b4e8-404c-84bf-239f7cbf4e3d/
- that will require also Piotr Dollar's toolbox:  http://vision.ucsd.edu/~pdollar/toolbox/doc/index.html
- for matches using Deep Matching:  http://lear.inrialpes.fr/people/revaud

Note that we initially use the first version of SED, whose results are computed using the corresponding model 'modelFinal.mat'. 
More recent versions give similar performance.

### Usage

EpicFlow creates a .flo file in an usual .flo format
(for instance, see Middlebury dataset for code reading/displaying it). 

Type "./epicflow" for list of available options.
An example usage is given here (set paths between <>).

Use matlab
```
matlab -nodesktop -nojvm -r "addpath(<path_to_sed>); 
addpath(genpath(<path_to_piotr_toolbox>)); 
load('modelFinal.mat');
I = imread(<im1name>); 
if size(I,3)==1, I = cat(3,I,I,I); 
end; 
edges = edgesDetect(I, model); 
fid=fopen(<edgefile>,'wb'); 
fwrite(fid,transpose(edges),'single'); 
fclose(fid); 
exit"
<path_to_deepmatching>/deepmatching <im1name> <im2name> -png_settings -improved_settings -out <matchfile>
```

Use C
```
./epicflow <im1name> <im2name> <edgefile> <matchfile> <outputfile> [options]
```

### Citation

If you use our code, please cite our paper:

@inproceedings{revaud:hal-01142656,
  TITLE = {{EpicFlow: Edge-Preserving Interpolation of Correspondences for Optical Flow}},
  AUTHOR = {Revaud, Jerome and Weinzaepfel, Philippe and Harchaoui, Zaid and Schmid, Cordelia},
  BOOKTITLE = {{Computer Vision and Pattern Recognition}},
  YEAR = {2015},
}
 
###LICENCE CONDITIONS

Copyright (C) 2014 Philippe Weinzaepfel

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.


