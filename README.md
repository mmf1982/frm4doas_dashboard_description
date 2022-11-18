# Description of the dashboard

## start page

This is the start page view, showing all instruments currently included in the processing:

![dahboard_1](https://user-images.githubusercontent.com/38353016/202756477-f25a8196-0264-4d32-a888-2c20e70fb9f1.png)

* Each image consists of 3 -- 6 horizontal blocks, each representing a module.
* While not very well visible in the overview page, each such block is build up of 28 columns and three rows.
* The rows will be described later, each column is a day, the right most column is "yesterday".
* The last column (so "yesterday") of each instrument determines the color of the station and instrument name, red means something is not quite allright, green means all is ok.
* The last column can be blanc: there is a certain level1 file receiving delay, y, allowed for each station; if no level1 file was received in the last x days, all last min(x, y) columns are colored blanc and the color of the header is taken from the latest file that was received if this is within y, otherwise it is red. For example, there are missing files in both of the Utsteinen instruments, but they are both green, because the number of missing files x is smaller than the allowed delay y, and the last processed file resulted in no problems. However, Cabauw also has missing files and although the number of missing files x is also lower than the number of allowed files, the header is red, because the last "legal" file had some problem (which in this case comes from a directory change of level1 files not yet specified in the checker).
* Each image is a link to the respective instrument, e.g. clicking on Uccle 1689_2 brings you to the instrument overview page:

## instrument overview page

This is the instrument overview page for an instrument with only tropo processing:

![dahboard_2](https://user-images.githubusercontent.com/38353016/202756604-34b3c5ac-0059-4992-ad66-d8a4b6694522.png)


Each module, here _L1_, _qdoas_m_ and _tropo_, consists of three rows:

1. number of files for the indicated day
2. number of observations for the indicated day, for _strato_, there are two numbers, one each for AM and PM.
3. short info on module specific checks:
   - for _L1_, this is the time difference between the calculated solar noon at the station's location and the time of the measurement with the lowest solar zenith angle. If this is larger than 10 min, this will cause this module to appear red.
   - for _qdoas_m_ or _qdoas_s_ (the former being the qdoas processing preceeding the tropospheric profiling, the latter being the qdoas processing preceeding the stratospheric NO2 profiling or the total ozone column retrieval), different variables are checked and tested whether or not they are within the median ± 3 std. If any of the variables currently checked are outside this region, an error code is produced and a list of occured errors can be found at the right-hand side of the matrix overview plot.
   - neither of the modules producing level2 files (_tropo_, _o3strato_ or _no2strato_) fills the "checks" row at the moment, the row is blanc.

From the instrument overview page, one has the following two possibilities to go further: - following the link to the monthly module overview page for the corresponding by click the blue link, here _L1_, _qdoas_m_ or _tropo_, in the column "Links" - open a daily module page for the corresponding instrument by clicking on corresponding day column in the corresponding module block.

## monthly module overview page

The shown variables on the monthly overview page depend on the module in question. As an example, I show here the start of the _qdoas_m_ page from Uccle.

![dahboard_3](https://user-images.githubusercontent.com/38353016/202756663-59b975d3-fa6a-4fd4-8d7e-3548c8731951.png)


Some general comments hold:

* Shown are always the last 28 days, whether or not they are present.
* The first row always shows a bar plot of the number of files. This should be one.
* The second plot always shows the number of measurements and indicated in there is the median-3 std line as a black/ red line. In case of _L1_, _qdoas_m_ or _qdoas_s_, this is the number of measurements. In case of _tropo_, this is the number of scans and in case of _no2strato_ and _o3strato_ there are two plots, black for am and red for pm, and it is the number of measurements used for the am and pm retrieval, respectively.
* all but the first two plots have the following plotting tools available:

   ![dahboard_4](https://user-images.githubusercontent.com/38353016/202756779-12627130-6efd-4a76-bd61-dab6906cff2e.png)
  * pan tool (active by default)
  * box zoom (click to make active, deactivates pan tool)
  * tab (active by default, this initiates going to the daily file)
  * reset (click to reset view)
  * undo (click to go to previous view)
  * save (click to save and download as png).
* each dot is a link to the daily module file for the indicated day at the indicated instrument.

## list of variables for monthly module overview pages

Here is a list of additional plots for each module (additional to the two named above that are the same in each module) that are module specific:

### _L1_

* local solar noon and time of the measurement having the smallest solar zenith angle. Also indicated are the ± 10 min lines around the calculated solar noon.
* solar zenith angle of the measurement with the lowest solar zenith angle
* (daily) median of the relative radiance and also indicated is the monthly median of the daily medians.
* (daily) maximum radiance with monthly median of this

### _qdoas_m_ and _qdoas_s_

All monthly overview plots are shown for each window in a different color, according to the legend. The legend is clickable to toggle the corresponding window, however, the plots are not inter-connected, so toggling one plot, will not hide the same window in another plot. While the first two should be the same in all windows, they are still plotted for each window.

* median of slit function parameter (with monthly median ±3 std ranges)
* median of calibration shift (with monthly median ±3 std ranges)
* median of rms (with monthly median ±3 std ranges)
* median of wavelength_shift (with monthly median ±3 std ranges)
* median of resol_cross_section_contribution (variable accounting for differences in resolution between calib ref and spectrum), Screenshot from 2022-11-14 13-47-55

### o3strato and no2strato

This module is called o3strato although it should be called o3total. Since names are directly extracted from the folder structure, this has currently this name. It needs to be adjusted in the future.

* AM and PM VCD

### tropo

* mean number of elevation angles per scan (with median - 3 std)
* mean broken cloud flag per day (0 is no broken clouds, 1 is broken clouds, so the closer to 0, the more unflagged scans)
* for each window, one plot displaying mean mmf, mapa and overall_qa flag.

## daily module file

Mostly, the same parameters are displayed as for the monthly overview files. Some comments:

* at the top, the name and path of the log file is indicated (less interesting for you)
* just below, the name of the file which content is displayed, is indicated
* No mean or median lines are included in the plots.
* For _no2strato_ and _o3strato_, AM and PM plots are both present.
* most plots have a _lin_ and a _log_ tab which changes one or both of the axes between linear and log, where it makes sense.
* at the top, one case go directly go to the previous or next day, without having to go back to the monthly overview page.
* if a plot shows more than one line (e.g. AM and PM or measured and simulated, or apriori and profile), the lines can be toggled via a click on the legend
* _L1_ daily plots might take a while to load, they offer the possibility to plot each spectrum (since the tab tool is activated by default, a click on any measurement will plot the corresponding spectrum, holding the shift button and clicking on another point, will add another spectrum; one can activated the box select tool and then draw a box containing several points right away to plot several spectra).
* Similar to the _L1_ daily pots, the _tropo_ daily plots offer the posibility to plot more details (corresponding profiles and measured and simulated dscds) when selecting (via activated tab selector or via activable box select) points in the time series.

