# one-indexed-vec

> A scientific computing library with **1-based indexing** — matching
> mathematical notation.

[![Crates.io](https://img.shields.io/crates/v/one-indexed-vec.svg)](https://crates.io/crates/one-indexed-vec)
[![Documentation](https://docs.rs/one-indexed-vec/badge.svg)](https://docs.rs/one-indexed-vec)
[![License](https://img.shields.io/badge/license-MIT%20OR%20Apache--2.0-blue.svg)](#license)
[![CI](https://github.com/huanghu578/one-indexed-vec/actions/workflows/ci.yml/badge.svg)](https://github.com/huanghu578/one-indexed-vec/actions)

## Overview

`one-indexed-vec` provides [`Vec1<T>`], a `Vec`-like container whose first
element lives at **index `1`**. This matches the indexing conventions of
mathematics, Fortran, MATLAB, Julia, and most scientific literature — no
more off-by-one bugs when translating formulas to code.

Beyond the container, the library ships a growing collection of scientific
algorithms organized by discipline:

| Module | Feature | Contents |
|--------|---------|----------|
| `vec1_core` | always | The 1-based container, `Index1`, basic numeric ops |
| `math` | `math` | Sequences, series, Fourier analysis, orthogonal polynomials, FFT |
| `numerical` | `numerical` | Integration, ODEs, root finding, optimization, sliding windows |
| `linear` | `linear` | Matrices, LU/QR/Cholesky, eigenvalues, linear solvers |
| `signal` | `signal` | FIR/IIR filters, window functions, correlation |
| `stats` | `stats` | Descriptive statistics, regression, distributions |
| `physics` | `physics` | Quantum mechanics, thermodynamics, optics |
| `chemistry` | `chemistry` | Atomic data, kinetics, thermodynamics |

## Installation

```toml
[dependencies]
one-indexed-vec = "0.2"
For a minimal build:

toml
[dependencies]
one-indexed-vec = { version = "0.2", default-features = false, features = ["std", "numerical"] }
Quick start
rust
use one_indexed_vec::{Vec1, vec1};

let v = vec1![1.0, 2.0, 3.0, 4.0, 5.0];

// 1-based indexing
assert_eq!(v[1], 1.0);
assert_eq!(v[5], 5.0);

// Basic numeric operations
assert_eq!(v.sum(), 15.0);
assert_eq!(v.mean(), 3.0);

// Prefix sum
let ps = v.prefix_sum();
assert_eq!(ps[3], 6.0);
Feature flags
Feature	Default	Depends on	Description
std	Yes	—	Enable std; without it the crate is no_std
math	Yes	—	Sequences, series, orthogonal polynomials, FFT
numerical	Yes	—	Numeric algorithms, integration, ODEs, root finding
linear	Yes	—	Matrices, decompositions, eigenvalues
signal	Yes	—	Filters, window functions, correlation
stats	Yes	numerical	Descriptive statistics, regression, distributions
physics	Yes	math	Quantum mechanics, thermodynamics, optics
chemistry	Yes	—	Atomic data, kinetics, thermodynamics
serde	No	—	Serialize / deserialize Vec1
Examples by discipline
The examples/ directory contains one runnable example per scientific
discipline. Run any of them with:

bash
cargo run --example math_fourier
Mathematics
math_sequences — arithmetic, geometric, Fibonacci, linspace

math_fourier — Fourier series reconstruction of a square wave

math_fft — Fast Fourier Transform, comparison with DFT

Numerical methods
numerical_integration — trapezoidal rule, Simpson's rule, Gauss-Legendre

Linear algebra
linear_solve — Gaussian elimination, LU decomposition, Cholesky

Signal processing
signal_filter — moving average, FIR filters, window functions

Statistics
stats_regression — descriptive statistics, linear regression, Pearson r

Physics
physics_quantum — infinite square well, hydrogen levels, harmonic oscillator

Chemistry
chemistry_kinetics — first-order decay, Arrhenius, pH, Beer-Lambert

Migration from 0.1.x
In 0.1.x the container was called VecIndexFromOne<T>. As of 0.2.0
the canonical name is Vec1. The old name is kept as a deprecated type
alias for backward compatibility:

rust
#![allow(deprecated)]
use one_indexed_vec::VecIndexFromOne;

let v = VecIndexFromOne::from(vec![1, 2, 3]);
assert_eq!(v[1], 1);
Numeric algorithms that previously lived under one_indexed_vec::ops are
now methods on Vec1, grouped by discipline. The ops module is an empty
deprecated placeholder so that old use statements continue to compile.

The VecIndexFromOne alias will be removed in 1.0.

no_std support
The crate is no_std compatible. Disable the std feature and enable
only what you need. Floating-point math is provided by [libm], so all
algorithms work without the standard library.

toml
[dependencies]
one-indexed-vec = { version = "0.2", default-features = false, features = ["math", "numerical"] }
Design principles
1-based indexing everywhere — v[1] is the first element.

Safety first — v.get(0) returns None; v[0] panics with a clear message.

No off-by-one translations — formulas map directly to code.

Organized by discipline — math, numerical, linear, signal, stats, physics, chemistry.

Feature-gated — pay only for what you use.

no_std friendly — all algorithms work without std.

Related crates
ndarray — N-dimensional arrays

nalgebra — Linear algebra

num-complex — Complex numbers

License
Licensed under either of:

Apache License, Version 2.0 (LICENSE-APACHE)

MIT license (LICENSE-MIT)

at your option.

Contribution
Unless you explicitly state otherwise, any contribution intentionally
submitted for inclusion in the work by you, as defined in the Apache-2.0
license, shall be dual-licensed as above, without any additional terms or
conditions.