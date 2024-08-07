## Contributing instructions

We welcome contributions to our guidance or other resources. If you would like to suggest a change, please either [raise an issue](https://github.com/BenCuff/github-pages-test/issues), [email us](mailto:ukhsa_hopstats@ukhsa.gov.uk) or raise a pull request. 

The sections below describe the setup of this repository and how to reproduce some of the markdown features used within the guidance pages. 


### Cloning and interacting with this repository

In a new folder, using GitBash (or equivalent), run the following code:
```
git clone https://github.com/BenCuff/github-pages-test
```

Open the .Rproj file to interact with the contents. You should not need to set any remotes for push/pull operations.

Note that for now, pushing to the main branch is allowed. Before we go live, this branch will be protected, meaning you will need to create a new branch and merge into main via a pull request. 

Remember to run `git pull` regularly to keep up to date with the main branch. 


#### Pushing commits to GitHub

Once you have made changes, use `git status` to check what you are about to commit. 

Then use `git add .` to stage files for the commit. 

Then use `git commit -m "your commit message"` to commit the change, inserting an appropriately descriptive commit message. 

Then use `git push` to push the change to GitHub. In the actions tab, you will see an action running to deploy to [the live page](https://bencuff.github.io/github-pages-test/).

## Building websites with Jekyll and GitHub

[See a useful resource for working with Jekyll in GitHub here](https://carpentries-incubator.github.io/jekyll-pages-novice/). 

### Folder and file structure
The root folder can be used to store any non-website content. 

Anything contained within `docs` is used to render the live site. 

Individual pages should be contained within the `docs` folder (not in sub-folders), and in .md format. 

The `_includes` folder is used to store .html/.js snippets to be inserted into other files via Liquid commands (for example, `{% include site-nav.html %}`).

The `_layouts` folder is used to store larger template files. 

The `assets` folder is used to store .css stylesheets and images. 

The `_config.yml` file can be used to store sitewide values. These are then inserted to other pages via Liquid commands (for example, `{{ site.email }}`). 

### Creating direct download links for files
Direct download links are used for files such as the QA review conversation tool. 

To get a link:
1. Navigate to the file in the assets/downloads folder in GitHub (click on the actual file).
2. Right-click "Raw", and "Copy link address".
3. Paste that URL into your markdown file, formatting as with any other link. 

### Markdown commands used in this site
Most of what goes into the .md files will be standard markdown. Some other code is custom built for this site, relying on scripts found within the `_includes` folder.

The features used within this site can be replicated as follows.

#### Block quotes

Add an arrow (">") to the start of each line. You can use other markdown tags (headers, bullets) within this. 

```
> ## Main messages
>
> - Message 1
> - Message 2
> - Message 3
```

#### Expandable sections

First include the hidden content within a 'capture' block like below. 

Make sure to add a unique number to the end of each block title. Numbers should be unique across all expandable blocks in the whole document. 

```
{% capture expandable_content_1 %}
Content goes here, written in normal markdown.
{% endcapture %}

{% capture expandable_content_2 %}
This is a second expandable section.
{% endcapture %}
```

Then you can use the following code to include expandable sections with the appropriate titles. 

The 'block-start' and 'block-end' lines are needed for styling. 

The parameter given in 'content' should match the title of the relevant capture block declared above. 

Be careful to use a unique number in each line (numbers should also be unique within the entire markdown file). The title will display within the button used to expand the section. 

```
{% include expandable-block-start.html %}
  {% include expandable-section.html number="1" content=expandable_content_1 title="This is the first title" %}
  {% include expandable-section.html number="2"  content=expandable_content_2 title="This is the second title" %}
{% include expandable-block-end.html %}

```


#### Code blocks
````
```
Code block
line 2
line 3
```
````


#### Images

To add images to a page, first add the file to the `docs/assets/img/` folder.

Then link using the following code, adding the correct filepath and alt-text:

`<img src="assets/img/laptophands.jpg" alt="A picture of a person working at a laptop">`


##### Image and text side-by-side
If you want to have an image next to some text, you can do that using the code below. 

Note that you should specify the image width and height. 


```
<div class="image-text-container">
    <img src="assets/img/image.png" width="460px" height="318px" alt="provide some alternative text here">
    <p>The text goes here</p>
</div>
```

#### Title+content cards (like the ones found in the QA guidance)

First include the card content within a 'capture' block like below. 

Make sure to add a unique number to the end of each block title. Numbers should be unique across all cards in the whole document. 

```
{% capture card_content_1 %}
Content goes here, written in normal markdown.
{% endcapture %}

{% capture card_content_2 %}
This is content for a second card.
{% endcapture %}
```

Then you can use the following code to include cards with the appropriate titles. 

The 'container-start' and 'container-end' lines are needed for styling. 

The parameter given in 'content' should match the title of the relevant capture block declared above. 

```
{% include cards-container-start.html %}
  {% include card.html content=card_content_1 title="This is the first title" %}
  {% include card.html content=card_content_2 title="This is the second title" %}
{% include cards-container-end.html %}

```
