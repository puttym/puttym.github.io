---
layout: post
title: Jekyll post template and other things
date: 2020-01-30
category: general
---

### First six lines

```yaml
---
layout: post
title: Title
date: 2020-01-30
category: category
---
```

Latex: Include code beween `$$...$$`.

### Running the Jekyll server
  1. Go to root directory. This is the place where `_posts` directory is located.
  2. Run the command `bundle exec jekyll serve`.
  3. Open a browser and type the url: `127.0.0.1:4000`

### Pushing to github
  1. Go to `_posts` directory
  2. `git add <filenames>`
  3. `git commit -m "<Message>"`
  4. `git push -u origin master`
