[![flake8](https://github.com/fjosw/pyerrors/actions/workflows/flake8.yml/badge.svg)](https://github.com/fjosw/pyerrors/actions/workflows/flake8.yml) [![CI](https://github.com/fjosw/pyerrors/actions/workflows/CI.yml/badge.svg)](https://github.com/fjosw/pyerrors/actions/workflows/CI.yml) [![](https://img.shields.io/badge/python-3.6+-blue.svg)](https://www.python.org/downloads/)
# pyerrors
`pyerrors` is a python package for error computation and propagation of Markov chain Monte Carlo data.
It is based on the **gamma method** [arXiv:hep-lat/0306017](https://arxiv.org/abs/hep-lat/0306017). Some of its features are:
* **automatic differentiation** as suggested in [arXiv:1809.01289](https://arxiv.org/abs/1809.01289) (partly based on the [autograd](https://github.com/HIPS/autograd) package)
* **treatment of slow modes** in the simulation as suggested in [arXiv:1009.5228](https://arxiv.org/abs/1009.5228)
* coherent **error propagation** for data from **different Markov chains**
* **non-linear fits with x- and y-errors** and exact linear error propagation based on automatic differentiation as introduced in [arXiv:1809.01289]
* **real and complex matrix operations** and their error propagation based on automatic differentiation (cholesky decomposition, calculation of eigenvalues and eigenvectors, singular value decomposition...)

There exist similar implementations of gamma method error analysis suites in
- [Fortran](https://gitlab.ift.uam-csic.es/alberto/aderrors)
- [Julia](https://gitlab.ift.uam-csic.es/alberto/aderrors.jl)
- [Python 3](https://github.com/mbruno46/pyobs)

## Installation
To install the most recent release of `pyerrors` run
```bash
pip install git+https://github.com/fjosw/pyerrors.git 
```

## Usage
The basic objects of a pyerrors analysis are instances of the class `Obs`. They can be initialized with an array of Monte Carlo data (e.g. `samples1`) and a name for the given ensemble (e.g. `'ensemble1'`). The `gamma_method` can then be used to compute the statistical error, taking into account autocorrelations. The `print` method  outputs a human readable result.
```python
import pyerrors as pe

obs1 = pe.Obs([samples1], ['ensemble1'])
obs1.gamma_method()
obs1.print()
```
Often one is interested in secondary observables which can be arbitrary functions of primary observables. `pyerrors` overloads most basic math operations and `numpy` functions such that the user can work with `Obs` objects as if they were floats
```python
import numpy as np
obs3 = 12.0 / obs1 ** 2 - np.exp(-1.0 / obs2)
obs3.gamma_method()
obs3.print()
```

More detailed examples can be found in  the `examples` folder:

* [01_basic_example](examples/01_basic_example.ipynb)
* [02_correlators](examples/02_correlators.ipynb)
* [03_pcac_example](examples/03_pcac_example.ipynb)
* [04_fit_example](examples/04_fit_example.ipynb)
* [05_matrix_operations](examples/05_matrix_operations.ipynb)


## License
[MIT](https://choosealicense.com/licenses/mit/)
