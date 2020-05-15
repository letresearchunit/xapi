# Dictionary Extension for xAPI

Dictionary is a must have tool in the box of every language learner. As such, there should be a way to tract learner interaction with a dictionary in a pedagogical context. We define xAPI verbs and activities for use in computerized dictionaries (web or application based).

This document specifies 2 new verbs (Browsed, Set), reuse 5 existing verbs (Searched, Bookmarked, Listened), defines 5 activities (Application, Entry, Index, Page, Settings) and one new activity type.

## Document Status

Version 1.0 RC

Author: Louis Lecailliez

<!-- ## Reading List

https://xapi.com/blog/deep-dive-activity/ (lu)

https://xapi.com/blog/activity-type-forgotten-iri/ (lu)

https://xapi.com/blog/profile-recipes-vs-xapi-profiles/ (lu) -->

## Verbs

Prefix for all newly defined entites is <span style="color:blue;">https://github.com/letresearchunit/xapi/dictionary/</span>.

Profile IRI:  <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>profile

| Verb | IRI |
|---|---|
| Opened | http://activitystrea.ms/schema/1.0/open |
| Closed | http://activitystrea.ms/schema/1.0/close |
| Searched | http://activitystrea.ms/schema/1.0/search | # search in index
| Browsed | <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>verb/browsed | # browse an entry
| Bookmarked | http://id.tincanapi.com/verb/bookmarked |
| Listened | http://activitystrea.ms/schema/1.0/listen |
| Set | <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>verb/set |

## Activities Identifiers & Types

The IRIs below define types that can by used as Activity, that is as value for the object.type property. It also lists the acceptable extension properties.

###Application

A dictionary application (web-based or not).

| Property | Value |
|---|---|
| Id | <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>activity/application |
| Type | https://w3id.org/xapi/acrossx/activities/search-engine |
|Extension | <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>activity/application/extension |

#### Extension

| Property | Type | Required |
|---|---|---|
|name| string| Optional |
|version| string|Optional|
|platform|string|Optional|

### Entry

A dictionary entry. <br>Example: the entry for "advice" in the [Cambridge Dictionary](https://dictionary.cambridge.org/fr/dictionnaire/anglais/advice).

| Property | Value |
|---|---|
| Id | <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>activity/entry |
| Type | http://activitystrea.ms/schema/1.0/article |
|Extension | <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>activity/entry/extension |

#### Extension

| Property | Type | Required |
|---|---|---|
|identifier| string| Required |
|from|string|Optional|
|through|string|Optional|

### Index

A dictionary index or search page. <br>Example: "Search by Chang-Jei" page of the [Chinese Character Variants Dictionary](http://dict.variants.moe.edu.tw/variants/rbt/query_by_standard_tiles.rbt).

| Property | Value |
|---|---|
| Id | <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>activity/index |
| Type | http://activitystrea.ms/schema/1.0/collection |
|Extension | <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>activity/index/extension |

#### Extension

| Property | Type | Required |
|---|---|---|
|identifier| string|Required|
|searched_term|string|Optional|
|from|string|Optional|
|through|string|Optional|


### Page

A dictionary page that in not the home page or search page. Typically, an about or help page. <br>Example: The information page of the Japanese-French Dictionary project [Jibiki](https://jibiki.fr/informations.php).

| Property | Value |
|---|---|
| Id | <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>activity/page |
| Type | http://activitystrea.ms/schema/1.0/page |
|Extension | <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>activity/page/extension |

#### Extension

| Property | Type | Required |
|---|---|---|
|identifier| string |Required|
|from|string|Optional|
|through|string|Optional|


### Settings

Settings of a dictionary. <br>For example, the transcription system to use for display in a Japanese dictionary.

| Property | Value |
|---|---|
| Id | <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>activity/settings |
| Type | <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>activity_type/settings |
|Extension | <span style="color:gray;">https://github.com/letresearchunit/xapi/dictionary/</span>activity/settings/extension |

#### Extension

| Property | Type | Required |
|---|---|---|
|name| string |Optional|
|value| string | Optional |

## Verb/Activity Compatibility

| | Entry | Index | Page | Application | Settings |
|---|---|---|---|---|---|
|Opened|- |- |- | ✓ | ✓ |
|Closed|- |- |- | ✓ | ✓ |
|Searched|- | ✓ |-| - | - |
|Browsed|✓|✓|✓|-|-|
|Bookmarked|✓|-|✓|-|-|
|Listened|✓|-|-|-|-|
|Set|-|-|-|-|✓|

## Design notes

### Identifier

Identifiers are typed as string. This way web-based applications can use URL while other applications can use internal identifiers.

### From, Through

All activities compatible with the <i>browsed</i> verb have the following two extensions: <i>from</i>, <i>through</i>. While <i>identifier</i> identifies the current <i>entry</i>, <i>page</i> or <i>index</i>, the <i>from</i> property stores the previous <i>entry</i>, <i>page</i> or <i>index</i> identifier and <i>throught</i> contains the way (URL or internal identifier) that was use to navigate to it.

<!--
todo examples:

- app launch (= browse home page) BROWSED/Page, BROWSED/Index
- search pluie in French index BROWSED/Index, SEARCHED/Index
- browse pluie entry BROWSED/Entry
- navigate to 𒀭 NAVIGATED
-->


