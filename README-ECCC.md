# SPI Description

SPI is a scientific and meteorological virtual globe offering immense processing, analysis and visualization capabilities, with a user interface similar to Google Earth and NASA World Wind. SPI uses an "always 3D" rendering method. Everything is always rendered in three dimensions, looking from the top it looks like a regular 2D map, but moving the camera around gives a new perspective of things.

SPI is built in Tcl/Tk. Most of the rendering and scientific functionalities are built as binary extensions to Tcl in the form of objects and functions and then used in SPI’s Tcl source code.

An exhaustive API described in another document allows for very powerful scripting, going from generation of a map to calculating flux along the path of a shape like country boundary. This API can be used to interact with many kind of data like RPN standard file, CMC trajectories, ESRI shapefiles, GeoTIFF imagery, BURP observation files and more,.

# [SPI Documentation](https://wiki.cmc.ec.gc.ca/wiki/SPI)
# [SPI API Documentation](https://wiki.cmc.ec.gc.ca/wiki/SPI/Documentation#Developer_documentation)

# Getting the source code
```shell
git clone --recursive git@gitlab.science.gc.ca:ECCC_CMOE_APPS/SPI-Bundle
```

This will provide you with the source for the following dependent packages
* [SPI-External](https://gitlab.science.gc.ca/ECCC_CMOE_APPS/spi-external)
* [SPI](https://gitlab.science.gc.ca/ECCC_CMOE_APPS/spi)
* [eerUtils](https://gitlab.science.gc.ca/ECCC_CMOE_MODELS/libeerutils)
* [GenPhysX](https://gitlab.science.gc.ca/ECCC_CMOE_APPS/genphysx)

# Building SPI
* You will need cmake with a version at least 3.12
```shell
. ssmuse-sh -x /fs/ssm/main/opt/cmake-3.21.1
```
* [bison](https://www.gnu.org/software/bison) version 3.0+
* [Mako](https://pypi.org/project/Mako) is needed to build Mesa3D
```shell
pip install Mako
```

## Optional dependencies
* codetools and compilers
```shell
. . r.load.dot rpn/code-tools/ENV/cdt-1.6.0/SCIENCE/inteloneapi-2022.1.2
```

* [librmn](https://gitlab.science.gc.ca/RPN-SI/librmn)
* [vgrid](https://gitlab.science.gc.ca/RPN-SI/vgrid)
```shell
. r.load.dot rpn/libs/20220216
```

* External dependencies ([GDAL](https://gdal.org/), [eccodes](https://confluence.ecmwf.int/display/ECC), [libecbufr](https://github.com/ECCC-MSC/libecbufr), [fltlib](https://sourceforge.net/projects/fltlib)). Within the ECCC/SCIENCE network, a package containing all the dependencies can be loaded
```shell
export CMD_EXT_PATH=/fs/ssm/eccc/cmd/cmds/ext/20220726; . ssmuse-sh -x $CMD_EXT_PATH
```

## Geographical base map database ([GDB](https://eer.cmc.ec.gc.ca/software/SPI/DBGeo/DBGeo.tgz))
The geographical database (GDB), contains the base map geographical data used by SPI and takes up to 13GB of space
Download and decompress it into it's final installation directory if it has'nt been installed before.
Define the GDB_PATH variable to the location of the geographical database for SPI to use it:
```shell
export GDB_PATH=[GDB extract path]/data
```

## Environment setup
The build process requires the definition of a variable indicating where the build will occur otherwise the current path will be used
```shell
export SSM_DEV=[where to build]
```

## Launching the build
```shell
cd SPI-Bundle
./makeit -build -reconf
```

## building packages
```shell
makeit -pack
```
