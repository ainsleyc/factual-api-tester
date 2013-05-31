factual-api-tester
==================

Command line testing tool for Factual API

### Setup

    git clone https://github.com/ainsleychong/factual-api-tester.git
    cd factual-api-tester
    npm install
    
The tool looks for a yaml config file to provide the API oauth key and secret under ~/.factual/factual-auth.yaml:

    key: 6Mueo89QbxGNBH4wbdz7sX9i03mxLQJvAG7HMU5x (not a real key)
    secret: TgGoy6HcJLJpxKfmsncyljATtZRxnqGNvRNSpDCx (not a real secret)
    
To get a key and secret please visit https://www.factual.com/partners/register
    
### Running

factual-api-tester can be called directly from the shell, so adding it to your PATH will allow it to be called from anywhere.

    ./factual-api-tester

Interface:

    TARGET: api.v3.factual.com

    Available queries:
    0) /t/places?filters={"country":"US"}
    1) /t/places?geo={"$within":{"$rect":[[34.06110,-118.42283],[34.05771,-118.41399]]}}
    2) /t/places-v3/resolve?values={"name":"McDonalds","address":"10451 Santa Monica Blvd","region":"CA","postcode":"90025"}
    3) /t/places-v3/submit?user="TestUser"&values={"name":"NotARealPlace","latitude":"90","longitude":"0"}

    query: <type a query # here>

Sample output:

    nock('http://api.v3.factual.com:80')
        .get('/t/places-v3/resolve?values=%7B%22name%22:%22McDonalds%22,%22address%22:%2210451%20Santa%20Monica%20Blvd%22,%22region%22:%22CA%22,%22postcode%22:%2290025%22%7D')
        .reply(200, "{\"version\":3,\"status\":\"ok\",\"response\":{\"data\":[{\"name\":\"McDonald's\",\"address\":\"10451 Santa Monica Blvd\",\"locality\":\"Los Angeles\",\"region\":\"CA\",\"postcode\":\"90025\",\"website\":\"http://www.mcdonalds.com\",\"latitude\":34.056585197104994,\"longitude\":-118.42584905764551,\"country\":\"us\",\"tel\":\"(310) 474-3160\",\"factual_id\":\"c730d193-ba4d-4e98-8620-29c672f2f117\",\"fax\":\"(310) 474-6230\",\"category_ids\":[347],\"category_labels\":[[\"Social\",\"Food and Dining\",\"Restaurants\"]],\"chain_id\":\"ab4a3530-d68a-012e-5619-003048cad9da\",\"chain_name\":\"McDonald's\",\"neighborhood\":[\"West LA\",\"Westwood\",\"Century City\",\"Westside Village\",\"West Los Angeles\"],\"status\":\"1\",\"resolved\":true}],\"included_rows\":1}}", { 'access-control-allow-origin': '*',
        'cache-control': 'max-age=2592000',
        'content-type': 'application/json; charset=utf-8',
        date: 'Fri, 31 May 2013 19:08:51 GMT',
        server: 'nginx/1.2.6',
        'x-factual-throttle-allocation': '{"expensive":"0%","burst":"0%","daily":"0%"}',
        'transfer-encoding': 'chunked',
        connection: 'Close' });

Help can be found by:

    ./factual-api-tester --help

Additional queries can be added by appending them to factual-api-tester/queries.txt:

    { "action":"get", "path":"/t/places?filters={\"country\":\"US\"}" }
    { "action":"get", "path":"/t/places?geo={\"$within\":{\"$rect\":[[34.06110,-118.42283],[34.05771,-118.41399]]}}" }
    { "action":"get", "path":"/t/places-v3/resolve?values={\"name\":\"McDonalds\",\"address\":\"10451 Santa Monica Blvd\",\"region\":\"CA\",\"postcode\":\"90025\"}"}
    { "action":"post", "path":"/t/places-v3/submit?user=\"TestUser\"&values={\"name\":\"NotARealPlace\",\"latitude\":\"90\",\"longitude\":\"0\"}" }
