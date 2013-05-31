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

    query:

Help can be found by:

    ./factual-api-tester --help

Additional queries can be added by appending them to factual-api-tester/queries.txt.
