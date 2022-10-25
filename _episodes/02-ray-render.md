---
# Please do not edit this file directly; it is auto generated.
# Instead, please edit 02-ray-render.md in _episodes_rmd/
title: "Rayrender højdemodeller"
teaching: 0
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---





Enten skal det kun være eksempelkode. Eller også skal jeg uden om problemerne
med at der ikke er et grafisk interface når dette renderes.

This:
<img src="../fig/taiwan.jpg" alt="plot of chunk unnamed-chunk-2" width="400px" style="display: block; margin: auto;" />

Shaded relief map of Taiwan. Made by https://mobile.twitter.com/researchremora

#How to?
These libraries

~~~
library(rgdal)
~~~
{: .language-r}



~~~
Loading required package: sp
~~~
{: .output}



~~~
Error: package or namespace load failed for 'rgdal' in dyn.load(file, DLLpath = DLLpath, ...):
 unable to load shared object '/home/runner/work/_temp/Library/rgdal/libs/rgdal.so':
  libgdal.so.26: cannot open shared object file: No such file or directory
~~~
{: .error}



~~~
library(dplyr)
~~~
{: .language-r}



~~~

Attaching package: 'dplyr'
~~~
{: .output}



~~~
The following objects are masked from 'package:stats':

    filter, lag
~~~
{: .output}



~~~
The following objects are masked from 'package:base':

    intersect, setdiff, setequal, union
~~~
{: .output}



~~~
library(rayshader)
~~~
{: .language-r}



~~~
Error in dyn.load(dynlib <- getDynlib(dir)) : 
  unable to load shared object '/home/runner/work/_temp/Library/rgl/libs/rgl.so':
  libGLU.so.1: cannot open shared object file: No such file or directory
~~~
{: .output}



~~~
Warning: Loading rgl's DLL failed.
~~~
{: .warning}



~~~
Warning: Trying without OpenGL...
~~~
{: .warning}



~~~
Error: package or namespace load failed for 'rayshader':
 .onLoad failed in loadNamespace() for 'rgl', details:
  call: rgl.init(initValue, onlyNULL)
  error: OpenGL is not available in this build
~~~
{: .error}



~~~
library(elevatr)
~~~
{: .language-r}



~~~
Error: package or namespace load failed for 'elevatr' in dyn.load(file, DLLpath = DLLpath, ...):
 unable to load shared object '/home/runner/work/_temp/Library/units/libs/units.so':
  libudunits2.so.0: cannot open shared object file: No such file or directory
~~~
{: .error}



~~~
library(raster)
~~~
{: .language-r}



~~~
Error: package or namespace load failed for 'raster' in dyn.load(file, DLLpath = DLLpath, ...):
 unable to load shared object '/home/runner/work/_temp/Library/terra/libs/terra.so':
  libproj.so.15: cannot open shared object file: No such file or directory
~~~
{: .error}

Getting the boundaries - in this example for Denmark:

~~~
denmark <- readRDS(url("https://geodata.ucdavis.edu/gadm/gadm4.0/Rsf/gadm40_DNK_0_sf.rds"))
~~~
{: .language-r}

Get the elevation from
Amazon Web Services Terrian Tiles and the Open Topography global datasets API:

~~~
dem <- get_elev_raster(denmark, z = 6)
~~~
{: .language-r}



~~~
Error in get_elev_raster(denmark, z = 6): could not find function "get_elev_raster"
~~~
{: .error}



~~~
denmark_dem <- raster::mask(dem, denmark)
~~~
{: .language-r}



~~~
Error in dyn.load(file, DLLpath = DLLpath, ...): unable to load shared object '/home/runner/work/_temp/Library/terra/libs/terra.so':
  libproj.so.15: cannot open shared object file: No such file or directory
~~~
{: .error}



~~~
denmark_mat <- raster_to_matrix(denmark_dem)
~~~
{: .language-r}



~~~
Error in raster_to_matrix(denmark_dem): could not find function "raster_to_matrix"
~~~
{: .error}



~~~
denmark_mat %>% 
  sphere_shade(texture= "imhof3") %>% 
   plot_3d(denmark_mat, windowsize = c(1200,1200),
                     zscale = 20, zoom = 0.75, phi = 89, theta = 0, fov = 0, background = "black")
~~~
{: .language-r}



~~~
Error in plot_3d(., denmark_mat, windowsize = c(1200, 1200), zscale = 20, : could not find function "plot_3d"
~~~
{: .error}



~~~
render_snapshot(filename = "../fig/denmark2.png", samples = 100, width = 6000, height = 6000)
~~~
{: .language-r}



~~~
Error in render_snapshot(filename = "../fig/denmark2.png", samples = 100, : could not find function "render_snapshot"
~~~
{: .error}

<img src="../fig/denmark2.png" alt="plot of chunk unnamed-chunk-10" width="400px" style="display: block; margin: auto;" />

{% include links.md %}
