# Musicoin 3.0 – Web Music Player

## Overview

The Musicoin 3.0 Web Music Player is a reference client for playing
music registered in the Musicoin ecosystem. The focus is not on building
a full commercial streaming service, but on demonstrating:

- How to link on-chain metadata with off-chain audio files
- How to trigger the original Musicoin-style value distribution model
- How to display track and artist information stored in the smart contract

## Core Goals

- Play registered tracks using a simple web player
- Show on-chain data:
  - Track ID, artist, album, tags
  - Per-play economic model (e.g. revenue split)
- Trigger on-chain or off-chain accounting for each playback

## Key Features

- Track list with filter / search
- Playback controls:
  - Play / pause / seek
  - Playlist support
- Display:
  - Artist name, homepage, Twitter/X link
  - Track metadata and hash
- Integration with Musicoin 3.0 smart contract:
  - Retrieve track metadata and revenue distribution schema
  - Optionally notify smart contract or accounting server on play events

## Architecture

- **Frontend**: Web SPA (e.g. React with HTML5 audio element)
- **Backend**:
  - Metadata API (optional)
  - Storage for audio files (S3, IPFS gateway, or other)
- **Blockchain**:
  - Smart contract that stores:
    - Track IDs and hashes
    - Artist address
    - Distribution configuration

## Playback Flow (Example)

1. Load track list from indexer / API
2. For selected track:
   - Fetch metadata from Musicoin 3.0 contract
   - Fetch audio URL from off-chain storage
3. Start playback in browser
4. On playback event (e.g. complete or threshold):
   - Record play event off-chain
   - Optionally call contract function (`recordPlay(...)`) to log usage

## Roadmap

1. MVP: single-track playback with on-chain metadata
2. Playlist and basic library UI
3. Integration with sampling studio (re-using audio resources)
4. Mobile-friendly responsive UI

## Contribution

- New UI components for playlist and queue
- Advanced features (EQ, waveform display, etc.)
- Optimization for low-bandwidth environments

## License

TBD.
