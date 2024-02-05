# REMOTE CODE EXECUTION AS A SERVICE

This repository contains the two stages of the `RCE as a Service` challenge for the [LosFuzzys](https://hack.more.systems/) `Glacier CTF` 2022.

The contents of `./stage1` and `./stage2` are almost identical. There are minor differences in the source code (`Program.cs`) in order to make stage 2 harder and the Dockerfiles specify different names and ports so that both stages can be run simultaneously.

The project itself is a `.NET6 Minimal Web API`. One of its endpoints compiles user-provided code on-the-fly.

I've written extensively about it [here](https://gebir.ge/blog/privesc-part-1/) and [here](https://gebir.ge/blog/privesc-part-2/), but I **strongly** suggest to only read those articles *after* trying your hands on the challenge.

## Installation

With `.NET6` being cross-platform, you should be able to compile the binaries yourself with the appropriate [tooling](https://dotnet.microsoft.com/en-us/download/dotnet/6.0) installed.

However, containerizing the applications with the help of the provided `Dockerfiles` is the recommended way. Have a look at the `build_and_start.sh` and `build_and_start_stage2.sh` scripts for a rough idea.

In order to verify connectivity, you can send a `GET` request to the root path of the application (stage 1):
```shell
curl --request GET \
  --url http://localhost:8001/
```
