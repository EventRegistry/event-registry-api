# Event Registry API changelog

This repository simply lists the recent changes to the Event Registry for the users who use the system through the API but don't use the [Python SDK](https://github.com/EventRegistry/event-registry-python).

## (2017-06-14)

**Added**
- when querying for articles or events, you can now additionally specify parameters `sourceLocationUri` and `sourceGroupUri`. Parameter `sourceLocationUri` can be used to specify a location URI (obtained with [location autosuggest methods](http://eventregistry.org/documentation#suggLocations)) to use a set of news sources from a specific geographic location. The locations used can be cities or countries. `sourceGroupUri` can be used to use in search a set of news sources that belong to a manually curated list of news sources (such as top business related sources, top entertainment sources, ...).
- when querying a list of articles, valid sorting values are now also `sourceAlexaGlobalRank` (global rank of the news source) and `sourceAlexaCountryRank` (country rank of the news source).
- when returning articles, the details returned about the news source can now also include the source image. To obtain the source image specify `*IncludeSourceImage=true` where the `*` prefix should be determined based on the type of the query you are making. The returned information about the source will then include two new fields: `image` and `thumbImage`.

**Changed**
- the previous query flag `*IncludeSourceImportance` is now changed to `*IncludeSourceRanking`. The change is due to the fact that there are now multiple rankings for the source that we return. The returned value about the source is no longer property `importance`, but an object `ranking` that contains three ranks: `importanceRank`, `alexaGlobalRank` and `alexaCountryRank`.
- the previous query flag `*IncludeSourceTag` was now changed to `*IncludeSourceSourceGroups`. The returned value about the source now no longer returns property `tag` (which was not used anywhere yet) but returns `sourceGroups` array.
- the previous query flag `*IncludeArticleSocialScore` was now changed to `*IncludeArticleShares`. Set it if you wish to obtain the information about the number of times the article was shared on social media.
- the article data model (JSON format in which information about the article is returned) has changed: The `socialScore` property is now named `shares` to better represent the content. The returned object can now include also shares on Google Plus, Pinterest, LinkedIn. To view the full data format, see [Article Data Model](https://github.com/EventRegistry/event-registry-python/wiki/Data-models#article-data-model) page.
- the source data model has changed: `importance` property was changed to an object `ranking` containing multiple indicators of source importance.

**Deprecated**
- when sorting articles, `sortBy` value `sourceImportance` is now deprecated. Use value `sourceImportanceRank`. Is is equvalent to reversed value of `sourceImportance` therefore also make sure to negate your existing value of `sortByAsc` value. The parameter was changed to make it comparable to added sorting options `sourceAlexaGlobalRank` and `sourceAlexaCountryRank` which also represent rankings (lower value means better value).


