## Kitsu JSON API

This is a wrapper for the JSON API provided by Kitsu for Node.js.
Full documentation can be found on their [website](https://kitsu.docs.apiary.io/#introduction/json-api).

## How to get start

Install with NPM ```npm i kitsu-json-api```
```javascript
import KitsuApi from 'kitsu-json-api';
```
or
```javascript
const KitsuApi =  require('kitsu-json-api');
```
then
```javascript
let kitsuApi =  new KitsuApi();
```

## Methods/Functions

#### execute()
 Execution method for this wrapper API. You must call this to run the query/api call to kitsu!
#### query(keyword)
 First method you need to call to properly call the API (I will move this to the constructor b/c it makes more sense). The query function takes in a parameter that is a category the API allows you to query. For example if you want to query for animes you would do
 ```javascript
  kitsuApi.query('anime')
 ```
  Check [here](https://kitsu.docs.apiary.io/#reference) to see which categories you can query.
#### paginationOffset(number)
  Sets the [offset for pagination](https://kitsu.docs.apiary.io/#introduction/json-api/pagination) when receiving data.
#### paginationLimit(number)
  Sets the (limit for pagination)[https://kitsu.docs.apiary.io/#introduction/json-api/pagination] when receiving data.
#### filter(filterKey, [ filterValues ])
  Allows you to (filter the category you)[https://kitsu.docs.apiary.io/#introduction/json-api/filtering-and-search] query based on attributes of that category. Check [here](https://kitsu.docs.apiary.io/#reference) to find what attributes the category has.
#### sort([ attributes ])
  This methods takes in an array of flags and
  [sorts based off the flags](https://kitsu.docs.apiary.io/#introduction/json-api/sorting) given by Kitsu. I haven't found all of them but some are specified in the documentation.
#### includes([ relationships ])
"You can include related resources with include=[relationship].
          You can also specify successive relationships using a .. A comma-delimited list can be used to [request multiple relationships](https://kitsu.docs.apiary.io/#introduction/json-api/includes)."

#### sparse(fieldKey, [ fieldValues ])
"You can request a resource to only return a [specific set of fields in its response](https://kitsu.docs.apiary.io/#introduction/json-api/sparse-fieldsets). For example, to only receive a user's name and creation date:
          (e.g /users?fields[users]=name,createdAt)"


## Example
```javascript
  kitsuApi
    .query('anime') // anime category
    .filter('season', ['winter', 'spring']) // filter by winter and spring
    .filter('seasonYear', ['2017']) // filter by year 2017
    .paginationLimit(10) // set limit
    .paginationOffset(2) // set offset
    .sort(['followersCount', 'followingCount']) // sort by follower count and following count
    .execute(); // execute the query
```
