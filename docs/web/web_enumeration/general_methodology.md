
# general_methodology

## take note of actions

Actions on the site should be interecepted and analyzed.  Anything that results in a change in the state of the site, session, or database has potential for abuse. 


## fuzzing

Fuzz everything. Notable targets include

- APIs
	- fuzz for functions
	- fuzz for parameters
- Data posted to an app that modifies a database, such as registration, or changing fields
	- fuzz for bad characters
	- fuzz for sequential parameters (IDOR type bugs)