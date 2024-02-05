# RCE as a Service (Stage 1)
## Details
- Category: Web
- Domain: localhost
- Port: 8001
- Author: GEBIRGE

## Description

Cloud computing is trending? Says your **grandpa**!

`Edge Computing` is the future! And the future is now. Today!

Give us a lambda and an array to operate on and our modern `.NET6`-powered backend will compute the results on an edge near your user in *no time*.

But please don't try to run custom code, because [this incident will be reported](https://imgs.xkcd.com/comics/incident.png).

(Goal: Read `flag.txt` at the filesystem's root.)

## Deployment

A `Dockerfile` is provided together with the `build_and_start.sh` script. Depending on the use case, you might have to change the script. The `podman` command can simply be replaced with `docker`.
The important part is to map port 8080 *inside* the container to port 8001 of the host.

In order to verify connectivity, you can send a `GET` request to the root path of the application:
```shell
curl --request GET \
  --url http://localhost:8001/
```

Files to include for participants:
+ `Program.cs` for the source code (makes the challenge more clear, I think)
+ `api_usage.md` for curl examples ("legit" usages of the fishy endpoint)

## Solution

You can have a look at `curl.org` for possible solution payloads.

Hints for players:

Our endpoint `/rce` takes a query in the form of a [lambda expression]((https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions)) and a string array to operate on.

Otherwise I've written extensively about it [here](https://gebir.ge/blog/privesc-part-1/) and [here](https://gebir.ge/blog/privesc-part-2/).



