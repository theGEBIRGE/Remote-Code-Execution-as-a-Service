# RCE as a Service (Stage 2)
## Details
- Category: Web
- Domain: localhost
- Port: 8002
- Author: GEBIRGE

## Description

It came to our attention that a highly advanced `APT` targeted our `edge computing system`. In order to stop the attacks, we implemented *even more advanced* mitigations.

Think `seccomp`, but for the `web`!

Now there's **no** way an attacker could run malicious code, right?

(Goal: Read `flag.txt` at the filesystem's root.)

## Deployment

A `Dockerfile` is provided together with the `build_and_start_stage2.sh` script. Depending on the use case, you might have to change the script. The `podman` command can simply be replaced with `docker`.
The important part is to map port 8080 *inside* the container to port 8001 of the host.

In order to verify connectivity, you can send a `GET` request to the root path of the application:
```shell
curl --request GET \
  --url http://localhost:8002/
```

Files to include for participants:
+ `Program.cs` for the source code (to highlight the difference to stage 1)
+ `api_usage.md` for curl examples ("legit" usages of the fishy endpoint)

## Solution

You can have a look at `curl_stage2.org` for possible solution payloads.

Basically we now block `IO` operations through the standard library with a simple regex.
One possible solution could be to compile a custom .NET6 library that `does` use `System.IO` and load it dynamically *inside* our request to do the necessary flag reading operation.

Otherwise I've written extensively about it [here](https://gebir.ge/blog/privesc-part-1/) and [here](https://gebir.ge/blog/privesc-part-2/).
