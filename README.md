# OpenCensus::Jaeger

This repository contains the source to `opencensus-jaeger` gem. This library is a plugin for Ruby OpenCensus that exports data to Jaeger.   
OpenCensus is a platform and provider-agnostic framework for distributed tracing and stats collection. For more information, see https://opencensus.io.  
This library is not official and is created by me - [luongvo209](https://www.github.com/luongvo209). I wrote this at the time when there were no exporter to jaeger for opencensus ruby.  
I have not published this gem to reserve the name for the official gem. Plus, it is not tested. In fact, I just wrote an example to confirm that it works.  
I am awaiting reviews from official OpenCensus's side (I have emailed @dazuma and the official Opencensus's mailing list) since I hope that it would one day make it to the official organisation of opencensus. Or at least I know that I don't conflict with someone on their side if they are already working on this.  

# Running Example

The example is just a running webserver with two endpoints:  

1. One main endpoint `/` returning `Hello world` to test tracing with Opencensus on the Rack Middleware level
2. One endpoint `/lengthy` would make an outgoing http request and then sleep for some seconds to test tracing with Opencensus on Faraday Middleware level and test adding a custom span.

To setup, first you need to run Jaeger, whose introduction could easily be found here: https://www.jaegertracing.io/docs/1.8/getting-started/  
I would recommend using one command to start everything, although the things that we need the most is the UDP Agent running at port 6381, as this exporter will send span data to the jaeger agent via UDP over thrift protocol.  

```bash
docker run -d --name jaeger \
  -e COLLECTOR_ZIPKIN_HTTP_PORT=9411 \
  -p 5775:5775/udp \
  -p 6831:6831/udp \
  -p 6832:6832/udp \
  -p 5778:5778 \
  -p 16686:16686 \
  -p 14268:14268 \
  -p 9411:9411 \
  jaegertracing/all-in-one:1.8
```

Then install all the necessary gems and run the server:   
```bash
cd examples
bundle
bundle exec rackup -s thin -p 4567
```
If there is any error installing with bundle, you should tinker the gemfile a bit since I load this gem locally with a `path`.   
After everything is up and running, head to `localhost:4567` and play around with the endpoints I listed above.  
Also, you would need to go to `localhost:16686` to see the traces display by jaeger UI, which means that we succeeded in collecting them via Opencensus and exporting data to Jaeger.  

# Installation
TBD
## Usage
TBD
## Development
TBD
## Contributing
TBD
## Working proof 
<img width="1678" alt="image" src="https://user-images.githubusercontent.com/15828926/51026192-8d4c4200-15c0-11e9-873d-b189023cd670.png">  

![image](https://user-images.githubusercontent.com/15828926/50948201-3e28e300-14d4-11e9-87ee-f5d97b756131.png)
