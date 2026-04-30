---
title: Assisted Coding
---

::: questions ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

-

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::: objectives :::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

- Understand the difference between traditional coding, assisted coding,
  and vibe coding
- Use an LLM to create a Python script to map coordinates to counties
- Introduce the geopandas package and geospatial concepts
- Read through generated code to understand how it works

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

This lesson will use LLM-assisted coding to create a Python script that
we can use to assess the coordinates in the `coords.json` file.

## Coding styles

- **Traditional coding:** Low trust. Coder writes out their code
  manually, referring to documentation or forums if they get stuck.
- **Assisted coding:** Medium trust. Coder consults with an LLM to write
  blocks of code that the coder than reviews and integrates into the
  larger application. They can ask the LLM follow-up questions to better
  understand the code and test blocks as they go to ensure that code is
  working correctly.
- **Vibe coding:** High trust, resource intensive. Coder relies on the
  LLM to write most/all of their code, even an entire application. They
  review out and provide the LLM additional prompts to modify
  functionality but mostly do not touch the code itself.

Using LLMs shifts the focus of the coder from **writing code** to
**reading and testing code**. They can be very useful for understanding
what code is doing, but be careful--some studies suggest that
over-reliance on LLMs may reduce persistence and independent
performance. Working through problems is critical to learning how to
write and read code.

**Code generated using assisted methods must be vetted before being
run.** Risks of running unvalidated code include:

- **Accidental deletion of files.** Functions like `os.unlink()` or
  `shtuil.rmtree()` can delete files or entire directories. Opening a
  file in write mode will delete its contents.
- **Cybersquatting attacks.** Generated code may include hallucinated
  package names, which can be used by adversarial actors to install
  malacious software in an attack known as slopsquatting.

Earlier in the lesson, we considered some ways we might vet coordinates
returned by an LLM. Possibilities included:

- Using a map to check each set of coordinates
- Comparing coordinates to existing specimens with similar locality
  information
- Checking whether the coordinates fall in the expected administrative
  division

We will work on the third option here.

::: challenge ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

Prompt the LLM to write Python code to determine which US county a set
of coordinates is in, then answer the following questions:

1.  Can you follow the code returned by the LLM?
2.  What concepts are unfamiliar to you?
3.  How can we improve the prompt?

Remember: You can use the LLM itself to ask about unfamiliar concepts.

::: solution :::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

Concepts that commonly occur in the code returned for this prompt but
that are not covered in the Python lesson include:

- Python objects like classes, functions, and `__main__`
- Geospatial concepts like shapefiles, coordinate reference systems,
  spatial indexes, and spatial joins
- External libraries like geopandas, shapely, and pyogrio

Because generative AI is non-deterministic, this list is not
comprehensive.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

How can we improve this prompt?

# Introduction to geopandas

`geopandas` is a geospatial library based on `pandas`. It allows us to
draw maps and perform geospatial analyses (like calculating distances
and areas) using similar syntax to `pandas`.

Geospatial analysis is an enormous topic. This overview will be limited
to concepts that are likely to appear in the generated code.

```python
import geopandas as gpd
import pandas as pd
```

Let's load the JSON file we created in the previous lesson. First we'll
use the `read_json()` method to load the JSON file as a `DataFrame`:

```python
df = pd.read_json("data/coords.json")
df
```

```{.output}
```

<style>
  table.dataframe { display: block; overflow-x: auto; white-space: nowrap; }
  table.dataframe tbody tr:hover { background-color: #ccffff !important; }
  table.dataframe tr:nth-child(even) { background-color: #f5f5f5; }
  table.dataframe th { text-align: right; font-weight: bold; }
  table.dataframe td { text-align: right; }
</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>stateProvince</th>
      <th>county</th>
      <th>decimalLatitude</th>
      <th>decimalLongitude</th>
      <th>geodeticDatum</th>
      <th>coordinateUncertaintyInMeters</th>
      <th>georeferenceRemarks</th>
      <th>sourceURL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>United States</td>
      <td>New Jersey</td>
      <td>Union</td>
      <td>40.725962</td>
      <td>-74.350546</td>
      <td>WGS84</td>
      <td>120</td>
      <td>Locality described as 100 m southwest of the i...</td>
      <td>https://www.bing.com/maps?cp=40.726597~-74.349...</td>
    </tr>
  </tbody>
</table>

Now we'll create a `GeoDataFrame` from the `DataFrame`:

```python
geodf = gpd.GeoDataFrame(
    df,
    geometry=gpd.points_from_xy(df["decimalLongitude"], df["decimalLatitude"]),
    crs=4326,
)
geodf
```

```{.output}
```

<style>
  table.dataframe { display: block; overflow-x: auto; white-space: nowrap; }
  table.dataframe tbody tr:hover { background-color: #ccffff !important; }
  table.dataframe tr:nth-child(even) { background-color: #f5f5f5; }
  table.dataframe th { text-align: right; font-weight: bold; }
  table.dataframe td { text-align: right; }
</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>country</th>
      <th>stateProvince</th>
      <th>county</th>
      <th>decimalLatitude</th>
      <th>decimalLongitude</th>
      <th>geodeticDatum</th>
      <th>coordinateUncertaintyInMeters</th>
      <th>georeferenceRemarks</th>
      <th>sourceURL</th>
      <th>geometry</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>United States</td>
      <td>New Jersey</td>
      <td>Union</td>
      <td>40.725962</td>
      <td>-74.350546</td>
      <td>WGS84</td>
      <td>120</td>
      <td>Locality described as 100 m southwest of the i...</td>
      <td>https://www.bing.com/maps?cp=40.726597~-74.349...</td>
      <td>POINT (-74.35055 40.72596)</td>
    </tr>
  </tbody>
</table>

A coordinate reference system (CRS) is used to measure locations on or
near the Earth's surface. Components of a spatial reference include:

- An ellipsoid that apprixmates the shape of the Earth
- A point of origin (for example, the Prime Meridian)
- A unit (typically either degrees or minutes)
- Axes and order

Different CRS are suited to different tasks. Some CRS are worldwide
while some are optimized for specific regions. Common CRS include:

- WGS84 (EPSG:4326) (worldwide, used by GPS)
- NAD83 (EPSG:XXXX) (North America)

The main thing to know here is that **the CRS must be the same when
comparing datasets.** Changing from one coordinate system to another is
referred to as projection. Use the `to_crs()` method to project a
`GeoDataFrame` to another CRS. There are many ways to specify the new
CRS, but the easiest is by EPSG code: `"epsg:4326"` or `4326`:

```python
geodf = geodf.to_crs(4326)
```

::: keypoints ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

-

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
