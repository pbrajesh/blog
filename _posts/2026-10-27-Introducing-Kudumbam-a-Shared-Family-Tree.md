---
layout: post
title: "Introducing Kudumbam, a Shared Family Tree"
date:   2026-10-27 23:30:00 +0530
categories: welcome
tags: [kudumbam, family-tree, angular, postgres, raspberry-pi]
---

This post is a quick summary of Kudumbam, a family tree app that relatives sign in to and build together, and how it runs on a Raspberry Pi at home.

## What Is Kudumbam?

*Kudumbam* means "family" in Tamil. The app is a shared family tree: instead of one person keeping a GEDCOM file on their laptop, everyone in the family signs in and sees the same tree, and the people allowed to edit it can add relatives, fix dates, and fill in the gaps that only they remember.

Any family can use it. A tree starts empty, or from a GEDCOM (`.ged`) file exported from another family tree app, and one site can host many families, with each tree visible only to the relatives invited to it.

## Features

*   **Tree browsing:** an hourglass view with the centred person's ancestors above and their descendants and spouses below. Click a card to open it, double-click to re-centre the tree, and drag or scroll to pan and zoom. A **People** list lets you search anyone and jump to them.
*   **Editing:** names, dates, places, and notes, plus quick actions to add a father, mother, spouse, son, daughter, brother, or sister. Every change is saved for everyone straight away, undo and redo included.
*   **Members and roles:** an owner invites relatives by email as a `viewer` (see and export), an `editor` (change the tree), or another `owner` (also manage members). The Members page even writes the invitation message for you to send on WhatsApp or email.
*   **This is me:** a member can open their own card and claim it. Once an owner approves the claim, the tree opens on that person, their card is marked **You**, and **Find me** jumps back to it.
*   **GEDCOM import and export:** import any GEDCOM 5.5.x file and export GEDCOM 5.5.1. Tags the editor does not understand are kept and written back unchanged, so nothing is lost on a round trip.
*   **Two people editing:** if a relative changed the same people first, your change is not saved over theirs; you see the latest tree and are asked to make the change again.
*   **In-app help:** a **Help** page, open without signing in, explains the app for family members and for tree owners.

## How It Is Built

Kudumbam is split into two repositories:

*   **[kudumbam-web](https://github.com/pbrajesh/kudumbam-web):** the browser app, built with Angular 20 and D3.js, which draws the tree.
*   **[kudumbam-app](https://github.com/pbrajesh/kudumbam-app):** the API server, built with Node, Express 5, and PostgreSQL, which checks who is allowed to do what.

Everything runs on a **Raspberry Pi**. Apache serves the built Angular app and passes `/api/*` to the Node server, which talks to a local PostgreSQL database. Relatives reach it from anywhere through a **Cloudflare Tunnel**, so there are no ports to open on the home router.

*   **Sign-in:** handled by **Supabase**, with Google or an email link. Supabase is used for sign-in only. The API checks each token against Supabase's public keys and needs no Supabase secret, and all family data stays on the Pi.
*   **Backups:** a nightly `pg_dump` on the Pi (14 days kept), and a daily copy into a private schema in Supabase Postgres, so a dead SD card does not mean a lost family history.

## See It in Action

A two-minute walkthrough of the app, using a made-up family, is attached to the [kudumbam-web v1 release](https://github.com/pbrajesh/kudumbam-web/releases/tag/v1) ([download the MP4](https://github.com/pbrajesh/kudumbam-web/releases/download/v1/kudumbam-walkthrough.mp4)).

**Resources:**

*   Kudumbam web app: [https://github.com/pbrajesh/kudumbam-web](https://github.com/pbrajesh/kudumbam-web)
*   Kudumbam API server: [https://github.com/pbrajesh/kudumbam-app](https://github.com/pbrajesh/kudumbam-app)
*   Walkthrough video: [https://github.com/pbrajesh/kudumbam-web/releases/tag/v1](https://github.com/pbrajesh/kudumbam-web/releases/tag/v1)
