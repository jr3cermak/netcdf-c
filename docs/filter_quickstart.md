NetCDF-4 Filter QuickStart
==============================

\tableofcontents

<!--  double header is needed to workaround doxygen bug  -->

NetCDF-4 Filter QuickStart {#nc_filters_quickstart}
==============================

> For full **Filters** documentation, see \ref filters.

**The `libnetcdf.so` library cannot talk to plugin libraries directly. Instead, it requires an "interface" library, which acts as a go-between.  The interface libraries are built by the netCDF libraries, when the underlying plugin libraries are detected during configure/build.**

Building and Installing the Interface Libraries {#nc_filters_qs_building}
----------------------------------

When configuring netcdf via either the `configure` script or via `cmake`, you'll need to specify the location to install the interface libraries, as follows:

* configure: `--with-plugin-dir=<absolutely directory>`
* cmake: `-DPLUGIN_INSTALL_DIR=<absolutely directory>`

After compiling and installing `libnetcdf`, the interface libraries for those filters detected will be installed in the user-specified `<absolute directory>`.


Using the Interface Libraries at Run-time {#nc_filters_qs_runtime}
---------------------------------

For historical reasons, `libnetcdf` uses the environmental variable `HDF5_PLUGIN_PATH` to local the interface libraries at run-time. 


Example Workflow (blosc) {#nc_filters_qs_workflow_example}
--------------------------------------------------

From scratch, the steps to get this to work are as follows, and assumes `libhdf5` was installed.

1. Install the filter library, and the associate development headers.
2. Configure netCDF with `--enable-plugins` and `--with-plugin-dir=$HOME/netcdf-plugins`
3. Ensure `blosc` is specified in the generated `libnetcdf.settings` file.  
4. Run make, make install.

Once built and installed, set the environmental variable `HDF5_PLUGIN_PATH=$HOME/netcdf-plugins`.  

The reason this works is because:

1. NetCDF builds the interface library.
2. `ncdump` knows where to find the interface library because `HDF5_PLUGIN_PATH` is set.  

