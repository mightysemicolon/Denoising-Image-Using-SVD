# Image Denoising Using SVD

Removing Gaussian noise from a color image with a truncated SVD.

The reason this works: a natural image has a lot of structure, so most of it is captured by the first singular values. Random noise has no structure and is spread over all singular values more or less equally. If we keep only the first `k` singular values, we keep most of the image and throw away most of the noise.

## Steps

1. Read the image (`pic5.jpeg`, 2736 x 3648 pixels, RGB).
2. Add Gaussian noise with mean 0 and standard deviation 100 (on the 0 to 255 scale) to every pixel and channel. This is very strong noise.
3. Compute the SVD of each color channel of the noisy image separately.
4. Rebuild each channel from the first `k` singular values and vectors, `A_k = U_k S_k V_k^T`, for `k = 50, 100, ..., 500`, and save the result for each `k`.
5. Plot the singular values of the three channels.

## What to look for

There is a trade-off in `k`:

- small `k`: the noise is gone but the image is blurry, fine details are lost
- large `k`: the details come back, but so does the noise

In the singular value plot there are a few very large singular values at the start and then a long flat part. The flat part is mostly noise, so a good `k` is somewhere around the point where the curve becomes flat. In this notebook the comparison between different `k` is visual, from the saved images.

## Files

- `project-5.ipynb` : the notebook
- `pic5.jpeg` : the test image

## Requirements

numpy, matplotlib

The image is large, so the three SVDs take some time.

## Reference

Lars Eldén, *Matrix Methods in Data Mining and Pattern Recognition*, SIAM.
