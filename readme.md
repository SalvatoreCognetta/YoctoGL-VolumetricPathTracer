# Yocto/Pathtrace: Tiny Path Tracer

In this homework, you will learn how to build a simple path tracer with support
for subdivision surfaces, displacement and subsurface scattering. 
In particular, you will learn how to 

- handle subdivision surfaces,
- handle normal mapping (we have implemented displacement for you),
- write a path tracer with support for homogeneous volumes.

## Framework

The code uses the library [Yocto/GL](https://github.com/xelatihy/yocto-gl),
that is included in this project in the directory `yocto`. 
We suggest to consult the documentation for the library that you can find 
at the beginning of the header files. Also, since the library is getting improved
during the duration of the course, se suggest that you star it and watch it 
on Github, so that you can notified as improvements are made. 

In order to compile the code, you have to install 
[Xcode](https://apps.apple.com/it/app/xcode/id497799835?mt=12)
on OsX, [Visual Studio 2019](https://visualstudio.microsoft.com/it/vs/) on Windows,
or a modern version of gcc or clang on Linux, 
together with the tools [cmake](www.cmake.org) and [ninja](https://ninja-build.org).
The script `scripts/build.sh` will perform a simple build on OsX.
As discussed in class, we prefer to use 
[Visual Studio Code](https://code.visualstudio.com), with
[C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools) and
[CMake Tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools) 
extensions, that we have configured to use for this course.

You will write your code in the file `yocto_pathtrace.cpp` for functions that 
are declared in `yocto_pathtrace.h`. Your renderer is called by `yscenetrace.cpp` 
for a command-line interface and `ysceneitraces.cpp` that show a simple 
user interface.

This repository also contains tests that are executed from the command line
as shown in `run.sh`. The rendered images are saved in the `out/` directory. 
The results should match the ones in the directory `check/`.

## Functionality

In this homework you will implement the following features:

- **Subdivision Surfaces** in functions `subdivide_catmullclark()`:
    - implement Catmull-Clark subdivision following the slides
    - while the solution should match the one in Yocto/Shape, your 
      implementation _cannot_ use the Yocto one, neither calling it nor 
      adapting the code – I will be able to tell since the Yocto/Shape code 
      supports more features
- **Normal Mapping** in function `eval_normalmap()`:
    - implement normal mapping as per the slides
    - you can use `triangle_tangents_fromuv()` to get tangents
- **Volumetric Path Tracing** in function `trace_path()`:
    - follow the slides and implement a volumetric path tracer
    - you have to also implement all support functions, 
      namely `XXX_transmittance()` and `XXX_scattering()`
    - you can use the corresponding functions in Yocto/Math

## Extra Credit

Here we put options of things you could try to do. For this homework, you
get full extra-credit points only when implementing delta tracking. You 
will still get points if you add some more scenes to the renderer. 

- **Delta Tracking** in path tracer:
    - integrate delta tracking for smoke and clouds
    - based your implementation on 
      [pbrt](http://www.pbr-book.org/3ed-2018/Light_Transport_II_Volume_Rendering/Sampling_Volume_Scattering.html)
    - to integrate it, you have to implement a new `sample_transmittance()` 
      that both samples the distances and returns the weight
    - also you have to add volumes to the renderer, which for now can be a hack
      to either hardcode a function that makes one or use a procedural
    - this should be a hack; you will have the option of writing a full volume 
      renderer in HW04
- **MYOS**, make your own scene:
    - create additional scenes that you can render from models assembled by you
    - in this case, you are only allowed to create
        - a scene that uses subsurface scattering in a prominent manner
        - a scene that uses subdivision surfaces in a prominent manner
        - a _realistic_ scene that looks real; use _only_ the models from 
          [3DModelHaven](https://3dmodelhaven.com) and make it complex
          using many models and all textures
    - also include license files for everything you download

## Submission

To submit the homework, you need to pack a ZIP file that contains the code 
you write and the images it generates, i.e. the ZIP _with only the 
`yocto_pathtrace/` and `out/` directories_.
The file should be called `<lastname>_<firstname>_<studentid>.zip` 
(`<cognome>_<nome>_<matricola>.zip`) and you should exclude 
all other directories. Send it on Google Classroom.
