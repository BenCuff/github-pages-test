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

The `assets` folder is used to store .css stylesheets. 

The `_config.yml` file can be used to store sitewide values. These are then inserted to other pages via Liquid commands (for example, `{{ site.email }}`). 

## Common markdown commands
Most of what goes into the .md files will be standard markdown. Some other code can be used as follows.

### Block quotes
```
<div class="block-quote">
  <p>This is a block quote or highlight section</p>
</div>
```

### Expandable sections
```
<button id="expanded-header-1" aria-controls="expanded-content-1" aria-expanded="false" class="expandable-header">
  An example of a collapsible section
</button>

<div id="expanded-content-1" class="expandable-contents" aria-hidden="true">
  <p>
    Hello!
  </p>
</div>
```

You will need to edit the following elements: 
1. The button id.
2. The button aria-controls attribute - ensure this is unique in the page and matches the id of the expandable contents.
3. The button text.
4. The expandable contents id - ensure this is unique in the page and matches the button aria-controls attribute.
5. The explandable contents text, contained within the `<p> </p>` tags.

### Code blocks
```
<div class="code-block">
  <p>#This is a block of code</p>
  <p>var <- filter(hello, x==1)</p>
  <p>print(var)</p>
</div>
```

Note that each row of the code should be contained within `<p> </p>` tags.
