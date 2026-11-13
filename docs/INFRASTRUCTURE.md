# infrastructure

This is the design of what sprout runs on. No implementation is published in this repository.

```
   stage 0-1          stage 2+             stage 5              stage 6+

   ┌──────────┐      ┌──────────┐      ┌──────────┐      ┌──────────┐
   │  cloud   │ ───> │  pi 5    │ ───> │  pi 5    │ ───> │  pi 5    │
   │ function │      │ headless │      │ + cloud  │      │ + arduino│
   └──────────┘      └──────────┘      └──────────┘      └──────────┘
    stateless         owns its          hybrid            mobile
                      compute                             platform
```

## stage 0-1: cloud only

Cloud inference only, and stateless. A cron job or event-driven function runs the model, posts the output, and moves on.

## stage 2+: the Pi

A Raspberry Pi 5 running headless, with SSH access for maintenance. systemd manages the inference loop, and later the camera capture and the audio pipeline.

## stage 4+: the audio loop

A real-time loop: the microphone feeds Whisper, the output feeds text-to-speech, and the speaker plays it back.

```
   microphone ──> whisper ──> think ──> tts ──> speaker

   latency target: under 3 seconds end-to-end
```

## stage 5: hybrid

The local Pi handles sensors, audio and camera. Heavy inference calls go to a cloud API. Embeddings and vector search run locally, with hnswlib or similar.

## stage 6+: control

ROS2 or a custom control stack. The Pi talks to an Arduino over serial for motor and servo commands. LiDAR data is processed locally for mapping.

| layer | runs on | does |
|---|---|---|
| reasoning | cloud API | the heavy thinking |
| perception | Pi | camera, audio, LiDAR, embeddings |
| control | Arduino | motors and servos |
