# vimwiki

## Quickstart 
https://vimwiki.github.io/

Press <Leader>ww to go to your index page. 
By default it is located in ~/vimwiki/index.wiki.

Feed it with the following example:
```
= My knowledge base =
    * Tasks -- things to be done _yesterday_!!!
    * Project Gutenberg -- good books are power.
    * Scratchpad -- various temporary stuff.
```

Place your cursor on Tasks and press Enter to create a link. Press Enter again to open it. Edit the new page, save it, and press Backspace to jump back to your index.
A Vimwiki link can be constructed from more than one word. Just visually select the words to be linked and press Enter. Try it with Project Gutenberg. The result should look something like:

```
= My knowledge base =
    * [[Tasks]] -- things to be done _yesterday_!!!
    * [[Project Gutenberg]] -- good books are power.
    * Scratchpad -- various temporary stuff.
```

See :h vimwiki for the full documentation.

## Key Bindings 
* <Leader>ww – Open the default wiki index file
* <Leader>ws – Select and open wiki index file
* <Enter> – Follow/Create wiki link
* <Backspace> – Go back to parent(previous) wiki link
* <Tab> – Find next wiki link
* <Shift-Tab> – Find previous wiki link
* <Leader>wi – Open the diary wiki index
* <Leader>w<Leader>w – Open diary entry for today 

### ToDO Key Bindings
* Add a checkbox using `ctrl-<Space>`
* Use `gl<Space>` to remove checkbox
* Toggle an item complete use `ctrl-<Space>` with your cursor on the line you want to toggle. 
* Todo lists also work for nested items, simply indent the item. Vim folding works with nested lists. Toggling will also mark all sub-items.
* For an item that might be partially complete, use `gln` to toggle forward completion levels, and use `glp` to toggle backwards completion levels. 
* See `:help vimwiki-todo`

For more keys, see :h vimwiki-mapping

## Commands
:Vimwiki2HTML – Convert current wiki page to HTML
:VimwikiAll2HTML – Convert all your wiki pages to HTML

For more, see :h vimwiki-commandss

## Syntax 
See :h vimwiki-syntax
