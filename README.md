# nginx-jaeger-all-in-one

Combines [`nginx`](https://hub.docker.com/_/nginx) and [`jaegertracing/all-in-one`](https://hub.docker.com/r/jaegertracing/all-in-one) into a single alpine container, so that Jaeger OTLP via HTTP collector can be used with CORS. I needed a way to submit traces directly to Jaeger for local development, without complicating the setup further than `docker run`.

## Getting Started

> The following command is based on [Jaeger: Getting Started](https://www.jaegertracing.io/docs/1.44/getting-started/#all-in-one) "all in one" example command.

```sh
docker run -d --name jaeger \
  -e COLLECTOR_ZIPKIN_HOST_PORT=:9411 \
  -e COLLECTOR_OTLP_ENABLED=true \
  -p 6831:6831/udp \
  -p 6832:6832/udp \
  -p 5778:5778 \
  -p 16686:16686 \
  -p 4317:4317 \
  -p 4318:4318 \
  -p 14250:14250 \
  -p 14268:14268 \
  -p 14269:14269 \
  -p 9411:9411 \
  bengreenier/nginx-jaeger-all-in-one
```

Then you'll have the appropriate CORS headers to communicate directly with `:4318` from a browser.
