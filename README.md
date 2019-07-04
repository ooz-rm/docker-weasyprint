---
title: WeasyPrint HTML to PDF Microservice
description: A ready to use, OpenShift compatible, HTML to PDF microservice for your application.
author: WadeBarnes
resourceType: Components
personas: 
  - Developer
  - Product Owner
  - Designer
labels:
  - weasyprint
  - html
  - pdf
  - microservice
---
# WeasyPrint HTML to PDF Microservice

The [docker-weasyprint](https://github.com/robertomorelli/docker-weasyprint) project bundles [Weasyprint](http://weasyprint.org/) into an easy to use, OpenShift compatible, HTML to PDF microservice with a simple REST interface.

# Images

Pre-built images can be found here; [robertomorelli/weasyprint](https://hub.docker.com/r/robertomorelli/weasyprint)

`docker pull robertomorelli/weasyprint`

# Usage - Docker Example

Run the docker image, exposing port 5001

```
docker run -p 5001:5001 robertomorelli/weasyprint
```

A `POST` to `/pdf` on port 5001 with an html body will result in a response containing a PDF. The filename may be set using a query parameter, e.g.:

```
curl -v -X POST -d @test.html -JLO http://127.0.0.1:5001/pdf?filename=result.pdf
```

This example will use the file `test.html` and return a response with `Content-Type: application/pdf` and `Content-Disposition: inline; filename=result.pdf` headers.  The body of the response will be the PDF rendering of the html document.

The [presentational hints](https://www.w3.org/TR/html/rendering.html#the-css-user-agent-style-sheet-and-presentational-hints) can be enabled with the query paramneter `presentational-hints`:

```
curl -v -X POST -d @test.html -JLO http://127.0.0.1:5001/pdf?filename=result.pdf&presentational-hints=true
```

In addition `/health` is a health check endpoint and a `GET` returns 'ok'.
