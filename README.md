# Static blog generator sketch

## Basic concept

- Transform set of markdown files into HTML blog
	- Per-article HTML pages
		- Main HTML page with recent articles
		- RSS feed
- Start by hardcoding webpage template etc
- Libraries required
	- Will need to generate HTML and templating is the standard solution
		- Seems like Jinja is widely-used including in Flask, might as well try it: https://jinja.palletsprojects.com/en/3.1.x/
	- Will need to store some metadata on articles
		- SQLite seems suitable, or a flat file, but probably SQLite which I would like to try anyways
			- Now built into Python: https://docs.python.org/3/library/sqlite3.html
	- Will need a Markdown engine to parse posts:
		- https://pypi.org/project/Markdown/
	- Will need to emit RSS 
		- Feedgen seems like the defacto standard: https://github.com/lkiesow/python-feedgen
	- I could use argparse for a command line tool but I think it's kinda annoying compared to Click so I'll use that

## Basic logic flow to post:
 1. Add a Markdown file to a directory of posts
 2. Execute a command to parse the directory
 3. Output HTML of Markdown files transformed to HTML and inserted into Jinja template to the filesystem
 4. Use `git push` to upload to Github pages
 
 Follow-up enhancements:
 * Diff directory of posts against prior state in SQLite to detect any new posts. 
	 * Alternate option: treat file modification date as post time— n.b. file creation isn't available on Unix systems
 * Emit an RSS feed