---
categories:
 - Programming 
tags:
 - blog
 - technical
---
# Developing FOSS tools for python development 
I like python (though I eventually want to learn Rust). I like the idea that the programming language should be obvious and readable and user-friendly.  
But unlike C++ or C, which have decades-old development tools such as gcc and clang, python's ecosystem is much more mixed.  
For the purposes of this post, I'm going to focus on the language server protocol, which allows our editor to use all these tools listed here. 
While many python libraries predate LSP and therefore offer clients directly for each editor, LSP will drastically reduce this workload.
## Python LSPs
Currently, there are a couple of python lsp servers under active development
1. pylance, used in VScode - proprietary
2. pyright, used inside pylance - open source
3. [python-lsp-server](https://github.com/python-lsp/python-lsp-server)/pylsp - open source 
4. [jedi-language-server](https://github.com/pappasam/jedi-language-server) - open source 
5. [anakin-language-server](https://github.com/muffinmad/anakin-language-server) - open source 
### The Microsoft Language Servers - pyright and pylance.
Pyright is probably the fastest language server and pylance the most feature-complete. However, since pylance is closed source, it cannot be used in neovim as easily. 
Pyright misses features as a result since it is only part of a full language server. 
### Python-ls-server 
The other three all belong to a common ancestor - [python-language-server](https://github.com/palantir/python-language-server), developed and abandoned by palantir. Its codebase was forked twice - 
1. The obvious sucessor, python-lsp-server, is a direct fork of python-language-server. It retains a plugin architecture and supports many features. 
2. A common library pygls - is a generic library for langauge server development *in* (but not nessicarily *for*) python.  

The second is used by jedi-language-server, which only uses Jedi for features. Pylsp uses jedi and other libraries such as pycodestyle and is therefore more feature-complete.
### Anakin-language-server
This is in between jedi-language-server and pylsp, and supports other libraries such as pyflakes and mypy. However, it still uses pygls. It has less frequent development and support than pylsp but is quite promising.
### pygls 
Pygls and pylsp have a common heritage and therefore are very similar. However, pygls defines all its methods using pydantic dataclasses, making it much easier to develop new plugins, since the LSP API is stored in python, not on Microsoft's website. Frustrated at using dictionaries everywhere, I tried to port pylsp to pygls. And while the similarities made it much easier than it should have been, I was left with 3 glaring issues:
1. Pygls doesn't support custom workspace and Document types properly. This will take just a few lines of code and a pull request
2. Pygls doesn't support multiple workspaces, at least not in the same way as pylsp 
3. Pygls is designed around decorators, while pylsp is designed around pluggy. This can be fixed with an ugly function which registers each plugin hook to each feature. Possibly, this could be implemented in pygls itself.  

However, this effort takes longer and isn't ready yet, so will be left here.
## Frustrations with python tools
Between these python tools: pylsp, black flake8, etc, I found two issues that I wanted to personally address:
1. Autoimport. Pylsp lacks autoimport which pyright and pycharm have.
2. Configuration. A new standard, pyproject.toml has been created. But existing tools aren't as smart as they should be about it, and don't document its usage properly.
### Autoimport 
To begin, I looked at a pylsp [issue](https://github.com/python-lsp/python-lsp-server/issues/34). To begin, I created [pylsp-autoimport](https://github.com/python-lsp/python-lsp-server/issues/34), which retroactively formats the entire document to add missing imports. While the library its based on is well-designed for its purpose, I found it lacking in what I really wanted - on-demand completions. To find that, I went to the [rope](https://github.com/python-rope/rope/pull/464) library, and redesigned its autoimport code.  
The restrictions I had to work in limited the design slightly:
1. I had to support python 3.6 and above
2. I had to use only the standard library
3. I had to maintain some backwards compatibility with the existing implementation  

But I designed a new autoimport system, which takes several deviations from the existing one.
1. It searches for *all* installed modules, something existing ones do not do. 
2. It uses pathlib instead of rope's own resource system, making directory operations very fast 
3. It uses the standard library AST with its own logic instead of the existing patched ast system. It only checks the first level of the AST.
4. It uses sqlite3 instead of pickle. Furthermore, the database is fully persistent. I did have to learn some basic SQL to implement this.
5. While half the code is object-oriented, in the main sqlite module, it uses a series of functions and namedtuples to spread out parsing between multiple processes. This makes it possible to index 700mb of modules in around 3 seconds.  

With the help of the maintainer, Lie Ryan, I was able to improve this design, using generators and Named Tuples. This has been since merged and released. (A Bug prevents it from working on windows due to windows inserting files into ``sys.path``.)
### Configuration
Problem: python tools need to be configured from a variety of configuration files, validate that configuration, and document it. The current methods are inconsistent and many do not support the ``pyproject.toml`` as a first class citizen.
Solution: [pytoolconfig](https://github.com/bageljrkhanofemus/pytoolconfig).
Rather than try to explain what it does, I'll link [the documentation](https://pytoolconfig.readthedocs.io/en/latest/). But some of the challenges I faced were:
Getting it approved to be used by a maintainer required making the dependency tree minimal. Instead of using pydantic models, I switched to dataclasses. This caused several issues:
1. The dataclasses API is different and slightly worse 
2. Pydantic provided features such as creating a nested model from a dictionary 
3. Pydantic would validate and convert basic datatypes 

However, pydantic could be used as a drop in replacement for dataclasses, negating point 3 for tools. But a fourth issue emerged: Pydantic is better at type-hinting its code than the standard library. 
Python dataclasses work by using a decorator to convert a normal class to a dataclasss. Once the dataclass is instantiated, it is its own standalone type with dataclass features. However, decorated types do not share a commond base - there is no ``Dataclass`` equivalent to ``BaseModel``. Except there is, only its only in Pydantic, and only when type-checking is enabled. Since pydantic is not a hard dependency, pytoolconfig is filled with typing issues that cannot be fixed easily.  
Despite these issues, I have a working pull request for rope to use pytoolconfig, and will look into its usage in other tools like pylsp or pycodestyle.
Furthermore, I added a unique feature to pytoolconfig - reading PEP 621 information. For example, pytoolconfig can read the dependencies of a project. Autoimport can then only scan for those dependencies, drastically reducing caching time. 
## Conclusion
Developing these tools has been a pretty fun experience and more productive than spending that time gaming or other activities. It also taught me alot about programming in python and helps other people. I'll post a follow up when these are merged/if a pygls rewrite of pylsp happens.
