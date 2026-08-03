# Coefficient Giving \u2014 Proposal Reference Library

A one-page site that lists every reference document for the proposal, grouped into
the three domains, with a search box and download links. The writing team gets a
single URL. You maintain it by editing one JSON file \u2014 no re-uploading of the page
itself, ever.

```
coefficient-library/
\u251c\u2500 index.html      \u2190 the page itself (don't need to touch this again)
\u251c\u2500 papers.json     \u2190 the database \u2014 this is the only file you'll edit day-to-day
\u2514\u2500 papers/         \u2190 optional folder, only if you want to host PDFs directly in the repo
```

---

## 1. Create the repo

1. Go to github.com \u2192 **New repository**.
2. Name it something like `coefficient-giving-library`.
3. Make it **Public** (GitHub Pages' free tier requires a public repo, unless you have GitHub Team/Enterprise).
4. Don't initialize with a README (you already have one here).

## 2. Upload these three files/folders

In the new repo, click **Add file \u2192 Upload files**, and drag in:
- `index.html`
- `papers.json`
- the `papers/` folder (you can leave it empty for now, or delete it entirely if you plan to only link out to Drive/Dropbox instead of hosting files in the repo)

Commit directly to `main`.

## 3. Turn on GitHub Pages

1. In the repo, go to **Settings \u2192 Pages**.
2. Under "Build and deployment," set **Source: Deploy from a branch**.
3. Branch: `main`, folder: `/ (root)`. Save.
4. GitHub will give you a URL like:
   `https://<your-username>.github.io/coefficient-giving-library/`
   It takes 1\u20132 minutes to go live the first time.

## 4. Share that one link with the writing team

That URL is the whole deliverable. Bookmark it, put it in the proposal doc header,
whatever \u2014 it always reflects whatever is currently in `papers.json`.

---

## 5. Adding a new document (the day-to-day workflow)

You never touch `index.html` again. Just add an object to the array in `papers.json`.

**If you're linking out** (Google Drive, Dropbox, a journal page, an OSF link, etc.) \u2014
this is the fastest path and what "avoid manual uploading" means in practice:

```json
{
  "id": "stake-004",
  "title": "Multi-stakeholder Governance Models in National Health Data Systems",
  "authors": "Osei, K. & Fernandez, L.",
  "year": 2024,
  "domain": "stakeholder",
  "type": "pdf",
  "tags": ["governance", "multi-stakeholder", "policy"],
  "description": "Comparative review of governance models across 6 countries; useful for the stakeholder-mapping section.",
  "link": "https://drive.google.com/file/d/XXXXXXX/view?usp=sharing"
}
```

**If you'd rather host the actual file in the repo** (works fully offline, no Drive
permissions to manage), drop the PDF into the `papers/` folder and point `link` at
a relative path:

```json
{
  "id": "data-012",
  "domain": "data_stewardship",
  "title": "A Federated Model for Cross-Border Health Data Sharing",
  "authors": "Chen, M.",
  "year": 2023,
  "type": "pdf",
  "tags": ["federated data", "privacy", "interoperability"],
  "description": "Proposes a federated query model as an alternative to centralized data pooling.",
  "link": "papers/chen-2023-federated-model.pdf"
}
```

### Field reference

| Field | Required | Notes |
|---|---|---|
| `id` | yes | any unique short string |
| `title` | yes | full title |
| `authors` | no | free text |
| `year` | no | number |
| `domain` | yes | must be exactly one of: `stakeholder`, `data_stewardship`, `facility_integration` |
| `type` | no | `pdf`, `doc`, `link`, `dataset` \u2014 just shown as a badge, purely cosmetic |
| `tags` | no | array of short strings, shown as pills, searchable |
| `description` | no | 1\u20132 sentence summary shown on the card |
| `link` | yes | a full URL, or a relative path like `papers/filename.pdf` if the file lives in this repo |

Commit the change (directly in the GitHub web UI: open `papers.json` \u2192 pencil icon
\u2192 edit \u2192 "Commit changes"). The live page updates within a few seconds \u2014 no build
step, no redeploy.

**Delete the three `sample-00x` entries** already in `papers.json` once you've added
real ones; they're just there to show the shape of the data and confirm the page works.

---

## 6. Bulk-adding many papers at once

Once you share the actual papers, the fastest way to bulk-populate `papers.json` is
to paste the reference list to Claude along with this schema and ask it to generate
the JSON array in one go, rather than hand-typing each entry.

## Notes

- Search matches title, authors, description, and tags.
- The domain tabs filter; search and domain filter combine (search applies within
  whichever tab is active).
- If a repo is private and you're on GitHub's free plan, Pages won't be available \u2014
  either make the repo public or upgrade, since your reference documents likely
  aren't sensitive enough to require a private repo, but worth checking with your team.
