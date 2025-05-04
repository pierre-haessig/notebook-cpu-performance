# A decade of office notebook processors

This post is the summary of me researching whether it is worth replacing my Lenovo [Thinkpad T470](https://www.notebookcheck.net/Lenovo-ThinkPad-T470-Core-i5-Full-HD-Notebook-Review.198130.0.html) notebook, a 2017 model bought 2nd hand in 2020. While the conclusion is that I’ll probably wait a bit more, this was a nice data research about the evolution of the computing power of office notebooks over the last decade.

Hopefully this post can help people in search of refurbished notebooks these days, since it’s easy to get lost in the processors references (*“how does an Intel Core i5-8250U compares to an i5-10210U?”* Spoiler: they are almost the same!)

In this post I focus on key results while the full dataset and associated Python code is available in the Github repository https://github.com/pierre-haessig/notebook-cpu-performance/.

- TODO add link to the abl

### Dataset description

**About the score**: I've extracted computing performance scores from the [Geekbench 6](https://www.geekbench.com/) data brower https://browser.geekbench.com/ which conveniently make their database public *(in exchange of Geekbench users automatically contributing to the database for free)*. This test provides both a **Single-Core** and **Multi-Core** score. The former is useful to assess the  execution speed of one application (webmail, text editor, spreadsheet...), while the latter is geared towards multi-tasking (or some computations which can exploit all processor cores like video encoding, I believe). Geekbench explains that these scores are **proportional to the processing speed**, so a score which is twice as large means a processor that is twice as fast, that is a computing task completed in half the time, if I got it right.

**About the processors selections**: I've extracted the scores for CPUs found in **typical refurbished office notebooks**, that is **midrange** & **low power** CPUs, aka *Intel Core i5* processors, from the so-called [U series](https://www.makeuseof.com/intel-u-vs-p-vs-h-laptop-cpus/), but also corresponding *AMD Ryzen 5*. The earliest model is the Intel Core i5-5200U launched in 2015, while the most recent is the Intel Core Ultra 125U/135U from late 2023 (there wasn't enough data for the Intel Core Ultra 2xx models of 2024). Notice that there are no refurbished notebooks of 2023 yet on the market, so there is some amount of guessing on what will be the "typical office notebook CPUs" of 2023-2025.

### CPU performance charts

Enough speaking, here are two graphs of processors performance.

#### Rank CPU performance

First a dot plot/boxplot chart showing  CPU performance, ranked by Single-Core performance (which is *close, but not quite*, the same as Multi-Core rank):

![CPUs_GB6_logstats_short_sort-Single_q50](../Geekbench 6 plots/CPUs_GB6_logstats_short_sort-Single_q50.png)

The horizontal scale for the score is logarithm, so that each vertical grid line means a difference by a factor 2. This allows superimposing Single-Core (blue) and Multi-Core (green) data.

The diamonds are the Median scores, while the lines show the variability. Indeed, there is not unique value for each CPU, due to the many factors which can affect computing performance: temperature, power source (battery vs AC adapter) and energy saving policy (max performance vs max battery life). To account for this, I've collected about **1000 samples** for each CPU on which I've computed quantiles. The thick lines show the quantiles 25%–75% (also called interquartile range, which contains half the samples) while the thin line ended by mustaches show the quantiles 10%–90% (the most extreme deciles which contain 80% of the samples).

Notice that to avoid data overcrowding, this the “short” version of the chart where I picked one CPU model per generation, while there are typically two (like i5-1135 and i5-1145, with very close performance). The full (twice as long) variant can be find in the [chart repository](https://github.com/pierre-haessig/notebook-cpu-performance/tree/main/Geekbench%206%20plots), along with the sorted by Multi-Score variant.

#### CPU peformance over time, with trend

The  second chart shows performance **evolution over time**. Only median score is shown here, to avoid overcrowding the graph, but with all the CPU models of the dataset. This graph is **interactive** (perhaps a mouse is required, though): hovering each point reveals the processor name and details (number of cores).

![CPUs_bydate_linear_withreg](../Geekbench 6 plots/CPUs_bydate_linear_withreg.png)

The dot color and shape discriminate the CPU designer: Intel vs AMD (the  classical term “manufacturer” is not appropriate for AMD, neither for the latest Intel products). The gray dotted line shows the exponential trend, that is a constant-rate growth rate, in the spirit of Moore’s law (doubling every 2 years), albeit with a *much smaller rate*, see comments below.

This second plot was done with [Vega-Altair](https://altair-viz.github.io/) which is very nice for data exploration and interactivity. However, it is perhaps a bit less customizable than my “old & reliable” plotting companion, [Matplotlib](https://matplotlib.org) [link...], used for the first chart. In particular, I didn't manage to replicate to the nice log2 scale which I created by manually fiddling with the ticks position and label (see [Retrieve_geekbench.ipynb](https://github.com/pierre-haessig/notebook-cpu-performance/blob/main/Retrieve_geekbench.ipynb) notebook, “Log2 scale variant”), but could be achieved more cleanly with Matplotlib’s [tick formatter](https://matplotlib.org/stable/gallery/ticks/tick-formatters.html). So here is the log2 variant of the performance over time chart, albeit with the raw log2 scores, where the exponential becomes a straight line

![CPUs_bydate_log_withreg](../Geekbench 6 plots/CPUs_bydate_log_withreg.png)

The raw log2 score values of [0, 1, 2, 3] corresponds to [1000, 2000, 4000, 8000] (general formula: <span style='font-family:serif;'><i>y</i> = 1000 × 2<sup><i>x</i></sup></span>)). Also, because there are also grid lines for half scores (0.5→1000×√2 ≈ 1414), scores which are different by factor 2 are here separated by two grid lines instead of just one in the first plot.

### Comments of CPU performance

#### 1\) General trend

Sure, there has been *some* progress in CPU performance over the decade 😌

- *but* the progress is faster for Multi-Core than Single-Core performance. In details,  the exponential trend curve fitting yields: 
- **Single-core** trend: +12% per year (±1%), or, said differently, a time to double the performance of about 6.25 years (±10 months)
- **Multi-core** trend: +20%/y ±2%/y, or a time to double the preformance of about T=3.75 years (±4 months)
- see [CPUs_plot.ipynb](https://github.com/pierre-haessig/notebook-cpu-performance/blob/main/CPUs_plot.ipynb) notebook for details
- → in all case, the growth well slower than the 2 years (that is +41%/y) of the [Moore’s law](https://en.wikipedia.org/wiki/Moore's_law)

#### 2\) Effect of increased core count

There is clear effect of diminishing returns

- from about 2010 until 2017 (Intel 7th gen, with the Core i5-7*00U), notebook CPUs shipped with 2 cores, with a Multi-Core score close to twice the Single-Core one (2000 vs 1000 for Intel Core i5-7300U)
- from 2018 to 2021, notebook CPUs embed 4 cores, but with Multi-Core to Single-Core scores ratio between 2.5 and 3.0 (at least for median score)
- fast forward to 2024, the most recent CPUS come with 6 (AMD) or even 10–12 cores (Intel, albeit with only 2 P[owerful?] cores), and the Multi-Core score gets close to 4 times the Single-Core one (8000 vs 2000 for Core Ultra 125U).

#### 3\) Off the trend

The exponential fits gives a false sense of a smooth progress while the true evolution is a bit more stepwise, with some processors “lagging behind” and others “ahead of their time”:

- AMD CPUs before 2020 (Ryzen 7 PRO 2700U and Ryzen 5 PRO 3500U) are lagging behind their Intel counterpart, especially for Single-Core performance. Successors have closed the gap, (especially with  Ryzen 5 PRO 5650U)
- From 2018 to 2020, Intel has kept releasing “re-refreshed” versions of 2017 Kaby Lake (7th gen) architecture, so that the difference between the Intel Core i5-8250U (mid 2017), i5-8265U (mid 2018) and i5-10310U (early 2020) is pretty thin
- Performance of Intel processors make some nice leaps with the 11th and 12th gen (Core i5 11\*5G7 and 12\*5U), but things get more mixed starting 2023 with the new branding of “Core Ultra” processors, which comes with more variants (V and U series in the 2nd gen)

#### 4\) About performance variability

Up to this point, I've only commented the median score, while deferring the discussion about performance variability shown on the first plot.

- performance variability is quite large, with almost a factor two between the top 10% and bottom 10% (90% and 10% quantiles)
- The Single-Core score distribution is [left-skewed](https://en.wikipedia.org/wiki/Skewness), that is the median and top 10% scores are really close together, while most variability comes in the left tail of low scores. My interpretation is that the top score indicates the rated chip performance and the fact that the median is quite close means that about half the notebooks ride close to it. This means that it's quite easy to experience this rated performance in practice. Still, the bottom half can get much slower, but perhaps these are case where notebook are running in a “low power/max battery life” setting. If that’s the case, it not a bad news, because  notebook processors  are designed to dynamically adjust their frequency & voltage to save energy. 
  - This is why I always advice my students confronted to an unresponsive notebook to plug their AC adapter, especially when I make them run some [microgrid optimization code](https://pierreh.eu/Microgrids-X/).
  - Still, my father experienced a disappointingly low  score of 1200 with its i5-1245U powered laptop (median score is 1950), while we took care to plug the AC adapter and set the power strategy to max performance.
- The Multi-Core score distribution is on the other hand much more symmetric. I interpret this as meaning that it’s more difficult to reach the rated Multi-Core performance, at least with notebook CPUs. I guess that when all cores works simultaneously, the processor easily hits its maximum power or temperature limits, while one core working alone has much more to “express its talent”
- what is left to be explored is the **effect of notebook’s chassis**. Seeing for example the pretty large variabilty of [Intel Core i5-10210U](https://browser.geekbench.com/search?q=Intel+Core+i5-10210U), perhaps there exists clusters showing that the bottom performance comes from models. Indeed, part of the power management of notebooks is under. Question example: out of the the Dell Latitude 5410 and the HP ProBook 440 G7 which both feature this CPU, is one better than the other?

### Conclusion

*Et voilà*, I guess that's enough for one post. Of course I only covered computing metrics. For example when I said in the intro that Intel Core i5-10210U and i5-8250U are almost the same, these processor are still 2 years apart and the corresponding notebooks may come with different Wifi and Bluetooth connection standards, so that the 10210U may still be more interesting.

In a following post, I will write on the second part of this dataset: the **notebook offers table**, which links the system price to its cpu peformance, to get Pareto-style trade-off chart of price vs performance. Notice that this dataset and the draft plotting code is already available in the repository ([Offers_plot.ipynb](https://github.com/pierre-haessig/notebook-cpu-performance/blob/main/Offers_plot.ipynb) notebook).