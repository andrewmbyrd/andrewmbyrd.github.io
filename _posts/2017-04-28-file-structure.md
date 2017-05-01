---
layout: post
title: Requiring Files and You
thumbnail-path: "img/atom.png"
short-description: Navigating File Structures (especially in Ruby)
---

It may not be at all obvious to the novice developer how to navigate through a file structure. Even to the experienced developer, the bookkeeping of visually parsing through each indented folder name is tedious, at best.

I'll attempt here to explain the vagaries of how our computer goes about getting through file structures. Let's reference this file tree:

{:.center}
![Tree Structure](http://i.imgur.com/FJwvkdx.png)

`Example` is the so-called `root directory`. Every other folder within that are just directories. In order to get to, say `World.rb`, if I'm starting in `Example`, then I need to go `Section A/World.rb`. 

But there are times when you first need to navigate "up" in order to get to a file that you want. Say we now start where `Fun.rb` is. If I want to get to `World.rb` from there, then I need to go

- up once to get to `Section B`
- up once again to get to `Example`
- down into `Section A`

Therefore, the _relative path_ between `Fun.rb` to `World.rb` is `../../Section A/World.rb`

- `../` means go "up" one directory
- `./` is a reference to _this_ directory

Here is where `require` and `require_relative` come into play.

Now imagine we're in a situation in which we _need_ information from `World.rb` in order for `Fun.rb` to function. We need to somehow indicate that `Fun.rb` _requires_ the information from `World.rb`.

I _could_ put the line `require ../../Section A/World.rb`, and that would work, _as long as_ when I ran

```bash
ruby Fun.rb
```

My current working directory was at the location of `Fun.rb`. `require` statements look at the _current working directory_ in order to draw the relative path to the desired, required file.

`Require` can also look at the `$LOAD_PATH`. This would require manually adding the desired directory to the `$LOAD_PATH`, which is a global variable that all Ruby files will understand. The `$LOAD_PATH` is nothing more than an array of absolute path names from which files can be required (e.g home/user/username/documents/code/ruby/project).

A less variable way to include files is with `require_relative`. If I instead put the line
`require_relative ../../Section A/World.rb` at the top of `Fun.rb`, that will work _regardless of which directory I execute_

```bash
ruby AribitraryPath/Fun.rb
```
_from_.

The usefulness of `require_relative` has been captured in my Atom package [requirouter](https://github.com/andrewmbyrd/requirouter). Please use it and enjoy never having to apply the knowledge you've gained in this post!