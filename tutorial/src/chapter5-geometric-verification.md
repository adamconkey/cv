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
          0 &   0 &   1
        \end{array}
    \right]
```

The intrinsic parameters are unique to each camera, and can be estimated through a calibration procedure. Many cameras are factory calibrated and the intrinsics are provided along with the purchased camera.

### Extrinsics

While the intrinsics provide a mapping between image coordinates and camera coordinates, we need to also account for the fact that the camera may be physically located in different poses with respect to objects in the scene. Extrinsic parameters account for this by determining the camera's pose in the scene defined by a rotation and translation. If a reference frame is known (e.g. a checkerboard calibration pattern), then we can try to compute the camera's pose in the reference frame. Oftentimes there is no such reference frame, but we can still try to compute the _relative pose_ of the camera between two images of the same scene. We will leverage this idea in the code below.

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

### Feature Matching

The initial code will look familiar from the previous chapter on feature matching. We again open two images taken with the same camera in the same scene from the Kitti dataset, extract Akaze features for each of them, and compute the symmetric feature matches between them.

```rust
let src_image_a = image::open("res/0000000000.png").expect("failed to open image file");
let src_image_b = image::open("res/0000000014.png").expect("failed to open image file");

let akaze = Akaze::default();

let (key_points_a, descriptors_a) = akaze.extract(&src_image_a);
let (key_points_b, descriptors_b) = akaze.extract(&src_image_b);
let matches = symmetric_matching(&descriptors_a, &descriptors_b);
```


### Camera Intrinsics

Our goal is to utilize the feature matches to infer the motion of the camera in the scene. To do that, we require the intrinsic parameters of the camera used to capture the photos. Luckily for us, that information is provided with the Kitti dataset. We instantiate a camera instance with the provided focal length and principal point:

```rust
let camera = CameraIntrinsicsK1Distortion::new(
        CameraIntrinsics::identity()
            .focals(Vector2::new(9.842439e+02, 9.808141e+02))
            .principal_point(Point2::new(6.900000e+02, 2.331966e+02)),
        -3.728755e-01,
    );
```

You will notice there is one extra scalar value that we did not yet cover, which is the K1 distortion coefficient, as the name `CameraIntrinsicsK1Distortion` suggests. Distortion coefficients can help correct warps in the image due to imperfections in the camera lens.

**TODO:** Complete rest of walkthrough of code


## End

This is the end of this chapter.