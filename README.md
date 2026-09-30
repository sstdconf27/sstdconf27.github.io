# SSTD 2027 web site

Source of <https://sstdconf27.github.io>. The site is built with
[Jekyll](https://jekyllrb.com): you edit small text files, and GitHub turns
them into the finished pages every time you push to `main`.

The menu, the photo banner and the footer are written **once** and shared by
every page, so a page file contains nothing but that page's own content.

---

## 1. Where is everything?

```
_config.yml          conference name, dates, venue, city, banner photo
_data/               lists, one file each (see the table below)
pages/               one file per page, grouped like the menu
    home.html
    organizers.html
    calls/           calls.md, call-research.md, call-thesis.md, call-tutorials.md
    program/         program.md, schedule.html, keynotes.html, accepted-papers.md,
                     accepted-tutorials.md, awards.md, panel.md
    attend/          attend.md, registration.md, venue.md, travel.md, visa.md,
                     accommodation.md, attractions.md
images/              every photo and logo
_layouts/            page skeleton             (rarely edited)
_includes/           menu, banner, footer, and the blocks that turn the _data
                     lists into HTML            (rarely edited)
assets/              theme CSS / JavaScript / fonts; site-specific styles are
                     in assets/css/custom.css  (rarely edited)
```

Three more files sit in the top folder and should simply be left alone:
`robots.txt`, `sitemap.xml` (lists the pages for search engines, updates
itself) and `google55d8fd78eb7e966a.html` (proves to Google that we own the
site).

### "I want to change ..."

| What | Edit this file |
|------|----------------|
| Conference dates, venue, city, name, edition ("20th") | `_config.yml` |
| Banner photo at the top | `_config.yml` → `banner_image` |
| Menu bar and the grey sub-menus | `_data/navigation.yml` |
| Home page: About text | `pages/home.html` |
| Home page: Important Dates | `_data/important_dates.yml` |
| Home page: News | `_data/news.yml` |
| Home page: Sponsors | `_data/sponsors.yml` |
| Organizers | `_data/organizers.yml` |
| Program committees | `_data/program_committee.yml` |
| Keynotes | `_data/keynotes.yml` |
| Detailed program (timetable) | `_data/schedule.yml` |
| Any other page (calls, accepted papers, awards, panel, registration, venue, travel, visa, accommodation, attractions) | the page's file in `pages/` |

Every file in `_data/` and every page in `pages/` **starts with a short
explanation and an example to copy**.

---

## 2. Preview and publish

Preview on your computer (run in this folder):

```
jekyll serve
```

then open <http://localhost:4000>. The site is rebuilt each time you save a
file; reload the browser page to see the change. Exception: after editing
`_config.yml`, stop the command with Ctrl+C and start it again.

> Opening a file from `pages/` directly in the browser does not work - the
> files are ingredients, not finished pages. Always preview with
> `jekyll serve`.

Publish: commit and push to `main`. GitHub rebuilds the site in about a
minute.

---

## 3. Adding content - worked examples

### 3.1 Add a news item

Open `_data/news.yml` and add two lines **at the top of the list**:

```yaml
- date: "Jan 15, 2027"
  text: "The [Call for Papers](/calls.html) is now available."

- date: "Sept, 26, 2026"
  text: "Website Setup"
```

### 3.2 Set or extend a deadline

Open `_data/important_dates.yml` and fill in `date`. If a deadline is
extended, put the new date in `date` and the previous one in `old_date`; the
old one is shown crossed out.

```yaml
- label: "Paper submission deadline (Research / Demo / Industry tracks)"
  date: "May 18, 2027"
  old_date: "May 4, 2027"
```

### 3.3 Announce the conference dates

Open `_config.yml` and change one line. The banner on every page and the
"Location" sentence on the home page follow.

```yaml
  dates:    "August 23-25, 2027"
```

### 3.4 Add organizers

Open `_data/organizers.yml` and add entries at the bottom. The page shows
"Coming soon." until the first entry exists.

```yaml
- role: "General Co-chairs"
  people:
    - name: "Jane Doe"
      affiliation: "Example University, USA"
      url: "https://www.example.edu/~jdoe"
    - name: "John Smith"
      affiliation: "Sample Institute of Technology, Canada"
```

Keynotes (`_data/keynotes.yml`), program committees
(`_data/program_committee.yml`), sponsors (`_data/sponsors.yml`) and the
timetable (`_data/schedule.yml`) work the same way; each file shows its own
example.

### 3.5 Write a page

Open the page's file, e.g. `pages/attend/venue.md`. It looks like this:

```
---
layout: page
title: Venue
menu: attend
permalink: /venue.html
---
(a block of instructions and an example)

{% include blocks/coming-soon.html %}
```

Leave the part between the two `---` lines alone. Replace the last line with
your text:

```markdown
### Name of the Building, North Carolina State University

SSTD 2027 takes place at the **Name of the Building**, located at
[123 Example Street, Raleigh, NC 27606](https://maps.google.com/).

![Photo of the venue](/images/venue.jpg)

### Getting there

- 10 minutes by bus from downtown
- 20 minutes by taxi from the airport
```

The text is written in Markdown:

| You type | You get |
|----------|---------|
| `## Heading` | large centred heading (starts a new part of the page) |
| `### Heading` | medium heading |
| `#### Heading` | small heading |
| an empty line | new paragraph |
| two spaces at the end of a line | line break inside a paragraph |
| `**bold**` and `*italic*` | **bold** and *italic* |
| `[text](https://www.example.org)` | link to another site |
| `[Registration](/registration.html)` | link to a page of this site |
| `[name@example.org](mailto:name@example.org)` | e-mail link |
| `- item` | bullet point (indent by four spaces for a sub-item) |
| `1. item` | numbered list |
| `![description](/images/photo.jpg)` | image (put the file in `images/` first) |
| `![description](/images/photo.jpg){: width="160"}` | image, 160 pixels wide |
| `---` on a line of its own | horizontal line |

A table:

```markdown
| Category | Early (until July 15) | Late    |
|----------|-----------------------|---------|
| Regular  | USD 000               | USD 000 |
| Student  | USD 000               | USD 000 |
```

Two columns side by side (`col-6` = two per row, `col-4` = three per row;
on phones they stack automatically). Keep the empty lines:

```markdown
<div class="row">
<div class="col-6 col-12-narrow" markdown="1">

### Left column

Text of the left column.

</div>
<div class="col-6 col-12-narrow" markdown="1">

### Right column

Text of the right column.

</div>
</div>
```

Plain HTML (for example the `<iframe>` of an embedded Google Map) can be pasted
into a page as it is.

### 3.6 Add a new page

1. Copy an existing page, e.g. `pages/attend/venue.md`, to
   `pages/attend/grants.md`.
2. Change its first lines:

   ```
   ---
   layout: page
   title: Travel Grants
   menu: attend
   permalink: /grants.html
   ---
   ```

   `title` is the heading of the page, `menu` is the menu button it belongs to
   (`home`, `organizers`, `calls`, `program` or `attend`), and `permalink` is
   its address.
3. Add it to the menu in `_data/navigation.yml`, under the `children` of
   `attend`:

   ```yaml
       - title: "Travel Grants"
         url: /grants.html
         description: "Support for student attendees and how to apply."
   ```

To remove a page, delete its file and its lines in `_data/navigation.yml`.

### 3.7 Rules for the `_data/` files (YAML)

- **Indentation matters.** Use spaces, never tabs, and keep entries lined up
  exactly like the example in the file.
- **Put text in double quotes**: `title: "Indexing: A Survey"`. Without the
  quotes, a colon inside the text breaks the file.
- A line starting with `#` is a comment and is ignored.
- Long text (an abstract) goes after `>` on indented lines:

  ```yaml
    abstract: >
      First line of the abstract,
      which continues here.
  ```

If the site stops updating after a change to a `_data/` file, the file
probably has an indentation or quoting mistake; `jekyll serve` prints the
error.

---

## Credits

Design: [Tessellate](https://html5up.net/tessellate) by HTML5 UP, used under the
CCA 3.0 license (see `LICENSE.txt`). The "Design: HTML5 UP" credit in the footer
is required by that license.
