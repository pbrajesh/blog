---
layout: post
title: "The Cost of a Devin Jekyll Blog Post"
date:   2026-07-25 20:38:13 +0530
categories: welcome
tags: [devin, ai, cost, jekyll, agents]
---

This post looks at what it actually cost to have Devin AI write, verify, and open a pull request for a post on this Jekyll blog.

## The Session

In the [Introduction to Devin AI]({% post_url 2026-07-25-Introduction-to-Devin-AI %}) post, I walked through handing Devin a task prompt and reviewing the pull request it produced. That post was itself written by Devin, which makes it a convenient case study for the question everyone asks next: *what does it cost?*

Devin lists every session and its cost under **Settings > Usage & Limits > Sessions**. Here is the entry for the session that produced the introduction post:

![Devin Usage & Limits Sessions page showing the "Add Devin AI article to blog _posts" session created Jul 25, 2026 with a cost of $2.35]({{ "/assets/images/devin-session-cost-jekyll-post.png" | relative_url }})

*   **Session:** "Add Devin AI article to blog _posts"
*   **Created At:** Jul 25, 2026
*   **Cost:** $2.35

## What $2.35 Bought

The prompt was a few sentences: add a post under `_posts/` introducing Devin AI, follow the front matter and formatting of the existing Ollama post, and don't modify any other files. For that, the session delivered:

*   **Research and writing:** a structured article covering what Devin is, how it differs from a code-completion assistant, and a five-step quick start.
*   **Convention matching:** a date-prefixed filename, matching `layout`, `date`, `categories`, and `tags` front matter, and the same heading and list style as the other posts.
*   **Local verification:** cloning the repo, installing the Ruby dependencies, and running `bundle exec jekyll build` to confirm the site still builds.
*   **A reviewable pull request:** a branch, a commit, and a PR with a summary, ready for me to read the diff and merge.

My part was writing the prompt, reviewing the PR, and clicking merge. The result is the post that is live on this blog today.

## Is It Worth It?

For a content task like this, the comparison is not against a perfect human writer. It is against the time I would otherwise spend drafting, checking the front matter, and running the build myself, which is easily an hour or more for a post of that length. At $2.35, the agent costs less than a cup of coffee and finishes far faster than doing the work by hand.

A few things keep that number low and the output useful:

*   **Specific prompts:** naming the target directory, an example post to copy, and what *not* to change avoids expensive back-and-forth.
*   **Small, well-scoped tasks:** one post per session keeps the work focused and the diff easy to review.
*   **Review is still your job:** the cost covers the work, not the judgement. Read the post before you merge it, just as you would a teammate's PR.

Agentic coding tools are usually pitched at large engineering tasks, but small, repetitive content work in a Git repository is a sweet spot: the conventions are clear, the build gives a pass/fail check, and the pull request makes review easy. A few dollars per post is easy to justify.

**Resources:**

*   Introduction to Devin AI: [Introduction to Devin AI]({% post_url 2026-07-25-Introduction-to-Devin-AI %})
*   Devin: [https://devin.ai/](https://devin.ai/)
*   Devin Documentation: [https://docs.devin.ai/](https://docs.devin.ai/)

---
