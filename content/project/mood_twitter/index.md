+++
# Project title.
title = "Analysis of Diurnal and Seasonal Mood using Twitter Data"

# Date this page was created.
date = 2017-12-01T00:00:00

# Project summary to display on homepage.
summary = "An example of using the in-built project page."

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["natural language processing"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references 
#   `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides = ""

# Links (optional).
url_pdf = ""
url_slides = "/files/Final_Report_Li_Liu_Yao.pdf"
url_video = ""
url_code = ""

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
links = [{icon_pack = "fab", icon="twitter", name="Follow", url = "https://twitter.com/georgecushen"}]

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder. 
[image]
  # Caption (optional)
  caption = "Photo by rawpixel on Unsplash"
  
  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Smart"
+++

* Collected over 60GB of twitter data of year 2016
* Used VADER Sentiment Analysis to extract positive and negative affects from tweets
* Analyzed hourly diurnal mood change by day of the week
* Analyzed the relationship between mood change and number of friends/followers and device impact
* Calculated the top PMI words for morning/night
