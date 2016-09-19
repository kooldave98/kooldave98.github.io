---
layout: post
title:  "Dates & Times"
date:   2015-08-11 19:55:37 +0100
categories: software
---
In WorkSuite5 we are increasingly using date types in our service layer; we receive dates from user entry and hidden fields, and we output dates for presentation or in a round-trip back to the service layer for processing.

This document is an attempt to articulate what we are doing generally with dates, and foster consistency in how we handle dates across geographic regions and cultures.

#### There are 3 representations of dates in our system:

1. **Date requests**: User entered date data, that will need to be validated and processed.
2. **DateTimes**: Valid date data that is sent out by the service layer in forms, for tying together workflows in the application.
3. **Presentation format dates**: Dates that have been formatted for display purposes only.

Date requests are usually built from a `DD/MM/YYYY` input field, and is culture agnostic because each field has a strong identifier. These fields allow any kind of string in them, and hence why we need to validate before processing on the service layer. We can make strong assumptions on what the `DD:day`, `MM:month` and `YYYY:year` parts are on the processing end because they are named.
