---
categories:
 - Programming 
tags:
 - blog 
---
# Make a blog
Well this is boring
# Make a blog that uses markdown and automatically responds to changes via git using modern tool in language you don't know.
There we go.

So we basically have the following steps to do:
1. Watch for changes in a git repository
2. Compile to html and render it - this is where [pagic](https://github.com/xcatliu/pagic) comes into play
3. Use caddy reverse proxy to make it appear on [raspberry pi](https://bageljr.com)
## Render markdown over filesystem
Initially, I thought I'd write my own stuff but then decided to use pagic because why reinvent the wheel.
Early results are promising - the blog seems to work.
After fleshing out the blog a bit more, I got it to a nice state.
## Automation
I wanted to automate git file watching.
First I tried a shell script but that didn't really work so I moved to python.  
Then I tried installing deno - the js runtime - onto my rpi (aarch64/linux). Naturally Deno doesn't support aarch64 on linux. Of Course it wouldn't.   
This would also be when my raspberry pi crashed and stopped working.  
I make it do a lot of work. But I created a docker-compose setup to run an aarch64 build.   
But docker is stupid so I shall run it natively.
Now it runs on the rpi4 without docker via a simple python script.
Theoretically, the website should reflect the changes I make here after I push them.


Features to add 
- rss feeding
