LATEST CHANGES
--------------

- 2014-08-05 camera views can have different dimensions 
- 2014-08-05 camera numbers can be arbitrary (not necessary in the range (0, number of cameras - 1))

INTRODUCTION
------------

  The Probabilistic Occupancy Map is a procedure which estimates the
  marginal probabilities of presence of individuals at every location
  in an area of interest under a simple appearance model, given binary
  images corresponding to the result of a background-subtraction from
  different viewpoints.

  The appearance model is parametrized by a family of rectangles which
  approximate the silhouettes of individuals standing at every
  location of interest, from every point of view.

INSTALLATION AND TEST
---------------------

  This program should compile by typing `make' on any standard
  GNU/Linux system, as long as the libpng is installed with its header
  files.

  To run a simple test on the images provided in the archive just type

    ./pom test.pom

  It will generate several result files in the /tmp directory.

  If the program is not provided with a filename, it will process the
  standard input, but will not make any output.

CONFIGURATION FILE
------------------

The configuration file contains the following keywords

`ROOM <view width> <view height> <number of cameras> <number of locations>`

Defines the input image size, the number of cameras and the number
of locations in the area of interest. In case of differently sized images 
for each camera set the `<view width>` and `<view height>` to -1 and
specify the camera view sizes by the CAMERA keyword.
    
`CAMERA <camera number> <view width> <view height>`
  
Defines the input image size for a camera. Used only in the case 
of differently sized images. The dimensions have to be defined for
all the cameras specified in the ROOM keyword `<number of cameras>` parameter.
`<camera number>` can be arbitrary nonegative number.

`RECTANGLE <camera number> <location number> notvisible|<xmin> <ymin> <xmax> <ymax>`

Defines the parameters of a certain rectangle, standing for an
individual at a certain location viewed from a certain camera. All
non-specified rectangles are "not visible" by default.             

`INPUT_VIEW_FORMAT <input image filename format>`

Specifies the filenames of the input images produced by the
background subtraction. The immobile parts should be black (0, 0,
0) and the moving ones white (255, 255, 255). See FILENAME FORMAT
below.

`RESULT_VIEW_FORMAT <result image filename format>`

Specifies the filenames of the result images. See FILENAME FORMAT
below.

`RESULT_FORMAT <result filename format>`

Specifies the filenames of the result probability files, which
contains one marginal probability per line, hence as many lines as
there are locations of interest. See FILENAME FORMAT below.

`CONVERGENCE_VIEW_FORMAT <convergence file name format>`

Specifies the filenames of the images for individual iteration
during the convergence of the algorithm. Use with care, since tens
of images will be produced for every single frame.  See FILENAME
FORMAT below.

`PRIOR`

Sets the prior probability of presence (common to all
locations). Default is 0.01.

`SIGMA_IMAGE_DENSITY`

Sets the variance of the distance between the image produced by
the background subtraction and the ideal synthetic image. Default
is 0.01.

`MAX_NB_SOLVER_ITERATIONS`

Sets a bound on the number of iterations. Default is 100.

`PROBA_IGNORED`

Sets the probability of absence ignored by the solver to speed up
the convergence (use with care, it can produce false
positive). Default is 1.0
    
`PROCESS <first frame> <num frames>`
  
Last keyword in the configuration file. Starts processing of `<num frames>`
from `<first frame>`.

The file test.pom provided in the archive gives an example. Lines
starting with "#" are ignored.

FILENAME FORMAT
---------------

Every filename format in the configuration file is a string with the
following three "conversion specifications":

- %c camera number
- %f frame number
- %i iteration number

Some of these fields may be meaningless, depending with the
context. For instance the iteration number is defined only for
CONVERGENCE_VIEW_FORMAT.

REFERENCES
----------

  For more information about the POM algorithm, please check the
  section V and appendix A of:

  François Fleuret, Jérôme Berclaz, Richard Lengagne and Pascal Fua,
  "Multi-Camera People Tracking with a Probabilistic Occupancy Map",
  IEEE Transactions on Pattern Analysis and Machine Intelligence
  (TPAMI), 2008, 30(2), 267--282.

  This distributed version of the software is slightly slower than the
  one described in the article, for which many values such as the
  image size were hard-coded in the source to let the compiler
  optimize the code.

LICENSE
-------

  This source code is available under the terms of the version 3 of
  the GNU General Public License as published by the Free Software
  Foundation.

  In short: If you distribute a software that uses POM, you have to
  distribute it under GPL version 3, hence with the source
  code. Another option is to contact us to purchase a commercial
  license.

CONTACT
-------

  Please mail pom@epfl.ch for bug reports, comments and questions.  
  
## build  
-------
1. error: 'memset' was not declared in this scope  
  #include <string.h>  
2. error: invalid use of incomplete type 'png_info' {aka 'struct png_info_def'}  

Since libpng-1.5.0, direct access to these structs is not allowed. So, I have change the other code.  
png_get_rowbytes(png_ptr, info_ptr)  

  //color_type = info_ptr->color_type;  
  color_type = png_get_color_type( png_ptr,  info_ptr);//by hua  
  //bit_depth = info_ptr->bit_depth;  channels = info_ptr->channels;  
  bit_depth = png_get_bit_depth( png_ptr,  info_ptr);//by hua  
  channels = png_get_channels( png_ptr,  info_ptr);//by hua  
  http://www.libpng.org/pub/png/libpng-1.2.5-manual.html#section-4.3  
  
