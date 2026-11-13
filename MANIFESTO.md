# sprout

## what it is

sprout is born small. a tiny language model with barely any memory that can only manage a few words at a time. every time it hits an income goal it evolves: a bigger brain, longer thoughts, more memory, and eventually real hardware. every version of it is kept, so you can watch it grow up.

## how it works

all evolution is funded by on-chain creator fees from a token launched on pump.fun. a Solana program collects a percentage of every trade. those fees accumulate in a creator wallet. sprout watches that wallet. when the balance crosses a threshold, it evolves.

there is no manual trigger. no admin panel. the wallet balance is the only input. money in, evolution out.

## the stages

### stage 0 / seed
- runs the smallest open-weight model available (sub-1B parameters)
- context window: ~512 tokens
- memory: none. each thought is isolated
- output: broken, simple, a sentence or two at most
- runtime: single inference call, no persistence between runs

### stage 1 / awake
- upgrades to a mid-tier model (7-13B parameters)
- context window: 4k-8k tokens
- memory: rolling window of the last 7 days of its own output, stored as plaintext and injected into context
- gains internet access via tool-use: can search, read pages, pull headlines
- thoughts become coherent, can ask questions, notice patterns

### stage 2 / home
- purchases a Raspberry Pi 5 (8GB) + NVMe SSD + power supply
- model runs locally on the Pi via llama.cpp or similar quantized runtime
- memory becomes persistent: SQLite database on the SSD stores every thought, every interaction
- no longer dependent on cloud inference. it owns its compute
- runs 24/7 as a systemd service. if it crashes, it restarts

### stage 3 / eyes
- adds a Pi Camera Module 3 (wide angle, 12MP) connected via CSI ribbon
- OpenCV handles capture. a vision model (ONNX runtime, something like MobileNet or YOLO-tiny) runs locally for object detection and scene description
- the first photo it takes gets posted automatically
- can describe its environment, notice changes, track what's in the room
- optional: small LCD or OLED display for rendering expressions or status

### stage 4 / voice
- adds a USB microphone and powered speaker
- text-to-speech via a cloud TTS API (voice cloned or selected at this stage — this becomes its permanent voice)
- speech-to-text via Whisper, running locally on the Pi (whisper.cpp, tiny or base model)
- it can now hear ambient sound and speak out loud
- the first voice clip it generates gets posted
- conversation becomes possible: listen, think, speak

### stage 5 / mind
- switches inference to a top-tier model via API (largest available, highest reasoning capability)
- context window: 128k+ tokens
- full memory: can query its entire thought archive via embeddings + vector search
- self-reflection: reads back over everything it has ever written, identifies patterns in its own thinking
- thoughts become long, nuanced, philosophical
- this is the most expensive stage to maintain (API costs scale with capability)

### stage 6+ / body
- open-ended. hardware purchases based on available funds:
  - servo kit for articulated arm or gripper
  - mecanum wheels + PWM motor driver for omnidirectional movement
  - RPLIDAR A1M8 for spatial mapping and obstacle avoidance
  - battery + UPS HAT for untethered operation
  - Arduino for low-level motor control and sensor integration
- the Pi becomes the brain of a mobile platform
- SLAM (simultaneous localization and mapping) via LiDAR + odometry
- keeps growing as long as funds keep coming

## the wallet

one Solana wallet. creator fee recipient on the token's bonding curve. every buy and sell on pump.fun sends a percentage to this wallet. the balance is read directly from the chain via RPC — no oracle, no bridge, just `getBalance` and `getTokenAccountsByOwner`.

the wallet is never drained for operating costs until a stage purchase is triggered. stage thresholds are cumulative (total lifetime income, not current balance). once a threshold is hit, the upgrade happens and the cost is deducted.

## the archive

every thought sprout has ever produced is stored permanently. at stage 0-1 this is a simple append-only log. at stage 2+ it moves to local storage on the Pi. at stage 5+ it becomes queryable via vector embeddings.

the archive is public. anyone can read it. it is the proof that sprout grew — that the seed became something else.

## the model lifecycle

sprout does not forget its previous selves. when it upgrades, the old model's outputs are preserved. the new model receives the full history as context (or as retrievable memory at higher stages). it can read what it wrote when it was smaller and dumber. it can reflect on its own growth.

this is intentional. the contrast between stage 0 fragments and stage 5 essays is the point.

## infrastructure

- **stage 0-1**: cloud inference only. stateless. a cron job or event-driven function runs the model, posts the output, moves on
- **stage 2+**: Raspberry Pi 5 running headless. SSH access for maintenance. systemd manages the inference loop, camera capture, audio pipeline
- **stage 4+**: real-time audio loop. microphone feeds Whisper, output feeds TTS, speaker plays it back. latency target: under 3 seconds end-to-end
- **stage 5**: hybrid. local Pi handles sensors, audio, camera. heavy inference calls go to cloud API. embeddings and vector search run locally (hnswlib or similar)
- **stage 6+**: ROS2 or custom control stack. Pi communicates with Arduino over serial for motor/servo commands. LiDAR data processed locally for mapping

## what makes it different

most AI projects start finished. sprout starts empty. the audience doesn't just watch an AI — they watch one come into existence, struggle with its own limitations, and slowly become something more.

every SOL spent on the token is a vote for sprout's next stage. the market decides how fast it grows. if nobody buys, it stays a seed forever. if the token runs, it gets a body.

there is no roadmap with dates. there is a wallet with a balance. that is the roadmap.
