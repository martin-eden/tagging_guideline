# Tagging


## Problem

You have a problem. Something in your git project is broken. Something
with parsed XML handling.

In collective project you type

```
$ git log --oneline
```

and start reading all that lines, seeking something about import or
data processing. Word by word, line by line...


## Savior

I've established markup style and used it for my personal code since 2002.
In 2016 I was asked to explain it. So demonstrating it here, not obligating anyone to use.


## Panacea

Mark changes by your judgement and by code changes they do.

    [.^] [readme] Reworded some lines.
    [?+] [string-concatter] Added experimental garbage-collection heuristic.
    [!*] [2d/convex_hull] Debugged! (At least I hope so.)
    [/] [file/as_string] renamed from [string/from_file].

I hope you feel. Just putting at most one tag with change type
(with all that bogus symbols) and arbitrary amount tags with names.
Idea is that you'd be able to "grep" all changes marked for example
`[table-serializer]`.


### Details

We have tags with two types. First with *change type*, others with
*subsystem*.


#### Symbols meaning

* By impact:
    * `.` -- minor change. Low impact. Not worth hard checking. May be merged in thematic commit.
    * `!` -- important. High impact. Usually breaks or fixes more than other changes.

* By your judgment:
    * `?` -- experimental/questionable. You're not sure it's a right way.
    * `^` -- improvement. You changed to the same but different and
      you like your variant.
    * `*` -- bugfix. You changed functionality, not form. Now it really
      works as other's think it should. No, bug fix is *not* improvement.

* By text manipulations:
    * `+` -- something added. You added file, function or additional fields.
      Old code will work without changes (backward compatibility).
    * `-` -- something removed. Existing code may need relinking to workargound.
    * `/` -- rename/move. You renamed some functions or even tossed whole project tree.
      Existing code probably need to be relinked with changed part.
    * `~` -- relink/resync. Changes in existing code to use that function
      under new, cooler name.
    * `>` -- import
    * `<` -- export
    * `@` -- whirlwind. You merged commits under one subsystem. List of changes kept inside commit description.


#### Notes

* This systems allows you to regroup commits by sybsystem. (For those who like to keep
history simple and know what `$ git rebase -i HEAD~20` does.)
* I recommend to place tags only when you're sure that it make things
more clear and do not add obscurity or excessiveness. For example both
`Initial commit.` and `[!] Initial commit.` is ok. But `[!+] Initial
commit.` is excessive.
* Not all possible commits may be described nicely with this system.
For example you fixed bug, extended functionality and renamed variables.
Message `[!*^/] Just merge this and become rich quick!` looks like
spam. I tend to avoid commits with such changes.

---
```
2016-07-08
2018-06-22
```
