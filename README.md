## Cloning and interacting with this repository

In a new folder, using GitBash (or equivalent), run the following code:
```
git clone https://github.com/BenCuff/github-pages-test
```

Open the .Rproj file to interact with the contents. You should not need to set any remotes for push/pull operations.

Note that for now, pushing to the main branch is allowed. Before we go live, this branch will be protected, meaning you will need to create a new branch and merge into main via a pull request. 

Remember to run `git pull` regularly to keep up to date with the main branch. 


### Pushing commits to GitHub

Once you have made changes, use `git status` to check what you are about to commit. 

Then use `git add .` to stage files for the commit. 

Then use `git commit -m "your commit message"` to commit the change, inserting an appropriately descriptive commit message. 

Then use `git push` to push the change to GitHub. In the actions tab, you will see an action running to deploy to [the live page](https://bencuff.github.io/github-pages-test/).


## Folder and file structure
The root folder can be used to store any non-website content. 

Anything contained within `docs` is used to render the live site. 

Individual pages should be contained within the `docs` folder (not in sub-folders), and in .md format. 

The `_includes` folder is used to store .html/.js snippets to be inserted into other files via Liquid commands (for example, `{% include site-nav.html %}`).

The `_layouts` folder is used to store larger template files. 

The `assets` folder is used to store .css stylesheets and images. 

The `_config.yml` file can be used to store sitewide values. These are then inserted to other pages via Liquid commands (for example, `{{ site.email }}`). 

## Common markdown commands
Most of what goes into the .md files will be standard markdown. Some other code can be used as follows.

### Block quotes

Add an arrow (">") to the start of each line. You can use other markdown tags (headers, bullets) within this. 

```
> ## Main messages
>
> - Message 1
> - Message 2
> - Message 3
```

### Expandable sections

First include the hidden content within a 'capture' block like below. 

Make sure to add a unique number to the end of each block title. 

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


### Code blocks
````
```
Code block
line 2
line 3
```
````


### Images

To add images to a page, first add the file to the `docs/assets/img/` folder.

Then link using the following code, adding the correct filepath and alt-text:

`<img src="assets/img/laptophands.jpg" alt="A picture of a person working at a laptop">`