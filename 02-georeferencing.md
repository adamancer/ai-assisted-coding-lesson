---
title: 'Use Case: Georeferencing'
---

::: questions ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

- What is georeferencing?
- Why are some challenges with georeferencing?
- How can LLMs be used to address these challenges?

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::: objectives :::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

- Describe georeferencing
-

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

Georeferencing is the process of converting textual locality data to
coordinates. It is a critical workflow in long-lived natural history
collections where the majority of specimens were collected before GPS
existed. Researchers often filter by locality when searching for
specimens, and specimens without coordinates may not be used as
frequently. However, georeferencing is a time-consuming process, and
guidelines are complex. Despite the availability of several map-based
tools designed to speed up georeferencing (like GEOLocate and GeoPick),
only x% of NMNH specimen records have been georeferenced as of 2025.

Some researchers have suggested that LLMs can be used to georeference
collections at scale. Recent work has found that LLM approaches can be
as accurate as manual georeferences at a much lower cost in both money
and time.

::: callout ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

### LLMs and digitization

This workflow starts from specimens that have already been added to a
database. However, a large fraction of the NMNH collection has not been
digitized at all. LLMs are a promising tool for digitization efforts.
For example, many models are adept at reading and extracting data from
handwritten text, even cursive.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

The remainder of this lesson will use a chat-based approach to
**georeference locality strings with the goal of adding the coordinates
in the primary specimen database**. (A real-world implementation would
use an application programming interface, or API, which would allow us
to query the LLM programatically, but we've opted to use the more
familiar chat interface here.) This approach has several things to
recommend it:

1.  Georeferencing is time consuming and often tedious
2.  Recent work suggests that LLM georeferences are comparable to those
    done by people
3.  Geospatial data is relatively easy to validate to a degree where we
    can be confident that a point is at least in the right area
4.  Both the NMNH collection database and common data standards provide
    dedicated fields to annotate georeferences

But it also raises some red flags.

::: challenge ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

What are some risks associated with using an LLM for this workflow?

::: solution :::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

The primary risk is **recording/publishing inaccurate data.** Some
sources of error may include:

1.  Gross errors in coordinates resulting from confabulations or other
    similar errors. These may include fabricated coordinates and
    unreasonable uncertainty radii.
2.  Inconsistent results in response to prompts from the same locality
3.  Researchers may be hesistant to use LLM-generated data

More generally, risks might include running insecure code.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::: challenge ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

How can these risks be mitigated?

::: solution :::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

1.  Annotate georeferences so that users know that AI has been used. Be
    aware that:
    1.  Researchers accessing data in bulk may not bother to read those
        annotations
    2.  Researchers may omit AI georeferences if they are clearly
        flagged
2.  Validate the georeferences, for example, by comparing them to manual
    georeferences, checking the coordinates against administrative
    boundaries, and checking the consistency of coordinates returned by
    similar prompts.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::: keypoints ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

-

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
