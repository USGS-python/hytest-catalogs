# hytest-catalogs

```python
import intake
url = 'https://raw.githubusercontent.com/USGS-python/hytest-catalogs/main/hytest_intake_catalog.yml'
cat = intake.open_catalog(url)
list(cat)
```
produces a list of datasets, for example:
```
['conus404-40year-onprem',
 'conus404-2017-onprem',
 'conus404-2017-cloud',
 'nwis-streamflow-usgs-gages-onprem',
 'nwis-streamflow-usgs-gages-cloud',
 'nwm21-streamflow-usgs-gages-onprem',
 'nwm21-streamflow-usgs-gages-cloud',
 'nwm21-streamflow-cloud',
 'nwm21-scores',
 'lcmap-cloud']
 ```
 The characteristics of indivdual datasets can be explored:
```python
cat['lcmap-cloud']
```
producing
```yaml
lcmap-cloud:
  args:
    consolidated: false
    storage_options:
      fo: s3://nhgf-development/lcmap/lcmap.json
      remote_options:
        requester_pays: true
      remote_protocol: s3
      target_options:
        requester_pays: true
    urlpath: reference://
  description: LCMAP, all 36 years
  driver: intake_xarray.xzarr.ZarrSource
  metadata:
    catalog_dir: https://raw.githubusercontent.com/USGS-python/hytest-catalogs/main
 ```
 and xarray-type datasets can be loaded with `to_dask()`, while panda-type datasets can be loaded with `.read()`:
```python
ds = cat['lcmap-cloud'].to_dask()
df = cat['nwm21-scores'].read()
```
