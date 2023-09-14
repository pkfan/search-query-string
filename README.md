# search-query-string
you can easily use following functions to partse url search query to javascript object

OR 

Object to url search query string


```javascript

        function pkfan_searchQuery_to_object(){
            if(window.location.search){
                //remove "?" sign from search string url
                var searchString = window.location.search.substring(1);

                //transform queryString into ['paginate=10', 'amir=12', 'rizwan=wrew']
                searchStringArray = searchString.split('&');

                queryStringObject = {};

                searchStringArray.forEach(nameValue=>{
                        let [name,value] = nameValue.split('=');
                        queryStringObject[name] = value;
                });

                return queryStringObject;
            }
            else {
                return {};
            }
        }

        function pkfan_object_to_searchQuery(queryStringObject){
            var queryStringAgain = '';

            var nameValueCounter = 1;

            for(let [name,value] of Object.entries(queryStringObject)){

                if(nameValueCounter == 1){
                    name = `?${name}`;
                }
                else{
                    name = `&${name}`;
                }

                queryStringAgain = `${queryStringAgain}${name}=${value}`;

                nameValueCounter++;
            }

            return queryStringAgain;
        }


            //see following code how use above function and change current url to new one

            var searchQueryObject = pkfan_searchQuery_to_object();

            searchQueryObject['page'] = 10;

            var newSearchQuery = pkfan_object_to_searchQuery(searchQueryObject);

            var fullUrlWithQuerySearch = `${window.location.origin}${window.location.pathname}${newSearchQuery}`;

            console.log(fullUrlWithQuerySearch);

            window.location = fullUrlWithQuerySearch;


```

# usage of pkfan_searchQuery_to_object()

```javascript
// if search query string is (?paginate=30&page=5&q=pkfan)
// then output will be {paginate: '30', page: '5', q: 'pkfan'} object

// ?paginate=30&page=5&q=pkfan
pkfan_searchQuery_to_object();

output: {paginate: '30', page: '5', q: 'pkfan'}

```

# usage of pkfan_object_to_searchQuery(object);

```javascript
  // if object is {paginate: '30', page: '5', q: 'pkfan'} 
  // then output will be (?paginate=30&page=5&q=pkfan) object

  pkfan_object_to_searchQuery({paginate: '30', page: '5', q: 'pkfan'});

  output will be (?paginate=30&page=5&q=pkfan)
```
