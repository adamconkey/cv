# Geometric Verification

In this chapter, we will build off of the feature matching example from the previous chapter by utilizing feature matches, together with information about the camera, to infer camera motion between the images being compared. We will see a few new concepts including camera parameters, consensus algorithms, and estimators. 


## Camera Parameters

In order to relate image features to objects in the 3D scene captured by the camera, we require a parameterization to convert between 3D space and image coordinates. We will briefly intrinsic and extrinsic parameters and how they work together to achieve this mapping. 

### Intrinsics
The pinhole camera model a common camera parameterizeration, which is an idealized model that constructs the projected image based on how light beams would pass through a point aperature. This model does not account for the challenges of real lenses (e.g. distortion, blurring) but is a reasonable approximation of the geometric mapping between 3D space and image space.

The parameters of interest are the focal length $(f_x, f_y)$,  which describes the distance between the projected image and the camera, and the principal point $(c_x, c_y)$ which determines the center of the image plane. These together comprise the intrisics matrix:

```math
K = \left[
        \begin{array}{cc}
        f_x &   0 & c_x \\
          0 & f_y & c_y \\
          0 &   0 &   1 \\
        \end{array}
    \right]
```

The intrinsic parameters are unique to each camera, and can be estimated through a calibration procedure. Many cameras are factory calibrated and the intrinsics are provided along with the purchased camera.

### Extrinsics

While the intrinsics provide a mapping between image coordinates and camera coordinates, we need to also account for the fact that the camera may be physically located in different poses with respect to objects in the scene. Extrinsic parameters account for this by determining the camera's pose in the scene defined by a rotation translation. If a reference frame is known (e.g. a checkerboard calibration pattern), then we can try to compute the camera's pose in the reference frame. Oftentimes there is no such reference frame, but we can still try to compute the _relative pose_ of the camera between two images of the same scene. We will leverage this idea in the code below.

## Consensus Algorithm - ARRSAC

**TODO:**


## Estimators - Eight Point Algorithm

**TODO:**






## Running the program

Make sure you are in the Rust CV mono-repo and run:

```bash
cargo run --release --bin chapter5-geometric-verification
```

If all went well you should have a window and see this:

**TODO:** Add image


## The code

**TODO:** Add walkthrough of code


## End

This is the end of this chapter.