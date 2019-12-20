## Create MacBeth Color Calibration finders and Color Adjustment algorithm

* Author: Gary Bradski
* Link: [The feature request](https://github.com/opencv/opencv/issues/16207)
* Status: **Draft**
* Platforms: **All**
* Complexity: 1-2 man-months

## Introduction and Rationale

Color calibration is extensively used in film and for photometric needs, but OpenCV neglects this basic area. We need to create a couple of functions that will
* Find a MacBeth ColorChecker chart and its homography (robust please to someone holding its corners by hand)
* Return the colors
* Run a color adjustment algorithm on it

## Proposed solution

- Create a function that will robustly find common MacBeth charts (allowing for partial occlusion of hands holding the corners) and their homography
   - [This one](https://www.bhphotovideo.com/c/product/1014557-REG/dgk_color_tools_dkk_set_of_2_dkk_poly_bag_2.html/?ap=y&ap=y&smp=y&smp=y&lsft=BI%3A514&gclid=CjwKCAiA3OzvBRBXEiwALNKDP9L-mJu6IEZO3qlDo4SD_CHNb6MevNkPl4AuVk5dxSzfcrYr2IhghRoC4bcQAvD_BwE)
   - and the [standard one](https://www.edmundoptics.com/p/large-x-rite-colorchecker/4243?gclid=CjwKCAiA3OzvBRBXEiwALNKDPy5GoLSCEXkDR5sDTSyf5GnrYpKjdcMKPqIIvISZ_ljhwD8_WLjXWxoCx9YQAvD_BwE)
- Rectify the chart and find each color value in order (detecting partial occlusion of say hands holding he corners)
- Apply a color correction algorithm
   - [Linear correction matrix](http://www.imatest.com/docs/colormatrix/)
   - [More extensive list of linear and polynomial corrections](http://im.snibgo.com/col2mp.htm)


## Impact on existing code, compatibility

Overall, the external API will not change.

## Possible alternatives

Many, you could find the chart and correct colors using a trained deepnet. It would be good to create the above functions and then maybe a toolbox app that ran them.

## References

* [Macbeth chart](https://en.wikipedia.org/wiki/ColorChecker)
   - [Linear correction matrix](http://www.imatest.com/docs/colormatrix/)
   - [More extensive list of linear and polynomial corrections](http://im.snibgo.com/col2mp.htm)
   - [Vinyl Macbeth Chart](https://www.bhphotovideo.com/c/product/1014557-REG/dgk_color_tools_dkk_set_of_2_dkk_poly_bag_2.html/?ap=y&ap=y&smp=y&smp=y&lsft=BI%3A514&gclid=CjwKCAiA3OzvBRBXEiwALNKDP9L-mJu6IEZO3qlDo4SD_CHNb6MevNkPl4AuVk5dxSzfcrYr2IhghRoC4bcQAvD_BwE)
   - [Standard Macbeth chart](https://www.edmundoptics.com/p/large-x-rite-colorchecker/4243?gclid=CjwKCAiA3OzvBRBXEiwALNKDPy5GoLSCEXkDR5sDTSyf5GnrYpKjdcMKPqIIvISZ_ljhwD8_WLjXWxoCx9YQAvD_BwE)
- Rectify the chart and find each color value in order (detecting partial occlusion of say hands holding he corners)