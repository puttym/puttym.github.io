---
layout: post
title: "Updating TexLive on Ubuntu"
date: 2020-06-17
category: programming
permalink: update-texlive
---

This post is intended to help you install the *latest* version of TeXLive
(including `pdflatex`, `xelatex`, and many other things). If you haven't
installed TexLive on your system yet, please jump directly to Step 4. These
instructions should also work on Mac, but I have tested them only on an Ubuntu
system.  

Of course, TexLive can be installed from Ubuntu's software repository. While
that method is easier and probably more polular, it never gives you the latest
version of Tex and other related software. Therefore, it's not at all an option
for updating to the latest version.

Let's get started now.

1. **Find out the latest version of TexLive available for installation**\\
   Go to this [page](https://www.tug.org/texlive/acquire-netinstall.html) and check for the
   information on latest version. Currently, it is TexLive 2020.

2. **Find your installed version**\\
   Open a terminal, and run this command:
   ```shell
   tex --version
   ```
   This command will print many lines, but information we want is in the
   very first line. If the year is less than 2020, it's probably a good idea
   to update.

3. **Removing the installed version of TeXLive**\\
   Before installing the latest version of TexLive, it's better to remove
   the version you already have. To remove TexLive completely, run the 
   following commands, one after the other, in a Terminal.

   ```shell
   sudo apt-get purge texlive*
   sudo rm -rf /usr/local/texlive/*
   rm -rf ~/.texlive*
   sudo rm -rf /usr/local/share/texmf
   sudo rm -rf /var/lib/texmf
   sudo rm -rf /etc/texmf
   sudo apt-get remove tex-common --purge
   rm -rf ~/.texlive
   ```

4. **Installing TexLive**\\
   * Download the `.tar.gz` file from the link given [here](https://www.tug.org/texlive/acquire-netinstall.html).

   * Extract the contents of the file to a suitable location. After extraction
   you should see a directory with a name similar to `install-tl-20200615`.
   Inside this directory, among other things, there is a file by name `install-tl`.

   * Open a Terminal, navigate to the aforementioned directory, and run the
   following command.
   ```shell
   perl install-tl
   ```
   This starts the installation process which goes on for a long time (A little
   more than an hour on my laptop).

5. **Updating the `PATH` variable**\\
   After all the packages are installed, we have update the `PATH` variable
   with the installation location of the files. This is just a way of telling
   the computer about the location of executable files related to \*TeX.
   Therefore, whenever we use \*TeX commands, the computer knows where to
   look for the right files.

     *  To update the `PATH` variable, run the following command in the Terminal.
     ```shell
     gedit ~/.bashrc
     ```
     This opens a text editor window. Here we are just editing a text file, and
     you can use any text editor (I generally use GVim).

     Add the following lines to the `/.bashrc` file.

     ```shell
     # TexLive
     export PATH="/usr/local/texlive/2020/bin/x86_64-linux:$PATH"
     export MANPATH="/usr/bin/local/texlive/2020/texmf-dist/doc/man:$MANPATH"
     export INFOPATH="/usr/bin/local/texlive/2020/texmf-dist/doc/info:$INFOPATH"
     ```

     * Save and close the file, and run the follwoing command in the terminal.

     ```shell
     source ~/.bashrc	#Execute ~/.bashrc in the current shell
     hash -r
     which tex
     which xelatex
     which pdflatex
     ```
     The last three commans should print out the path to different programmes
     which you might use.

    Your TexLive installation is complete now.  


**References**
1. [StackOverflow](https://tex.stackexchange.com/questions/95483/how-to-remove-everything-related-to-tex-live-for-fresh-install-on-ubuntu)
2. [Tex User Group](https://tug.org/pipermail/texworks/2016q4/006594.html)
