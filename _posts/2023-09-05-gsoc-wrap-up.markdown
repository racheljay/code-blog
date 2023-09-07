---
layout: post
title:  "Google Summer of Code Wrap-up"
---
# Summary:
This summer I have been working on improving the test history visibility for the web-platform-test dashboard [(wpt.fyi)](https://wpt.fyi/about). The goal of this project was to improve both the UI for seeing historical test results at a glance, while also improving the way test history was being fetched from Google Datastore. The previous method for observing test history made several individual calls to the datastore, and those needed to be reduced as much as possible.

# UI Improvements:
I decided to go with Google Charts to represent the history data in a far more readable manner. The previous implementation had the history represented in a grid (much like a github contribution graph). This made the data difficult to parse visually, and it meant you had to hover over squares to get any additional information about an individual run. The timeline layout from Google Charts is a much better representation of how test behavior has changed over time. It has also made it a bit more clear which tests are exhibiting flaky behavior.


# Completed Pull Requests:
* [ frontend starter and endpoint for new test history grid #3368 ](https://github.com/web-platform-tests/wpt.fyi/pull/3368)
* [ Fix links on chart navigating to bad URLs #3410 ](https://github.com/web-platform-tests/wpt.fyi/pull/3410)
* [ Update history endpoint #3411 ](https://github.com/web-platform-tests/wpt.fyi/pull/3411)
* [ Get data from local datastore instead of from mock JSON #3434 ](https://github.com/web-platform-tests/wpt.fyi/pull/3434)
* [ change testHistoryEntry format #3440 ](https://github.com/web-platform-tests/wpt.fyi/pull/3440)
* [ update dev data and mock json to use ISO date format #3442 ](https://github.com/web-platform-tests/wpt.fyi/pull/3442)
* [ Fix chart data order #3449 ](https://github.com/web-platform-tests/wpt.fyi/pull/3449)
* [ Refresh history data when page is changed #3459 ](https://github.com/web-platform-tests/wpt.fyi/pull/3459)
* [ Add date sort to history handler #3463 ](https://github.com/web-platform-tests/wpt.fyi/pull/3463)
* [ height based on subtest name #3471 ](https://github.com/web-platform-tests/wpt.fyi/pull/3471)
* [ Add history handler tests #3485 ](https://github.com/web-platform-tests/wpt.fyi/pull/3485)