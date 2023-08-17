# Geometric Verification

In this chapter, we will build off of the feature matching example from the previous chapter by utilizing feature matches, together with information about the camera, to infer camera motion between the images being compared. We will see a few new concepts including camera intrinsic parameters, consensus algorithms, and estimators. 


## Camera Intrinsic Parameters

In order to relate image features to objects in the 3D scene captured by the camera, we require a parameterization to convert between image coordinates and 3D space. The pinhole camera model is the most common parameterizeration to achieve this, which is an idealized model that constructs the projected image based on how light beams would pass through a point aperature. This model does not account for the challenges of real lenses (e.g. distortion, blurring) but is a reasonable approximation of the geometric mapping between 3D space and image space.

**TODO:** Provide some matrices and describe the parameters (focal, prinicpal point). This should be enough for a simple intro, and then in the code the K1 distortion is used, that can mentioned in passing when describing the code.


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