---
title: The Labs Infrastructure
description: A short overview of how the Labs pages load, parse, and render content.
date: 2025-11-20
---

The Labs section is designed to stay extremely lightweight, fast, and source-of-truth aligned with GitHub. Every lab note lives as a Markdown file inside the `notes/labs/` directory of the repository. Nothing is duplicated or cached locally; the website always pulls the latest version directly from GitHub.

https://github.com/ahson01/notes


When a Labs page loads, the server fetches the repository’s tree using the GitHub API and identifies all `.md` or `.mdx` files under `labs/`. Each file’s raw content is retrieved from `raw.githubusercontent.com` and parsed using **gray-matter**, which extracts the frontmatter (title, description, date) and separates it from the Markdown body.

For individual lab pages, the server again fetches the raw Markdown file, parses it, and converts it to HTML using **Marked**. Before sending the HTML to the client, the system scans for GitHub repository links. Any direct repo URL is replaced with a styled GitHub repo card that includes the repository name, description, stars, and primary language, fetched using the GitHub REST API.

This setup keeps all content versioned, fully author-editable in plain Markdown, and instantly updatable across the site whenever the GitHub repo changes.
