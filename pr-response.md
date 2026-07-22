# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename
**What I did:** 
Renamed all "save_to_watchlist" to "add_to_watchlist" to fit the naming convention
**How I verified:** I used project-wide search using CTRL + SHIFT + F, and searched up "save_to_watchlist" before the changes. After the changes, the exact files that showed up no longer show up, and now falls under "add_to_watchlist".

## Comment 2 — Deduplication
**What I did:**
Created a WatchlistEntry query, finding to see if the film_id and user_id already exists. If it does, then we raise an error. If not, then the program adds the entry into the database.
**How I verified:** I verified by comparing it to the "add_to_collection" function in collection.service.py. Seeing that both functions operate similarily, I made sure to check whether WatchlistEntry contained it, and return the adequate response based on it.

## Comment 3 — Missing test
**What I did:**
**How I verified:**

## Comment 4 — Default visibility
**My position:**
**Reasoning:**
**Tradeoff acknowledged:**

## Comment 5 — Sort order
**My position:**
**Reasoning:**
**Engagement with reviewer's point:**

## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->