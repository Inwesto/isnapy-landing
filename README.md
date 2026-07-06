# iSnapy landing — layered live-video version

Updated landing page with:
- layered hero composition: phones, videos, glove clash overlay, VS badge, caption
- default live video source set to `https://staging-api.isnapy.com`
- random video endpoint: `/landing/random-videos?limit=24`
- real `<video>` playback inside the iPhone screens
- `object-fit: cover` + `object-position: center center` so videos fill phone frames without stretching
- `glove-clash.png` as separate overlay asset with alpha transparency

## Files to upload/replace in GitHub

Upload/replace these files in the GitHub `isnapy-landing` repo:
- `index.html`
- `logo.png`
- `glove-clash.png`
- `README.md`
- `CNAME`

## Backend endpoint expected

The default API is staging:

```js
https://staging-api.isnapy.com/landing/random-videos?limit=24
```

Expected response:

```json
{
  "videos": [
    {
      "id": 1,
      "video_url": "https://staging-api.isnapy.com/media/videos_processed/video_1_mobile.mp4",
      "thumbnail_url": "https://staging-api.isnapy.com/media/thumbnails/video_1.jpg",
      "battle_power": 51
    }
  ]
}
```

The landing intentionally does not use the thumbnail as the visible poster layer. The phone frames should show real muted autoplay video.

## Override API for testing

Production/staging can be switched without editing files:

- staging default: `https://isnapy.com`
- explicit staging: `https://isnapy.com/?api=https://staging-api.isnapy.com`
- production later: `https://isnapy.com/?api=https://api.isnapy.com`

## Browser checks

Open DevTools console and look for:

```text
iSnapy landing videos loaded from https://staging-api.isnapy.com/landing/random-videos?limit=24
```

If videos do not play, test one returned URL directly:

```bash
curl -I https://staging-api.isnapy.com/media/videos_processed/video_1_mobile.mp4
```

Expected:

```text
HTTP/1.1 200 OK
content-type: video/mp4
```

CORS test:

```bash
curl -I -H "Origin: https://isnapy.com" https://staging-api.isnapy.com/landing/random-videos?limit=2
```

Expected:

```text
access-control-allow-origin: https://isnapy.com
```
