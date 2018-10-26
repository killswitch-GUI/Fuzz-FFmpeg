# fuzz-ffmpeg


### Build & Deploy
Step 1)
```
docker-compose up -d --build
```
Step 2)
```bash
docker exec -ti <DOCKER NAME HERE> bash
```
Step 3)
```bash
python3 /afl-utils/afl-multicore -c ffmpeg_afl_scripts/afl_mc_ffmpeg.json start 12
```
step 4)
```bash
python3 /afl-utils/afl-stats -c test.conf -d stats.db 
```


## checking in

```bash
cd /ffmpeg_output#
cat */fuzzer_stats | grep unique_crashes | uniq
cat */fuzzer_stats | grep unique_hangs| uniq
```
