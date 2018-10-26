# Fuzz-FFmpeg


### Build & Deploy
Step 1) Build the solution.
```
docker-compose up -d --build
```
Step 2) Drop into docker image.
```bash
docker exec -ti <DOCKER NAME HERE> bash
```
Step 3) Start your workload.
```bash
python3 /afl-utils/afl-multicore -c ffmpeg_afl_scripts/afl_mc_ffmpeg.json start 12
```
step 4) Collect stats!
```bash
python3 /afl-utils/afl-stats -c test.conf -d stats.db 
```


## Checking in

```bash
cd /ffmpeg_output#
cat */fuzzer_stats | grep unique_crashes | uniq
cat */fuzzer_stats | grep unique_hangs| uniq
```
