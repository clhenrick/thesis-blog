MFA DT Thesis Blog
===========
Blog running on [Jekyll](http://jekyllrb.com/) for documenting my thesis process in the Parsons MFA Design and Technology program

## Note
### Jekyll Theme
I'm using the [Pixyll Theme](http://www.pixyll.com/) by [John Otander](https://github.com/johnotander), with some additional custom tweaks :) 

### Setting Up Jekyll using Github Projects Pages
In addition to your `github-username.github.io` repo that automatically maps to the root url (http://github-username.github.io), you can serve up sites by using a `gh-pages` branch for other repos so they're available at `github-username.github.io/repo-name`.

This will require you to modify the `baseurl` option in the _config.yml file like so:

```
# Site settings
title: Repo Name
email: your_email@example.com
author: Author Name
description: "Repo description"
baseurl: "/repo-name"
url: "http://github-username.github.io"

# Build settings
markdown: kramdown
permalink: pretty
paginate: 3
```

Notice the forward slash in front of the "repo-name" and no trailing forward slash.

Then, to run Jekyll locally, in terminal do: `jekyll serve --baseurl '' --watch`