---
title: 'Creating Bashstrap: bootstrap for your terminal'
author: bazclark
layout: post
permalink: /creating-bashstrap/
dsq_thread_id:
  - 1681486643
categories:
  - Tech
---
[Bashstrap][1] is a quick way to spruce up OSX terminal. It cuts out the fluff, adds in timesaving features, and provides a solid foundation for customizing your terminal style.<!--more-->

![bashstrap screenshot][2]

## Feature list

### Faster directory navigation

*   Open your current directory in Sublime Text (with just 2 characters)
*   Jump directories rapidly, without having to set aliases—using Z (my favorite feature!)
*   Tab bar displays your current directory
*   Lots of quick shortcut aliases that I use for git and moving around directories

### Customized bash prompt line

*   Git branch status inline
*   ☠ ahoy! An easily customizable symbol 
*   Stripped out extraneous text 

### Updated color scheme

*   Colored &#8216;ls&#8217;
*   Syntax highlighted &#8216;cat&#8217;

[Install via Github (takes 10 mins)][1]

* * *

In the rest of this post I&#8217;ll go into detail on how I configured the features. I&#8217;m not an expert at customizing terminal—if you notice anything that could be improved, please leave a comment or open a pull request.

## Supports

### Bash, not zsh

I don&#8217;t have a need for any of [z shell&#8217;s features][3] so I decided not to go that route. Bash is capable of a lot of those features now, like command-line completion. I looked at [oh-my-zsh][4] briefly, but there weren&#8217;t any themes to my liking.

### iTerm, not Terminal

This was primarily because I had a lot of difficulty customizing the stock terminal that comes with OSX. It was way easier to edit colors and preferences in iTerm 2. There are some [iTerm features][5] that I&#8217;d expect to use in the future too.

### Sublime Text, not Vim

I use Sublime Text for virtually all text editing so decided to leave out the .vimrc that customizes Vim.

## File Organization

File organization based on [Mathias Bynens epic dotfiles][6].

The installation notes on the repo cover installing to your home directory, which is where OSX looks for your dotfiles. This works perfectly, but I found that housing my dotfiles in their own folder and symlinking to them from my home directory gave a lot of advantages.

It makes it easier to backup, version and share my dotfiles by creating a Github repo for them. There&#8217;s even a landing page dedicated to [dotfiles on Github][7].

To install to a folder:

1.  Fork and clone the [Bashstrap repo][1] to a subfolder of your home directory. I keep my dotfiles in ~/Code/dotfiles.

2.  Backup your current dotfiles (optional)
    
        cp ~/.bash_profile ~/.bash_profile_old
        cp ~/.bashrc ~/.bashrc_old
        cp ~/.gitconfig ~/.gitconfig_old
        

3.  Create symlinks to the new dotfiles
    
        ln -s ~/.bash_profile ~/your/path/to/.bash_profile
        ln -s ~/.bashrc ~/your/path/to/.bashrc
        ln -s ~/.gitconfig ~/your/path/to/.gitconfig
        ln -s ~/.gitignore ~/your/path/to/.gitignore
        ln -s ~/.hushlogin ~/your/path/to/.hushlogin
        

Side note: I wish I&#8217;d realized there&#8217;s a [Sublime Text syntax highlighting package for dotfiles][8] before I started work on customizing them. It&#8217;s really helpful!

## Productivity Features

### Open files and directories in Sublime Text

There are multiple ways to set this up, some more complicated than others. The best I found is a this one-liner that&#8217;s included in the .bash_profile.

*   alias s=&#8217;open -a &#8220;Sublime Text 2&#8243;&#8216;

This enables you to just type &#8220;s .&#8221; to open the current directory in Sublime Text. Or &#8220;s file-name.ext&#8221; to open a file.

### Z directory jumping

Possibly my favorite feature is Z (not to be confused with zsh, which is a totally different thing).

Z removes a lot of the need for cd&#8217;ing around directories. Instead you type &#8220;z&#8221; then any substring of the name of the directory you want to jump to. For example I can be in any dir and type &#8220;z dotf&#8221; to jump straight into my dotfiles dir. This means I don&#8217;t need to bother setting up aliases for frequently visited directories! It works really really well.

You need to cd around a bit after installing it so that it builds up a memory of the directories you visit. Here&#8217;s the [Z repo][9].

### Changing the bash prompt

My bash prompt is simply &#8220;[user] in [current-directory] on [current-git-branch]&#8220;, where current-git-branch will only display if I&#8217;m within a dir that has a git repo. This came straight from [@gf3&#8242;s bash prompt][10]. I really dig it, and made a few customizations.

For more bash prompt hacking, this [Reddit topic][11] contains a lot of good inspiration, and this [Stack Overflow][12] too.

### Silence the &#8220;welcome, last login was at X&#8221; message

.hushlogin is awesome. Credit to [Mathias][13].

### Display the current dir name as the tab title

With multiple tabs open it&#8217;s nice to be able to see what&#8217;s going on in them. I found a [nice little one-liner for this on Stack Exchange][14], it now lives in my .bash_profile. It displays just the name of the current directory as the tab title.

### Aliases

Z is amazing and eliminates a lot of the need for aliases but there are still some spots where they&#8217;re useful. I added in &#8220;..&#8221;, &#8220;&#8230;&#8221; and &#8220;&#8230;.&#8221; to skip back 1, 2 or 3 directories. I stuck in a couple of aliases to directories that I use frequently too, these can be easily customized and added to.

I use &#8220;ls&#8221; and &#8220;ls -la&#8221; a lot, so there are a number of ls aliases. Typing &#8220;l&#8221; gives you the colorized list in long format, and &#8220;la&#8221; includes dotfiles in the list. These show the directories in blue, which is nice for scannability.

If you&#8217;d like &#8220;cat&#8221; with syntax highlighting you can use the &#8220;c&#8221; alias. You&#8217;ll just need to install [Pygments][15] first.

### Shortcut key binding

Binding shortcut keys to things I want (delete previous word, skip to EOL, etc) seems like a pain in the ass. Instead I opted to get used to the bash shortcuts. Here&#8217;s a [list of the shortcuts I use the most][16].

## Style Updates

I installed [iTerm 2][17] because color tweaking in OSX terminal was a painful process and taking me hours. iTerm 2 lets you preview as you select from the color pallete, which rocks.

### Font

I played around with a lot of fixed width fonts, including Adobe&#8217;s [Source Code Pro][18], and in the end settled on Menlo that comes with OSX. I like 16pt Menlo regular. This can be changed in iTerm Preferences > Profiles > Default > Text > Regular Font (make sure you change the Non-ASCII version to be the same too).

It looks a lot better without bold too. I switched to the non-bold font by unchecking &#8220;Draw bold text in bold font&#8221; in iTerm Preferences > Profiles > Default > Text > Text Rendering.

### Color scheme

The bash prompt edits in .bash_profile took care of a lot of the coloring. But there were still a few things that needed tweaking.

I wanted a lighter blue for the directory highlighting. The quickest way I found to change this was by changing the iTerm blue color. iTerm Preferences > Profiles > Default > Colors > click Blue and make it lighter.

### Cursor

While you&#8217;re in the iTerm color settings you might notice cursor colors too. These are really fun to change! Bright green or pink make really nice cursor colors. Click the &#8220;Smart cursor color&#8221; checkbox, then you can edit Cursor color.

I also like having selection text as the same color as the cursor. I went for bright green, with black text.

Also, my preference is for the thin vertical bar cursor. This can be change in iTerm Preferences > Profiles > Default > Text > Cursor.

### Unicode symbol

The avatar of the bash prompt! I made this really easy to change by creating a variable for it in .bash_profile. Just command+f for &#8220;symbol&#8221;. A few favorites: ⚡ ☠ ☢ ♥. [Tables worth of symbols here][19] to copy paste in.

## That&#8217;s all for now!

All of these tweaks and features are included, it only takes 10 minutes to install.

[Bashstrap on Github][1]

 [1]: https://github.com/barryclark/bashstrap
 [2]: https://raw.github.com/barryclark/bashstrap/master/screenshot.png
 [3]: http://en.wikipedia.org/wiki/Z_shell#Features
 [4]: https://github.com/robbyrussell/oh-my-zsh
 [5]: http://www.iterm2.com/#/section/features/
 [6]: https://github.com/mathiasbynens/dotfiles
 [7]: http://dotfiles.github.io/
 [8]: https://github.com/mattbanks/dotfiles-syntax-highlighting-st2
 [9]: https://github.com/rupa/z
 [10]: https://github.com/gf3/dotfiles
 [11]: http://www.reddit.com/r/programming/comments/697cu/bash_users_what_do_you_have_for_your_ps1/
 [12]: http://stackoverflow.com/questions/103857/what-is-your-favorite-bash-prompt
 [13]: https://github.com/mathiasbynens/dotfiles/blob/master/.hushlogin
 [14]: http://apple.stackexchange.com/questions/90725/for-iterm2-how-do-i-make-the-working-directory-appear-in-the-window-title/90737#90737
 [15]: http://pygments.org/
 [16]: http://www.howtogeek.com/howto/ubuntu/keyboard-shortcuts-for-bash-command-shell-for-ubuntu-debian-suse-redhat-linux-etc/
 [17]: http://www.iterm2.com/#/section/home
 [18]: http://blogs.adobe.com/typblography/2012/09/source-code-pro.html
 [19]: http://en.wikipedia.org/wiki/Unicode_symbols