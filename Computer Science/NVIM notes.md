	using nvchad with video from dreams of code on set up for C++
**
debugging: 
in order to debug, you need to set the markers for the compiler for debugging: 
	`clang++ --debug scriptname.cpp -o main`
	- in order to set a watch expression, you move the cursor in the watch section and move into insert mode and name the variable to watch
	- 
Keybinds: 
- append end: A
- append beginning: I
- delete word from start of the word: dw
- delete till end of line: d$
- delete from cursor to end of word including last : de
- bring to beginning of the word: 0
- fix a whole line: U
- redo: ctrl-r
- indent inside curly braces: `>i}` 
- change until end of word: ce
- change the entire line: cc *useful!*
- beggining of the file: gg
- specific line: #+G
- get line number: ctrl+ G
- cycle through searches: n
- cycle backwards: N
- search backwards: ?
- move cursor to matching bracket: % (on a bracket)
- :#,#s/old/new/g sub out in the range of lines
- :%s/old/new/gc: sub out in the whole file but prompting for each one
-  Typing ":set xxx" sets the option "xxx".  Some options are:
        'ic' 'ignorecase'       ignore upper/lower case when searching
        'is' 'incsearch'        show partial matches for a search phrase
        'hls' 'hlsearch'        highlight all matching phrases
     You can either use the long or the short option name.

  7. Prepend "no" to switch an option off:   :set noic
  8. how to close the current window you're in: ctrl + w + c

- set breakpoint: leader (space) + d + b
- start debugging
what is a vim register?

#### multiline editing: 
- go into visual block mode
- highlight the area
- shift + i
- insert what you need to insert
- exit to normal mode
- it will apply


#### Lvim notes
- format - 'lf' - prettier like
- split the window vertically: `:vsplit`

# Vim Regex Guide: Matching from Beginning to Ending Characters

This guide explains how to match strings between two characters using **Vim's regex** engine, particularly useful in Neovim or Vim editors.

---

## ✅ Goal

Match everything **between** a starting and ending character (e.g. quotes, tags, brackets), but only **replace or highlight the text in between**, not the delimiters.

---

## 🔧 Regex Tools in Vim

* `\zs` – Start of match (included in replacement)
* `\ze` – End of match (excluded from replacement)

These markers are **exclusive** — they let you define what part of a match is **actually substituted**.

---

## 🧪 Basic Example: Match Text Between Double Quotes

### Original Text:

```txt
"This is text" and "Another one"
```

### Vim Command:

```vim
:%s/"\zs[^\"]*\ze"/newvalue/g

:%s/class="[^>]*"/class="new-class"/g
--this one matches the pattern and replaces the whole classname tag
```

### Breakdown:

* `"` – match opening quote
* `\zs` – mark the **start** of the actual match
* `[^\"]*` – match everything up to but not including the next `"`
* `\ze"` – mark the **end** of the actual match at the next `"`

### Result:

```txt
"newvalue" and "newvalue"
```

---

## 🧪 Another Example: Match Text Between `>` and `>`

If you have:

```html
<div>First</div><div>Second</div>
```

### Problem:

```vim
/\zs>.*\ze>
```

This will match:

```
>First</div><div>Second<
```

Because `.*` is **greedy**.

### ✅ Fix:

```vim
/\zs>[^>]*\ze>
```

This will match only the content between the **first** pair of `>`s.

---

## 🧠 Tips

* Always use **negated character classes** (e.g. `[^>]`, `[^\"]`) to avoid greediness.
* `\zs` and `\ze` allow fine-grained control over what gets replaced.
* Use `/` to search and `:%s/.../.../g` to substitute across the file.

---

## 🛠️ Example Command Patterns

| Description                 | Command             |
| --------------------------- | ------------------- |
| Match between quotes        | `"\zs[^\"]*\ze"`    |
| Match inside angle brackets | `>\zs[^>]*\ze>`     |
| Match inside parentheses    | `\((\zs[^)]*\ze)\)` |

---

## 💬 Need More Help?

Let me know what specific pattern or structure you're trying to match — HTML, JSON, code blocks, etc., and I can tailor the regex for your case.
