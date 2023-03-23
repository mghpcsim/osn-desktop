# OSN-desktop for use on Binder / JupyterHub

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/mghpcsim/osn-desktop.git/HEAD)


Uses [jupyter-remote-desktop-proxy](https://github.com/jupyterhub/jupyter-remote-desktop-proxy)
to work.

## How to use this repo

### Install the applications you want

Install the applications you want. 
There are three main ways to do this:

#### From `apt` via `apt.txt`

Many common Linux GUI applications are available to be installed from
the [Ubuntu Apt Repositories](https://packages.ubuntu.com). Adding their
name to `apt.txt` file is usually enough to get them installed. Note that
by default right now, the base image used by Binder and repo2docker is
using Ubuntu 18.04 Bionic, which can be a bit outdated.

#### From `conda` via `environment.yml`

A lot of scientific GUI applications are also packaged via [conda-forge]
and can be installed by editing the `environment.yml` file to include them.
For example, [qgis](https://anaconda.org/conda-forge/qgis) is a popular
Geospatial GUI application, and is available on conda-forge. You can install
it by adding `qgis` under `dependencies` in `environment.yml`.

#### Manually, with a `postBuild` script

Sometimes the application you want is not available in apt or conda-forge,
or at least not the version you want. You've to manually install them
by writing a script in [`postBuild`](https://repo2docker.readthedocs.io/en/latest/config_files.html#postbuild-run-code-after-installing-the-environment)
file to download the app manually (wia `wget` maybe) and extract the executable
application somewhere. You don't have `root` access here, so some of the things
you need to do might be limited. Consider writing your own `Dockerfile` instead.

Spack and EasyBuild are very useful here but require some work and patience to setup.

### Setup a desktop shortcut for GUI apps

When the repo is launched on Binder / desktop is used on JupyterHub, a shortcut
that users can click to launch your app is pretty nice. This template contains
sample `app.desktop` file you can use to setup this shortcut. Our `start` script
will automatically make sure that any `.desktop` files (which is how most Linux
desktops indicate a shortcut file) are put on the user Desktop.

1. Rename the file from `app.desktop` to `<your-app-name>.desktop`
2. Open the file, and fill in values for `Name`, `Exec` and optionally `Icon`
3. Commit the file
