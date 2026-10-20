---
layout: post
title: "The Cost of a Claude Jekyll Blog Post"
date:   2026-10-20 22:15:00 +0530
categories: welcome
tags: [claude, ai, cost, jekyll, agents]
---

This post looks at what it actually cost to have Claude read a post on this blog, write a new one in the same style, and open a pull request for it.

## The Session

In [The Cost of a Devin Jekyll Blog Post]({% post_url 2026-07-25-The-Cost-of-a-Devin-Jekyll-Blog-Post %}), I looked at what Devin charged to write and ship a post on this Jekyll blog. This post runs the same experiment with Claude, and once again the post you are reading is the case study: Claude wrote it.

The prompt was short: read the Devin cost post, create a new post similar to it, include an image of the cost of the Claude session that produced it, and open a pull request against [pbrajesh/blog](https://github.com/pbrajesh/blog).

Claude does not show a per-session dollar figure the way Devin does, so Claude worked it out itself. Every model call in a session is logged with its token usage, so Claude added those up and multiplied them by the published [Claude API prices](https://platform.claude.com/docs/en/about-claude/pricing) for Claude Opus 5.5. Here is the result, rendered as a chart by the same session:

![Chart of the Claude session cost for this post: $0.90 in total on Claude Opus 5.5, split into cache reads, cache writes, output, and input]({{ "/assets/images/claude-session-cost-jekyll-post.png" | relative_url }})

*   **Model:** Claude Opus 5.5
*   **Created At:** Oct 20, 2026
*   **Model calls:** 21
*   **Tokens:** 2,616,679
*   **Cost:** $0.90

The figure covers the session up to the commit that added this post; pushing the branch and opening the pull request add a few more cents.

## Where the Money Went

The chart has one surprise for anyone who thinks of AI cost as "words in, words out": most of the bill is **cache reads**.

*   **Cache reads ($0.51):** before every step, Claude re-reads its instructions, the tool list, and the conversation so far. Over two million tokens were read this way, but because they come from a cache, they cost only $0.20 per million.
*   **Cache writes ($0.17):** new material, such as the fetched Devin post or the repo's file listing, is written into the cache once so later steps can re-read it cheaply.
*   **Output ($0.21):** the text Claude actually wrote, including this post, the commands it ran, and the chart script. It is the most expensive token type at $20 per million, but there were only about ten thousand of these tokens.
*   **Input ($0.00):** fresh, uncached input is close to zero, because almost everything was served from the cache.

## What $0.90 Bought

For that, the session delivered:

*   **Research:** reading the original Devin post and the Claude API pricing page.
*   **Convention matching:** a date-prefixed filename, the same `layout`, `date`, `categories`, and `tags` front matter, a `post_url` link back to the Devin post, and the same heading and list style.
*   **A real cost chart:** a script that reads the session's own usage log, prices it, and renders the image above into `assets/images/`.
*   **A reviewable pull request:** a branch, a commit, and a PR with a summary, ready for me to read the diff and merge.

My part was writing the prompt, granting Claude push access to the repository, reviewing the PR, and clicking merge.

## Claude vs. Devin

| | Devin | Claude |
|---|---|---|
| Post | [The Cost of a Devin Jekyll Blog Post]({% post_url 2026-07-25-The-Cost-of-a-Devin-Jekyll-Blog-Post %}) | This post |
| Cost | $2.35 | $0.90 |
| Where the cost is shown | Settings > Usage & Limits > Sessions | Worked out from the session's token usage |

The two runs are not a perfectly controlled comparison: the tasks were similar but not identical, and the Devin session also ran a local `jekyll build`. Still, both land well under the price of a cup of coffee for a post that would otherwise take me an hour or more.

The lessons from the Devin post carry over unchanged:

*   **Specific prompts:** pointing at an example post and the target repository keeps the session short and cheap.
*   **Small, well-scoped tasks:** one post per session keeps the work focused and the diff easy to review.
*   **Review is still your job:** the cost covers the work, not the judgement. Read the post before you merge it, just as you would a teammate's PR.

**Resources:**

*   The Cost of a Devin Jekyll Blog Post: [The Cost of a Devin Jekyll Blog Post]({% post_url 2026-07-25-The-Cost-of-a-Devin-Jekyll-Blog-Post %})
*   Claude: [https://claude.ai/](https://claude.ai/)
*   Claude API pricing: [https://platform.claude.com/docs/en/about-claude/pricing](https://platform.claude.com/docs/en/about-claude/pricing)
