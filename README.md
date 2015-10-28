### What's wrong with contentEditable

[Nick Santos (medium) on "Why contentEditable is terrible"](https://medium.com/medium-eng/why-contenteditable-is-terrible-122d8a40e480#.9ufahzkm5)

["Piotrek Koszuliński (CKEditor) on "contentEditable — the good, the bad, and the ugly"](https://medium.com/content-uneditable/contenteditable-the-good-the-bad-and-the-ugly-261a38555e9c#.6ksozblw5)

[Piotrek Koszuliński (CKEditor) on "Fixing contentEditable"](https://medium.com/content-uneditable/fixing-contenteditable-1a9a5073c35d#.g6ectyosw)

[List of contentEditable browser inconsistencies by Guardian](https://github.com/guardian/scribe/blob/master/BROWSERINCONSISTENCIES.md)

### Light at the end of a tunnel?

[The Editing Task Force](http://w3c.github.io/editing/)

### Problematic use cases in the wild

- [Facebook](http://facebook.com) implements rich editing via textarea and an overlayed element on top to visualize mentions
- [Google plus](http://plus.google.com) has `contenteditable="plaintext-only"` which seems to be completely JS-driven plain element
- [Grammarly](http://grammarly.com) implements grammar-correcting-underlines via textarea + element on top (reasons: contenteditable is slow to render, no way to clean markup, hard to do proper selection/annotations)
- Quip has a hybrid editor (each paragraph is a contenteditable line; same with http://notion.so)
- [Trix editor](http://trix-editor.org/) ignores contentEditable and maintains its own internal model (to avoid dealing with x-browser inconsistencies and complexities); same with [ProseMirror](https://github.com/ProseMirror/prosemirror#prosemirror)


### contentEditable=minimal

[Original discussion from June 2014](https://lists.w3.org/Archives/Public/public-webapps/2014AprJun/0296.html)

Julie Parent breaking down potential `contentEditable=minimal` functionality:

1. Selections: Enable selections, perform cursor movement, scoping the boundaries on which the selection can operate.
2. Input: Perform dom modifications, dispatch events, not limited to keyboard input, also includes IME, paste, drop, etc.
3. Spell check: Enable spell check, modify the dom (or dispatch an event) when the user selects a replacement
4. Formatting magic: bold when the user hits control + b, change directionality on Ctrl+LeftShift , etc.

[Piotr Koszuliński on current progress with contentEditable=minimal](https://lists.w3.org/Archives/Public/public-editing-tf/2015Sep/0011.html)

[W3C ticket on contentEditable=plaintext](https://www.w3.org/Bugs/Public/show_bug.cgi?id=14554)

### What about this kind of tiered solution?

| contentEditable value  | Fires events  | Draws cursor | Mutates DOM | Formatting |
| ---------------------- |:-------------:| ------------:| -----------:| ----------:|
| minimal                |   yes         |  no          |    no       |   no       |
| minimal-with-cursor    |   yes         |   yes        |     no      |         no |
| minimal-with-mutation  |   yes         |    yes       |      yes    |         no |
| true                   |   yes         |    yes       |      yes    |        yes |
