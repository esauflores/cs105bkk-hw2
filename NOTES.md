# HW2 notes

## What did you try?

I went module by module: `errors.py` first (following the provided `NotSignedUpError`), then `Event.sign_up`, `cancel` and `place` in `event.py`, then `Club` in `club.py`. I ran `python -m pytest` after each part, ran `python club.py` to see the chat, and tried the limits by hand: a capacity of 0, a title that is taken, joining twice, leaving an event you never joined, and `handle("hello")`.

## What broke, and how did you fix it?

The visible tests passed, so the risk was in the hidden ones. In `Event.place`, `self.waitlist.index(member)` raises `ValueError` for a member who isn't waiting, so I catch it and raise `NotSignedUpError` instead, with `from None` so only the club's error shows. In `Club.handle` I catch only `SignupError`: a wider `except Exception` would turn real bugs into "Sorry" messages, so a line that isn't a command is checked before the `try`, not caught after it.

## What would you do differently next time?

Next time I would write my edge cases as pytest tests (for example that `cancel` moves the first waiting member up), because then they run on every push like the given tests.
