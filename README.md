# Standalone Architecture Library

This repository now contains a single-file standalone website: `index.html`.

Features included:
- Standalone HTML (single file) with side navigation and page content area.
- Admin login (simple password) accessible via the "Admin" button in the header.
- Admin panel to add/edit/delete pages (HTML, URL iframe pages, Gallery pages with image upload), manage submenus, and reorder top-level menu items via drag-and-drop.
- Search bar in the header to find pages by title or content.
- Dark mode toggle saved to localStorage.
- Simple view tracking: how many times a page has been opened (stored in localStorage) and visible in the Admin > Site Stats section.
- Gallery block for pages (upload images via the admin editor; stored as data URLs in localStorage).

Important notes and editing instructions

1) Make permanent edits by editing `index.html` in the repository
- This standalone app stores any admin changes in the user's browser localStorage. If you want changes to be permanent (so any user visiting the site sees them), you must edit the `PAGES_DATA` array in `index.html` directly and commit the change to GitHub.
- The `PAGES_DATA` variable is near the top of the file and contains an array of page objects. Each page object looks like:

  {id: 'unique-id', title: 'My Page', type: 'html', content: '<h1>Hi</h1>', parent: '', order: 0}

  - type = 'html' shows internal HTML content.
  - type = 'url' shows the `url` field in an iframe.
  - type = 'gallery' shows an image gallery from `images` (array of data-URLs).

2) Admin password
- The admin password is defined at the top of `index.html` as `ADMIN_PASS`. Change it to a secure password before making the repo public. This is a client-side check only and is not secure for sensitive deployments.

3) How persistence works
- Runtime edits are saved to `localStorage` on the browser that made them.
- To make edits visible to all users, update `PAGES_DATA` in `index.html` and push to this repository.

4) Adding internal pages (step-by-step)
- Open `index.html` in a text editor.
- Find the `PAGES_DATA` array near the top of the file.
- Add a new object for your page. Example for an HTML page:

  { id: 'modern-villa', title: 'Modern Villa', type: 'html', content: '<h1>Modern Villa</h1><p>Project description...</p>', parent: 'projects', order: 2 }

  For a URL page:

  { id: 'docs', title: 'Design Docs', type: 'url', url: 'https://example.com', parent: '', order: 3 }

  For a gallery page (images must be added via the admin UI or by embedding data-URLs in the `images` array):

  { id: 'villa-gallery', title: 'Villa Gallery', type: 'gallery', images: [/* data-URLs or paths */], content: '<p>Photos</p>', parent: 'projects', order: 1 }

- Save and commit your changes to the repo. When users load the site, if their browser localStorage has no saved pages, the site will load from `PAGES_DATA`.

5) Making the admin system secure (notes)
- This standalone admin is client-only. The password check occurs in JavaScript and cannot be relied on for real-world security. For a production site, host a backend (API) with real authentication and storage.

6) Export / Import
- Use Export in the side nav to download a JSON of the current pages. Use Import in Admin to paste JSON and import pages.

7) GitHub Pages
- You can publish this repository with GitHub Pages (Settings -> Pages) to serve `index.html` as a static site.

If you'd like, I can:
- Add more example pages and images.
- Hook this to a backend (Firebase, Netlify Functions, or your own API) for shared persistence and secure admin authentication.

---

I have pushed `index.html` and this README to `jackeichelberger3-beep/website1-1` on the `main` branch. Open the repository or visit GitHub Pages (after enabling) to view the site.
