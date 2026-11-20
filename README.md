
name: GTA Auto Clips

on:
  workflow_dispatch:
    inputs:
      stream_url:
        description: "Paste permitted YouTube Live Replay URL"
        required: true
        type: string

jobs:
  prepare:
    runs-on: ubuntu-latest
    steps:
      - name: Check video URL
        env:
          VIDEO_URL: ${{ inputs.stream_url }}
        run: |
          if [[ "$VIDEO_URL" =~ ^https://(www\.)?(youtube\.com|youtu\.be)/ ]]; then
            echo "YouTube URL received successfully"
          else
            echo "Invalid YouTube URL"
            exit 1
          fi
