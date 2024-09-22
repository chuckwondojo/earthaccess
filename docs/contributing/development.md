# Development

## Getting the code

1. Fork [nsidc/earthaccess](https://github.com/nsidc/earthaccess)
1. Clone your fork (`git clone git@github.com:{my-username}/earthaccess`)

In order to develop new features or fix bugs etc. we need to set up a virtual
environment and install the library locally.

## Quickstart development

The fastest way to start with development is to use nox. If you don't have nox,
you can use `pipx run nox` to run it without installing, or `pipx install nox`.
If you don't have pipx (pip for applications), then you can install with
`pip install pipx` (the only case were installing an application with regular
pip is reasonable). If you use macOS, then pipx and nox are both in brew, use
`brew install pipx nox`.

To use, run `nox` without any arguments.  This will run type checks and unit
tests using the installed version of Python on your system.

You can also run individual tasks (_sessions_ in `nox` parlance, hence the `-s`
option below), like so:

```console
nox -s typecheck              # Run typechecks
nox -s tests                  # Run unit tests
nox -s integration-tests      # Run integration tests (see note below)
nox -s build_docs -- --serve  # Build and serve the docs
nox -s build_pkg              # Build an SDist and wheel
```

Nox handles everything for you, including setting up a temporary virtual
environment for each run.

**NOTE:** In order to run integration tests locally, you must set the
environment variables `EARTHDATA_USERNAME` and `EARTHDATA_PASSWORD` to your
username and password, respectively, of your
[NASA Earthdata](https://urs.earthdata.nasa.gov/) account (registration is
free).

## Manual development environment setup

While `nox` is the fastest way to get started, you will likely need a full
development environment for making code contributions, for example to test in a
REPL, or to resolve references in your favorite IDE.  This development
environment also includes `nox`.

Create and activate a virtual environment with `venv`, which comes by default
with Python, in the `.venv` directory:

```bash
python -m venv .venv
source .venv/bin/activate
```

Install `earthaccess` in editable mode with optional development dependencies:

```bash
pip install --editable ".[dev,test,docs]"
```

??? note "For conda users"

    For your convenience, there is an `environment.yml` file at the root of this
    repository, allowing you to create a conda environment quickly, as follows:

    ```bash
    conda env create --file environment.yml
    ```

## Managing Dependencies

If you need to add a new dependency, edit `pyproject.toml` and insert the
dependency in the correct location (either in the `dependencies` array or under
`[project.optional-dependencies]`).
