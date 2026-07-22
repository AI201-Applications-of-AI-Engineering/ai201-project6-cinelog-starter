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
**What I did:** I created a new test file, test_watchlist.py, that tests the updated add_to_watchlist after it was fixed. The pytest checks whether the film is checked or not, and then runs the test.
**How I verified:** I verified this by running "pytest \test\test_watchlist.py," which successfully passed.

## Comment 4 — Default visibility
**My position:** The default should be set to public rather than private.
**Reasoning:** If we were to set the default to private for everyone, there would be very little social activities by default. Many users may think that the app is dead/dying, and quit before using it. This would kill the product in the long run, whereas having the default set to public allows new/continuing users to see that the app is still alive.
**Tradeoff acknowledged:** If "public=True", then theoretically, everyone's watchlist is public. However, if some people wanted their watchlist to be private, and didn't know it was private by default, it may cause privacy issues.

## Comment 5 — Sort order
**My position:** default to "date added" rather than alphabetical
**Reasoning:** Many users want to see that their watchlist has updated. If we kept it alphabetical and we always add something at the end of the alphabet, the user has to manually scroll every time to the bottom to see whether the film was added or not. 
**Engagement with reviewer's point:** Any stress caused to the user because of program functionality could cause them to quit using the program rather than retaining them. Keeping it defaulted to "date added" allows the user to know that the top are the most recently added, and if they want to watch in order of they were added, they can go to the very bottom or reverse the list. Furthermore, the only purpose in having alphabetical besides aesthetic reasons is for searchability.

## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->