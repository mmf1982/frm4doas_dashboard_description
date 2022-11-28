# Description of the dashboard

## Table of Contents  
[start page](#start-page)  

[instrument overview  page](#instrument-overview-page)

[monthly instrument module page](#monthly-module-overview-page)

[daily instrument module page](#daily-module-file)

## start page

This is the start page view, showing all instruments currently included in the processing:

![dashboard starting page](https://user-images.githubusercontent.com/38353016/204289387-a7efd522-5fde-41d0-a1d6-9037bfbadccd.png)

* Each image consists of 3 -- 6 horizontal blocks, each representing a module:
   - the first will always be _L1_
   - the second (and maybe third) will be qdoas, "qdoas_s" is the qdoas analysis preceding the o3total and no2strato processing, _qdoas_m_ is the _qdoas_ processing preceeding the tropospheric processing. Depending on which processing is active for the station, one or both qdoas are displayed
   - the following rows represent _tropo_, _o3total_, _no2strato_, depending on the station
* While not very well visible in the overview page, each such block is build up of 28 columns and three rows, each square beeing either red, green or white.
* The rows will be described later, each column is a day, the right most column is "yesterday".
* The last column (so "yesterday") of each instrument determines the color of the station and instrument name, red means something is not quite allright, green means all is ok.
* The last column can be white: there is a certain level1 file receiving delay, y, allowed for each station; if no level1 file was received in the last x days, all last min(x, y) columns are colored white and the color of the header is taken from the latest file that was received if this is within y, otherwise it is red. For example, there are missing files in both of the Uccle instruments, but they are both green, because the number of missing files x is smaller than the allowed delay y, and the last processed file resulted in no problems. However, Bremen 1673_2 also has missing files and although the number of missing files x is also lower than the number of allowed files y, the header is red, because the last "legal" file had some problem.
* Each image is a link to the respective instrument overview page, e.g. clicking on Uccle 1689_2 brings you to the [instrument overview page](#instrument-overview-page)
<sub>[(back)](#table-of-contents)</sub>
## instrument overview page

This is the instrument overview page for an instrument with only tropo processing:

![instrument overview page](https://user-images.githubusercontent.com/38353016/204289452-5bd95469-1122-4dea-972a-bffae66eded5.png)

The station overview page has two elements:
- a matrix overview showing each module, see below
- an area (light red background) showing checks on qdoas that showed a problem (errorcodes)

In the matrix overview, each module, here _L1_, _qdoas_m_ and _tropo_, consists of three rows:

1. number of files for the indicated day
2. number of observations for the indicated day: 
   - for _L1_, this indicates the total measurement number
   - for _qdoas_, this indicates the total number of measurements processed with qdoas
   - for _o3total_ or _no2strato_,  there are two numbers, indicating the number of measurements used individually for AM and PM processing
   - for _tropo_, this indicates the number of scans
3. short info on module specific checks:
   - for _L1_, this is the time difference between the calculated solar noon at the station's location and the time of the measurement with the lowest solar zenith angle. If this is larger than 10 min, this will cause this box to appear red.
   - for _qdoas_m_ or _qdoas_s_, different variables are checked and tested whether or not they are within the median ± 3 std. If any of the variables currently checked are outside this region, an error code is produced and a list of occured errors can be found below the matrix overview plot in the light red area. Please see Section [details on qdoas checks](#qdoas_m-and-qdoas_s) for more info.
   - neither of the modules producing level2 files (_tropo_, _o3strato_ or _no2strato_) fills the "checks" row at the moment, therefore, the row is blanc.

From the instrument overview page, one has the following two possibilities to go further:
- following the link to the [monthly module overview page](#monthly-module-overview-page) for the corresponding module by click the green link, here _L1_, _qdoas_m_ or _tropo_, in the header of each section.
- open a [dailymodule page](#daily-module-file) for the corresponding instrument by clicking on corresponding day column in the corresponding module block.

If there are four or more modules (i.e. for any station that does not only have _tropo_ processing, or not only _no2strato_ processing, the matrix overview part is scrollable. If needed, the area indicating the error codes is also scrollable.
<sub>[(back)](#table-of-contents)</sub>
## monthly module overview page

The shown variables on the monthly overview page depend on the module in question. As an example, I show here the start of the _qdoas_m_ page from Uccle.

![monthly module overview page](https://user-images.githubusercontent.com/38353016/204289512-8023e1c7-e70b-49cf-933a-3e8214bdcde5.png)

Some general comments hold:

* Shown are always the last 28 days, whether or not they are present. If they are missing, they are now shown.
* The first row always shows a bar plot of the number of files. This should be exactly one.
* The second plot always shows the number of measurements and indicated in there is the "median-3 std" line as a black line (black and red lines in the case of _no2strato_ or _o3total_, the former indicating am, the latter pm). As mentioned above, in case of _L1_, _qdoas_m_ or _qdoas_s_, this is the number of measurements. In case of _tropo_, this is the number of scans and in case of _no2strato_ and _o3total_ it is the number of measurements used for the am and pm retrieval, respectively.
* all but the first plot have the following plotting tools available (However, if your screen is very small, you might not be able to see all the tools):

   ![dahboard_4](https://user-images.githubusercontent.com/38353016/202756779-12627130-6efd-4a76-bd61-dab6906cff2e.png)
  * pan tool (active by default)
  * box zoom (click to make active, deactivates pan tool)
  * tab (active by default, this initiates going to the daily file)
  * reset (click to reset view)
  * undo (click to go to previous view)
  * save (click to save and download as png).
* each dot is a link to the daily module file for the indicated day at the indicated instrument.

The module specific variables are described in the following subsections.
<sub>[(back)](#table-of-contents)</sub>
### _L1_

* local solar noon and time of the measurement having the smallest solar zenith angle. Also indicated are the ± 10 min lines around the calculated solar noon.
* solar zenith angle of the measurement with the lowest solar zenith angle
* (daily) median of the relative intensity (wavelength mean of (radiance)/exposure time) and also indicated is the monthly median of the daily medians.
* (daily) maximum radiance with monthly median of this
<sub>[(back)](#table-of-contents)</sub>
### _qdoas_m_ and _qdoas_s_

All monthly overview plots are shown for each window in a different color in the same plot, according to the legend. The legend is clickable to toggle the corresponding window, however, the plots are not inter-connected, so toggling one plot, will not hide the same window in another plot, but panning and zooming (in time) will act on all plots. While the first two should be the same in all windows since they concern the calibartion, they are still plotted for each window.

* median of slit function parameter (with monthly median ±3 std ranges)
* median of calibration shift (with monthly median ±3 std ranges)
* median of constant offset (with monthly median ±3 std ranges)
* median of rms (with monthly median ±3 std ranges)
* median of wavelength_shift (with monthly median ±3 std ranges)
* median of resol_cross_section_contribution (variable accounting for differences in resolution between calibration reference and spectrum)

All these parameters take currently the whole day into account. Although the median should in principle circumvent the problem of sunset/sunrise effects, it might be advisable to choose a better indicator than the median and suggestions are welcome.
<sub>[(back)](#table-of-contents)</sub>
### _o3strato_ and _no2strato_

* am and pm VCD without indication of monthly median.
<sub>[(back)](#table-of-contents)</sub>
### _tropo_

* mean number of elevation angles per scan (with median - 3 std)
* mean broken cloud flag per day (0 is no broken clouds, 1 is broken clouds, so the closer to 0, the more unflagged scans)
* for each window, one plot displaying mean mmf, mapa and overall_qa flag.
<sub>[(back)](#table-of-contents)</sub>
## daily module file

Mostly, the same parameters are displayed as for the [monthly overview](#monthly-module-overview-page) files. Some comments:

* at the top, the name (and path, only internally due to security regulations) of the log file is indicated.
* just below, the name of the file which content is displayed, is indicated
* No mean or median lines are included in the plots.
* For _no2strato_ and _o3strato_, AM and PM plots are both present.
* most plots have a _lin_ and a _log_ tab (upper left corner, if present) which changes one or both of the axes between linear and log, where it makes sense.
* at the top, one can go directly to the previous or next day (buttons in the gray sticky header), without having to go back to the monthly overview page.
* if a plot shows more than one line (e.g. AM and PM, or measured and simulated, or apriori and profile), the lines can be toggled via a click on the legend
<sub>[(back)](#table-of-contents)</sub>
### L1
* _L1_ daily plots might take a while to load
* in the sticky header, the color coding is indicated, each color indicates a certain measurement type.
* the first panel shows the relative intensity (wavelength mean of intensity over exposure time)
* second panel shows exposure time
* they offer the possibility to plot each spectrum:
   - the tab tool is activated by default, a click on any measurement in either the relative intensity or exposure time plot, will plot the corresponding spectrum in the lowest panel
   - holding the shift button and clicking on another point, will add another spectrum
   - one can activated the box select tool and then draw a box containing several points right away to plot several spectra.
   - a click in an area without any points goes back to the no-measurement-selected view.
* note the log/ lin tabs in the upper left corner of each plot.
<sub>[(back)](#table-of-contents)</sub>
### _qdoas_

![qdoas](https://user-images.githubusercontent.com/38353016/204289675-fd000ba1-0486-4c69-8135-d06e174574c7.png)

* the first two panels (both shown in the first line), show calibration diagnostics: the slit function parameter 1 (sfp 1) and the calibration shift (calib shift). Both are shown as a function of wavelength sub-window index and hence indicate the stability over the wavelength range.
* the other panels show the same parameters described in the [monthly overview pages](#monthly-module-overview-page), simply without taking the daily median.  <sub>[(back)](#table-of-contents)</sub>

### _o3total_
![o3 total](https://user-images.githubusercontent.com/38353016/204289721-b93046cb-e0ac-40cb-be7b-32ea67c21053.png)

3 panels are shown for the _o3total_:
* QA (0 ok, 1 fail) 
* vertical column density (VCD) including error bars
* measured SCD including error bars, as function of solar zenith angle (green for am, red for pm, as indicated in the legend)
<sub>[(back)](#table-of-contents)</sub>
### _no2strato_
![no2strato](https://user-images.githubusercontent.com/38353016/204289770-f59c3400-fd93-4d16-b35e-21f186d05a1e.png)

5 panels are shown for _no2strato_:
* first line:
   - QA (0 ok, 1 fail)
   - degree of freedom (DOF)
   - vertical column density (VCD) including error bars
* second (am) and third (pm) line: 
   - profiles: a-priori (green) and retrieved (red)
   - measured (green) and simulated (red) slant column densities (SCD), the former including error bars.
<sub>[(back)](#table-of-contents)</sub>   

### _tropo_
![tropo](https://user-images.githubusercontent.com/38353016/204289825-fd27c617-fa7c-45c0-af7f-d422fff26ae9.png)

* the first panel shows a daily time series of a number of flags:
   - the broken cloud flag (dashed black)
   - the overall flag for all trace gases retrieved from the measurements of the instrument in question, with color coding according to the legend
* Similar to the _L1_ daily pots, the _tropo_ daily plots offer the posibility to plot more details (corresponding profiles and measured and simulated dscds) when selecting (via activated tab selector or via activatable box select) points in the time series.
* each row (they come in pairs of two: one trace gas row followed by the corresponding o4 window and aerosol retrieval) following the flag panel, consists of:
   - a time series of the integrated quantity (VCD or AOD) (left)
   - the retrieved profile (if a measurement or measurements are selected) (middle)
   - measured and simulated dscs (right)
* the color coding, similar to the L1 daily plots, is indicated in the header, mapa has circles, mmf has crosses, each three different colors to indicate the flagging condition.
* on the right, one can de-select either of the two codes (mapa, mmf) in each set of two rows
* if two or more trace gases use the same o4 window for its base aerosol retrieval, the aerosol retrieval row is duplicated and shown after each of the trace gases.
<sub>[(back)](#table-of-contents)</sub>
