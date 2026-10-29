# TTS service discovery

This repository contains only the current public address of a personal text-to-speech service. It contains no API keys, model weights, or audio recordings.

Clients should fetch `endpoint.json`, read `api_base_url`, and POST JSON `{ "text": "..." }` to `/tts`, authenticating with their separately configured `Authorization: Bearer ...` key. The response is WAV audio.

Resolve the manifest at startup, cache it for 60 seconds, and resolve it again after connection failures. Use a timestamp query parameter and `Cache-Control: no-cache` to reduce stale cache responses. GitHub caching and network failures may still delay updates. If `enabled` is false, retry later. Do not forward the TTS key to GitHub; it is sent only to the validated service host.

Only trust an HTTPS `*.trycloudflare.com` service hostname without URL credentials, query, fragment, or custom port. The manifest is address discovery, not a fixed reverse proxy. The host computer must remain online; interruptions during recovery are expected.
