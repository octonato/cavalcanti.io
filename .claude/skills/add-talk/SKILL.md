---
name: add-talk
description: Publish a new talk on the Talks page, or update an existing one, from a YouTube video or a slide deck folder under static/presentations/.
argument-hint: <youtube-url | youtube-id | presentations-folder>
---

Publish or update a talk from this source: `$ARGUMENTS`

If the argument is empty, ask for a YouTube URL or a folder under `static/presentations/`, then stop.

## How talks work

- Each talk is one file in `content/talks/<slug>.md`, with TOML front matter.
- The Talks page lists every file in `content/talks/` automatically. Do not edit `content/talks/_index.md`.
- Read two or three files in `content/talks/` before writing. Match their front matter, tone and length.

Front matter keys:

| Key | Set when | Value |
|---|---|---|
| `title` | always | Talk title |
| `date` | always | Date of the talk, `YYYY-MM-DD` |
| `description` | always | One sentence for the talk tile |
| `youtube` | video | YouTube video ID |
| `duration` | video | Video length in seconds |
| `slides` | slides | Folder name under `static/presentations/` |
| `thumbnail` | slides | `/presentations/<folder>/img/<file>` |

The list layout uses the YouTube thumbnail when `youtube` is set, else `thumbnail`. It shows the duration only when `duration` is set.

Body layout, in this order:

```
{{< youtube <id> >}}

{{< slides <folder> >}}

<summary paragraph>

Recorded at <event>.
```

Keep only the shortcodes the talk has. Use "Presented at <event>." when the talk has no video.

## Steps

### 1. Identify the source

- A YouTube URL or an 11-character ID is a **video**. Extract the ID from `watch?v=`, `youtu.be/`, `/live/` or `/embed/` URLs.
- Anything else is a **deck**. Accept a folder name or a path. Resolve it to `static/presentations/<folder>/`. Check that `index.html` exists there. If not, list the folders in `static/presentations/` and ask.

### 2. Find the talk to update

Grep `content/talks/` for `youtube = "<id>"` or `slides = "<folder>"`.

- One match: update that file.
- No match: list the existing talks (title, date, and whether each has a video and slides). Ask whether the source belongs to one of them or starts a new talk. Suggest the most likely match by title.

### 3. Gather metadata

**Video.** Download the watch page:

```
curl -sL -H "Accept-Language: en" "https://www.youtube.com/watch?v=<id>" -o "$TMPDIR/yt.html"
```

Then grep it for these JSON fields. Take the first match of each.

- `"title":"…"`: the video title. Drop the speaker name and any event suffix, like " by Renato Guerra Cavalcanti".
- `"lengthSeconds":"…"`: the `duration`.
- `"publishDate":"…"`: the default `date`.
- `"shortDescription":"…"`: the source for the summary and the event name.

If the download fails or the fields are missing, ask for the values.

**Deck.**

- Title: the `<title>` tag of `index.html`.
- Content: extract the slide text from `index.html`. Strip tags, styles and scripts. Use it for the summary.
- Thumbnail: list the images in `img/`. If there is one, use it. If there are several, ask which one. If there is none, ask for an image path.
- Date and event: ask. A deck has no reliable date.

### 4. Draft the file

**New talk.**

- Slug: the title in lowercase kebab case, without punctuation. Check that `content/talks/<slug>.md` does not exist.
- Write the front matter and body as shown above.
- `description`: one sentence, under 120 characters.
- Summary: one paragraph of 3 to 5 short sentences, in the voice of the existing talks.

**Existing talk.**

- Add the keys and the shortcode for the new source. Keep the existing title, date, description and summary unless the user asks to change them.
- A video and a deck can both be on one talk. Keep the `thumbnail` key when you add a video.
- If the talk already has the source, refresh its derived key. Set `duration` for a video and `thumbnail` for a deck. Ask what else to change.

Show the full draft and ask for approval or edits. Write the file only after approval.

### 5. Check the build

Run `hugo --destination "$TMPDIR/talks-check"`. Report errors. Delete `$TMPDIR/talks-check` afterwards.

Report the file path and the talk URL: `/talks/<slug>/`. Do not commit.
