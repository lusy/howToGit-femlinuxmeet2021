# howToGit-femlinuxmeet2021

This repository contains the slides for a hands-on git crash course (in German) given at the [Feminist Linux Meetup](https://feminist-linux.diebin.at/) in June 2021.

## to view the presentation

* checkout this repo
* checkout [revealjs](https://github.com/hakimel/reveal.js) in the same directory under the name `reveal.js`
* open the `slides.html` file in your browser

## to build the slides

* checkout this repo
* checkout [revealjs](https://github.com/hakimel/reveal.js) in the same directory under the name `reveal.js`
* edit the source of the slides: the `slides.md` file

* install [pandoc](https://github.com/jgm/pandoc/releases/)

### html slides

use `pandoc -s --mathjax -i -t revealjs slides.md -o slides.html` to convert the slides to a html presentation

### latex slides

use `pandoc -t beamer slides.md -o slides.pdf` to convert the slides to a latex beamer presentation


## license

This presentation is licensed under the Creative Commons Attribution-ShareAlike 4.0 (CC BY-SA 4.0) License. For more detailed information, visit [https://creativecommons.org/licenses/by-sa/4.0/](https://creativecommons.org/licenses/by-sa/4.0/)

