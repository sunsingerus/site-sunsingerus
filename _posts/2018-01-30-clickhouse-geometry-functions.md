---
ID: 362
post_title: ClickHouse. Geometry functions
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/clickhouse-geometry-functions/
published: true
post_date: 2018-01-30 20:54:23
---
ClickHouse provides several geometry-related functions:
<ul>
<li><code>greatCircleDistance</code></li>
<li><code>pointInEllipses</code></li>
<li><code>pointInPolygon</code></li>
</ul>
However, there are (at least for now) no official docs available, so we need to take a look into sources.

<h5>greatCircleDistance</h5>

As we can see in <a href="https://github.com/yandex/ClickHouse/blob/288c6c8406fba0edc503630490364ab1c1f4036d/dbms/src/Functions/FunctionsGeo.h#L31" rel="noopener" target="_blank">sources</a>
<pre>
The function calculates distance in meters between two points on Earth specified by longitude and latitude in degrees.
The function uses great circle distance formula https://en.wikipedia.org/wiki/Great-circle_distance.
Throws exception when one or several input values are not within reasonable bounds.
Latitude must be in [-90, 90], longitude must be [-180, 180]
</pre>

As as an example, let's calculate distance between London and Paris
<table>
<tr><td><strong>City</strong></td><td><strong>Latitude</strong></td><td><strong>Longitude</strong></td></tr>
<tr><td>London</td><td>51.50853</td><td>-0.12574</td></tr>
<tr><td>Paris</td><td>48.85341</td><td>2.34880</td></tr>
</table>
Pay attention to parameters order - first comes longitude. Function call would be like the following
<pre>
SELECT floor(greatCircleDistance(-0.12574, 51.50853, 2.34880, 48.85341)) AS distance;
</pre>
We have distance of 343867 meters, which is about 344 km or 214 miles

<h5>pointInEllipses</h5>

As we can see in <a href="https://github.com/yandex/ClickHouse/blob/288c6c8406fba0edc503630490364ab1c1f4036d/dbms/src/Functions/FunctionsGeo.h#L163" rel="noopener" target="_blank">sources</a>
<pre>
The function checks if a point is in one of ellipses in set.
The number of arguments must be 2 + 4*N where N is the number of ellipses.
The arguments must be arranged as follows: (x, y, x_0, y_0, a_0, b_0, ..., x_i, y_i, a_i, b_i)
</pre>
Where <strong>X</strong> and <strong>Y</strong> are coordinates of the point to check and <strong>Xi</strong>, <strong>Yi</strong>, <strong>Ai</strong> and <strong>Bi</strong> are parameters of each ellipse as described in <a href="https://www.mathopenref.com/coordgeneralellipse.html" rel="noopener" target="_blank">general equation of an ellipse</a>.

Let's check whether point (1,1) in inside ellipse with x=2 y=2 a=3 b=3
Pay attention to parameters - <strong>float</strong> numbers required.
<pre>
select pointInEllipses(1.0, 1.0, 2.0, 2.0, 3.0, 3.0);
</pre>

<h5>pointInPolygon</h5>

This <a href="https://github.com/yandex/ClickHouse/blob/288c6c8406fba0edc503630490364ab1c1f4036d/dbms/src/Functions/FunctionsGeo.cpp#L75" rel="noopener" target="_blank">function</a> checks whether specified point is inside specified (by vertexes) polygon.
<pre>
pointInPolygon((x, y), [(x1, y1), (x2, y2), (x3, y3)...])
</pre>

Let's check whether point (1,1) is inside a square with side length equal to 2
<pre>
select pointInPolygon((1,1), [(0,0),(2,0),(2,2),(0,2)]);
</pre>