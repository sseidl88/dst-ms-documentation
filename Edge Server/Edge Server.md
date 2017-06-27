> The Edge Server `(Spring Cloud ZUUL)` provides an authentication entry point and routing rules for all requests in the platform.

Github project: [https://github.com/in-the-keyhole/dst-edge](https://github.com/in-the-keyhole/dst-edge)


`ZUUL` allows routing filter rules to be applied. The configuration below in the `application.yml` file routes `API` calls to services and to `static` content. 


    zuul:
      ignoredServices: '*'
      routes:
          api:
            path: /api/**
            url: http://localhost:8083
            stripPrefix: false
          static:
            path: /**
            url: http://localhost:4200
