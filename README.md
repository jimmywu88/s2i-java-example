# s2i-java-example

This example is intentionally NOT using Spring Boot, Vert.x or whatever other simple (non-containerized) Java
server framework, but for clarify shows how to launch any Java application with a class with a main() method
(using the Java built-in com.sun.net.httpserver.HttpServer; *JUST* for illustration of S2I).


## Local

For local building, install s2i either from source https://github.com/openshift/source-to-image/releases/ or e.g. via:

    sudo dnf install source-to-image

Now to build the simplest possible Java server with OpenShift Source-To-Image (S2I) using the fabric8io-images/s2i builder:

    s2i build https://github.com/vorburger/s2i-java-example fabric8/s2i-java vorburger:s2i-java-example

or

    git clone https://github.com/vorburger/s2i-java-example ; cd s2i-java-example
    s2i build . fabric8/s2i-java vorburger:s2i-java-example

Now run it like this:

    docker run -p 8080:8080 vorburger:s2i-java-example

and see "hello, world" when accessing http://localhost:8080 - it works!


## OpenShift

To do the same as above directly inside your OpenShift instance:

    TODO


## Advanced

### Container options

All options documented on https://github.com/fabric8io-images/s2i/tree/master/java/images/jboss
are typically specified in [`.s2i/environment`](.s2i/environment), but  for quick testing can obviously also be specified on the `docker run` CLI like so:

    docker run -e "JAVA_MAIN_CLASS=ch.vorburger.openshift.s2i.example.Server" -p 8080:8080 vorburger:s2i-java-example


### fabric8io-images/s2i local build

If you do not like to use the possibly not latest fabric8/s2i-java from hub.docker.com you can of course first also just:

    docker build https://github.com/fabric8io-images/s2i.git#master:java/images/jboss


## TODO points

* Why aren't changes taken into account on 2nd build?
* Why isn't it incremental?  Keep re-downloading Maven basics, every time..
* Support Gradle!
* Monitoring..


## More background

* https://github.com/fabric8io-images/s2i
* https://github.com/fabric8io-images/s2i/tree/master/java/images/jboss
* https://github.com/fabric8io-images/s2i/issues/112
