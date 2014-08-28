<<<<<<< HEAD
# Pixyll

[pixyll.com](http://www.pixyll.com)

![Pixyll screenshot](https://cloud.githubusercontent.com/assets/1424573/3847467/134aa236-1e66-11e4-8421-4e8c122118dc.png)

Pixyll is a simple, beautiful theme for Jekyll that emphasizes content rather than aesthetic fluff. It's mobile _first_, fluidly responsive, and delightfully lightweight.

It's pretty minimal, but leverages large type and drastic contrast to make a statement, on all devices.

This Jekyll theme was crafted with <3 by [John Otander](http://johnotander.com)
([@4lpine](https://twitter.com/4lpine)).

## Getting Started

If you're completely new to Jekyll, I recommend checking out the documentation at <http://jekyllrb.com> or there's a tutorial by [Smashing Magazine](http://www.smashingmagazine.com/2014/08/01/build-blog-jekyll-github-pages/).

### Installing Jekyll

If you don't have Jekyll already installed, you will need to go ahead and do that.

```
$ gem install jekyll
```

### Fork, then clone

Fork the repo, and then clone it so you've got the code locally.

### Modify the _config.yml

The `_config.yml` located in the root of the Pixyll directory contains all of the configuration details
for the Jekyll site. The defaults are:

```yml
# Site settings
title: Pixyll
email: your_email@example.com
author: John Otander
description: "A simple, beautiful theme for Jekyll that emphasizes content rather than aesthetic fluff."
baseurl: ""
url: "http://pixyll.com"

# Build settings
markdown: kramdown
permalink: pretty
paginate: 3
```

### Jekyll Serve

Then, start the Jekyll Server. I always like to give the `--watch` option so it updates the generated HTML when I make changes.

```
$ jekyll serve --watch
```

Now you can navigate to `localhost:4000` in your browser to see the site.

### Using Github Pages

You can host your Jekyll site for free with Github Pages. [Click here](https://pages.github.com/) for more information.

### Contact Form

If you'd like to keep the contact form, which uses <http://forms.brace.io/>, you will need to update the email address.

Currently, the `contact.md` has the following:

```html
<form action="https://forms.brace.io/johnotander@icloud.com" method="POST" class="form-stacked form-light">
```

Where it says `johnotander@icloud.com`, you will need to change that to the email that you wish to have the form data sent to. It will require you to fill the form out when you push it live for the first time so that you can confirm your email.

### Put in a Pixyll Plug

If you want to give credit to the Pixyll theme with a link to <http://pixyll.com> or my personal website <http://johnotander.com> somewhere, that'd be awesome. No worries if you don't.

### Enjoy

I hope you enjoy using Pixyll. If you encounter any issues, please feel free to let me know by creating an [issue](https://github.com/johnotander/pixyll/issues). I'd love to help.

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## Thanks to the following:

* [BASSCSS](http://basscss.com)
* [Jekyll](http://jekyllrb.com)
* [Refills](http://refills.bourbon.io/)
* [Solarized](http://ethanschoonover.com/solarized)
=======
thesis-blog
===========

Blog running on Jekyll for documenting my thesis process in the Parsons MFA Design and Technology program
>>>>>>> f799dd6ed6519f40e1cdd755d00de0e292a0c033
