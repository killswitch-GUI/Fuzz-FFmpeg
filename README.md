# fuzz-ffmpeg


### Build & Deploy
```docker-compose up -d --build```

```bash
python3 /afl-utils/afl-multicore -c ffmpeg_afl_scripts/afl_mc_ffmpeg.json start 12
```

```bash
python3 /afl-utils/afl-stats -c test.conf -d stats.db 
```
