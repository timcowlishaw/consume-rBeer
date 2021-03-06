consume-rBeer
=============

A spider/scraper for ratebeer.com

Goals:
------
* spider for all known breweries, beers, styles, and users (public profiles and histories)
* parse each of these four page types and output the parsed data into various formats, probably an sqlite db to start


Simple Use:
-----------
To grab all the ratings for  a **beer** (Stone Ruination IPA) and the make a histogram (using matplotlib's pylab):

	> import Beer
	> import pylab
	> ruin = Beer.Beer(14709)
	> ruin.scrape_user_rating_list()
	> pylab.hist([rating for (name, userid, rating) in ruin.ratings], bins=20)
	
And you should see a nice 20 bin histogram of these ratings, which as of 22 Jan 2012, peaked at just above 4.0, with a gaussian shape.

You can make a similar histogram but this time for *every* beer for a **brewery** (Redemption):

	> import Brewery
	> import pylab
	> redemption = Brewery.Brewery(rb_id=11318)
	> redemption.parse()
	> for beer in redemption.beers:
	>     beer.scrape_user_rating_list()
	> hist([rating for (name, uid, rating) in beer.ratings for beer in redemption.beers], bins=20)

This one produces a few clusters of bin magnitudes, with the peak at around 3.5

Neat!

