The page contains Frequently Asked Questions and Answers for them and list of well known problems with links to related discussions.

# Build & Install
**Q:** _OpenCV has very powerful testing framework, but it's not a part of distribution. Why?_  
**A:** "ts" is internal module, it is not designed for using it externally - so it was removed from regular public modules list.
You may consider [opencv_contrib](https://github.com/opencv/opencv_contrib) approach of developing OpenCV external modules. (`-DOPENCV_EXTRA_MODULES_PATH=path1\;path2` - note on backslash before `;`, required by "bash").  
**Discussion:** [#8408](https://github.com/opencv/opencv/issues/8408)  
  
**Q:** _OpenCV build fails with internal compiler error (a.k.a ICE) or segmentation fault on my ARM board. What can I do?_  
**A:** OpenCV team does not work on such kind of bug reports and the best solution for it is to file bugs to compiler team. However there are several popular solutions to fix the problem:
- Reduce amount of build jobs in make and even remove `-j` option from `make` command line. Each build job is dedicated compiler process that consumes RAM. Serial build without `-j` consumes minimal amount if RAM.
- Add swap space in your OS. Relates to previous one.
- Use cross compilation approach:[link](https://docs.opencv.org/master/d0/d76/tutorial_arm_crosscompile_with_cmake.html)
- Update compiler.  

**Discussion:**  

# Hardware & OS

# Video I/O, Image I/O, Data serialization

# Classic Computer Vision

# DNN