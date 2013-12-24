HTTP Regulator
==============

HTTP Regulator is a HTTP forward proxy that regulates concurrent HTTP requests to an API.  Most rate limiters will simply return 503 when the rate is exceeded, but the HTTP Regulator will slow down the request rate to meet the limit.  By having a separate HTTP server, this allows multiple processes to access the API without having to worrying about exceeding the limit.

Requires
--------

* Bash
* Groovy (via Bash)

Usage
-----

    usage: http-regulator
        --local-port <number>              the port this server runs on.
                                           default: 30080
        --min-delay <ms between request>   the minimum number of milliseconds
                                           to wait between requests.  for
                                           example 300 request/second use 4.
                                           for 500 request/10 min use 1200
        --query <name=value>               additonal query parameter to
                                           include with the target request
        --target-host <url>                the target host to proxy to.  eg.
                                           http://example.com:8080

Example
-------
To start a server that will work with Riot's API using the develeopment key limit of 500 requests every 10 minutes (1000*10*60/500 => 1200)

    ./http-regulator --min-delay 1200 --target-host https://prod.api.pvp.net --query api_key=<YOUR API KEY>

Now API requests to `http://localhost:30080/<API PATH>` will automatically add the `api_key` as a query parameter.

Copyright and License
---------------------
<pre>
Copyright 2013 Ronald Chen

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
</pre>

