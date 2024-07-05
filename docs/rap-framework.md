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

<style>
  td, th{
    width: 30%;
  }
  
  td:first-child{
    background-color:unset;
  }
</style>



This page outlines a number of standards to work towards when developing and improving upon a Reproducible Analytical Pipeline (RAP). For an introduction on what RAP is, and what benefits it can bring, please see the [introduction to RAP page](rap)”.

In our framework, we present bronze, silver and gold standards, offering major benchmarks to work towards, with each subsequent standard reflecting a more transparent, reproducible and robust pipeline. You do not need to aim for gold for every project; instead, the standard you should aim for depends on the needs of the project. 

These standards are largely based upon the “Minimum” and “further” standards of RAP developed by the Government Analysis Function [1]. For an explanation of how our standards differ from theirs, please see the [appendix](#Appendix). Our standards also align with those presented within the [Health RAP playbook](https://nhsengland.github.io/Health-RAP-Playbook-Alpha/). 

While we would like all analytical pipelines to eventually meet one of these standards, it is important to stress that RAP does not need to be an all or nothing exercise. Even implementing just some of the principles outlined here will bring about improvements to your processes and outputs [2][3]. Trying to achieve all of these standards in one go may be too daunting a task and so incremental improvements are the suggested way to go.

It is also important to recognise that some of principles that form these standards may not always be possible. For example, where remote connections to databases are not permitted, this cannot be automated (which is one of the principles in our bronze standard). In such cases, the aim should be to apply RAP to the other areas where principles can be applied [4]. (Note though that it is preferred to have a direct connection to databases wherever possible, as any “black-box” processes conducted in extracting and preparing data for analysis might undermine some of the benefits of RAP [5].)

For more support on how to meet these standards, including information on how to join our helpful UKHSA RAP community, please contact <UKHSA.RAP@ukhsa.gov.uk>.


## Overview

The following table gives a quick overview of the principles that form each standard. More detailed explanations are given in the sections to follow.

| The Bronze standard 🥉 | The Silver standard 🥈 | The Gold standard 🥇 |
|:------- |:------- |:------- |
| Use open source analytical software | Meet the Bronze standard | Meet the Silver standard |
| Have minimal manual steps for data extraction and analysis | Have minimal manual steps for the production of outputs | Have unit testing for functions |
| Follow good practice for quality assurance, integrating quality assurance checks throughout the pipeline | Use functions as reusable blocks of code | Have error handling for functions |
| Have well-commented code and project documentation | Adhere to a common code style | Include documentation for functions |
| Make code available to other analysts | Have automated input data validation | Use packaging |
| Use version control | - | Log data and analysis checks |
| Use peer review to ensure reproducibility (checking whether pipelines meet these standards) | - | Implement continuous integration |
| - | - | Implement dependency management |



## The Bronze standard 🥉

To meet the bronze standard for RAP, your project should :

- use open source analytical software (preferably R or Python)
- have minimal manual steps (for example, minimal copy-paste, point-click, drag-drop operations) for data extraction where permissions allow (for example, using SQL code), and for the analysis steps used to produce numbers, tables and charts
- follow good practice in quality assurance, integrate quality assurance checks throughout the analysis, automated where appropriate, supplemented with semi-automated and manual checks (see our other guidance on quality assurance)
- have well-commented code and documentation embedded as part of the project, rather than being saved elsewhere
- be open and available to other analysts (including external users where appropriate) on a shared drive or on GitHub or GitLab, rather than a personal storage area 
- use version control software such as Git and GitHub to create and maintain a recorded history of the project, and version control your input data
- use peer review to ensure that the analysis is accurate and reproducible, and that the pipeline meets the rest of this standard



{% capture bronze_1 %}
Modern tools such as R or Python are preferred over tools such as SPSS, Stata or SAS because they are better at reading a range of different data formats, support modularised code, and can be used to automate the creation of outputs in a range of different formats (for example, markdown, HTML, Word, Excel and PowerPoint files - this will become important for meeting the silver standard principles later on) [7]. 

They also reduce (or eliminate) the number of times where data needs to be moved from one programme into another (for example, from SPSS into Excel into Word) [8]. Open source, such as R and Python, is also better for transparency compared to other proprietary software where licenses are required to run the code. Those licenses can also be expensive, whereas there are no costs involved for most applications of R and Python. All of this is also in line with the [Technology Code of Practice](https://www.gov.uk/guidance/the-technology-code-of-practice#be-open-and-use-open-source).

See this handy guide: [R for applied epidemiology and public health](https://epirhandbook.com/en/index.html). 

{% endcapture %}


{% capture bronze_2 %}
Minimising the number of manual steps through automation helps reduce the risk of human error and improves efficiency.

Data extraction and analysis should be automated as much as possible, recognising that some manual steps may be required in some situations (e.g., where direct connections to databases are not possible). 

Automation should ideally be done in R or Python (see the "use open source analytical software" principle). Various other principles in the framework help with how to write good code (for example, including good documentation, using functions, applying good code style).

While automation is encouraged, this does not mean the entire pipeline needs to be run in one single step. For example, trying to pull and shape data and produce outputs in the same line(s) of code might make it difficult to debug errors, and for other analysts to follow what you are doing or reuse parts of your code for similar projects [6]. Your project should instead be separated out into several stages, for example using separate scripts for each main stage of the pipeline. 

{% endcapture %}


{% capture bronze_3 %}
Simply being reproducible does not mean that you are doing your analysis correctly [9]. It is important to quality assure each stage of the process, not just the end product (though this also remains important!). Quality assurance should align with the principles outlined in the Aqua Book [10] and the Code of Practice for Statistics [11] for those who have adopted the code.

Please refer to [our more detailed guidance on quality assurance](quality-assurance) for more information.

Checks should be built in at various points throughout the code to flag anything unexpected for further (human) exploration. These might print warning messages into the console for example, or output more detailed markdown files flagging where potential issues might exist. Note that while many quality assurance checks can be automated, some human input will always be needed, such as for final proof readings and checking that automated text still matches the figures [6]. 

Broader, more manual checks should also take place, such as checking that the analysis and outputs meet user needs and checking that any assumptions about the model or method are likely to be true - you can find examples in our [QA log template](quality-assurance). Code reviews are also advised. 

To formalise your quality assurance processes and to keep an audit trail, it is a good idea to have defined roles (particularly the "assurer" and "analyst" roles), and keep detailed QA logs. Both of these are described within our [guidance on quality assurance](quality-assurance).

{% endcapture %}


{% capture bronze_4 %}
Having good quality documentation accompanying your code is important for reproducibility. The simplest form of documentation is code comments. These can be supplemented with additional documentation such as a “README” file [5][7]. Standard Operating Procedures (SOPs), QA logs, assumptions logs are other good methods of documentation. 

Good documentation will help improve the reuse of code, either by other analysts using it for the first time or by the same analyst using it in the future [5]. It should explain what the code does and how it can be used, including what options or parameters are available, examples of how to run it, and an explanation of any software or environment dependencies [9]. It should be embedded as part of the project, rather than being saved elsewhere, so that it can be easily found [1]. 

{% endcapture %}


{% capture bronze_5 %}
It is a good idea to make code available to others because this means that the pipeline can be reproduced should the usual analyst go on annual or sick leave, or leave the organisation. It should be stored in a place that is accessible to others (not on a local drive). Keeping code in a repository such as GitHub can also make it easier to find and provides a back up in case of accidental deletion [9] (excluding anything sensitive such as datasets and database connection details). 

Ideally, the code should be made publicly available for transparency, but this may not always be appropriate [8]. Please adhere to any organisational policy on this.

{% endcapture %}


{% capture bronze_6 %}
Version control is important for documenting what changes have been made when, why, and by whom, as well as helping to ensure that people running your code know that they are using the right version [3][7][8][9][12]. It can act as a safety net, allowing you to roll back to earlier versions of code in the event of an issue, or to review how an earlier report was produced [5][9].

GitHub (or GitLab) can be used as a central repository to store your code and version history, allowing it to be easily accessed by others. Sharing code via GitHub can also help avoid duplication of work when other analysts are looking to perform similar tasks [1]. GitHub also allows analysts to be open about areas they have identified for improvement via an issues log, also inviting ideas from others [3]. Private repositories can be used for internal use only, or public repositories can be used to make your code more openly available. Please adhere to our organisational policy on open repositories (which is currently being developed).

It is important not to commit anything sensitive to version control repositories, such as datasets, secret keys and credentials. Datasets should be excluded to avoid disclosing any personal information. It is recommended that keys and credentials should be saved in a separate file that can still be used within the project, but which is excluded from the repository. Pre-commit hooks, such as those provided by the UKHSA 'cookiecutter' tool (see more information Confluence and available on GitHub; an alternative is the cross-government “govcookiecutter” tool), or “.gitignore” exclusions can help mitigate this risk. Remember that even when sensitive information is included deep within the version history, these can be checked out and viewed [12].

While datasets are usually not committed to repositories, it is still important to ensure that some form of version control is applied to the source data, so that others know what version of the data was used for the analysis [7]. If your project relies on snapshot CSV files, rather than connecting to a database directly, it is good idea to store those files in a read-only folder, to prevent them being modified or deleted - any changes like this could make it difficult to reproduce the same outputs in the future [7][9][12]. For these files, it is important to ensure that they are saved prior to any data cleaning taking place, so that that data cleaning process can be documented within the production pipeline [12].

Even where direct connections to databases are made, it may be a good idea to save a copy of a tidy dataset (the minimum dataset needed to produce an output, rather than the full underlying dataset [8][2]) at some point in the pipeline to keep a record of the data used, and so that it can also be reused in other projects [2]. Please adhere to proper information governance procedures when doing this, however, avoiding saving copies of anything that might be considered sensitive.

{% endcapture %}


{% capture bronze_7 %}
The purpose of the peer review here is to ensure that the analysis is fully reproducible and that it does indeed appropriately meet the principles outlined in the framework above.

It can, for example, involve a peer testing whether they can successfully run your code, checking that documentation is clear and complete, and checking that version control has been appropriately implemented. 

A peer review can also provide a useful opportunity to more thoroughly question your pipeline, and may help identify areas for improvement that have otherwise not been identified previously. This is likely best done by someone not already very familiar with the existing pipeline. 

The peer review should not just focus on the bronze standard but should also review silver and gold standard principles where they are applied. Having this principle in the bronze standard is just about ensuring that a peer review process is in place. 

{% endcapture %}


{% include expandable-block-start.html %}
  {% include expandable-section.html number="1" content=bronze_1 title="Use open source analytical software" %}
  {% include expandable-section.html number="2"  content=bronze_2 title="Have minimal manual steps for data extraction and analysis" %}
  {% include expandable-section.html number="3"  content=bronze_3 title="Follow good practice for quality assurance, integrating quality assurance checks throughout the pipeline" %}
  {% include expandable-section.html number="4"  content=bronze_4 title="Have well-commented code and project documentation" %}
  {% include expandable-section.html number="5"  content=bronze_5 title="Make code available to other analysts" %}
  {% include expandable-section.html number="6"  content=bronze_6 title="Use version control" %}
  {% include expandable-section.html number="7"  content=bronze_7 title="Use peer review to ensure reproducibility (checking whether pipelines meet these standards)" %}
{% include expandable-block-end.html %}



## The Silver standard 🥈

To meet the silver standard for RAP, your project should:

- achieve all of the principles included in the bronze standard
- have minimal manual steps (for example, minimal copy-paste, point-click, drag-drop operations) for the production of spreadsheet workbooks and reports for publication
- use functions as reusable blocks of code
- adhere to a common best practice code style
- have automated input data validation


{% capture silver_1 %}
Automating the production of outputs, such as reports, spreadsheets or dashboards, further reduces the risk of human error.

Note that this does not mean your outputs should necessarily be entirely automated. In some cases, this might be appropriate; in other cases, manual input may be needed for providing narrative in a report, for example. 

There are packages available to help produce reports automatically, such as [RMarkdown](https://rmarkdown.rstudio.com/), [Python-Markdown](https://pypi.org/project/Markdown/) and [Quarto](https://quarto.org/).

Spreadsheet workbooks can similarly be produced using the [a11ytables package for R](https://github.com/co-analysis/a11ytables) or [gptables for Python](https://github.com/best-practice-and-impact/gptables), for example.

Producing outputs in these ways means that you know all elements of the output are in sync, as everything is produced from that single pipeline [8]. With more manual approaches, forgetting to update the charts, for example, will mean that they are no longer in sync with what is presented in the text. A good test for how automated your pipeline is might be to think whether or not your outputs are deletable without worry. If you would not want to delete your outputs, because it would take time and energy to re-make them, then your end-to-end pipeline is not fully automated [12].
{% endcapture %}


{% capture silver_2 %}
Functions are particularly useful when you are repeating the same operations at multiple points in your code. Rather than writing out the same code each time you need to carry out an operation, you can create a function and call that each time instead.

This lessens the risk of error because if you need to change that operation, you only need to change the function definition, not each place in the code where it is run (some of which may otherwise be missed, causing inconsistencies). Functions also lend themselves nicely to sharing snippets of functional code with others [5].
{% endcapture %}


{% capture silver_3 %}
Working to a common code style makes it easier for other analysts to pick up your code as they will be able to interpret and understand it more quickly. For R users, the [tidyverse style guide](https://style.tidyverse.org/) is the most commonly used style in the global community. "[PEP 8](https://peps.python.org/pep-0008/)" is an alternative for Python users. 

You should also consult the [Duck Book](https://best-practice-and-impact.github.io/qa-of-code-guidance/intro.html) [12] for guidance on coding standards (which also includes some [handy checklists for quality assuring your code](https://best-practice-and-impact.github.io/qa-of-code-guidance/checklists.html)). 
{% endcapture %}


{% capture silver_4 %}
Validating your input data is important as the quality of your outputs will necessarily depend on the quality of the inputs. Remember: “[garbage in, garbage out](https://dictionary.apa.org/garbage-in-garbage-out)”.

This principle is intended to build upon the bronze standard quality assurance principle, introducing a more thorough interrogation of your input data. 

Validating inputs in an automated way at the very start of the pipeline allows you to quickly identify and address any quality issues early. You might produce code to check, for example, for missing data, incorrect data types, extreme or outlier values, and whether there have been any unexpectedly large changes in the latest iteration of a longitudinal dataset. Other sense checks can also be performed, depending on the nature of the project. You could have your code produce a markdown document which flags any rows that may warrant further exploration - this may be particularly useful for any reports which are run on a regular basis.
{% endcapture %}


{% include expandable-block-start.html %}
  {% include expandable-section.html number="8" content=silver_1 title="Have minimal manual steps for the production of outputs" %}
  {% include expandable-section.html number="9"  content=silver_2 title="Use functions as reusable blocks of code" %}
  {% include expandable-section.html number="10"  content=silver_3 title="Adhere to a common code style" %}
  {% include expandable-section.html number="11"  content=silver_4 title="Have automated input data validation" %}
{% include expandable-block-end.html %}