# Projects

1. aether - go package for editing, publishing to redis
1. aether-http - on mw2017 branch
  - this serves http and handles websocket connections
  - must be running
  - aether-http is a git submodule of this repository
1. realtime-fft-experiment - python time stretcher
  - audio i/o devices must be configured in `run.py`
  - depends on py libs sounddevice, scipy, numpy
  - received audio via soundflower from reaper
  - should output audio directly to our main audio output
  - must be running
  - to control via touch osc, can update send-ip in `run.py`, and the send ip address in our touchosc app
1. stretchosc - go package for sending osc commands to realtime-fft-experiment

**Important** Redis must also be running on the default port

# Reaper project

For some reason the virus patch does not always work initially. When opening the project we have to go and manually load the virus preset in the vst editor.