---
layout: post
title:  "FindABuilder.com"
date:   2017-09-09 11:53:03 -0500
categories: Projects API MongoDB
image: /images/fab
---

### Opportunity
Aggregate new home construction data from 300+ home builder websites into a common database to create one of the largest collections of new construction home listings in North America.

The majority of the residential real estate market is served by the existing MLS system.  Sites like Realtor.com and Zillow provide home buyers with a searchable list of properties nation wide.  However, new homes and available lots are often missing from MLS systems.  Many home builders prefer to market their properties through their own websites and do not feel existing aggregation services serve their interests.


### Existing Data
300+ websites built over a five year period all using the same custom built in-house CMS.

While the existing sites used the same CMS, it had been heavily customized for each.  MySQL tables varied in naming convention and content.  The 'community' table of one site was the 'communities' table of the next.  Older sites stored CSV lists in single fields while newer sites took advantage of one-to-many table relationships.  Only a few newer sites took advantage of foreign key relationships.  None of the schemas were documented.


### Solution
MongoDB, Python Eve, PHP, AngularJS

[![](/images/api2.jpg)](/images/api2.jpg) An update was made to the legacy CMS to provide an API to the existing MySQL data.  In order to handle a wide variety of undocumented data, MongoDB was chosen as the new database solution.  A nightly cron job was set up on a separate server to access the API on each site and update the MongoDB database.  As gaps were discovered in the data, The CMS was extended with a series of fallbacks for its API.

[![](/images/eve.jpg)](/images/eve.jpg) An off-the-shelf solution, [Python Eve](http://python-eve.org/), was selected to provide an API to the new MongoDB database.  Python Eve worked out-of-the-box as a fully functional REST API with minimal configuration saving time over building a custom solution.  Eve combined with MongoDB also provided for the geospatial queries required to search and filter the data later.

[![](/images/fabfinal.jpg)](/images/fabfinal.jpg) Finally, a proof-of-concept website was created to consume the API.  [FindABuilder.com](https://www.findabuilder.com/) displays aggregated data from all 300+ home builder websites to potential home buyers.
