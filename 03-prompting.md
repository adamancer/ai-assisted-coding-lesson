---
title: Prompting
---

::: questions ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

-

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::: objectives :::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

-

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

A prompt is a series of instructions submitted to an LLM to generate a
response. Prompt engineering is the creation of nature-language prompts
that coax the desired output from an LLM. The most familiar way to
submit a prompt to an LLM is via a chat interface, which proceed as
conversations.

::: callout ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

We will be working from the Etherpad and an LLM chat for this part of
the lesson.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

Consider the locality string **Springfield Township, NJ**.

Prompt the LLM to georeference this locality as follows:

<pre style="white-space: pre-wrap; border-left: 10px solid gray; margin-left: 42px;">
Please provide coordinates for Springfield Township, NJ
</pre>

Copy the response into the Etherpad for this lesson.

::: challenge ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

Read over the responses in the Etherpad. What do you notice about them?

::: solution :::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

Here are some common attributes of responses:

- Multiple localities match this string. Most responses will probably
  include two localities, but some may have three or even a different
  number.
- By default, the response is given as text, which makes it challenging
  to extract coordinates.
- Different responses may contain different coordinates.

Are there any outlier responses?

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

The initial response is promising but difficult to evaluate
quantitatively. We can update the prompt to produce output that is
easier for a script to parse.

<pre style="white-space: pre-wrap; border-left: 10px solid gray; margin-left: 42px;">
Please provide coordinates for Springfield Township, NJ. Include all localities matching this locality string. Output coordinates as JSON including the following keys for each match: country, stateProvince, county, decimalLatitude, decimalLongitude, geodeticDatum, coordinateUncertaintyInMeters, georeferenceRemarks, and sourceURL. The response should only include the JSON.
</pre>

::: callout ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

### Darwin Core

The field names used in this prompt are mostly from [Darwin
Core](https://dwc.tdwg.org/), a widely used natural history data
standard. NMNH uses Darwin Core to share its data with aggregators like
the [Global Biodiversity Information Facility (GBIF)](https://gbif.org).

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

We can also supply structured data:

<pre style="white-space: pre-wrap; border-left: 10px solid gray; margin-left: 42px;">
Please provide coordinates for the following locality:

stateProvince: NJ
municipality: Springfield Township
locality: 100 m SW of Hobart Ave and Beacon Rd

Include all localities matching this locality string. Output coordinates as JSON including the following keys for each match: country, stateProvince, county, decimalLatitude, decimalLongitude, geodeticDatum, coordinateUncertaintyInMeters, georeferenceRemarks, and sourceURL. The response should only include the JSON object.
</pre>

Create a file called `coords.json`. Open it with VS code or another text
editor. Copy the JSON from the last response into the file and save.
Please also copy the JSON to the Etherpad.

::: keypoints ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

-

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
