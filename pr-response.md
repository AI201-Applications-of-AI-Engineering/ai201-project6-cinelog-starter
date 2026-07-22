# PR Response Doc — CineLog Watchlist Feature

Screenshot of "git log --oneline"
<img width="1014" height="250" alt="image" src="https://github.com/user-attachments/assets/d3202b8c-af31-4177-b0d0-95f2fb8478d8" />

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->
Throughout the project, I utilized Claude to help me understand the program. I asked it to summarize what models.py was responsible for, what it depended on, check deduplication and if my changes were accurate to other parts of the project. In order to understand my flaws more, I asked Claude to also explain any counterarguments that could be made to my choices in Comments 4 and 5. It explained to me my flaws (storage reasoning was wrong, watchlist isn't an activity feed), and helped me clarify my real arguments (privacy and activity ordering). As I struggled on rebasing, I asked it to help me resolve the issue by telling me what happened when I rebased, and how to revert the changes back to what it was. Lastly, I asked it to verify that my commit messages followed conventional commit format, and was able to properly readjust my commit messages to properly reflect the convention.

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
**What conflicted:** Had a conflicting .gitignore conflict, alongside UUID issues, causing my "git rebase origin/main" to completely remove my WatchlistEntry in models.py
**How I resolved it:** I had Claude help me fix the rebasing issues. Since no merge conflicts arose, it was just models.py. I had Claude restore models.py to what it was before the rebase and updated the docstrings/comments. 
**How I verified no conflict remains:** I saw that the rebase successfully passed in the terminal. Furthermore, after I reverted models.py back to what it was before, I reran the watchlist.py test, and it worked again.

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->

The watchlist feature manually adds a film to a user's watchlist, making sure that the film exists and is not already in the watchlist. In order to simplify the UI for the users, I set the default visibility for the watchlist to "public" and set the sort order to "date added" instead of alphabetical. The idea here was that setting it to public will allow users to see others' social activities, and setting sort order to "date added" simplified the searching for users wanting to see what they've added. To manually test this feature out:

Open the terminal
Run "pytest tests/test_watchlist.py"
