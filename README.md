# R-Projections-Workshop
A workshop on understanding and using projections for spatial data in R

## Expected Outcomes

The expected outcome of this workshop is not that you will understand everything about projections by the end of the 2 hours.  Learning and understanding projections for geospatial data is (perhaps unfortunately) a life-long endevor.  My expectation is that by the end of this workshop, you will have a better understanding of what a projection is, why you would choose one over another, and how to apply them correctly to geospatial data in R.  Will you have questions later?  Of course!  That is entirely expected.

## Classroom Expectations

Learning is sometimes difficult.  Projections are confusing.  As I stated early, I hope to mitigate this, but let's recognize it up front.  I have some rules for my classroom for just these kinds of situations:

1. I expect you to ask questions. 
1. I want you to ask "dumb" questions as well as "smart" questions (whatever those terms mean for you).  All questions are valid.
1. You may answer questions.  I highly encourage you to discuss your questions with others in the room.  Maybe you can figure it out together.  If you want more input, ask someone else.
1. I will do my best to answer your questions, but reserve the right to say "I don't know" or "I will need to do some research and get back to you" or ask the people in the room if they know the answer.  One person can't know everything.
1. You can and should take breaks when you need to.  Step outside, walk around, I won't be offended.  Brains need a break.  If you need to take this home and work on it later, that's fine too!


# Coordinate Reference System (CRS)

**CRS = Datum + Projection + Additional Parameters**

*A common analogy employed to teach projections is the orange peel analogy.  If you imagine that the earth is an orange, how you peel it and then flatten the peel is similar to how projections get made.   We will also use it here.*

## Datum

A **Datum** is a model of the shape of the earth.

It has angular units (i.e. degrees) and defines the starting point (i.e. where is (0,0)?) so the angles reference a meaningful spot on the earth.

Common global datums are WGS84 and NAD83.  Datums can also be local, fit to a particular area of the globe, but ill-fitting outside the area of intended use.

When datums are used by themselves it's called a *Geographic Coordinate System*.

*Orange Peel Analogy: a datum is your choice of fruit to use in the orange peel analogy.  Is the earth an orange, a lemon, a lime, a grapefruit?*

![Citrus fruit on display at the market](https://farm3.staticflickr.com/2260/2508805118_500f5bba28_n.jpg)



## Projection

A **Projection** is a mathematical transformation of the angular measurements on a round earth to a flat surface (i.e. paper or a computer screen).

The units associated with a given projection can be linear (feet, meters, etc.) or angular (degrees).

Many people use the term "projection" when they actually mean "coordinate reference system". (With good reason, right?  Coordinate References System is long and might make you sound pretentious.)  One example is the title of this workshop... but you wouldn't know what it was about if I said it was a workshop on "Coordinate Reference Systems in R", would you?

*Orange Peel Analogy: a projeciton is how you peel your orange and then flatten the peel.*

![An orange peeled like a map projection](http://blogs.lincoln.ac.nz/gis/wp-content/uploads/sites/16/2017/03/laranjoide_1.jpg)

Image source: http://blogs.lincoln.ac.nz/gis/2017/03/29/where-on-earth-are-we/


## Additional Parameters

Additional parameters are often necessary to create the full coordinate reference system.  For example, one common additional parameter is a definition of the center of the map.  The number of required additional parameters depends on what is needed by each specific projection.

*Orange Peel Analogy: an additional parameter could include a definition of the location of the stem of the fruit.*


# Notation for Coordinate Reference Systems in R

You have two options for identifying a CRS in most R commands.  The documentation for a command that requires projection information will tell you which is required.  Often you can choose between the two options.

## EPSG Code

An EPSG Code is an ID that has been assigned to most common projections to make reference to a particular projection easy.

The main advantages to using this method of specifying a projection are that it is standardized and ensures you have the same parameters every time.  The disadvantage is that if you need to know the parameters used by the projection or it's name, you have to look them up, but that's fairly easy to to at [spatialreference.org](http://spatialreference.org/ref/epsg/).  Also, you can't customize the parameters if you use an EPSG code.  For example: `EPSG:27561`

*A note on linguistics:* EPSG stands for "European Petroleum Survey Group"... but everyone just says EPSG.

## PROJ.4 String

PROJ.4 is an open source library for defining and converting between coordinate reference systems.  It defines a standard way to write projection parameters.  For example: `+proj=lcc +lat_1=49.5 +lat_0=49.5 +lon_0=0 +k_0=0.999877341 +x_0=6 +y_0=2 +a=6378249.2 +b=6356515 +towgs84=-168,-60,320,0,0,0,0 +pm=paris +units=m +no_defs`

Two important advantages to using this option are (1) the parameters are human-readable and immediately transparent and (2) the strings are easily customized.  The main disadvantage to this option is that it's easy to make a mistake when you reproduce the string, accidentally changing parameters.

*A note on linguistics:* PROJ.4 is commonly pronounced "prodge four" ("PROJ" rhymes with "dodge"); PROJ is short for "projection".  The 4 is because we're currently using the 4th version of this library.



---------------------------------------
# Hands-On Tutorial



---------------------------------------
# Resources Used to Compile this Tutorial:

1. [Rspatial.org](http://rspatial.org/spatial/rst/6-crs.html)
1. [Data Carpentry Intro to Geospatial Data with R](http://www.datacarpentry.org/R-spatial-raster-vector-lesson/)
1. [University of Colorado's Map Projections](https://www.colorado.edu/geography/gcraft/notes/mapproj/mapproj_f.html)
1. [International Institute for Geo-Information Science and Earth Observation (ITC)](http://kartoweb.itc.nl/geometrics/map%20projections/mappro.html)
1. [Carlos Furuti's Projections Page](http://www.progonos.com/furuti/MapProj/Normal/TOC/cartTOC.html)

Map Projection Fun:

1. [xkcd's Map Projections](https://xkcd.com/977/)
1. [Jason Davies' Map Projection Transitions](https://www.jasondavies.com/maps/transition/)
1. [Carlos Furuti's Printable Projections](http://www.progonos.com/furuti/MapProj/Normal/ProjPoly/Foldout/foldout.html) Global projections you can print and assemble


---------------------------------------

## Previous notes:

What is Latitude & Longitude?
= angular measurements from an arbitrary zero

What is a projection?
= making angular measurements on a sphere into a flat surface

WHY projections?
= minimizing distortions in the flattening process

Define Projection vs. Reproject


Let's break stuff! = the hands-on portion of the program

First, we'll look at projections visually.

Open QGIS

You'll need to turn off projection on the fly to see the difference between new layers.
 Options --> CRS tab --> Pick "Don't enable 'on the fly' reprojection' from the Default CRS for New Projects options.

Load a shapefile - suggestion: CA Counties

Reproject your shapefile
- right click --> save as --> pick a new name (put the EPSG code in the name) --> pick a new projection (start with CA Albers NAD 27)

Turn off projection on the fly... not much difference b/n CA Albers NAD 83 & NAD 27

Reproject the shapefile again with another... try UTM Zone 10 N (32610) and Australian Albers (3577)


Ideas:
 * Try making measurements like distance or area

