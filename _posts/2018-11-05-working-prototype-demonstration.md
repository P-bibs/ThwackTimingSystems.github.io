---
layout: post
title: Working Prototype Demonstration
date: '2018-11-05T12:37:00.000-08:00'
author: Thwack Timing Systems
tags: 
modified_time: '2018-11-05T12:37:42.601-08:00'
blogger_id: tag:blogger.com,1999:blog-7296530259499110162.post-1897253878559285543
blogger_orig_url: https://thwacktiming.blogspot.com/2018/11/working-prototype-demonstration.html
---

Here's a video that demonstrates progress on the prototype so far.
> A video used to be here demonstrating an older prototype of the Thwack Timing Gate. It has since been lost. For the most up to date demo, see the website's landing page [here](Thwacktiminggate.com)

This video shows the following features functioning properly<br /><br /><b>Basic Software - </b>Both the Arduino and Pi are running infinite loops to check for button presses and received packets, as well as writing data to files if the need arises.<br /><br /><b>Custom Communication Protocol transmitted via Xbee</b> - the start signal was transmitted from the Arduino in a custom designed packet that was then decoded by the finish line. This packet included a checksum to verify the packet's integrity<br /><br /><b>Flask Web Server </b>- the Pi is hosting a web server that successfully responds to GET requests made to it with JSON files that represent racing results so far.<br /><br /><b>App for Retrieving Results - </b>The Android phone is running a custom made app that makes http requests to the pi and then formats the results to display racer results so far.<br /><br /><br />