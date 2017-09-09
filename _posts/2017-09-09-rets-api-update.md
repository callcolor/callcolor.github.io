---
layout: post
title:  "Real Estate API Update"
date:   2017-09-09 10:53:03 -0500
categories: Projects MLS RETS API MongoDB
image: /images/rets
---

### Opportunity
Provide single-entry of home listing data for builders who market properties with real estate agents.

Real estate agents working with home builders were syndicating listings using the MLS (Multiple Listing Service).  Utilizing the MLS data on home builder websites would save time and provide more accurate data to potential buyers.  However, because a primary goal is to be time-saving, the system must be simple and seamless to the user in order to be practical.


### Issues
There are hundreds of regional real estate listing standards with constantly changing schemas.

Those familiar with real estate websites like Zillow expect the MLS system to be one coherent system but it is divided into hundreds of independently developed regional vendors.

While the majority of vendors utilize an XML based system called [RETS][wiki-rets], or Real Estate Transaction Standard, RETS does not prescribe a single security standard or a unified data schema.

Each regional vendor has their own data schema and although a standard schema has been strongly recommended regional influence prevents the standard from being followed.  Even simple data like bathroom count or square footage will be represented differently by different regions.  Field names vary (baths, bathrooms, baths_full, fullBaths, baths_total) and regional variations exist in the way values are represented as well.  For example, 2.1, 2.5, 2 1/2, Full: 2 and Half: 1, are all used by one system or another to represent the same information.  Square footage may be recorded as a single integer (1345) in one system and as a string range (1,000 to 1,500) in another.  There is no guarantee that any single data property will be provided.

Vendors are constantly updating their schema.  New data properties are added or fields are modified to more closely match the standard schema.

Additionally, vendors have countless unique data properties that may be regionally significant.  For instance, lake access or rights to a dock may add significant value to a home but would only exist in regions where water access is common.

Clients often did business in multiple MLS regions meaning they would need data to be normalized to appear consistent on their websites.


### Existing Stack
PHP, MySQL

An existing system utilizing a MySQL database required constant support.  Only a basic field set defined in a single MySQL table was recorded.  Vendor fields were mapped to the local MySQL fields one-by-one.  When a vendor updated their schema, fields would need to be remapped.  When a custom regional field was needed it required adding the field and its translations to the database, and adding support to several different locations in PHP and Javascript code.  Since any data properties not expressly handled were lost, any changes on either side required all data be downloaded again from the vendor.  Vendors often limited the number of daily queries, resulting in temporary bans from the regional data.


### Solution
MongoDB, AngularJS, Material Design

[![](/images/mlsadmin.jpg)](/images/mlsadmin.jpg) To simplify the system a NoSQL solution was implemented utilizing MongoDB and a material design, AngularJS admin portal.  Rather than mapping fields independently for each vendor, a global behind-the-scenes field map was utilized that allowed new vendors to be added much more quickly.  Additionally, since the global field map did not need to be updated as vendors adapted to the standard schema, those support issues were eliminated.

[![](/images/mlsadd.jpg)](/images/mlsadd.jpg) Standard fields are translated into a normalized schema based on the Creative Commons licensed [schema.org][schema-org].  Regional-only fields were retained in the data and made available to applications downstream.  When new regional fields were added, no updates were needed, since MongoDB was able to store a complete set of data properties.

[![](/images/mlsres.jpg)](/images/mlsres.jpg) MongoDB also provides a well-documented query language which is used to query the normalized data.  A 'find' URL parameter is passed to MongoDB via a PHP-based API.  Any field, standard or custom, can be used in a query.  Indexes on standard fields allow the Mongo queries to be performant even when custom fields are used and with millions of properties in the database.


[wiki-rets]: https://en.wikipedia.org/wiki/Real_Estate_Transaction_Standard
[schema-org]: http://schema.org/SingleFamilyResidence
