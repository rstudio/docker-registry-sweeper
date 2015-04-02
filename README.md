# docker-registry-sweeper
-------

### Overview

The docker-registry-sweeper is a command line utility to identify and remove unreferenced images
from a docker registry. Currently, S3 backed registries are supported. Other backend storage drivers
may be added in the future.

The principle of operation for the docker-registry-sweeper is a mark and sweep. On each run, all images and 
repositories are scanned, and graph of images and repositories is created. To avoid potential race conditions that are 
inherit to the way docker-registry works, the docker-registry-sweeper utilizes a multi pass mark and sweep. On the 
first pass, newly dereferenced images are written to a file. On subsequent passes, any image that remains dereferenced 
for a configurable amount of time will be removed. 
 
### Usage

```
docker-registry-sweeper -a 7d sweep
```

This will sweep the registry of any unreferenced images older then 7 days.

### Development

**Setup Environment**

```
# virtualenv is recommended
virtualenv path/to/virtualenv

source path/to/virtualenv/bin/activate

pip install -r requirements.txt
```



