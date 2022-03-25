---
layout: page
title: LARRA
description: Multilateration Receiver Redundancy Analyzer
img: assets/img/larra_intro1.png
importance: 1
category: work
---
LARRA (**LA**m **R**eceiver **R**edundancy **A**nalyzer) is tool for analysis of multilateration coverage, probability of detection and it also simulates degraded states of the system.

## Introduction
The LAM (Local Area Multilateration) system needs specific number of receiving stations. The number of stations depends on the covered area, system design and budget of the operator. From the multilateration principle at least 4 stations are necessary, however, small LAM system typically consist of 8 - 20 stations, large system cosists of tens (40 - 60) of stations. Typical system works well in operational, non-degraded state and acceptable in defined degraded state. The degraded state is defined by the manufacturer, typically N-1, N-2. It means the system is still operational with one or two non-functional stations (or more if defined so), the accuracy or probability of detection is reduced but still meets specification.

In order to understand the performance of the LAM system installed at the Prague airport the LARRA analyzer was developed. LARRA analyzes LAM performance in a mesh grid with cell resolution of 50 m over the whole airport. 
Available metrics calculated by LARRA:
  - total number of detections by the whole system
  - number of contributing recivers in each cell
  - total number of detections by each station
  - probability of detection of each station
  - degradations simulator - simulator of N-X state

## Data used in the analysis
LARRA uses ASTERIX data in Cat020. The item I020/400 in ASTERIX record contains information about receivers contributing to each detection. For the purpose of the analysis the are conditioned:
  - Vehicles are filtered out, only aircrafts remain in processing (based on offline ICAO address database).
  - Manually selected ICAO adresses are excluded from processing (site monitors, unknown vehicles, test transponders, interrogators).
  - Target reports with GSB=1 in ASTERIX I020/020 remain in processing, airborne targets are filtered out.
  - Target reports with RAB=0 in ASTERIX I020/020 are filtered out (site monitors).
  - Target reports with CNF=0 in ASTERIX I020/170 remain in processing. Unconfirmed reports are filtered out.
  - Target reports coming from outer area of the airport are filtered out.

## Data processing
There are three stages of data:
  1. ASTERIX recoreded data in binary format, raw data recorded by target processsor, hourly rate.
  2. Intermediate data that contain: position X, Y, contributing receivers. For future use measured height, geometric height and DOPs from I020/500 are stored as well. Intermediate data are pickled on daily basis.
  3. Processed data, stored on daily basis (one day, one file). In each file two matrix object are stored:
    a. Total number of detections for each square of mesh grid by the whole system. Size of the matrix: (num_cells_x, num_cells_y, 1), 2D matrix.
    b. Number of detections for each square by each station. Size of matrix: (num_cells_x, num_cells_y, num_of_receiving_stations), 3D matrix.

LARRA dashboard allows to create dataset for given range of dates (eg. to study performance during isolated degraded states). When creating dataset, daily detections by system and stations are merged over the desired period. Output is two files, first contains total number of detections over the whole period, second contains number of detections for each cell by each station accumulated over the whole period.

## Probability of detection for receiver

## Dashboard
All metrics and analyses are presented on the web gui interface. Let's go through all possibilities of the web interface.

### Preparation
Allows to create a dataset. It is possible to create datasets for separate Target Processors (if data are available) and for given date range. Date range is selectable on two click in double calendar, as default the maximum available data range is prefilled.
Already available datasets are displayed in table next to the calendar. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/larra-prep.png title: "Dataset preparation" class: "img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Preparation of the dataset, list of available datasets.
</div>

### Statistics - Total number of detections
Shows map of the airport with colored layer indicating number of detection in each cell by the whole system. The number is displayed in cursor label on hover over the cell. Total number of detections by each station are also shown in the table. This statistics is useful for identification of low-traffic cells.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/larra-detections.png title: "Total number of detections" class: "img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Total number of detections color-coded in map. Number of total detections by each station in the table. Number of detection in single cell is shown as cursor label on hover.
</div>

### Statistics - Number of contributing receivers
For selected dataset the map with colored layer is displayed. Color of the cell corresponds to the number of receivers contributing to position detection. For each cell the number of receivers contributing to position detection is presented also in cursor label. It is possible to click in the figure (which selects the cell under examination) and contributing receivers for selected cell are then added to the map.
In orded to decide if receiver contributes or not it is necessary to select desired probability of detection. The probablity of detection is selectable in the range from 0 to 100 %.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/larra-receivers.png title: "Number of contributing receivers" class: "img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Number of contributing receivers color-coded in map. Probability of detection for receivers contributing to selected cell listed in the table. Number of contributing receiver for a single cell is shown as cursor label on hover. Cell is selectable on click.
</div>

### Statistics - Number of detections by receivers
Shows map of the airport with colored layer indicating number of detection in each cell by each station - selectable in the radio list. The number of detections is displayed in cursor label on hover over the cell. This statistics is useful for identification of low traffic cells.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/larra-rx-detections.png title: "Total number of detections" class: "img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Total number of detections by each receiver color-coded in map. The receiver is selectable by radio buttons on the left. Number of detection by the receiver in single cell is shown as cursor label on hover.
</div>


To give your project a background in the portfolio page, just add the img tag to the front matter like so:


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/1.jpg title: "example image" class: "img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/3.jpg title: "example image" class: "img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/5.jpg title: "example image" class: "img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% responsive_image path: assets/img/5.jpg title: "example image" class: "img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal it's glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% responsive_image path: assets/img/6.jpg title: "example image" class: "img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% responsive_image path: assets/img/11.jpg title: "example image" class: "img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% responsive_image path: assets/img/6.jpg title: "example image" class: "img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% responsive_image path: assets/img/11.jpg title: "example image" class: "img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %}
