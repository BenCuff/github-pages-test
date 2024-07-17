---
title: "Accessibility: Data visualisation"
layout: guidance-page

page-group-title: "Accessibility"
page1: 
  url: data-vis
  name: "<u>Data visualisations</u>"
page2: 
  url: spreadsheets
  name: "Spreadsheets"
---
> ## Main messages
>- Data visualisations must be compliant with current accessibility legislation.
>- You should choose an appropriate and consistent way to visualise different types of data.
>- Colours, text, and formatting should be carefully applied in order to aid interpretation of data visualisations.
>- Data visualisations should be easy to understand for users of all backgrounds.

Throughout this document, citations are given as numbers in square brackets. They link to a full reference list which can be found at the end of this document.

We are currently developing some accessible UKHSA branded colour palettes. For now, you may wish to use the Analysis Function palettes.

## Introduction

This guidance is intended as a practical handbook for creating charts and charts. It condenses the most relevant Government resources on data visualisation together with the Statistics Production Division's own experience producing official statistics and working with statistics producers. While the information on this page is by no means comprehensive, we hope that it provides a useful overview of best practices and how to implement them.

Good accessibility brings benefits to all users, improving the quality and value of our statistics, and the trust users have in us as an organisation. It is particularly important for people with disabilities, remembering that [20% of the working-age population report having a disability](https://www.gov.uk/government/statistics/the-employment-of-disabled-people-2021/the-employment-of-disabled-people-2021#:~:text=1%20in%205%20of%20the%20working%2Dage%20population%20are%20classed%20as%20disabled,-Figure%203a%3A%20Proportion&text=Source%3A%20Annual%20Population%20Survey%20%E2%80%93%20data,to%20question%201%20(see%20below)). We welcome any contributions from colleagues who may wish to share their own knowledge, charts, or code to incorporate into this document.

R code to produce a minimal reproducible example is available under each chart. They were made using a standard ggplot2 theme which can be found below. If you have any questions about our R resources or need any assistance using them, don't hesitate to email the Statistics Production Division at [UKHSA_HOPSTATS@ukhsa.gov.uk](mailto:UKHSA_HOPSTATS@ukhsa.gov.uk) and we'll be happy to help in any way that we can!



{% capture expandable_content_1 %}

```
theme_af <- function(font_size = 12, font_family = NULL, grid = "y", tick_mark = NULL, ...){
 
  # Base theme:
  theme <- theme_grey(base_size = font_size) +
 
    # Analysis Function chart style:
    theme(
 
      # Pass in the dots:
      ...,
 
      # Panel:
      panel.background = ggplot2::element_blank(),
      panel.border = ggplot2::element_blank(),
 
      # Global font size:
      text = ggplot2::element_text(size = font_size),
 
      # Title:
      plot.title.position = "plot", # applied to subtitle too.
 
      # Sub-title (y-axis label):
      plot.subtitle = ggplot2::element_text(
        family = font_family,
        size = font_size,
        margin = ggplot2::margin(b = 10)),
 
      # ...and my axe(s):
      axis.title = ggplot2::element_text(
        family = font_family,
        size = font_size,
        colour = "#000000"
      ),
 
      axis.text = ggplot2::element_text(
        family = font_family,
        size = font_size,
        colour = "#000000"
      ),
 
      # Legend:
      legend.title = ggplot2::element_blank(),
      legend.text = ggplot2::element_text(family = font_family,
                                          size = font_size,
                                          colour = "#000000"),
 
      # Caption:
      plot.caption.position = "plot",
      plot.caption = ggplot2::element_text(family = font_family,
                                           size = font_size,
                                           colour = "#000000"),
 
      # Facets:
      strip.background = ggplot2::element_blank(),
      strip.text = ggplot2::element_text(family = font_family,
                                         size = font_size,
                                         hjust = 0), # Don't want bold face
 
    )
 
  #
  if (inherits(grid, "character")) {
 
    grid <- tolower(grid)
 
    if (regexpr("x", grid)[1] > 0) theme <- theme + theme(panel.grid.minor = ggplot2::element_blank(),
                                                          panel.grid.major.x = ggplot2::element_line(colour = "#D9D9D9"),
                                                          panel.grid.major.y = ggplot2::element_blank(),
                                                          axis.line.x = ggplot2::element_blank(),
                                                          axis.line.y = ggplot2::element_line(colour = "#D9D9D9"))
 
    if (regexpr("y", grid)[1] > 0) theme <- theme + theme(panel.grid.minor = ggplot2::element_blank(),
                                                          panel.grid.major.x = ggplot2::element_blank(),
                                                          panel.grid.major.y = ggplot2::element_line(colour = "#D9D9D9"),
                                                          axis.line.x = ggplot2::element_line(colour = "#D9D9D9"),
                                                          axis.line.y = ggplot2::element_blank())
 
    if (regexpr("xy", grid)[1] > 0) theme <- theme + theme(panel.grid.minor = ggplot2::element_blank(),
                                                           panel.grid.major.x = ggplot2::element_line(colour = "#D9D9D9"),
                                                           panel.grid.major.y = ggplot2::element_line(colour = "#D9D9D9"),
                                                           axis.line.x = ggplot2::element_line(colour = "#D9D9D9"),
                                                           axis.line.y = ggplot2::element_line(colour = "#D9D9D9"))
 
  } else {
 
    theme <- theme + theme(panel.grid = ggplot2::element_blank())
 
  }
 
  if (inherits(tick_mark, "character")) {
 
    tick_mark <- tolower(tick_mark)
 
    if(grepl("x", tick_mark)) {
 
      theme <- theme + theme(axis.ticks.x = ggplot2::element_line(colour = "#D9D9D9"))
      theme <- theme + theme(axis.ticks.y = ggplot2::element_blank())
 
    }
 
    if(grepl("y", tick_mark)) {
 
      theme <- theme + theme(axis.ticks.x = ggplot2::element_blank())
      theme <- theme + theme(axis.ticks.y = ggplot2::element_line(colour = "#D9D9D9"))
 
    }
 
    if(grepl("xy", tick_mark)) {
 
      theme <- theme + theme(axis.ticks.x = ggplot2::element_line(colour = "#D9D9D9"))
      theme <- theme + theme(axis.ticks.y = ggplot2::element_line(colour = "#D9D9D9"))
 
    }
 
  } else {
 
    theme <- theme + theme(axis.ticks.x = ggplot2::element_blank())
    theme <- theme + theme(axis.ticks.y = ggplot2::element_blank())
 
  }
 
  theme
 
}
```
{% endcapture %}
{% include expandable-block-start.html %}
  {% include expandable-section.html number="1" content=expandable_content_1 title="Analysis Function ggplot2 theme" %}
  {% include expandable-block-end.html %}

## Choosing the right chart

Charts are particularly effective when used to highlight key points in a publication [1]. You should choose the type of chart based on the type of data and the trend you are trying to show. 

This section gives some specific recommendations for presenting categorical data or time series data in an accessible way. 

### Categorical data

Bar charts work well for comparing different categories

When making a bar chart, consider whether there is a logical ordering to the bars that groups similar categories together. For example, you could order age groups from lowest to highest or place bars to adjacent geochartical regions next to eachother. If there is no logical ordering, it is often most helpful to present bars in order of size.

Stacked or clustered bar charts can be used to display two different categorical variables in one chart. However, each individual stack or cluster should usually contain no more than four categories as a rule of thumb, to avoid clutter. This is especially the case for stacked bar charts, as a larger number of categories makes comparisons between bars much more difficult. If you have a large number of categories, it is usually best to split your data into several bar charts. The section "Avoiding cluttered charts" contains examples of ways to break down charts that contain too many categories, including reformatting them as small multiples charts.

It is best practice when making clustered bar charts to leave a small gap between each bar in a cluster to help users distinguish more easily between bars. A wider gap should be left between clusters, again to help users easily distinguish different clusters [1].

{% capture card_content_1 %}
Example 1: Percentage of positive tests for three disease strains at five testing centres in England, 2024
    <img src="assets/img/Data viz/Example 1.png" width="450px" alt="">
{% endcapture %}

{% capture card_content_2 %}
Example 2: Percentage of positive tests for three disease strains at five testing centres in England, 2024
   <img src="assets/img/Data viz/Example 2.png" width="450px" alt="">
{% endcapture %}

{% include cards-container-start.html %}
  {% include card.html content=card_content_1 title="To be avoided: no space within clusters " %}
  {% include card.html content=card_content_2 title="Best practice: applying spacing to clustered bar charts" %}
{% include cards-container-end.html %}


{% capture expandable_content_2 %}
```
# Create data frame:
df <- data.frame(Strain = c(rep("Strain A", 5), rep("Strain B", 5), rep("Strain C", 5)),
                Centre = c(rep(c("Centre 1", "Centre 2", "Centre 3", "Centre 4", "Centre 5"))),
                Positivity = c(1, 1.2, 1.3, 1.4, 1.5, 3.1, 3.5, 5, 4.9, 4.4, 4.4, 5.1, 5.2, 5.6, 5.7),
                check.names = F)
 
# Load ggplot2 package:
library(ggplot2)
 
# Make chart:
ggplot(df, aes(x = Centre, y = Positivity, fill = Strain)) +
  geom_bar(stat = "identity",
           position = position_dodge(0.8),
           width = 0.7) +
  scale_y_continuous(breaks = seq(0, 7, 1),
                     expand = expansion(mult = c(0, 0.02)),
                     limits = c(0, 7)) +
  scale_fill_manual(values = af_colours(type = "categorical", n = 3)) +
  labs(subtitle = "Per cent positive (%)",
       x = NULL,
       y = NULL) +
  theme_af(font_size = 20,
            legend.position = "bottom",
            tick_mark = "x")
```
{% endcapture %}
{% include expandable-block-start.html %}
  {% include expandable-section.html number="2" content=expandable_content_2 title="R code for Example 2" %}
  {% include expandable-block-end.html %}
  
### Time series data

Line charts are most often used to show time series data. They work well for showing how multiple variables change over a period of time [1] [3].

If you are only showing one time series variable, a bar chart can also be used. However, stacked and clustered bar charts should not be used for displaying multiple time series variables as they make comparisons difficult.

Below, the stacked bar chart on the left makes non-adjacent categories in the same bar difficult to compare: here, the “All” and “Male” categories appear the same size in many of the bars. Furthermore, it is difficult to see how categories other than the bottom one change over time. Changes in the “Male” bar are clearly displayed, but trends in the other two categories are harder to identify at a glance. (Note that stacking totals on top of individual categories is also not good practice here.) Where there is only one category, a bar chart is easy to read, as can be seen on the right.

{% capture card_content_3 %}
Example 3: Annual unemployment rates by gender, UK, 2008 to 2024
    <img src="assets/img/Data viz/Example 3.png" width="450px" alt="">
{% endcapture %}

{% capture card_content_4 %}
Example 4: Annual unemployment rates for all genders, UK, 2008 to 2024
   <img src="assets/img/Data viz/Example 4.png" width="450px" alt="">
{% endcapture %}

{% include cards-container-start.html %}
  {% include card.html content=card_content_3 title="To be avoided: showing multiple categories in time series data with stacked bar charts" %}
  {% include card.html content=card_content_4 title="Best practice: using bar charts or line charts for time series data only when there is one category" %}
{% include cards-container-end.html %}

{% capture expandable_content_3 %}
```
# Load dplyr, tidyr (for data manipulation) and ggplot2 (for data visualisation):
library(tidyverse)
 
# Create data frame:
df <- data.frame(year = 2008:2024,
                Male = c(4.1,5.2,6.4,7.5,8.0,9.0,9.5,9.7,9.4,8.2,7.1,6.0,6.2,6.7,7.6,8.0,7.2),
                Female = c(6.4,7.3,8.7,9.1,8.5,11.2,11.1,11.1,11.7,10.4,9.1,8.0,6.8,9.7,8.4,8.2,8.2),
                check.names = F) %>%
  mutate(All = (Male + Female)/2) %>%
  pivot_longer(cols = 2:4, names_to = "gender", values_to = "unemployed")
 
# We want to show tick marks for every year not just the x-axis labels:
year_seq <- seq(2008, 2024, 1)
year_seq[seq(2008, 2024, 1) %% 4 != 0] <- ""
 
# Make chart:
df |>
  filter(gender == "All") |>
  ggplot(aes(x = year, y = unemployed)) +
  geom_bar(stat = "identity",
           width = .8,
           fill = "#12436D") +
  scale_x_continuous(breaks = 2008:2024,
                     labels = year_seq) +
  scale_y_continuous(breaks = seq(0, 12, 2),
                     expand = expansion(mult = c(0, 0.02)),
                     limits = c(0, 12)) +
  labs(subtitle = "Annual unemployment rate (%)",
       x = NULL,
       y = NULL) +
  theme_af(font_size = 20,
            legend.position = "bottom",
            tick_mark = "x")
```
{% endcapture %}
{% include expandable-block-start.html %}
  {% include expandable-section.html number="3" content=expandable_content_3 title="R code for Example 4" %}
  {% include expandable-block-end.html %}
  
Below, the clustered bar chart on the left resolves some of the issues with comparability seen in the stacked bar chart above, but is more visually crowded as the bars become thinner and harder to focus on. Stacked and clustered bar charts are also not a good choice when you wish to display the total of all categories alongside the individual groups. The inclusion of a separate bar for "All" in the two bar charts above can incorrectly imply to users that this is a third, distinct category.

When multiple categories are involved, it is best practice to use a line chart like the one on the right. In this chart, differences between categories and time points are easy to identify. The overall trends are clearly displayed and can be understood at a glance. Note that the lines have been labelled directly rather than with a legend: this is how line charts should be labelled.

{% capture card_content_5 %}
Example 5: Annual unemployment rates by gender, UK, 2008 to 2024
    <img src="assets/img/Data viz/Example 5.png" width="450px" alt="">
{% endcapture %}

{% capture card_content_6 %}
Example 6: Annual unemployment rates by gender, UK, 2008 to 2024
   <img src="assets/img/Data viz/Example 6.png" width="450px" alt="">
{% endcapture %}

{% include cards-container-start.html %}
  {% include card.html content=card_content_5 title="To be avoided: showing multiple categories in time series data with stacked bar charts" %}
  {% include card.html content=card_content_6 title="Best practice: using bar charts or line charts for time series data only when there is one category" %}
{% include cards-container-end.html %}
  
  
{% capture expandable_content_4 %}
```
# Here we will use the data frame `df` from Example 4:
ggplot(df, aes(x = year, y = unemployed, colour = gender)) +
  geom_line(linewidth = 1.2) +
  scale_x_continuous(breaks = 2008:2024,
                     expand = expansion(mult = c(0.02, 0.2)),
                     labels = year_seq) +
  scale_y_continuous(breaks = seq(0, 12, 2),
                     expand = expansion(mult = c(0, 0.02)),
                     limits = c(0, 12)) +
  scale_fill_manual(values = af_colours(type = "categorical", n = 3)) +
  labs(subtitle = "Annual unemployment rate (%)",
       x = NULL,
       y = NULL) +
  theme_af(font_size = 20,
            legend.position = "none",
            tick_mark = "x") +
  coord_cartesian(clip = "off") +
  geom_text_repel(aes(label = gender, x=year, y = unemployed),
                  size = 6, # Font size
                  xlim = max(df_36$year) + 2,  # Limits for where on the x-axis the label can appear
                  ylim = c(4, 11), # Limits for where on the y-axis the label can appear
                  force = .1,
                  point.size = NA,
                  box.padding = 1,
                  segment.color = "#D9D9D9",
                  data = df_36 %>%
                    group_by(gender) %>%
                    filter(year == max(year)))
```
{% endcapture %}
{% include expandable-block-start.html %}
  {% include expandable-section.html number="4" content=expandable_content_4 title="R code for Example 6" %}
  {% include expandable-block-end.html %}
  
See the "communicating without colour" section below for more information on how to format a chart like this, including how to directly label lines.

### Weekly and quarterly time series data

Some types of time series data, especially health data, are often gathered and interpreted on a weekly or quarterly basis. 

If you are using a bar chart to show quarterly data, you should not colour every bar according to quarter as this can be difficult to read. One of the benefits of using week or quarter numbers is that it allows the same point in time to be compared across multiple years: for instance, comparing data from the most recent quarter with data from the same quarter last year. If you would like users to compare specific values in this way, this may be better achieved with plain text or a table than a chart. Analysis function guidance notes that “a well structured table can often be as powerful as a chart” in these situations, and that another option is to include both.

{% capture card_content_7 %}
Example 7: quarterly survey respondents, England and Wales, 2022 to 2023
    <img src="assets/img/Data viz/Example 7.png" width="450px" alt="">
{% endcapture %}

{% capture card_content_8 %}
Example 8: quarterly survey respondents, England and Wales, 2022 to 2023
   <img src="assets/img/Data viz/Example 8.png" width="450px" alt="">
{% endcapture %}

{% include cards-container-start.html %}
  {% include card.html content=card_content_7 title="To be avoided: using colours to indicate quarter number on a bar chart" %}
  {% include card.html content=card_content_8 title="Best practice: label all quarters directly and use the same colour for each" %}
{% include cards-container-end.html %}

{% capture expandable_content_5 %}
```
# Create data frame:
df <- data.frame(Year = c(rep(2022, 4), rep(2023, 4)),
                Quarter = c(rep(c("Q1", "Q2", "Q3", "Q4"), 2)),
                count = rnorm(8, mean = 30, sd=5),
                check.names = F)
 
library(tidyverse)
library(tsibble) # for yearquarter()
 
# Make plot:
df |>
  as_tibble() |>
  mutate(quarter = yearquarter(paste(Year, Quarter, sep = " "))) |>
  ggplot(aes(quarter, count)) +
  geom_col(fill = "#12436D") +
  scale_x_yearquarter(date_labels = "Q%q %Y") +
  scale_y_continuous(breaks = seq(0, 50, 10),
                     expand = expansion(mult = c(0, 0.02)),
                     limits = c(0, 50)) +
  labs(subtitle = "Number of survey respondents",
       x = NULL,
       y = NULL) +
  theme_af(font_size = 20,
            legend.position = "bottom",
            tick_mark = "x")
```
{% endcapture %}
{% include expandable-block-start.html %}
  {% include expandable-section.html number="5" content=expandable_content_5 title="R code for Example 8" %}
  {% include expandable-block-end.html %}
  
ISO weeks are a useful standardisation that allows data to be compared easily with previous years. However, many users may not be familiar with how to interpret week numbers, especially when data starts midway through a calendar year and/or covers multiple years. Therefore when displaying weekly data, it may be helpful to give a brief explanation of this measurement system, or replace the labels on your x-axis with calendar dates that correspond to the start of each week.

When showing weekly data, one option might be to include some calendar dates below the week numbers. To avoid clutter, you do not need to label every week number, but should at least label:

- the beginning and end of the series 
- January and December, if they are not the beginning and end of the series

{% capture card_content_9 %}
Example 9: weekly test positivity rates, UK, past 52 weeks (no calendar dates)
    <img src="assets/img/Data viz/Example 9.png" width="450px" alt="">
{% endcapture %}

{% capture card_content_10 %}
Example 10: weekly test positivity rates, UK, past 52 weeks (including calendar dates)
{% endcapture %}

{% include cards-container-start.html %}
  {% include card.html content=card_content_9 title="To be avoided: using only week numbers to indicate time" %}
  {% include card.html content=card_content_10 title="Best practice: including month and year information" %}
{% include cards-container-end.html %}

{% capture expandable_content_6 %}
```

```
{% endcapture %}
{% include expandable-block-start.html %}
  {% include expandable-section.html number="6" content=expandable_content_6 title="R code for Example 10" %}
  {% include expandable-block-end.html %}

The charts above show data on a weekly scale, which is why it is best practice to label the start and end of the series with the month and year, as can be seen on the right. Because the chart shows data from 2021 and 2022, the end of 2021 and the beginning of 2022 have been labelled as well. A lighter grey has been used for the month labels so they do not distract too much from the message of the chart.

## Guidance for all charts

All published charts must include the following:

- an accessible alternative (text description or accessible table)
- a data source referenced in the surrounding text
- an appropriately tagged title (including figure number)
- axis and series labels


{% capture expandable_content_7 %}
It is a legal requirement under UK accessibility legislation that all non-text web content published by the Government also be presented in an alternative format that conveys the same information.

For a chart, you may choose between providing a table or a text description [1] [4]. Think about what would be most beneficial to the user: if they would want to understand a trend, this might be best served via a description in the text. If they would want to read exact values then a table may be better. 

If you choose to use a table, you can provide a link to a downloadable [accessible spreadsheet document](https://confluence.collab.test-and-trace.nhs.uk/display/SHT/Spreadsheet+accessibility). Small tables can also be placed directly beneath a chart, displayed as HTML rather than an image (although it is best not to simply repeat information already given in the chart). [5]

In most cases, it is advised to provide a text description (often in addition to a link to a spreadsheet). This text is best placed directly above or beneath the chart. Text descriptions should clearly indicate which figure they refer to, such as "Figure X shows...", "Description of figure X:...", or similar. Your description should aim to provide users with an understanding of the relationships and patterns that your chart is trying to communicate. It does not need to state every single feature or data point displayed [1].

GOV.UK and other platforms that support HTML allow you to add a hidden "alt text" attribute in the image metadata, but you should not put your text description there. Placing it near the image instead makes the text easier to find and share to all users.
{% endcapture %}

{% capture expandable_content_8 %}
Be clear about the source of your data and whether the data is available to download and make this information as easy to find as possible. In most cases, a link to an underlying dataset will suffice. For external sources, try to provide the name of the publication or data set which you are referencing, being as specific as possible and providing a direct link if one is available. If your publication uses multiple external data sources, you should provide a link under each chart [1].
{% endcapture %}

{% capture expandable_content_9 %}
The title should communicate the geocharty, time period, and variables that are displayed and is also a good place for including the figure number of the chart [1].

Titles should be provided in the body of the publication text rather than generated within the chart image. If you are publishing on GOV.UK or another platform in an HTML format, this allows them to be tagged correctly as headings using HTML [1].

{% endcapture %}

{% capture expandable_content_10 %}
Both the x and y axes should be given an appropriate title, including units if applicable. An x-axis title is not necessary when the name of the variable it shows can be easily determined based on the axis labels. For instance, a line chart whose x-axis shows years does not need to be labelled "Year", and a bar chart with a bar for each region of England does not need a label saying "Region": this information is evident from the labels and plot title. Axes that show day or week numbers should still be titled.
{% endcapture %}


{% include expandable-block-start.html %}
  {% include expandable-section.html number="7" content=expandable_content_7 title="Accessible alternative" %}
  {% include expandable-section.html number="8" content=expandable_content_8 title="Data source" %}
  {% include expandable-section.html number="9" content=expandable_content_9 title="Title" %}
  {% include expandable-section.html number="10" content=expandable_content_10 title="Axis and series labels" %}
{% include expandable-block-end.html %}

## Ranking

Si currently adding content here

{% capture card_content_11 %}
Example 11
{% endcapture %}

{% capture card_content_12 %}
Example 12
{% endcapture %}

{% include cards-container-start.html %}
  {% include card.html content=card_content_11 title="To be avoided: " %}
  {% include card.html content=card_content_12 title="Best practice:" %}
{% include cards-container-end.html %}


{% capture expandable_content_11 %}
```

```
{% endcapture %}
{% include expandable-block-start.html %}
  {% include expandable-section.html number="11" content=expandable_content_11 title="R code for Example 12" %}
  {% include expandable-block-end.html %}
  

## Breaking the axis

“Breaking” an axis occurs when part of a continuous axis is left out. Rather than starting at 0, the axis may begin at a higher value, or it may begin at 0 but exclude a range of values that contain no data points.

This can be a useful way to compare categories that have very small differences between them. However, it is best practice in bar charts to avoid this for the y-axis. This is because the bars in a bar chart are intended to be proportional representations of the different categories.

{% capture card_content_12 %}
Example 13: Number of cases, UK, 2014 to 2024
<img src="assets/img/Data viz/Example 13.png" width="450px" alt="">
{% endcapture %}

{% capture card_content_13 %}
Example 14: Number of cases, UK, 2014 to 2024
<img src="assets/img/Data viz/Example 14.png" width="450px" alt="">
{% endcapture %}

{% include cards-container-start.html %}
  {% include card.html content=card_content_12 title="To be avoided: breaking the y-axis when using a bar chart" %}
  {% include card.html content=card_content_13 title=" Best practice: start the y-axis at zero in bar charts" %}
{% include cards-container-end.html %}
  
{% capture expandable_content_12 %}
```
# Create data frame:
df <- data.frame(year = seq(2014, 2024, 1),
                      cases = rnorm(n = 11, mean = 45, sd = 1))
 
# We want to show tick marks for every year not just the x-axis labels. Make every second x-axis label blank:
year_seq <- seq(2014, 2024, 1)
year_seq[seq(2014, 2024, 1) %% 2 != 0] <- ""
 
#
df |>
  ggplot(aes(year, cases)) +
  geom_col(fill = "#12436D") +
  coord_cartesian(y = c(40, 50)) +
  scale_x_continuous(breaks = 2014:2024,
                     labels = year_seq) +
  scale_y_continuous(breaks = seq(40, 50, 2),
                     expand = expansion(mult = c(0, 0.02)),
                     limits = c(0, 50)) +
  labs(subtitle = "Number of cases",
       x = NULL,
       y = NULL) +
  theme_af(font_size = 20,
            tick_mark = "x")
```
{% endcapture %}
{% include expandable-block-start.html %}
  {% include expandable-section.html number="12" content=expandable_content_12 title="R code for Example 14" %}
  {% include expandable-block-end.html %}
  

Above, the bar chart on the left shows an example of a misleading break in the y-axis. In the bar chart on the right, best practice has been followed for formatting a y-axis that starts at 0.

If you need to break the y-axis, you should use a line chart, dot plot, or other alternative chart and indicate the break clearly on the chart by:

- making the break in the y-axis clear using a [broken axis symbol](https://en.wikipedia.org/wiki/File:Y-axis_break.svg) (two parallel lines striking diagonally through the axis)
- making the x-axis line the same colour and thickness as the gridlines
- making the y-axis and the axis break symbol thicker and darker than the gridlines and x-axis [1]

Axis breaks should only be used to show that the y-axis does not start at zero. Where you would like to display data points that contain an outlier, you should never break the axis halfway through.
  
  
## Chart colours and text

The colours and formatting of a chart can make a significant difference in its legibility. To ensure your chart can be read and understood by as many people as possible, it is best practice to:

- use a suitable and accessible colour palette [1] [6]
- ensure that you do not rely on colour alone to communicate information [1]
- use white for the background [1] [6]
- use light grey for gridlines [1] [6]
- avoid any images, patterns, or shading [1] [6]
- use black or dark grey text in a sans serif font [1] [6]
- avoid slanted or vertical text [1]
- ensure that text is large enough to be read easily [1]
  
### Using a suitable and accessible colour palette

It is an accessibility requirement that visual elements such as charts use colours that have a contrast ratio of at least 3:1 with their backgrounds [11]. The WebAim site contains more information on this requirement and has a contrast checker you can use to make sure that your colours are appropriate.

It is best to:

- not rely on colour alone to communicate information (directly label line charts or use a legend in the same order as categories in bar charts)
- avoid using a palette of more than 4 colours; do not use palettes of more than 6 colours (split charts up instead)
- for ordinal categories (such as age), use single-hue palettes (for example, different shades of blue) but ensure all colours have a good contrast with a white background
- not use single-hue palettes for non-ordinal categories (use different colours instead)
- use the [Analysis Function colour palette](https://analysisfunction.civilservice.gov.uk/policy-store/data-visualisation-colours-in-charts/).

### Communicating without colour

It is an accessibility requirement that charts do not rely on colour alone to communicate. This means that charts should be just as easy to understand if they are displayed in greyscale as they are in full colour [6]. However, the use of patterns and shading is not always a good way to distinguish between chart categories. Bar charts should not have patterned bars as these can be very difficult to distinguish, especially at small sizes and in the legend wherever the boxes are not large enough to properly show the pattern.

It is possible to use different data marker shapes or textured lines such as dotted or dashed lines to distinguish between variables on a line chart. However, these also increase clutter and caution is advised in using them [1] [6] [2].

{% capture card_content_14 %}
Example 15: Annual unemployment rates by gender, UK, 2008 to 2024
<img src="assets/img/Data viz/Example 15.png" width="450px" alt="">
{% endcapture %}

{% capture card_content_15 %}
Example 16: Annual unemployment rates by gender, UK, 2008 to 2024
<img src="assets/img/Data viz/Example 16.png" width="450px" alt="">
{% endcapture %}

{% include cards-container-start.html %}
  {% include card.html content=card_content_14 title="To be avoided: relying on colour alone to distinguish categories" %}
  {% include card.html content=card_content_15 title="Best practice: labelling the categories directly" %}
{% include cards-container-end.html %}

The chart on the left relies entirely on colour to communicate which line represents which category, presenting an accessibility issue. There is a particular issue here because the legend is not in the same order as the lines on the chart, which could be misleading. The chart on the right instead has each line labelled directly in accordance with best practice accessibility standards. 

{% capture expandable_content_13 %}
```
# Here we will use the data frame `df` from Example 4:
ggplot(df, aes(x = year, y = unemployed, colour = gender)) +
  geom_line(linewidth = 1.2) +
  scale_x_continuous(breaks = 2008:2024,
                     expand = expansion(mult = c(0.02, 0.2)),
                     labels = year_seq) +
  scale_y_continuous(breaks = seq(0, 12, 2),
                     expand = expansion(mult = c(0, 0.02)),
                     limits = c(0, 12)) +
  scale_fill_manual(values = af_colours(type = "categorical", n = 3)) +
  labs(subtitle = "Annual unemployment rate (%)",
       x = NULL,
       y = NULL) +
  theme_af(font_size = 20,
            legend.position = "none",
            tick_mark = "x") +
  coord_cartesian(clip = "off") +
  geom_text_repel(aes(label = gender, x=year, y = unemployed),
                  size = 6, # Font size
                  xlim = max(df_36$year) + 2,  # Limits for where on the x-axis the label can appear
                  ylim = c(4, 11), # Limits for where on the y-axis the label can appear
                  force = .1,
                  point.size = NA,
                  box.padding = 1,
                  segment.color = "#D9D9D9",
                  data = df_36 %>%
                    group_by(gender) %>%
                    filter(year == max(year)))
```
{% endcapture %}
{% include expandable-block-start.html %}
  {% include expandable-section.html number="13" content=expandable_content_14 title="R code for Example 16" %}
  {% include expandable-block-end.html %}


You should not use patterns on chart bars to distinguish different categories as these can make charts very hard to read, especially at smaller sizes. Instead, stacked and clustered bar charts can include direct labels, or you can include a legend in the same order as the categories and add a note that you have done so.

{% capture card_content_16 %}
Example 17: Number of buyers of eight car models by age, UK, 2024
<img src="assets/img/Data viz/Example 17.png" width="450px" alt="">
{% endcapture %}

{% capture card_content_17 %}
Example 18: Number of buyers of eight car models by age, UK, 2024
<img src="assets/img/Data viz/Example 18.png" width="450px" alt="">
{% endcapture %}

{% include cards-container-start.html %}
  {% include card.html content=card_content_16 title="To be avoided: using patterns to distinguish categories on a bar chart" %}
  {% include card.html content=card_content_17 title="Best practice: using a legend in the same order as the categories" %}
{% include cards-container-end.html %}


{% capture expandable_content_14 %}
```
# Load tidyverse meta-package:
library(tidyverse)
 
# Create data frame:
df <- crossing(model = LETTERS[1:8],
                age = c("0 to 24", "25 to 64", "65 to 74", "75 plus")) |>
        mutate(households = rnorm(32, mean = 5, sd = 2))
 
#
df |>
  ggplot(aes(model, households, fill = age)) +
  geom_col() +
  scale_fill_manual(values = af_colours("categorical", n = 4)) +
  scale_y_continuous(breaks = seq(0, 40, 10),
                     expand = expansion(mult = c(0, 0.02)),
                     limits = c(0, 40)) +
  labs(subtitle = "Number of households (thousands)",
       x = "Car model",
       y = NULL) +
  theme_af(font_size = 20,
            tick_mark = "x",
            legend.position = "bottom")
```
{% endcapture %}
{% include expandable-block-start.html %}
  {% include expandable-section.html number="14" content=expandable_content_14 title="R code for Example 18" %}
  {% include expandable-block-end.html %}

  