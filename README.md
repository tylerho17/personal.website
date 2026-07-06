# tyler ho — personal website

a private archive made public. the homepage is a letter, the archive is a contact sheet, field notes are a notebook, and selected work is an empty folder waiting for the next thing.

plain html / css / js. no frameworks, no build step, no dependencies. works on any static host (vercel, github pages).

## pages

| file | what it is |
|---|---|
| `index.html` | the letter — opening title card, then a short centered letter |
| `archive.html` | photographs — chronological contact sheet with a viewing-room modal |
| `field-notes.html` | notes — a notebook page holding real notes and future sections |
| `selected-work.html` | work — intentionally empty room, reserved for coding projects |
| `index-redesign_23_1.html` | old homepage filename, now just a redirect to `index.html` |
| `favicon.svg` | site favicon |
| `Photos/` | original photographs (never renamed, never compressed below web quality) |
| `Photos/thumbs/` | small 560px thumbnails used by the archive grid |

## how to preview locally

```bash
cd "personal.website"
python3 -m http.server 4321
# open http://localhost:4321
```

(any static file server works — the site is plain files.)

## how to maintain the archive

everything lives in **one array** in `archive.html` — search for `const archiveItems`.

each photo is one block:

```js
{
    file: 'my-photo.jpeg',            // exact filename inside Photos/ (case-sensitive!)
    title: 'short lowercase title',
    date: 'june 2026',                // what visitors see
    sortDate: '2026-06',              // yyyy-mm, for keeping order straight
    location: 'new york city',
    chapter: 'technology / new york', // museum-label grouping
    shortCaption: 'one honest line shown on hover and on the card front.',
    expandedCaption: 'the full story, shown when the card is flipped.',
    meaning: 'what it means, comma separated.',
    tone: 'editorial note to self — not displayed.',
    alt: 'plain description of the image for screen readers.',
},
```

### to add a photo

1. drop the image into `Photos/` (lowercase-hyphenated filename, `.jpeg`)
2. make a thumbnail (mac):
   ```bash
   cd Photos
   sips -s format jpeg -s formatOptions 70 -Z 560 "my-photo.jpeg" --out "thumbs/my-photo.jpeg"
   ```
   (if you skip this step the archive still works — it falls back to the original automatically, just loads slower.)
3. copy any block in `archiveItems`, edit the fields, and paste it in chronological position — **array order controls display order**, oldest first.

### to reorder / edit

cut and paste blocks in the array, or edit fields directly. no other file needs touching.

### rules that keep deploys working

- filenames are **case-sensitive** in production (`business-fraternity.JPG` must keep its uppercase extension)
- never rename or delete originals in `Photos/`
- keep originals under ~700kb where possible (compress big ones with `sips -s format jpeg -s formatOptions 75 -Z 1600`)
