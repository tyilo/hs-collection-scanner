# Hearthstone Collection Scanner

This tool can be used to get a list of the cards in your Hearthstone collection.
These can then be exported to easy update your collection on [HearthPwn](https://hearthpwn.com/).

This tool doesn't rely on being able to read memory from the Hearthstone process, but instead uses image recognition to figure out which cards you own. So before the cards can be recognized, you need to have a screenshot of each page of your collection.

Currently the tool doesn't detect golden cards and assumes that you don't own more than 2 copies of any card.


Installation
============

Python 3 and `pipenv` is required to run the scripts and install the additional dependencies.

To install the additional dependencies run:

```
pipenv install
```

The script needs to get a list of the current collectible cards and images of them.
To do so you need to get an API key from [here](https://market.mashape.com/omgvamp/hearthstone) and then create a file called `.env`, with the following contents:

```
HS_API_KEY = '<Your API key here>'
```


Taking screenshots of your collection
=====================================

To be able to find out what cards you own, the script needs a screenshot of each page of your collection. You need to place these in the `screenshots` directory.

When taking screenshots of your collection it is important, that the filenames of the screenshots are lexicographically ordered, so that the first page of your collection is in the screenshot with the first filename.

A helper tool `screengrabber` is provided to help with this on Linux.

Screengrabber tool
------------------

To use the screengrabber tool you need to have `imagemagick` and `xorg-xinput` installed.

To use it you need to first open Hearthstone and navigate to the first page of your collection.

Then you should run the tool using:
```
pipenv run ./screengrabber
```

and while it is running you should click through each page of your collection. When you reach the end, stop the tool by pressing ctrl+C.

You should now have a screenshot of each of your pages in the `screenshots` directory.


Recognizing cards from the screenshots
======================================

After taking the screenshots, running:
```
pipenv run ./card_detector
```

should list all the cards in your collection and copy some javacript code. If you paste this code in your browser console on the HearthPwn collection editor site, it will update your collection.

Note that this will probably take a long time to finish.


TODO
====

- Support golden cards
- Improve speed
- Improve screengrabber
