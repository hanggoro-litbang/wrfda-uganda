# Running WRF with no Data Assimilation
## Create Domain (Geogrid)
go to https://jiririchter.github.io/WRFDomainWizard/ \
Follow the steps to create a domain until you get the namelist.wps file as follows:
```console
&share
 wrf_core             = 'ARW'
 max_dom              = 2
 start_date           = '2025-05-02_03:00:00', '2025-05-02_03:00:00'
 end_date             = '2025-05-02_18:00:00', '2025-05-02_18:00:00'
 interval_seconds     = 21600
 io_form_geogrid      = 2
 debug_level          = 0
/

&geogrid
 parent_id            = 1, 1
 parent_grid_ratio    = 1, 3
 i_parent_start       = 1, 14
 j_parent_start       = 1, 14
 e_we                 = 50, 76
 e_sn                 = 50, 76
 geog_data_res        = 'default', 'default'
 dx                   = 9000
 dy                   = 9000
 map_proj             = 'mercator'
 ref_lat              = -6.289
 ref_lon              = 106.474
 truelat1             = -6.289
 pole_lat             = 90
 pole_lon             = 0
 geog_data_path       = 'geog'
 opt_geogrid_tbl_path = './geogrid/'
/

&ungrib
 out_format           = 'WPS'
 prefix               = 'FILE'
/

&metgrid
 fg_name              = 'FILE'
 io_form_metgrid      = 2
 opt_metgrid_tbl_path = './metgrid'
/
```
Create Working directory
```console
export geog_dir=/mnt/galon/GEOG
export wrf_dir=/home/{user}/WRF/WRFV4.7.0
export wps_dir=/home/{user}/WRF/WPS-4.6.0
cd ~/WRF
mkdir -p WDIR/no_asim
cd WDIR/no_asim
```
Linking necessary files
```console
ln -sf ${wps_dir}/ungrib/Variable_Tables/Vtable.GFS Vtable
ln -sf ${wps_dir}/ungrib/src/geogrid.exe .
ln -sf ${wps_dir}/metgrid/src/metgrid.exe .
ln -sf ${wps_dir}/geogrid/GEOGRID.TBL.ARW GEOGRID.TBL
ln -sf ${wps_dir}/link_grib.csh .
cp ${wps_dir}/namelist.wps .
```
edit namelist.wps file and adjust as previous step
```console

```
