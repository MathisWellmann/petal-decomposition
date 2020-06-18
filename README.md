# petal-decomposition

petal-decomposition provides matrix decomposition algorithms including PCA
(principal component analysis) and ICA (independent component analysis).

[![crates.io](https://img.shields.io/crates/v/petal-decomposition)](https://crates.io/crates/petal-decomposition)
[![Documentation](https://docs.rs/petal-decomposition/badge.svg)](https://docs.rs/petal-decomposition)
[![Coverage Status](https://codecov.io/gh/petabi/petal-decomposition/branch/master/graphs/badge.svg)](https://codecov.io/gh/petabi/petal-decomposition)

## Requirements

* Rust ≥ 1.38
* BLAS/LAPACK backend (OpenBLAS, Netlib, or Intel MKL)

## Features

* PCA with exact, full SVD (singular value decomposition)
* PCA with randomized, truncated SVD
* [FastICA](https://www.cs.helsinki.fi/u/ahyvarin/papers/NN00new.pdf)
* Serialization/deserialization (requires the `serde` feature)

## Examples

The following example shows how to apply PCA to an array of three samples, and
obtain singular values as well as how much variance each component explains.

```rust
use ndarray::arr2;
use petal_decomposition::Pca;

let x = arr2(&[[0_f64, 0_f64], [1_f64, 1_f64], [2_f64, 2_f64]]);
let mut pca = Pca::new(2);               // Keep two dimensions.
pca.fit(&x).unwrap();

let s = pca.singular_values();           // [2_f64, 0_f64]
let v = pca.explained_variance_ratio();  // [1_f64, 0_f64]
let y = pca.transform(&x).unwrap();      // [-2_f64.sqrt(), 0_f64, 2_f64.sqrt()]
```
