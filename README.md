# PySimple
A very simple [Python] application. Using the material in Docker's
[Get Started] guide this is a simple (classic) Python-based web-app
that uses Flask and Redis. You don't have to understand any of this,
the goal of this project is simply to provide a stable base for
demonstrating Docker.

You should be able to build and run the containerised app using
any suitably equipped Docker host. I used a `Mac` and Docker
community edition `v18.09.2`.

## Building
Build and tag the image...

    $ docker build -t friendlyhello .

And run it (in detached/non-blocking mode)...

    $ docker run -d -p 4000:8080 friendlyhello
    <container ID>

This will start the image as a container and map host port `4000` into the
container's on port `8080`. This port re-mapping is an essential part of the
Docker ecosystem. The _long-and-short_ of all of this is that you should now
be able to connect to the app at `http://localhost:4000`:

    $ curl http://localhost:4000
    
Now stop your container and remove the stopped container using its ID:

    $ docker stop <container ID>
    $ docker rm <container ID>

You can also use `docker-compose` and the built-in `docker-compose.yml`
configuration file to spin-up more than one container. In our compose
file also start a [Redis] container, a simple database that the app will
use (if it can) to count the number of visits made to its port.

    $ docker-compose build
    $ docker-compose up --detach

>   The docker-compose configuration exposes the application container
    using port 8080 on the local host.

And stop and remove the containers with: -

    $ docker-compose down
     
## Deploying to Docker Hub
Here, we'll deploy to the Docker hub. It's free and simple. We just need to
tag our image (with something useful like `2019.1`) and then push it.

    $ docker login -u alanbchristie
    [...]
    $ docker tag friendlyhello alanbchristie/pysimple:2019.1
    $ docker push alanbchristie/pysimple:2019.1

>   Here my hub account is `alanbchristie` and the registry there
    is `pysimple`. We're giving this image the tag `2019.1`.
    
>   Tags are handled very differently in Docker, it does not understand
    that `1` is better than `2` - they're just strings that happen to
    also be numbers.

With the Docker image pushed we can now _pull_ the application onto any
Docker-enabled machine and run it with the command:

    $ docker run -d -p 4000:8080 alanbchristie/pysimple:2019.1
    Unable to find image 'alanbchristie/pysimple:2017.1' locally
    2019.1: Pulling from alanbchristie/pysimple
    [...]

---

_Alan B. Christie_  
_September 2017_  

[Get Started]: https://docs.docker.com/get-started/part2/
[Python]: https://www.python.org
[Redis]: https://redis.io