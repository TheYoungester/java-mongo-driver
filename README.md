[![Build Status][ci-img]][ci] [![Coverage Status][cov-img]][cov] [![Released Version][maven-img]][maven]

# OpenTracing Mongo Driver Instrumentation
OpenTracing instrumentation for Mongo Driver.

## Installation

pom.xml
```xml
<dependency>
    <groupId>io.opentracing.contrib</groupId>
    <artifactId>opentracing-mongo-driver</artifactId>
    <version>0.0.4</version>
</dependency>
```

## Usage

```java
// Instantiate tracer
Tracer tracer = ...


// Instantiate Synchronous Tracing MongoClient
MongoClient mongoClient = new TracingMongoClient(tracer, ...);

// Instantiate Asynchronous Tracing MongoClient
MongoClient mongoClient = new TracingAsyncMongoClient(tracer, ...);

```

### Mongo Span Name
By default, span names are set to the operation performed by the Mongo client. To customize the span name, provide a MongoSpanNameProvider to the client that alters the span name. If a provder is not provided, the span name will remain the default.

```java
// Create TracingMongoClient with custom span name
TracingMongoClient client = new TracingMongoClient(
    tracer, 
    replicaSetAddresses, 
    credentials, 
    clientOptions, 
    new PrefixSpanNameProvider("mongo."));
Document doc = new Document();
client.getDatabase("db").getCollection("collection).insertOne(doc);
// Span name is now set to "mongo.insert"
```

## License

[Apache 2.0 License](./LICENSE).

[ci-img]: https://travis-ci.org/opentracing-contrib/java-mongo-driver.svg?branch=master
[ci]: https://travis-ci.org/opentracing-contrib/java-mongo-driver
[cov-img]: https://coveralls.io/repos/github/opentracing-contrib/java-mongo-driver/badge.svg?branch=master
[cov]: https://coveralls.io/github/opentracing-contrib/java-mongo-driver?branch=master
[maven-img]: https://img.shields.io/maven-central/v/io.opentracing.contrib/opentracing-mongo-driver.svg
[maven]: http://search.maven.org/#search%7Cga%7C1%7Copentracing-mongo-driver
