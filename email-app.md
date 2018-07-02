# Finished
- Added Zerobounce
- 

# To-dos 
- Clean up codes (including format checker and Zerobounce
- Add StrikeIron (seems no gem for this)

# Problems
- Legacy problems:
  - How to drop one file (without committing it on git)
  - 
- Should we deal with '+' in the 'validation' action?
  - Possible Solutions:
    1. Encode URL, and decode and extract email address from it.
    2. Ask client to do encode
    3. Use another controller to do encode.

- Do we need to give options on which kind of emails are considered as invalid? \
  (Currently toxic and desposable ones are also considered as 'invalid') - maybe easier to manage in future

- If two results from two companies conflict, what to do.

- Bulk validation?

- Should we use start or new? Basically should we keep a connection open? (if yes, then when do we close it?)
  1. NET::HTTP.start: open a new connection
  2. NET::HTTP.new: reuse an open connection

# !!!!!!!!Answer NOW !!!!!!
- Where to put configuration?
- Environment Configuration put where
- Where we need 'require'
