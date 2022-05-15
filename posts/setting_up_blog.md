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

Features to add 
- rss feeding
- git watching
