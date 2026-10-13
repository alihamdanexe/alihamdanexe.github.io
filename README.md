# Portfolio – how to maintain it

## Repo layout

```
index.html        the page (you should never need to edit it)
content.json      ALL text, links and photo assignments  <- you edit this
404.html          turns short links like /lab into section links
images/           put every photo here, original quality
    banner.jpg
    profile.webp
    lab-workspace.jpg
    ...
```

The page loads `content.json` and builds itself from it. Photos are shown as the original files you upload: nothing is resized or recompressed, so quality is never lost.
Upload the originals at the size you want people to see (a 2000 px wide photo is plenty), because the browser downloads the file as-is.

## Add or replace a photo

1. Upload the file into the `images/` folder on GitHub (Add file -> Upload files).
2. Open `content.json`, find the item, and set `"image"` to the exact file name, for example `"image": "lab-robotic-arm.jpg"`.
   Names are case-sensitive: `Arm.JPG` and `arm.jpg` are different files. Avoid spaces.
3. Commit. The site updates in a minute or two (hard refresh with Ctrl+Shift+R if you still see the old one).

To replace a photo without touching the JSON, upload a new file with the exact same name.

If a name is wrong or the file is missing, a grey picture placeholder appears instead of a broken image, and the browser console (F12) tells you which file name it could not find.

## Add a new item

Copy an existing item inside its list, paste it right after (keep the comma between items), and change the text and the image name.

- Lab project: inside `"projects"` in the `lab` section: `{ "title": "My Robot", "image": "lab-my-robot.jpg" }`
- Book: inside `"items"` in the `works` section.
- Achievement: inside `"items"` in `achievements`. `"icon"` is one of: trophy, medal, award, star, book, books, sigma, calculator, mic, cap, robot, chip, car, doc, news, school, tent, flask, chess, cube, camera, bolt, target, pencil, ruler, lightbulb, code, users, globe.
- Free resource: inside `"items"` in `resources`. Same icon names.
- Social card: inside `"items"` in `social`. Icons: instagram, linkedin, youtube, at (plus any above). Add `"comingSoon": true` instead of a link for a greyed-out card.

Items can be reordered by moving them up or down in the list. The order in the file is the order on the page.

## Reorder, rename or remove a section

Sections appear in the same order as in the `"sections"` list. Move a whole `{ ... }` block to reorder, delete one to hide it. `"nav"` is the word shown in the top menu (remove the line to keep a section out of the menu).

## Text formatting inside descriptions

- `**bold text**`
- `[link text](https://example.com)`
- `{email}` is replaced by the email address in `"site"`
- `[send me an email](mailto:{email}?subject=Collaboration)` opens an email with the subject "Collaboration"
- A description can be one string or a list of strings (each string is a paragraph).

JSON rules that cause 95% of problems: every text is in double quotes `"..."`, items are separated by commas, no comma after the last item, and a double quote inside text must be written `\"`.
If the page shows "content could not be loaded", paste `content.json` into any JSON validator (search "JSON validator") and it will point to the line.

## Short links with 404.html

GitHub Pages shows `404.html` for any address that does not exist. This one forwards the visitor to the matching section:

| You share | Visitor lands on |
|---|---|
| `yoursite/lab` | Lab section |
| `yoursite/books` | Books and published works |
| `yoursite/science-anecdotes` | Founder of Science Anecdotes |
| `yoursite/free-resources` | Free resources |
| `yoursite/collab` | Collaboration |
| `yoursite/contact` | Contact |
| `yoursite/lab/receiver-v2` | Lab, scrolled to the "Receiver V2" card and highlighted |
| `yoursite/books/arduino-tutorials` | The Arduino Tutorials book card |

The names that work are each section's `"id"` and its `"aliases"` in `content.json`. To make a new nickname, add it to `"aliases"` of that section. An item's name is its title in lowercase with dashes (`"Receiver V2"` becomes `receiver-v2`); you can also set `"id"` on an item to choose it yourself.
The same links also work with a `#`: `yoursite/#lab/receiver-v2`.

One setting: open `404.html` and look at `var BASE = "/";`
- Site at `https://USERNAME.github.io/` or your own domain: leave `"/"`.
- Site at `https://USERNAME.github.io/REPO-NAME/`: change it to `"/REPO-NAME/"`.

## Test locally (optional)

Opening `index.html` by double click will not work, because browsers block reading `content.json` from a file. Run `python -m http.server` in the repo folder and open `http://localhost:8000`.
