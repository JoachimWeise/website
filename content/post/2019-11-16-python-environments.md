---
title: Python virtual environments
subtitle: tbd tbd
date: 2019-11-15
# lastmod: 2019-11-29
bigimg: [{src: "/img/2019-11-16-python-environments.jpg", desc: "Amsterdam (2018)"}]
tags: ["python", "code"]
---

Anyone who works on Python projects and uses various packages will sooner or later have to deal with different versions of packages across different branches and projects. Because each project has its own set of dependencies, it’s a good practice to avoid mixing them. If all the dependencies are installed together in a single Python environment, then it will be difficult to discern where each one came from. In the worst cases, two different projects may depend on two different versions of a package, but with Python you can only have one version of a package installed at one time. What a mess! Virtual environments address this issue. A virtual environment, put simply, is an isolated working copy of Python which allows you to work on a specific project without worry of affecting other projects. 


<!--more-->

### Overview

At its core, the main purpose of Python virtual environments is to create an isolated environment for Python projects. This means that each project can have its own dependencies, regardless of what dependencies every other project has. You can think of a virtual environment as a carbon copy of a base version of Python. If you’ve installed Python 3.7.3, for example, then you can create many virtual environments based off of it. When you install a package in a virtual environment, you do it in isolation from other Python environments you may have. Each virtual environment has its own copy of the python executable.

The Python ecosystem offers various tools vor managing virtual environments. 

- `pip` is the central tool for installing and uninstalling packages. We could specify versions, run `pip freeze > requirements.txt` to output a list of installed packages to a text file, and use that same text file to install everything an app needed with `pip install -r requirements.txt`. But `pip` doesn't include a way to isolate packages from each other.
- `Pipenv` is a dependency manager for Python projects. While `pip` can install Python packages, `Pipenv` is recommended as it’s a higher-level tool that simplifies dependency management for common use cases. `Pipenv` is a rather new tool (born in 2017) that aims to bring the best of all packaging worlds to the Python world. Windows is considered a first-class citizen. It automatically creates and manages a `virtualenv` for your projects, as well as adds/removes packages from your `Pipfile` as you install/uninstall packages. It also generates the important `Pipfile.lock`, which is used to produce deterministic builds. Pipenv is primarily meant to provide users and developers of applications with an easy method to setup a working environment. 
- `virtualenv` is a tool to create isolated Python environments. `virtualenv` creates a folder which contains all the necessary executables to use the packages that a Python project would need. It can be used standalone, in place of `Pipenv`. Since Python 3.3, a subset of `virtualenv` has been integrated into the standard library under the `venv` module. 
- `venv` provides support for creating lightweight virtual environments with their own site directories, optionally isolated from system site directories. Each virtual environment has its own Python binary (which matches the version of the binary that was used to create this environment) and can have its own independent set of installed Python packages in its site directories. Note though, that the `venv` module does not offer all features of `virtualenv` (e.g. cannot create bootstrap scripts, cannot create virtual environments for other python versions than the host python, not relocatable, etc.). 
- `virtualenvwrapper` provides a set of commands which makes working with virtual environments much more pleasant. It also places all your virtual environments in one place.
- `conda` is the package management tool for Anaconda Python installations. Conda is a completely separate tool to `pip`, `virtualenv` and `wheel`, but provides many of their combined features in terms of package management, virtual environment management and deployment of binary extensions. `Conda` does not install packages from PyPI and can install only from the official Anaconda repositories, or anaconda.org (a place for user-contributed conda packages), or a local (e.g. intranet) package server. However, note that `pip` can be installed into, and work side-by-side with `conda` for managing distributions from PyPI.


### Links to documentation:

- PyPA guides: [here](https://packaging.python.org/guides/tool-recommendations/), [here](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/), and [here](https://packaging.python.org/tutorials/managing-dependencies/)
- `Pipenv`: https://pipenv.readthedocs.io/en/latest/  
- `virtualenv`: https://virtualenv.pypa.io/en/stable/
- `venv`: https://docs.python.org/3/library/venv.html
- `conda`: [https://docs.conda.io/.../manage-environments.html](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)


###  Further helpful articles:

- [Why Python devs should use Pipenv](https://opensource.com/article/18/2/why-python-devs-should-use-pipenv)
- [Pipenv & Virtual Environments](https://docs.python-guide.org/dev/virtualenvs/)