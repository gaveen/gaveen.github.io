---
title: My vim story
date: "2020-02-14"
author: 'Gaveen Prabhasara'
categories:
  - Personal
  - Tech
tags:
  - Setup
  - Vim
  - Vimfiles
  - Configuration
  - Linux
draft: true
---

Once you have used 'notepad.exe,' you have used all text editors—they said. A text editor is a text editor is a text editor—they said. After the first few years of running Linux/Unix professionally, I had subconsciously almost agreed with this idea, even though I knew Vim—more accurately, I thought I knew Vim. But when other people who actually knew how to use Vim used it, [Vim](https://en.wikipedia.org/wiki/Vim_(text_editor)) still looked like magic.

If you have worked in a command line at some point, I am sure you can appreciate the wisdom of learning how to use a text editing program properly. On Unix/Linux command lines, text is king. Therefore, learning how to manipulate text effectively goes a long way for your productivity. If you can open a file and edit its content, it enables you to configure your system.

The text editing program I prefer for these kinds of work is Vim. It is also the text editor I can almost always expect to find everywhere I log in—laptops and servers alike. Vim is available on all mainstream operating systems, including Linux, which is my OS of choice.

There are other text editors I use, such as [gedit](https://wiki.gnome.org/Apps/Gedit), [Apostrophe](https://gitlab.gnome.org/somas/apostrophe/), [Helix](https://helix-editor.com/), and even [Visual Studio Code](https://code.visualstudio.com/). But, whenever I am typing something, writing code, or editing a configuration file, I mostly end up with Vim.

Like many before me, I started my text editor journey by running `vim,` promptly feeling lost, failing to exit Vim, and finally resigning to reboot the computer instead. Thus, I initially became an `emacs` user—primarily because `nano` was not well-known then. Eventually, I learned minimum Vim use to get by, just enough to do basic text editing.

Since I knew Vim was much more capable than what I was using, I decided to invest in some actual learning time. It was a good time ago, but it had already been a few years since I started to use Vim daily. Vim has a notorious learning curve, but I feel that is mainly due to its different modes—more on that later. Anyway, I decided I wanted to customize my configuration of Vim (~2009, IIRC). Vim is powerful and versatile—and more importantly, did I mention I like it?

Back in the day, my Vim setup was a jumble of config files and a pile of plugins, dropped into a single directory until it croaked reasonably the way I wanted. It was done out of necessity because Vim did not have decent package management for plugins then. Later, when [Pathogen](https://github.com/tpope/vim-pathogen) came along, I jumped at the opportunity to organize vimfiles better. While Pathogen made it easier to organize vimfiles and manage plugins, it did not have an inbuilt way of tracking changes from multiple plugin sources over time.

At this point, I was already using [`git`](https://git-scm.com/). I was familiar with the then-new [`git submodules`](https://git-scm.com/docs/gitsubmodules) feature. I felt git submodules could be used to manage individual plugins effectively. I looked around to see if anyone had already thought of that. Even though I am pretty sure others may have thought about it—to the best of my knowledge—no one had publicly shared a similar setup. So I did it using git submodules—which became a humble brag for me. These past versions of my Vim configuration files are no longer there. An [archived, later version](https://github.com/gaveen/gavim) is in a git repo if you are curious.

Since then, the most prominent change in maintaining my Vim setup has been the switch to `vim-plug` for plugin management. The excellent vim-plug eliminated the need to juggle git submodules and made the whole process painless.

The sections below will describe the Vim configuration I am using. I will try to keep this post reasonably updated in the future because it might be helpful to someone—just like it helped me to read what others were doing.

A few things to note:
- These should, in theory at least, work with `vim` and [`neovim`](https://neovim.io/).
- When describing below, I have grouped some relevant sections together for convenience. They may be spread around in the actual `.vimrc` file.
- The latest version of my vim configuration can be found in the [`.vimrc` of the git repo](https://github.com/gaveen/vimfiles/blob/master/.vimrc), not this post.

***

## A Few Useful Vim Concepts

Before we begin, I would like to briefly introduce you to a few key vim concepts I wish someone had explained earlier.

**Vim has multiple modes.** Vim is what you call a 'modal' editor, which means Vim has different 'modes' to work with.

As an analogy, think of a smartphone these days. There is a limited number of ways you can interact with it physically, but you have a seemingly boundless amount of things you can do with it. For example, a simple tap on the screen behaves differently based on which mode you are in. The singular touch input in this example can mean different interactions such as waking up the screen, unlocking, launching the camera app, repositioning the focal point, focusing on something, taking a photo, sharing a photo with someone, liking a shared photo in another app, etc. Based on the context (or mode, if you will), a physical thing you do can give different results.

Vim is somewhat like that. There is an `Insert Mode` where you can input text (i.g., typing) into the editor. There is a `Visual Mode` where you can select a section of text to visually track which selection of text you are taking actions on (e.g., copy selected text). Then there is the `Normal Mode` where you do everything else, such as moving around and manipulating text (e.g., cut, copy, paste, delete, etc.).

You can learn more about these modes and how you enter/exit by checking the [Vim Wikibook](https://en.wikibooks.org/wiki/Learning_the_vi_Editor/Vim/Modes).

**Editing with Vim is like programming your text**. Which is a roundabout way of saying that Vim has shortcut keys or key-sequences. You can ask Vim to do simple actions or combine multiple instructions to do more complex ones, which can be intuitive once you learn the basics.

Since you are limited to interacting with software using input devices in your computer, there are bound to be limits to what you can input. Vim works around this by having shortcut keys or key sequences. Notice how I said key 'sequences' and not 'combinations'? Vim usually has shortcuts defined such that you can press keys followed by other keys rather than press them together.

For example, pressing the letter `d` within the `normal mode` tells Vim to 'delete' the next character. If you want to delete the next 5 characters, the instruction becomes `5d`. While `dw` deletes the next word, and `3dw` deletes the next 3 words, `dd` deletes the current whole line of text. `7dd` deletes 7 lines starting with the current. You get the idea.

If we take this a little further, you can say things like "delete text up to the next occurrence of character `,` by pressing `dt,` in the `normal mode` of course. These actions can be repeated by pressing `.`—while in `normal mode.` Want to change the text instead of deleting it? Replace the 'd' with a 'c' (e.g., `ct,`). Want to only select the text visually instead of both delete or change? Use 'v' instead of 'd' or 'c' (e.g., `vt,`). You can also throw directionality into the mix with the `h, j, k, l` as arrow key alternatives.

The good thing is that you do not have to remember everything. You can build up a set of instructions with building blocks, entering one key press at a time. Sort of like conducting an orchestra or programming your text editing. Pretty neat, right?

**You can define your own shortcuts.** Vim allows you to define your custom shortcuts in a couple of different ways, some of which you will see below.

The key is that Vim allows you to prefix your keyboard shortcut sequences with a special key called the `leader` key so that your own shortcuts will not conflict with inbuilt Vim shortcuts. To explain it further, I prefer to set shortcuts that do not break default Vim features, at least logically adjacent to their inbuilt counterparts if there are any, and do not hamper muscle memory in the long run. You can see if the configuration below adheres to this within reason.

**Vim `buffers` are different editing spaces, whereas Vim `tab pages` are not.** 'Vim buffers' should not be confused with 'Vim tab pages' or 'Vim windows.'

A `buffer` in Vim is an editing space in memory. You can have a file already opened there or save it to a file later, or you can discard it. You can have multiple buffers open in a Vim instance.

A `window` in Vim is a view into a buffer. You can decide if you only need a single 'buffer' inside a window. Or, you can decide to open multiple split windows (e.g., horizontal/vertical screen splits) in the same 'buffer.' For example, you can split your screen area into two windows and view two different locations of a file you have opened. However, note that the "window" mentioned here is a vim window (i.e., usually visible as a full-screen or a split-screen area)—not necessarily a graphical window like you are used to.

A `tab page` in Vim is a way to organize Vim windows. Each tab page can have multiple vim windows (e.g., split windows). Therefore, you can have the same buffer viewed inside different tab pages.

While these descriptions are not intuitive, you can see if the following summary helps. Vim help [summarizes this as](https://vimhelp.org/windows.txt.html#windows-intro):
A `buffer` is the in-memory text of a file.
A `window` is a viewport on a buffer.
A `tab page` is a collection of windows.

Trying to use tab pages as different file editing spaces is a common mistake that can lead to confusing errors if you have not grasped the above differences. If you are unsure what to use, try `buffers` first since they are the primitive you need as editing spaces. In Vim, you view them in 'windows' anyway. If you need 'tab pages,' you can introduce them into your workflow later.

**Vim is extensible with plugins.** You can add features/functions not inbuilt by default using plugins, which are programs written in `vimscript` or other programming languages. You will see below which plugins I am using.

To summarize these key concepts:
- Vim has multiple modes
- Editing with Vim is like programming your text
- You can define your own shortcuts
- Vim `buffers` are different editing spaces, whereas Vim `tab pages` are not
- Vim is extensible with plugins

***

## Explaining My Configuration

These are built around the default vim installation environment in the Fedora family of Linux distributions (i.e., including Fedora*, CentOS, and Red Hat Enterprise Linux) because those are my usual work environments.

My .vimrc starts with some basic settings. 
{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "basic.vim" >}}

With the comments accompanying them, these should be pretty self-explanatory. Most of these are basic convenience-oriented settings or improved visual cues.

I should, however, mention the `set autowrite`. According to the Vim documentation, [`autowrite`](https://vimhelp.org/options.txt.html#%27autowrite%27) can save the file automatically on some actions, even if you had not explicitly asked to save (i.e., "write" in Vim terminology).

I like to avoid surprises like this as much as possible. However, `autowrite` is one of these few exceptions I have left because it makes up for convenience. For example, it avoids the annoying 'unsaved content warning' when switching between buffers. If you do not want your content to be automatically saved when you switch between 'buffers,' you should probably avoid setting (i.e., enabling) it.

***

Next up is something that has a more pronounced effect on the text you will be editing—how the `tab` character/key is handled.

I know how polarizing the "Tabs vs Spaces" debate can be. Therefore, I will not get into it. I used to be in the 'tabs' camp, but I switched to using spaces instead of tabs where I could, mainly to get a reasonably consistent visual experience across different environments. However, I understand the accessibility benefit of using tabs for text alignment. People with some vision conditions can opt to increase the tab size. The same is not practical with regular spaces because they exist between every single word. I hope there are accessibility tools that handle these cases better. Ideally, we all should be able to use tab characters and get a consistent look. Unfortunately, tab width is configurable only in limited places. Since I find uneven alignments highly distracting, I opted to keep using spaces until there is a better way.

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "tabs.vim" >}}

I prefer to have 4 spaces per tab because most of the languages I work with these days (e.g., [Rust](https://www.rust-lang.org/)) play nicely with that. The [`smarttab`](https://vimhelp.org/options.txt.html#%27smarttab%27) and [`bs`](https://vimhelp.org/options.txt.html#%27bs%27) settings help with backspace among other things when you use spaces instead of tabs. If you do not set these, using backspace to delete all the expanded tab characters would become tedious.

I also have set Vim to automatically enter spaces when I press the tab key with `set expandtab.`This is another potential pitfall you should note. If you do not want to expand tab characters into spaces, avoid setting [expandtab](https://vimhelp.org/options.txt.html#%27expandtab%27).

Some tools (e.g., Python and Go) do not always handle spaces well when they expect tabs. For those, you need to set exceptions. I have set a few exceptions for tab handling later in the configuration.

***

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "search.vim" >}}

The comments here are pretty self-explanatory. Something to remember is if you set [`ignorecase`](https://vimhelp.org/pattern.txt.html#%2Fignorecase), case sensitivity is ignored everywhere patterns are used. This can lead to tricky situations when you use pattern search and replace types of actions. Therefore, I have left it disabled.

***

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "np.vim" >}}
{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "io.vim" >}}

Most of the settings here are on non-printable characters. Therefore, they do not affect the text you are editing. They only act as visual cues while you are in the editor.

The exception here is [`autoindent`](https://vimhelp.org/options.txt.html#%27autoindent%27), which actually indents text automatically based on the "indentation of the previous line." You can disable this by explicitly using `noautoindent` (i.e., disable temporarily by entering `:set noautoindent` in normal mode or adding `set noautoindent` to .vimrc).

You do not need to use a mouse with Vim—it is, in fact, discouraged. However, IMHO, there is no reason to take advantage of all input methods at your disposal. For example, I sometimes like to scroll at my own speed while visually scanning a file, notice something, and click to start editing there. While I love using Vim (and keyboards), I also am not militant about being keyboard-only. This is why I enabled the mouse too.

***

Vim also has a GUI version, usually called `gvim.`It has an interface similar to usual GUI programs, complete with toolbars, menubars, scrollbars, etc.

When I use gvim, I prefer clean and uncluttered windows, somewhat emulating what the terminal version looks like. If you prefer the GUI elements, you can skip these settings.

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "gvim.vim" >}}

Again, these settings are explained in the comments.

To find the name of your preferred font and always use it in gvim, you can do the following.
- First, in the normal mode of `gvim,` give `:set guifont=*` and hit enter. It will open the font selection dialog of your environment. The font you set this way is only temporary (i.e. until you close vim).
- Once you figure out the preferred selection, in 'normal mode,' give `:set guifont` and hit enter. It will show the name of the current font. You can use the name later in your .vimrc to set the font permanently. Note that you could use the escape character `\` before special characters like spaces in the font name.

In the example, I these days use the "Fira Code" font in the "Retina" typeface at the size "13" points. It translates to `set guifont=Fira\ Code\ weight=450\ 13` in the `.vimrc` file. If you want to set any other monospace font like [Fira Mono](http://mozilla.github.io/Fira/), [Source Code Pro](https://adobe-fonts.github.io/source-code-pro/), [DejaVu Mono](https://dejavu-fonts.github.io/), [Hack](https://sourcefoundry.org/hack/), etc., you can do so with [`guifont`](https://vimhelp.org/options.txt.html#%27guifont%27). If you use vim in a terminal instead of gvim, the font is inherited through terminal settings.

***

Next comes a unique single-line setting.

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "leader.vim" >}}

As explained earlier, Vim lets you define your shortcuts without risking conflicts with defaults, using a "leader," referred to in .vimrc as `<leader>.` The leader key is set to "`\`" by default. Due to the ease of reach, I prefer to set the leader key to be the `,` character. Therefore, `<leader>y` means pressing "`,` and `y`" one after the other.

Would this not conflict with inserting a comma?—you might wonder. There will be no conflict because you type in (i.e., insert) commas of your text in `insert mode` while you invoke shortcuts in `normal mode`.

***

Next is another preference part—plugin management. Vim also has an inbuilt plugin manager since version 8. However, I have not looked enough into it. Since my current setup works really well, I did not have a need to change it either.

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "plugins.vim" >}}

I use [`vim-plug`](https://github.com/junegunn/vim-plug) (by Junegunn Choi) as the plugin manager. It is written in vimscript. Therefore, does not need external runtimes or complex manual installation steps. With 'vim-plug,' installing and keeping plugins up-to-date is a breeze.

Plugins are defined between the 'vim-plug' invocations of `call plug#begin()` and `call plug#end().` I pass the parameter `'~/.vim/bundle'` to `call plug#begin()` to inform where to install my plugins. In this example, the parameter is a directory named `bundle` located inside the vim files directory `~/.vim.` I have it there because it is a leftover from when I used a different plugin manager.

I am not going to go one by one in this plugin list. However, as you can see above, I have grouped my plugins into a few areas:
- "Augment Vim behavior"
- "Augment UI elements"
- "Augment filetype handling and syntax highlighting"
- "Add utility"
- "Add colorschemes"

Since all of my plugins are added via GitHub, you can find out more by visiting the relevant repository pages. To get the URL of each plugin repository page, append the name in the plugin definition after "`https://github.com/`". For example, "easymotion/vim-easymotion" repository can be found at ["https://github.com/easymotion/vim-easymotion"](https://github.com/easymotion/vim-easymotion).

Some of these plugins either need to be configured or can be configured. Some of the features enabled by these plugins, along with the shortcuts they introduce, are documented in the [`README.md`](https://github.com/gaveen/vimfiles/blob/master/README.md) file of [the git repo](https://github.com/gaveen/vimfiles).

***

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "generic.vim" >}}
{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "ft.vim" >}}

These are pretty self-explanatory with the help of included comments.

One thing to note is the section where I have included tab behavior exceptions (e.g., for [Ruby](https://www.ruby-lang.org/) and [Go](https://golang.org/)) as I mentioned earlier. Some other exceptions are handled automatically by file-type plugins.

***

If you look closely at the sections of the same `.vimrc` file I have been explaining, you will notice it has a syntax. As I mentioned earlier, Vim has an inbuilt scripting language. You can use this language to write custom functions to make things easier for you by scripting them.

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "func_diff.vim" >}}

In the above example, there is a function with the name "`DiffWithSaved()`" which combines inbuilt features of Vim to find if there have been changes since you last saved. If there are, it will present the differences between the last saved state and the current state in a view similar to the Unix `diff.` Finally, it can be invoked with "`DiffSaved`."

I have defined a few more functions as well. Please note that `ToggleFullScreen()` function has an external dependency, an external program named `wmctrl`.

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "func_qfix.vim" >}}
{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "func_fullscreen.vim" >}}

While these functions define what to do, they are not automatically invoked. I have chosen to call them via shortcut keys or function keys.

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "map_shortcuts.vim" >}}

You can see that in the above, `DiffSaved` and `QuickfixToggle()` are configured to be invoked with `<leader>?` and `<leader>q` respectively. In my configuration, this respectively translates into pressing `,?` and `,q`.

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "map_cp.vim" >}}
{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "map_misc.vim" >}}

I have mapped some common shortcuts to cut/copy/paste with clipboard in `gvim.`These complement the inbuilt `x`, `y`, `p` for cut/copy/paste respectively, but for external clipboard (e.g., OS clipboard). I also have `<leader>v` (i.e., `,v`) to select the text pasted into Vim right after it was pasted.

In addition to custom shortcut keys, I have also mapped a few function keys (e.g., F1 - F12 keys in the keyboard) to do useful things.

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "map_fkeys.vim" >}}

You might notice that the convention I use is that function key mappings only change the editor environment, whereas anything that affects the actual text is mapped as shortcuts with a "leader" prefix.

In the above, I have remapped the F1 key as another `ESC` key to avoid accidental F1 key presses when reaching `ESC.` F4 toggles spellchecking, F7 uses the `junegunn/limelight.vim` plugin, and F11 calls the above-mentioned `ToggleFullScreen()` function. The rest should be self-explanatory.

I also have a shortcut for when you edit a file away, forgetting to open it with `sudo` privileges beforehand. Instead of pulling your hair out and starting from scratch, the following makes it convenient to use (i.e., instead of using `:w` to save, type `:w!!` to save with 'sudo' privileges).
{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "sudo.vim" >}}

***

I mentioned earlier that `buffers` are the way to go when you need multiple files open. The following section of the settings maps a few shortcut keys to make switching between buffers faster.

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "buffers.vim" >}}

In addition, I have also configured the plugin [`buftabs`](https://www.vim.org/scripts/script.php?script_id=1664) here. It shows which files you have opened at the bottom of the vim window. You can not point and click it to switch between buffers, but it is a minimalist indication of opened 'buffers' and statuses.

***

Finally, we have the exciting part—colorscheme! The first two lines, `termguicolors` and `background` set two values explicitly rather than trying to derive them from the environment.

{{< gist gaveen 4d32d0200ae49c0489be44d8cbf21cfc "colorscheme.vim" >}}

My `termguicolors` setting explicitly says that my terminal supports GUI colors. It does in my case because I mostly use [GNOME Terminal](https://gitlab.gnome.org/GNOME/gnome-terminal) that comes with [Fedora](https://getfedora.org/). If your terminal does not support GUI colors, setting this might break how colors are shown.

My `background` setting is to make my terminal background dark. Like many people who need to stare at a screen for a long time, I prefer dark themes whenever I have the option. Some colorschemes select between dark and light versions based on this value. This is why I have made 'dark' explicit. If you prefer a light, you can set it to 'light.'

If you do not need either of these two, then you should not set them because some colorschemes would look weird if you set the values differently from what they are expecting or capable of handling.

With those out of the way, I finally set a colorscheme. My colorscheme of choice has changed over time. These days, I prefer a theme called "[One](https://github.com/rakr/vim-one)," which has both a light and dark version (picked based on the `background` setting).

The end result should look something like [this (screenshot on Imgur)](https://i.imgur.com/lETk5yt.png).

***

That is about it for this post. Since it is already long, I did not try to include further details, like what the plugins do or which shortcuts they introduce. If you would like to hear about these details—or want to give me your comments—please let me know via [email](mailto:gaveen@gaveen.me?Subject=[Comment]%20gaveen.me%20-%20My%20Vim%20Story) or [@s](https://hachyderm.io/@gaveen).

_PS:_ I also re-posted this in [dev.to](https://dev.to/gaveen/my-vim-story-594d) where it gained a significant amount of interest (_e.g.,_ featured in the weekly "must-reads" list). Since this meant a lot more people read it there, the dev.to re-post is now another place where you can join the conversation. But this post remains the canonical source.
