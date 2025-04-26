# Notebook CPU performance analysis

by Pierre Haessig, spring 2025, [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

Goal: quantify and compare the computing performance of refurbished notebooks, or more generally the typical office-style notebook CPUs of the 2015–2025 decade.

## Data description

### Data sources: 

-  **Computing performance**: from [Geekbench 6](https://www.geekbench.com/) data brower https://browser.geekbench.com/
  - about 1000 samples collected for each CPU
  - summarized by quantiles
- **CPUs characteristics**: personal collection from Intel and AMD website
- **Notebook offers**: French computer refurbishing company  [ITjustGood](https://www.itjustgood.com/)

### CPU data selection:

- CPUs found in **typical refurbished office notebooks**, that is **midrange** & **low power** CPUs, aka Intel **Core i5** processors, from the [U series](https://www.makeuseof.com/intel-u-vs-p-vs-h-laptop-cpus/), but also corresponding AMD **Ryzen 5** processors (typically the PRO models)
- Earliest model: Intel Core i5-5200U, from early 2015
- Most recent model: Intel Core Ultra 125U/135U from late 2024 (the 2xx models from 2024 are also in the database, but without corresponding performance data due to their low deployment as of spring 2025)
  - remark: recent Intel Core Ultra processors have a complicated list of references and are not yet available as refurbished notebooks, so it's my guess on what will be the "typical office notebook CPUs" of 2024-2025

### Notebook offers selection:

From https://www.itjustgood.com/pc-portable/taille-de-l-ecran-14-pouces/resolution-full-hd-1920-x-1080/memoire-vive-ram-16-go.html?product_list_order=price_asc:

- 14 inches screen, with Full HD resolution (1920×1080)
- 16 GB of RAM
- no filter on disk capacity (varies from 250 GB to 1TB)

### Data availability

The data collection of this project is available in two places:

1. In Baserow tables (public read-only views):
    - [CPUs](https://baserow.io/public/grid/wLq_Mhbx1y8jm7z82Y1GuqrCpNtOCkBqdHHgYqoNP0M): characteristics and median Geekbench performance
      - helper table: [CPU Architectures](https://baserow.io/public/grid/QhMWCEkWl2jT_LMaULgfqu9JZ2r9TQn0RAQr8vClOZ0)
    - [Notebook offers](https://baserow.io/public/grid/q39BCdA9-8GFsRv_HIoyIJJjkUIPJ4FBZQ7WonqO2Ss): characteristics, price and crosslink to the corresponding CPU Geekbench performance data
      - helper table [Notebook series](https://baserow.io/public/grid/qjK_ot5toME-zCxTMdx8CwOxf3U3a6nx_R0kvCSGnqE)

2. In this repo, as static CSV files:
    - [CPUs.csv](CPUs.csv): export of the corresponding Baserow table
    - [CPUs_GB6_stats.csv](CPUs_GB6_stats.csv): aggregated statistics (mean and quantiles) of  [Geekbench 6](https://www.geekbench.com/) data samples. 
      - The median columns (`Single q50` and `Multi q50`) are the original sources of the `GB6 Single` and  `GB6 Multi` columns in the CPUs table
      - the raw samples are available in the [Geekbench 6](Geekbench%206) folder
    - [Offers.csv](Offers.csv): export of the corresponding Baserow table

## Data analysis

CPU data pipeline:

1. 🤖 CPU performance data scraping and aggregation: [Retrieve_geekbench.ipynb](Retrieve_geekbench.ipynb), which accesses the website  https://browser.geekbench.com/ → [CPUs_GB6_stats.csv](CPUs_GB6_stats.csv)
    - as a bonus create the detailed CPU performance charts, see the [Geekbench 6 plots](Geekbench%206%20plots) folder
2. ✍️ Manual copy of performance data to the Baserow [CPUs](https://baserow.io/public/grid/wLq_Mhbx1y8jm7z82Y1GuqrCpNtOCkBqdHHgYqoNP0M) table
3. 📡 Extraction to CSV from public API in [Retrieve_baserow.ipynb](Retrieve_baserow.ipynb) → [CPUs.csv](CPUs.csv)
4. 📊 Plotting in [CPUs_plot.ipynb](CPUs_plot.ipynb) 

Notebook offers data pipeline:

1. ✍️ Manual creation of the Baserow [Notebook offers](https://baserow.io/public/grid/q39BCdA9-8GFsRv_HIoyIJJjkUIPJ4FBZQ7WonqO2Ss) from  [ITjustGood](https://www.itjustgood.com/)
2. 📡 Extraction to CSV from public API in [Retrieve_baserow.ipynb](Retrieve_baserow.ipynb) →  [Offers.csv](Offers.csv)
3. 📊 Plotting in [Offers_plot.ipynb](Offers_plot.ipynb)

CPU performance plots: see all plots in [Geekbench 6 plots](Geekbench%206%20plots)

Example: Single & Multi-Core Geekbench 6 performance plot of each CPU of the short dataset: median and quantiles of the scores. Animated version (sorted by Single and then Multi-Core score)

![Single & Multi-Core Geekbench 6 performance plot of each CPU of the short dataset: median and quantiles of the scores](Geekbench%206%20plots/CPUs_GB6_logstats_short_sort-anim.gif)

