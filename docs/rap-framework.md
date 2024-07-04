---
title: "Reproducible Analytical Pipelines (RAP): bronze-silver-gold framework"
layout: guidance-page
page-group-title: "Reproducible Analytical Pipelines (RAP)"
page1: 
  url: rap
  name: "Introduction to RAP"
page2: 
  url: rap-framework
  name: "Bronze-silver-gold framework"
---


The purpose of this document is to outline a number of standards to work towards when developing and improving upon a Reproducible Analytical Pipeline (RAP). For an introduction on what RAP is, and what benefits it can bring, please see our other guidance: “[RAP: An introduction](rap)”.

In this document, we present bronze, silver and gold standards, offering major benchmarks to work towards, with each subsequent standard reflecting a more transparent, reproducible and robust pipeline. (Note that the standard you aim for should depend on the needs of the project - it may not always be necessary to aim for the Gold standard for every project.) These standards are largely based upon the “Minimum” and “further” standards of RAP developed by the Government Analysis Function [1]. For an explanation of how our standards differ from theirs, please see the [appendix](#). Our standards also align with those presented within the [Health RAP playbook](https://nhsengland.github.io/Health-RAP-Playbook-Alpha/). 

While we would like all analytical pipelines to eventually meet one of these standards, it is important to stress that RAP does not need to be an all or nothing exercise. Even implementing just some of the principles outlined here will bring about improvements to your processes and outputs [2][3]. Trying to achieve all of these standards in one go may be too daunting a task and so incremental improvements are the suggested way to go.

It is also important to recognise that some of principles that form these standards may not always be possible. For example, where remote connections to databases are not permitted, this cannot be automated (which is one of the principles in our bronze standard). In such cases, the aim should be to apply RAP to the other areas where principles can be applied [4]. (Note though that it is preferred to have a direct connection to databases wherever possible, as any “black-box” processes conducted in extracting and preparing data for analysis might undermine some of the benefits of RAP [5].)

For more support on how to meet these standards, including information on how to join our helpful UKHSA RAP community, please contact <UKHSA.RAP@ukhsa.gov.uk>.


### Overview

The following table gives a quick overview of the principles that form each standard. More detailed explanations are given in the sections to follow.

| The Bronze standard 🥉 | The Silver standard 🥈 | The Gold standard 🥇 |
| ------- | ------- | ------- |
| Use open source analytical software | Meet the Bronze standard | Meet the Silver standard |
| Have minimal manual steps for data extraction and analysis | Have minimal manual steps for the production of outputs | Have unit testing for functions |
| Follow good practice for quality assurance, integrating quality assurance checks throughout the pipeline | Use functions as reusable blocks of code | Have error handling for functions |
| Have well-commented code and project documentation | Adhere to a common code style | Include documentation for functions |
| Make code available to other analysts | Have automated input data validation | Use packaging |
| Use version control | - | Log data and analysis checks |
| Use peer review to ensure reproducibility (checking whether pipelines meet these standards) | - | Implement continuous integration |
| - | - | Implement dependency management |
