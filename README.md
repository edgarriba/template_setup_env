## Overview

This is a template repository to help with [ML Code Completeness Checklist](https://medium.com/paperswithcode/ml-code-completeness-checklist-e9127b168501) in order to replicate results with same software dependencies across different machines. 

**Why this is important ?**

At the time to replicate results using third-party repositories, or even when you share projects with your colleagues, the most common case is that *your version libraries are completely unaligned* respect to the ones producing the expected behaviour.

This is a huge and very time consuming problem that makes the whole task of reproducing and eventually improve methods results almost impossible. For these reasons - **use virtual environments !**

## Installation

In this repository are provided a couple of scripts that helps you to create the needed setup using [conda environments](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/environments.html)

You only need to **copy three files** in the root of your project - [`environment.yml`](https://github.com/edgarriba/template_setup_env/blob/master/environment.yml) [`setup_dev_env.sh`](https://github.com/edgarriba/template_setup_env/blob/master/setup_dev_env.sh)  [`path.bash.inc`](https://github.com/edgarriba/template_setup_env/blob/master/path.bash.inc)

After this, your project should have the following structure:
```
/my_project
  /docs
  /lib
  /test
  environment.yml
  path.bash.inc
  setup_dev_env.sh
  setup.py
  README.md
```

## Configure

Edit the [`environment.yml`](https://github.com/edgarriba/template_setup_env/blob/master/environment.yml) file according to your (and future users) needs.

It is highly recommended to pin your versions to make explicit the exact versions you need in your repo [[INFO]](https://before-you-ship.18f.gov/infrastructure/pinning-dependencies/)

```yaml
name: venv
channels:
  - conda-forge
  - pytorch

dependencies:
  - python>=3.6
  - pytorch>=1.4.0
  - torchvision>=0.5.0
  - opencv>=4.2.0
  - matplotlib>=3.2.1
  - pip:
    - kornia>=0.2.0
    - pytorch-lightning>=0.7.2
```

## Setup

Once you have prepared your [`environment.yml`](https://github.com/edgarriba/template_setup_env/blob/master/environment.yml), execute `./setup_dev_env.sh` in your bash terminal.

> the script above will create a hidden `.dev_env` in your project root where you will have stored all your project. This pattern helps to encapsulate and isolate the environment dependencies in a single directory.

Finally, to activate the conda environment, run `source path.bash.inc` and you'll get prompt to your terminal ready to use your replicated repository.
```bash
eriba@kornia:~/software/template_setup_env$ source path.bash.inc
(venv) eriba@kornia:~/software/template_setup_env$
(venv) eriba@kornia:~/software/template_setup_env$ python -c "import torch; print(torch.__version__)"                                                                                                       
1.4.0
```

**EXTRA** run `conda deactivate` just to get out of the environment.
```bash
(venv) eriba@kornia:~/software/template_setup_env$ conda deactivate
eriba@kornia:~/software/template_setup_env$ python
```

**NOTE:** this has been take from [`kornia`](https://github.com/arraiyopensource/kornia) github repository.
