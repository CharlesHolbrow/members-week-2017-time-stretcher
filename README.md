# About

My Spring 2017 member's week demo combines 6 different git repositories and a reaper session.
Below are some quick strach notes about how they are all connected. If you've stumbled accross this by accident, this probably won't make much sense.

# Projects

1. `aether` - go package for editing, publishing to redis
1. `aether-http` - go server for serving frontend
  - uses mw2017 branch
  - this serves http and handles websocket connections
  - **must be running**
  - aether-js is a git submodule of this repository.
1. `realtime-fft-experiment` - python time stretcher
  - **must be running**
  - audio i/o devices must be configured in `run.py`
  - depends on py libs sounddevice, scipy, numpy
  - receives audio via soundflower from reaper
  - should output audio directly to our main audio output
  - to control via touch osc, can update send-ip in `run.py`, and the send ip address in our touchosc app
1. `stretchosc` - go package for sending osc commands to realtime-fft-experiment
1. `aether-js` - javascript frontend
  - submodule of the aether-http project
1. `aether-midi` go server listens for midi commands
  - **must be running**
  - receives midi from reaper, sends commands to redis via `aether` package

**Important:** Redis must also be running on the default port

# aether-js submodule

This is our client frontend inside the aether-http submodule. We will need to `$ git submodule init`, `$ git submodule update`, and `$ make` it.

# Reaper project

For some reason the virus patch does not always work initially. When opening the project we have to go and manually load the virus preset in the vst editor.

# Setup

`$ export $GOPATH=$(pwd)`

To pull submodules, use:

`$ git submodule init`
`$ git submodule update`

Then repeat submodule init for `aether-js` inside of `aether-http`.

Configure input/output

1. Create aggregate audio device builtin/soundflower/babyface so reaper can send to multiple outputs
1. Reaper stretchable audio (from master track) to soundflower
1. Reaper sends midi to virtual midi port
1. `aether-midi` receives midi on same virtual midi port
1. `realtime-fft-experiment` received audio from soundflower, sends to babyface
1. `$ go install` and run `aether-midi` and `aether-http`
1. If we have a conda env for realtime-fft-experiment, `$ source activate audio` and `$python run.py` inside of `realtime-fft-experiment` dir
