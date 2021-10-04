# IBF-pipeline Rainfall

Heavy rainfall forecast pipeline to support Egyptian RCS.

## Introduction

This is a series of scripts running run daily to:
1. Extract latest rainfall forecast data from NOAA's GEFS and other input static data.
2. Check if there will be a heavy rainfall event in a several lead times
3. Create rainfall extents and calculated affected population,
4. Load the output to locations where they can be served to the dashoard.

### Prerequisites

1. Install Docker

### Installation

1. Clone this directory to `<your_local_directory>`/IBF-pipeline/

2. Change `/pipeline/lib/pipeline/secrets.py.template` to `secrets.py` and fill in the necessary secrets.

3. Find `data-rainfall.zip` in https://rodekruis.sharepoint.com/sites/510-CRAVK-510/_layouts/15/guestaccess.aspx?folderid=0fa454e6dc0024dbdba7a178655bdc216&authkey=AcqhM85JHZY8cc6H7BTKgO0&expiration=2021-11-29T23%3A00%3A00.000Z&e=qkUx50 and unzip in /pipeline/data, such that it now has subfolders /raster and /other.

4. Build Docker image (from the IBF-pipeline root folder) and run container with volume. ${PWD} should take automatically your Present Working Directory as the local folder to attach the volume though; if this fails, you can always replace it by the literal path (e.g. "C:/IBF-system/services/IBF-pipeline:/home/ibf" instead of "${PWD}:/home/ibf")

- Build image: `docker build . -t ibf-pipeline-rainfall`
- Create + start container: `docker run -it --entrypoint /bin/bash ibf-pipeline-rainfall`

5. All other scripts are summarized in runPipeline.py (as it will be run daily). Test it (from within Docker container) through:

```
run-pipeline
```

For operations, see status at [Azure Logic App](https://portal.azure.com/#@rodekruis.nl/resource/subscriptions/b2d243bd-7fab-4a8a-8261-a725ee0e3b47/resourceGroups/510Global-IBF-System/providers/Microsoft.Logic/workflows/510-ibf-rainfall-pipeline/logicApp).