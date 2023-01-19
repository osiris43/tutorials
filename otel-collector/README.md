# OpenTelemetry Collector with Filtering and Tail Sampling

The configuration file in this folder will configure an [OpenTelemetry collector](https://github.com/open-telemetry/opentelemetry-collector) to send information to [Honeycomb](https://www.honeycomb.io/).  It is set up for traces but is easy to adapt for metrics as well.

The included Dockerfile will create an image that can be run in the container orchestration platform of your preference.

Once running locally, you can send events to it from applications enabled for OpenTelemetry.  To tinker with the setup, it's easy to create a small [Flask app](https://opentelemetry.io/docs/instrumentation/python/getting-started/) in Python.  

Traces have three processors set up.  

|Processor|Notes|
|-------|--------|
| [Filter](https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/processor/filterprocessor) | This processor has an `include` and `exclude` section.  The `include` only allows spans through that contain approved `service.namespace` attributes.  This is a way to protect against unexpected events getting into Honeycomb and counting against your event budget.|
| [Tail Sampling](https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/processor/tailsamplingprocessor) | This processor enables greater flexibility for determining what events get sampled than do the `Filter` alone or the `Filter` and `Probabilisitic Sampler` together.  The example here enables you to send all events with an `http.status_code` greater than 399 while also probabilistically sampling successful events.|
| Batch | This processor is recommended for all configurations to enable batch sending of events.|