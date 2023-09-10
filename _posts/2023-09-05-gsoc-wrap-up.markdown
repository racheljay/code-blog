---
layout: post
title:  "Google Summer of Code Wrap-up"
---
Contributor: [Rachel Russell](https://github.com/racheljay)

Mentors: [Kyle Ju](https://github.com/KyleJu), [Daniel Smith](https://github.com/DanielRyanSmith)
## Summary:
This summer I have been working on improving the test history visibility for the web-platform-test dashboard [(wpt.fyi)](https://wpt.fyi/about). The goal of this project was to improve both the UI for seeing historical test results at a glance, while also improving the way test history was being fetched from Google Datastore. The previous method for observing test history made several individual calls to the datastore, and those needed to be reduced as much as possible.

### Viewing the new timeline:

In order to generate a timeline for an individual test, navigate to a specific test on [staging.wpt.fyi](https://staging.wpt.fyi/results). Below the chart displaying the most recent test results, click on the blue "Show New History" button. _(If there is no "Show New History" button or if there is only one button which shows the previous implementation, the feature flag for the new timeline may need to be enabled at [staging.wpt.fyi/flags](https://staging.wpt.fyi/flags))_
![img]({{ site.baseurl }}/assets/images/result-table.png)

Each browser will have it's own timeline representing past test behavior:

![img]({{ site.baseurl }}/assets/images/chrome-timeline.png)

## UI Improvements:
I decided to go with Google Charts to represent the history data in a far more readable manner. The previous implementation had the history represented in a grid (much like a github contribution graph).

### Previous Grid Implementation:
The previous test history grid is a bit difficult to parse visually, and you have to hover over the individual squares to get additional information about each run.
![img]({{ site.baseurl }}/assets/images/old-grid.png)
### New Timeline Implementation:
The timeline layout from Google Charts is a much better representation of how test behavior has changed over time. It is also more clear which tests are exhibiting flaky behavior.
![img]({{ site.baseurl }}/assets/images/flaky.png)

## Back End Implementation:
In order to reduce the amount of api calls, I worked with my mentors to create a script that would populate Google Datastore with all of the essential information needed to accurately show historical test behavior. Previously all of this information was stored individually for each sub test in a separate blob store. In order to access this data, they all had to be queried at once, which was a very expensive operation. In this new implementation, the data is being accessed from a new endpoint. This endpoint queries Datastore with a test ID, and gets all of the information for that test's history in one call.

## Overall Takeaways:
This was a great learning experience, especially as this project included both front end and back end elements.

On the front end, I had to gain experience with the Polymer library. Since Polymer is a depreciated library, the documentation was occasionally unhelpful and lacking in detail. This created a bit of a challenge. I had to rely a lot on examples from other areas of the code base as well as trial and error. It was great getting out of my comfort zone and trying a different front end library. Most of my previous front end work has been in React, so it was interesting to see the different ways the two libraries tackle similar issues, such as passing along properties and blending JavaScript with HTML.

I also had a great experience working with Go in the back end. I had _some_ previous experience with Go, but most of my experience has been in the front end. I had a lot of fun learning the ends and outs of querying Datastore, processing the necessary data, and making that data available on a new endpoint to populate the history charts. It was also a good learning experience to include a unit test to make sure that my logic was preforming exactly the way I intended it to.

<hr>

## Completed Pull Requests:
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

## Current Works In Progress:
* [ Correct subtest order #3496 ](https://github.com/web-platform-tests/wpt.fyi/pull/3496)

## Work To Be Completed:
* [ Add test history documentation #3488 ](https://github.com/web-platform-tests/wpt.fyi/issues/3488)
* [ Cleanup after new history timeline is complete #3451 ](https://github.com/web-platform-tests/wpt.fyi/issues/3451)
* [ Viewing test history timelines a second time displays with incorrect width #3487 ](https://github.com/web-platform-tests/wpt.fyi/issues/3487)
* [ Tests with entirely missing data will not refresh the previous timeline view #3486 ](https://github.com/web-platform-tests/wpt.fyi/issues/3486)