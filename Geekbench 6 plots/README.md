# Plots

## CPU performance plots

remark: the "red plots" needs to be updated

|                          | Sorted by Single-Core performance                            | Sorted by Multi-Core performance                             |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Short list, linear scale | ![CPUs_GB6_stats_short_sort-Single_q50](CPUs_GB6_stats_short_sort-Single_q50.png) | ![CPUs_GB6_stats_short_sort-Multi_q50](CPUs_GB6_stats_short_sort-Multi_q50.png) |
| Short list, log scale    | ![CPUs_GB6_logstats_short_sort-Single_q50](CPUs_GB6_logstats_short_sort-Single_q50.png) | ![CPUs_GB6_logstats_short_sort-Multi_q50](CPUs_GB6_logstats_short_sort-Multi_q50.png) |
| Long list, linear scale  | ![CPUs_GB6_stats_sort-Single_q50](CPUs_GB6_stats_sort-Single_q50.png) | ![CPUs_GB6_stats_sort-Multi_q50](CPUs_GB6_stats_sort-Multi_q50.png) |
| Long list, log scale     | ![CPUs_GB6_logstats_sort-Single_q50](CPUs_GB6_logstats_sort-Single_q50.png) | ![CPUs_GB6_logstats_sort-Multi_q50](CPUs_GB6_logstats_sort-Multi_q50.png) |

and the GIF animation which switch between Single- and Multi-Core performance sort:

- [CPUs_GB6_stats_short_sort-anim.gif](CPUs_GB6_stats_short_sort-anim.gif)
- [CPUs_GB6_logstats_short_sort-anim.gif](CPUs_GB6_logstats_short_sort-anim.gif)

## CPU along time

Plots made with [Vega-Altair](https://altair-viz.github.io/), so that the display of interactive versions need a web page which loads the JSON files. There are also static image exports.

Linear scale (JSON specification: [CPUs_bydate_linear_withreg.json](CPUs_bydate_linear_withreg.json))

![CPUs_bydate_linear_withreg](CPUs_bydate_linear_withreg.png) 

Log scale, superimposed on the same chart (JSON specification  [CPUs_bydate_log_withreg.json](CPUs_bydate_log_withreg.json))

![CPUs_bydate_log_withreg](CPUs_bydate_log_withreg.png)