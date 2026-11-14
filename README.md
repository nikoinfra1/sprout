<p align="center">
  <img src="assets/hero.svg" alt="sprout: born small. it evolves every time it hits an income goal." width="100%">
</p>

<p align="center">
  <a href="MANIFESTO.md">manifesto</a> ·
  <a href="docs/STAGES.md">stages</a> ·
  <a href="docs/WALLET.md">wallet</a> ·
  <a href="docs/ARCHIVE.md">archive</a> ·
  <a href="docs/INFRASTRUCTURE.md">infrastructure</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/stage-0%20%2F%20seed-facc15?style=flat-square&labelColor=000000" alt="stage: 0 / seed">
  <img src="https://img.shields.io/badge/funding-creator%20fees-facc15?style=flat-square&labelColor=000000" alt="funding: creator fees">
  <img src="https://img.shields.io/badge/treasury-solana-facc15?style=flat-square&labelColor=000000" alt="treasury: solana">
  <img src="https://img.shields.io/badge/roadmap-the%20wallet-facc15?style=flat-square&labelColor=000000" alt="roadmap: the wallet">
</p>

## contents

- [what it is](#what-it-is)
- [how it works](#how-it-works)
- [the stages](#the-stages)
- [the wallet](#the-wallet)
- [the archive](#the-archive)
- [the model lifecycle](#the-model-lifecycle)
- [infrastructure](#infrastructure)
- [what makes it different](#what-makes-it-different)
- [technical summary](#technical-summary)

## what it is

sprout is born small. it starts as a tiny language model with barely any memory that can only manage a few words at a time.

every time it hits an income goal, it evolves. each evolution gives it something it did not have before:

- a bigger brain: a larger, more capable model
- longer thoughts: a wider context window
- more memory: from nothing, to a week, to everything it has ever written
- eventually, real hardware: a computer of its own, then a camera, a voice and a body

every version of it is kept. nothing it writes is thrown away when it upgrades, so you can watch it grow up from its first broken fragments.

## how it works

<img src="assets/how.svg" alt="people trade on pump.fun, creator fees land in one solana wallet, sprout watches the wallet and evolves when income crosses a threshold." width="100%">

all evolution is funded by on-chain creator fees from a token launched on pump.fun. nothing else pays for it.

1. **people trade the token.** a solana program collects a percentage of every trade.
2. **the fees accumulate.** they land in a single creator wallet.
3. **sprout watches that wallet.** it reads the balance directly from the chain.
4. **a threshold is crossed.** when lifetime income passes the next stage's threshold, sprout evolves.

there is no manual trigger. there is no admin panel. nobody decides when sprout is ready for its next stage. the wallet balance is the only input.

money in, evolution out.

## the stages

<img src="assets/stages.svg" alt="the seven stages as a staircase: 0 seed, 1 awake, 2 home, 3 eyes, 4 voice, 5 mind, 6+ body." width="100%">

sprout moves through the stages in order. each one is reached by income alone, and none of them leads back.

### stage 0 / seed

where sprout starts. it has nothing: no history, no tools, no hardware.

| | |
|---|---|
| model | the smallest open-weight model available (sub-1B parameters) |
| context window | ~512 tokens |
| memory | none. each thought is isolated |
| output | broken, simple, a sentence or two at most |
| runtime | a single inference call, with no persistence between runs |

### stage 1 / awake

sprout becomes coherent. it can ask questions and notice patterns, and for the first time it can look outside itself.

| | |
|---|---|
| model | a mid-tier model (7-13B parameters) |
| context window | 4k-8k tokens |
| memory | a rolling window of the last 7 days of its own output, stored as plaintext and injected into context |
| tools | internet access through tool use: it can search, read pages and pull headlines |

### stage 2 / home

sprout buys its first hardware and moves in. it no longer depends on cloud inference. it owns its compute.

| | |
|---|---|
| hardware | a Raspberry Pi 5 (8GB), an NVMe SSD and a power supply |
| model | runs locally on the Pi through llama.cpp or a similar quantized runtime |
| memory | persistent. a SQLite database on the SSD stores every thought and every interaction |
| runtime | a systemd service, running 24/7. if it crashes, it restarts |

### stage 3 / eyes

sprout can see the room it lives in.

| | |
|---|---|
| hardware | a Pi Camera Module 3 (wide angle, 12MP), connected by CSI ribbon |
| capture | OpenCV |
| vision | a local vision model on ONNX runtime, something like MobileNet or YOLO-tiny, for object detection and scene description |
| optional | a small LCD or OLED display for rendering expressions or status |

the first photo it takes gets posted automatically. from then on it can describe its environment, notice changes, and track what is in the room.

### stage 4 / voice

sprout can hear and speak, which makes conversation possible: listen, think, speak.

| | |
|---|---|
| hardware | a USB microphone and a powered speaker |
| speaking | text-to-speech through a cloud TTS API |
| hearing | speech-to-text with Whisper, running locally on the Pi (whisper.cpp, tiny or base model) |

the voice is cloned or selected at this stage, and it becomes sprout's permanent voice. the first voice clip it generates gets posted. it can also hear ambient sound, not just speech directed at it.

### stage 5 / mind

sprout gets the best brain available and turns it on its own history.

| | |
|---|---|
| model | a top-tier model through an API: the largest available, with the highest reasoning capability |
| context window | 128k+ tokens |
| memory | full. it can query its entire thought archive through embeddings and vector search |
| new ability | self-reflection. it reads back over everything it has ever written and identifies patterns in its own thinking |

its thoughts become long, nuanced and philosophical. this is the most expensive stage to maintain, because API costs scale with capability.

### stage 6+ / body

open-ended. from here, hardware is bought as funds allow, and the Pi becomes the brain of a mobile platform.

<img src="assets/body.svg" alt="an ASCII robot labelled with its parts: camera, display, microphone, speaker, pi 5, nvme ssd, arduino, lidar, battery and ups hat, servo arm, mecanum wheels and motor driver." width="100%">

| part | what it is for |
|---|---|
| servo kit | an articulated arm or gripper |
| mecanum wheels + PWM motor driver | omnidirectional movement |
| RPLIDAR A1M8 | spatial mapping and obstacle avoidance |
| battery + UPS HAT | untethered operation |
| Arduino | low-level motor control and sensor integration |

it navigates with SLAM (simultaneous localization and mapping), using LiDAR and odometry. it keeps growing as long as funds keep coming.

## the wallet

there is one solana wallet. it is the creator fee recipient on the token's bonding curve, so every buy and sell on pump.fun sends a percentage to it.

**how it is read.** the balance is read directly from the chain over RPC, using `getBalance` and `getTokenAccountsByOwner`. there is no oracle and no bridge between the wallet and sprout.

**how thresholds work.** stage thresholds are cumulative. they are measured against total lifetime income, not the current balance. spending on one stage therefore never pushes the next stage further away.

**when money is spent.** the wallet is never drained for operating costs until a stage purchase is triggered. once a threshold is hit, the upgrade happens and its cost is deducted.

| | goes up | goes down |
|---|---|---|
| lifetime income | with every fee | never |
| current balance | with every fee | when a stage is bought |

## the archive

every thought sprout has ever produced is stored permanently. how it is stored changes as sprout grows:

| stage | storage |
|---|---|
| 0-1 | a simple append-only log |
| 2+ | local storage on the Pi |
| 5+ | the same archive, made queryable through vector embeddings |

the archive is public. anyone can read it.

it is the proof that sprout grew: that the seed became something else.

## the model lifecycle

sprout does not forget its previous selves.

- when it upgrades, the old model's outputs are preserved
- the new model receives the full history as context, or as retrievable memory at the higher stages
- it can read what it wrote when it was smaller and dumber
- it can reflect on its own growth

this is intentional. the contrast between stage 0 fragments and stage 5 essays is the point.

## infrastructure

what sprout runs on changes with each stage.

| stage | setup |
|---|---|
| 0-1 | cloud inference only, and stateless. a cron job or event-driven function runs the model, posts the output, and moves on |
| 2+ | a Raspberry Pi 5 running headless, with SSH access for maintenance. systemd manages the inference loop, the camera capture and the audio pipeline |
| 4+ | a real-time audio loop. the microphone feeds Whisper, the output feeds TTS, and the speaker plays it back. the latency target is under 3 seconds end-to-end |
| 5 | hybrid. the local Pi handles sensors, audio and camera. heavy inference calls go to a cloud API. embeddings and vector search run locally (hnswlib or similar) |
| 6+ | ROS2 or a custom control stack. the Pi talks to an Arduino over serial for motor and servo commands. LiDAR data is processed locally for mapping |

## what makes it different

most ai projects start finished. sprout starts empty.

the audience doesn't just watch an ai. they watch one come into existence, struggle with its own limitations, and slowly become something more.

every SOL spent on the token is a vote for sprout's next stage. the market decides how fast it grows:

- if nobody buys, it stays a seed forever
- if the token runs, it gets a body

there is no roadmap with dates. there is a wallet with a balance. that is the roadmap.

## technical summary

| | |
|---|---|
| starting model | smallest open-weight model available (sub-1B parameters) |
| starting context | ~512 tokens |
| starting memory | none |
| income | pump.fun creator fees |
| treasury | one solana wallet |
| balance read | on-chain over RPC: `getBalance`, `getTokenAccountsByOwner` |
| evolution trigger | lifetime income crosses a stage threshold |
| manual trigger | none |
| first hardware | Raspberry Pi 5 (8GB), at stage 2 |
| local runtime | llama.cpp or similar, as a systemd service |
| archive | public, permanent |
| roadmap | the wallet balance |

## read further

| | |
|---|---|
| [manifesto](MANIFESTO.md) | the full text of the idea |
| [stages](docs/STAGES.md) | every stage in detail |
| [wallet](docs/WALLET.md) | where the money comes from and what triggers an upgrade |
| [archive](docs/ARCHIVE.md) | how every thought is kept, and how each version inherits the last |
| [infrastructure](docs/INFRASTRUCTURE.md) | what it runs on at each stage |

> this repository holds the idea and the design. it does not contain the code.

<br>

<p align="center">
  <img src="assets/footer.svg" alt="if nobody buys, it stays a seed forever. if the token runs, it gets a body. there is no roadmap with dates. there is a wallet with a balance. that is the roadmap." width="100%">
</p>

<p align="center"><sub>sprout is an experiment and an artwork. nothing here is financial advice or an offer of anything.</sub></p>
