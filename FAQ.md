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

**Q:** _Why OpenCV does not provide functions with `wchar_t`, `wstring`? What about non-Latin symbols in file names?_  
**A:** OpenCV team decided to stay conservative and do not introduce new API calls with `wchar_t`, `wstring` and other string types By the following reasons:
- Most of image decoding and encoding libraries use standard `fopen` call to open files and extra `wchar_t` support requires domain libraries modification.
- Modern Linux, Mac OS and latest Windows releases support UTF-8 encoding that allows to use `std::string` as container to pass it to OpenCV functions.
- Popular FS, including solutions on Linux does not use `wchar_t` natively and the overloads are not cross platform.

There are 2 alternatives to use `wchar_t` strings with OpenCV (see discussion section for code snippets and solutions):

1. Convert `wchar_t` strings to UTF-8 and pass UTF-8 string as `cv::imread`, `cv::imwrite`, etc parameter. UTF-8 string is handled by system `fopen` call and it's behavior depends on OS support and locale. See `mbstowcs` in C++ standard for more details.

2. OpenCV provides `cv::imdecode` and `cv::imencode` functions that allow to decode and encode image using memory buffer as input and output. The solution decouples file IO and image decoding and allows to manage path strings, locales, etc in user code.  

**Discussion:** [4292](https://github.com/opencv/opencv/issues/4292#issuecomment-601686965), [5631](https://github.com/opencv/opencv/issues/5631), [13368](https://github.com/opencv/opencv/pull/13368)  
 
# Classic Computer Vision

# DNN