# HW2 notes

## What did you try?

I went module by module: `errors.py` first (following the provided `NotSignedUpError`), then `Event.sign_up`, `cancel` and `place` in `event.py`, then `Club` in `club.py`. I ran `python -m pytest` after each part, ran `python club.py` to see the chat, and tried the limits by hand: a capacity of 0, a title that is taken, joining twice, leaving an event you never joined, and `handle("hello")`.

## What broke, and how did you fix it?

`Event.place` first let the `ValueError` from `self.waitlist.index(member)` escape, so I caught it and raised `NotSignedUpError` instead, with `from None` so the traceback shows only the club's error. In `Club.handle` I had to be careful to catch only `SignupError`: a wider `except Exception` would have turned real bugs into "Sorry" messages, so a line that isn't a command is checked before the `try`.

## What would you do differently next time?

Next time I would write my edge cases as pytest tests (for example that `cancel` moves the first waiting member up), because then they run on every push like the given tests.
