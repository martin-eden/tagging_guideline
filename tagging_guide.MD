# Tagging

## Problem
You have a problem. Something in your git project is broken. Something
with parsed xml handling.

If it's collective project you type

`git log --oneline`

and start reading all that lines, seeking something about import or
data processing. Word by word, line by line...

## Panacea
Mark changes by your judgement and by code changes they do.

    [.^][readme] Reworded some lines.
    [?+][string-concatter] Added experimental garbage-collection heuristic.
    [!*] Debugged! (At least hope so.) Just want to mark this state...
    [/] [string/from_file] renamed to [file/as_string].

I hope you feel. Just putting at most one tag with change type
(with all that bogus symbols) and arbitrary amount tags with names.
Idea is that you'd be able to "grep" all changes marked for example
"table-serialize".

### Details
So we have tags of two types. At most one with *change_type*, any others
with *content_type*. I prefer to place *change_type* at beginning of message.

#### Symbols meaning
* By impact:
    * `.` -- minor change. Low impact. Not worth hard checking.
    * `!` -- important. High impact. Usually this change breaks or fixes
       more than other changes.

* By your judgment:
    * `?` -- experimental/questionable. You're not sure it's right way.
    * `^` -- improvement. You changed to the same but different and
      you like your variant.
    * `*` -- bugfix. You changed functionality, not form. Now it really
      works as other's think it should.

* By text manipulations:
    * `+` -- something added. You added file, function or records to
      table.
    * `-` -- something removed
    * `/` -- rename/move/relink. You renamed some variables inside file
      or changed to calls to new names or renamed/moved whole
      file. Or even tossed whole project tree. Point is that changed
      only form, not functionality. (*Please mention both new and old
      names to keep history chain reconstructable.*)
    * `>` -- import
    * `<` -- export

#### Notes
* So bugfix is not improvement. (I do not consider bugs normal so
their fixes are not improvements.)
* Common combo I use often is `.^` for reformatting.
* I recommend to place tags only when you're sure that it make things
more clear and do not add obscurity or excessiveness. For example both
`Initial commit.` and `[!] Initial commit.` is ok. But `[!+] Initial
commit.` is excessive.
* Not all possible commits may be described nicely with this system.
For example you fixed bug, extended functionality and renamed variables.
Message `[!*^/] Just merge this and become rich quick!` looks like
spam. I tend to avoid commits with such changes.

## Savior
I've established and used this style in my personal code since something
about 2002, over 14 years now. Recently I was asked for comments about it.
So demonstrating it here, not obligating anyone to use.
