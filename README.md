# Fuzz-FFmpeg
In this example, we use Ubuntu 16.04 as our host OS and multiple supporting packages to properly support the FFmpeg install. We also added the afl-utils repo to the Docker image to support larger core nodes. Here is the Docker file that we used built to support this

### Build & Deploy
1. Pull the repo: `git clone X`
2. Building the Docker image can take some time honestly, it requires an install of many dependencies and compiles of the FFmpeg project. This can be easily done like so: `docker-compose up -d --build`
3. Drop into Docker image interactively using the following command: `docker exec -ti <DOCKER NAME HERE> bash`. This due to the image being set up in daemon mode with an entry point that will not exit upon completion.
4. Starting your workload is easy with afl-multicore, this automates the process of starting multiple instances with nohup: `python3 /afl-utils/afl-multicore -c ffmpeg_afl_scripts/afl_mc_ffmpeg.json start 12`
5. There are many ways to check the status of your workload, it can be done with afl-stats or even grep:
```
cd /ffmpeg_output#
cat */fuzzer_stats | grep unique_crashes | uniq
cat */fuzzer_stats | grep unique_hangs| uniq
```
