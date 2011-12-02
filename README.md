A string fuzzymatching library!

It was written initially to power an autocomplete widget for backbone
models but I'm sure you can think of other creative uses.

### TODOs

Add a matchAllQuery() function that matches against all posibilities.

Warm up cache on popular queries on page load. i.e. keep track of each query where something is selected and for the top 10, run that query so results already stored.
Not on by default as it could seriously slow down site if you do too many.
Do a setTimeout thing so only do one query every .1 seconds as that shouldn't affect the responsiveness of the UI too much.

Add training api, simple count. if someone clicks you say match.train('project', 'id', 'query')
Next search, at each query, if there's an item that's been selected before
Boost it's score. Subtract 2 * number of times selected from its score divided by the levenstein distance from past queries where it was selected
to the current query. So for example, if it was selected before for "port" and the current query is po, subtract 1 from its score (2/2)
Next time, at "po" you'd subtract 3 from its score ((2 * 1) + (2 * 1) / 2)
The time after that at "po" you'd subtract 5 from its score ((2 * 2) + (2 * 1) / 2)
Might have to do a max subtraction, otherwise some popular items would always show up first even
if query is very different.

Store this training data in localstorage if possible. Otherwise, just keep it in memory.

Also let people pass in training data associated with a item. E.g. that'd be super useful for family history site.
Each time someone selects a person, send that data to server and then send it out to each connecting client periodically.

So training data should be loaded from localstorage. Items too old eliminated, saved back to localstorage, then merged with any training data passed in.
But don't save training data passed in? Keep local stuff seperate.

Make this work with Node.js.

Allow people to override settings for matching.

Allow to override # of matches to look at.

Option to precache results on server for big sets and pass in -- this is
especially helpful for mobile which is a bit underpowered for this.
Only useful for very static data sets.
