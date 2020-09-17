<p align="center">
    <img src="img/kb_logo.png?raw=true" width="200"/>
</p>

# kb. A minimalist knowledge base manager


Author: gnc <nebbionegiuseppe@gmail.com>

Copyright: © 2020, gnc

Date: 2020-09-11

Version: 0.1.1


## PURPOSE

kb is a text-oriented minimalist command line knowledge base manager. kb
can be considered a quick note collection and access tool oriented toward
software developers, penetration testers, hackers, students or whoever
has to collect and organize notes in a clean way.  Although kb is mainly
targeted on text-based note collection, it supports non-text files as well
(e.g., images, pdf, videos and others).

The project was born from the frustration of trying to find a good way
to quickly access my notes, procedures, cheatsheets and lists (e.g.,
payloads) but at the same time, keeping them organized.  This is
particularly useful for any kind of student. I use it in the context
of penetration testing to organize pentesting procedures, cheatsheets,
payloads, guides and notes.

I found myself too frequently spending time trying to search for that
particular payload list quickly, or spending too much time trying to find
a specific guide/cheatsheet for a needed tool. kb tries to solve this
problem by providing you a quick and intuitive way to access knowledge.

In few words kb allows a user to quickly and efficiently:

- collect items containing notes,guides,procedures,cheatsheets into
  an organized knowledge base;
- filter the knowledge base on different metadata: title, category,
  tags and others;
- visualize items within the knowledge base with (or without) syntax
  highlighting;
- grep through the knowledge base using regexes;
- import/export an entire knowledge base;

Basically, kb provides a clean text-based way to organize your knowledge.


## INSTALLATION

The installation of kb can be performed by simply doing:
```sh
git clone https://github.com/gnebbia/kb
cd kb
pip install -r requirements.txt
python setup.py install
```

**Tip** for GNU/Linux and MacOS users: For a better user experience,
also set the following kb bash aliases:
```sh
cat <<EOF > ~/.kb_alias
alias kbl="kb list"
alias kbe="kb edit --id"
alias kba="kb add"
alias kbv="kb view --id"
alias kbd="kb delete --id"
alias kbg="kb grep"
alias kbt="kb list --tags"
EOF
echo "source ~/.kb_alias" >> ~/.bashrc
source ~/.kb_alias
```

**Tip** for Windows users: Do not use notepad as %EDITOR%, kb is not
compatible with notepad, a reasonable alternative is notepadd++.

## USAGE

A quick demo of a typical scenario using kb:

![](img/kb_general_demo.gif)

A quick demo with kb aliases enabled:

![](img/kb_general_demo_alias.gif)

A quick demo for non-text documents:

![](img/kb_non_text_demo.gif)

### List artifacts

#### List all artifacts contained in the kb knowledge base:
```sh
kb list

# or if aliases are used:
kbl
```
![](img/kb_list_all.gif)

#### List all artifacts containing the string "zip":
```sh
kb list zip

# or if aliases are used:
kbl zip
```
![](img/kb_list_title_zip.gif)

#### List all artifacts belonging to the category "cheatsheet":
```sh
kb list --category cheatsheet
# or
kb list -c cheatsheet

# or if aliases are used:
kbl -c cheatsheet
```
![](img/kb_list_category.gif)

#### List all the artifacts having the tags "web" or "pentest":
```sh
kb list --tags "web;pentest"

# or if aliases are used:
kbl --tags "web;pentest"
```
![](img/kb_list_tags.gif)

#### List using "verbose mode":
```sh
kb list -v

# or if aliases are used:
kbl -v
```
![](img/kb_list_verbose.gif)


### Add artifacts

#### Add a file to the collection of artifacts
```sh
kb add ~/Notes/cheatsheets/pytest

# or if aliases are used:
kba ~/Notes/cheatsheets/pytest
```
![](img/kb_add.gif)

#### Add a file to the artifacts
```sh
kb add ~/ssh_tunnels --title pentest_ssh --category "procedure" \
    --tags "pentest;network" --author "gnc" --status "draft"
```
![](img/kb_add_title.gif)

#### Add all files contained in a directory to kb
```sh
kb add ~/Notes/cheatsheets/general/* --category "cheatsheet"
```
![](img/kb_add_directory.gif)

#### Create a new artifact from scratch
```sh
kb add --title "ftp" --category "notes" --tags "protocol;network"
# a text editor ($EDITOR) will be launched for editing
```
![](img/kb_add_from_scratch.gif)

### Delete artifacts

#### Delete an artifact by ID
```sh
kb delete --id 2

# or if aliases are used:
kbd 2
```

#### Delete multiple artifacts by ID
```sh
kb delete --id 2 3 4

# or if aliases are used:
kbd 2 3 4
```
![](img/kb_delete_multiple.gif)

#### Delete an artifact by name
```sh
kb delete --title zap --category cheatsheet
```
![](img/kb_delete_name.gif)


### View artifacts

#### View an artifact by id
```sh
kb view --id 3
# or
kb view -i 3

# or if aliases are used:
kbv 3
```
![](img/kb_view.gif)

#### View an artifact by name
```sh
kb view --title "gobuster"
# or
kb view -t "gobuster"
```
![](img/kb_view_title.gif)

#### View an artifact without colors
```sh
kb view -t dirb -n
```
![](img/kb_view_title_nocolor.gif)

#### View an artifact within a text-editor
```sh
kb view -i 2 -e

# or if aliases are used:
kbv 2 -e
```
![](img/kb_view_in_editor.gif)


### Edit artifacts

Editing artifacts involves opening a text editor.
Hence, binary files cannot be edited by kb.

The editor can be set by the "EDITOR" environment
variable.

#### Edit an artifact by id
```sh
kb edit --id 13

# or if aliases are used:
kbe 13 
```
![](img/kb_edit.gif)

#### Edit an artifact by name
```sh
kb edit --title "git" --category "cheatsheet"
# or
kb edit -t "git" -c "cheatsheet"
```

### Grep through artifacts

#### Grep through the knowledge base
```sh
kb grep "[bg]zip"

# or if aliases are used:
kbg "[bg]zip"
```
![](img/kb_grep.gif)

#### Grep (case-insensitive) through the knowledge base
```sh
kb grep -i "[BG]ZIP"
```
![](img/kb_grep_case_insensitive.gif)

#### Grep in "verbose mode" through the knowledge base
```sh
kb grep -v "[bg]zip"
```

### Import/Export/Erase a knowledge base

#### Export the current knowledge base
```sh
kb export
```
This will generate a .kb.tar.gz archive that can
be later be imported by kb.
![](img/kb_export.gif)

#### Import a knowledge base
```sh
kb import archive.kb.tar.gz
```
**NOTE**: Importing a knowledge base erases all the previous
data. Basically it erases everything and imports the knowledge base.
![](img/kb_import.gif)

#### Erase the entire knowledge base
```sh
kb erase
```
![](img/kb_erase.gif)


## NOTES

## COPYRIGHT

Copyright 2020 Giuseppe Nebbione.

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.
