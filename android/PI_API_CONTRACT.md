# Pi-to-Android API contract

The Android app connects to a Raspberry Pi service on a trusted local network. The phone does not receive raw ECG directly from the ESP32 or run ONNX inference.

## Endpoints used by this client

| Method | Path | Purpose |
| --- | --- | --- |
| `GET` | `/api/v1/status` | Check that the Pi bridge is online before opening the stream. |
| `WS` | `/api/v1/events` | Receive device, session, and forecast events. |
| `POST` | `/api/v1/replay/start` | Start POS102 or NEG024 replay with JSON `{"recording_id":"POS102"}`. |

The current app does not request session-list or session-detail endpoints. Its History screen stores completed summaries locally.

## Event envelope

Each WebSocket event has `type`, `schema_version`, `session_id`, `seq`, `timestamp_utc`, and `mode` (`live`, `replay`, `model_validation`, or `ui_demo`). The app uses `session_id` and increasing `seq` to avoid mixing and duplicating events.

### `device.status`

`pi_connection` and `pcb_connection` indicate `connected`, `connecting`, or `disconnected`. The Pi reports the physical device's state; switching views in the phone does not change the ESP32 mode.

### `session.state`

`phase` (`ready`, `collecting`, `processing`, `result`, `paused`, `stopped`, or `error`), `received_segments` or `valid_segments`, `elapsed_seconds`, and `message`. A real live observation is 600 seconds; the app may visually interpolate the clock between Pi updates, but the Pi's sample count and scoring state stay authoritative.

### `forecast.result`

`forecast_id`, `score`, optional numeric `threshold`, `quality`, `horizon_minutes`, and `model_id`, plus the common envelope. The app colors a result red only when a finite score is at or above a finite Pi-supplied threshold. Without a threshold, interpretation is unavailable. Replay results remain labeled as prerecorded simulations.

### Other recognized events

`signal.quality` accepts `valid`, `good`, `checking`, `low`, `poor`, `gap`, `data_gap`, or `unavailable`. `ecg.preview` may contain bounded display-only waveform `values` and `units`. `forecast.error` provides a `message` without a completed result.

## Example

```json
{
  "type": "session.state",
  "schema_version": 1,
  "session_id": "example-session",
  "seq": 12,
  "timestamp_utc": "2026-11-20T07:00:00Z",
  "mode": "live",
  "phase": "collecting",
  "received_segments": 3,
  "elapsed_seconds": 95,
  "message": "Collecting the 10-minute live ECG observation"
}
```

The development service uses port 8080 over HTTP/WebSocket. It is intended for an isolated local demo network, not direct Internet exposure.
