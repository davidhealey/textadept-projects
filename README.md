# textadept-projects
Provides alternative project support to the textadept editor.

## Summary

The [Textadept](http://foicica.com/textadept/) editor is cross platform and extremely fast. Although barebones, it is very extensible via lua.
As I developer, I prefer an editor with speed over an editor with everything builtin. Nothing is more frustrating than to hit a character only to wait on the editor to respond.  That's why I used Textadept as much as possible.

One pain point with Textadept is the project support.  This module was designed to add basic project support to Textadept with these features:

  * Project list
  * Quick open
  * Goto symbol within single file
  * Cross platform (Linux / Windows, OS X _should_ work but needs testing)

In the future, I plan to add the following:

  * Goto definition (via tag file)
  * Goto symbol with project (via tag file)
  * Build commands
  * Automatic linting

I currently use the quickopen tool on projects with over 34,000 files.  It's extremely fast on my machine, but YMMV. I have not tested on any spindle drives, just SSDs.

## Usage

First step is to clone this repo into your ~/.textadept/modules directory.

Next, add the below configuration to ~/.textadept/init.lua. Adapt to your environment as needed.

By default, the following key combinations are available:

  * Alt-g: Goto symbol within file (based on ctags tagging setup below)
  * Alt-o: Quick open within project
  * Alt-p: Project selector to file quick open

Sample Configuration

    local M = {}
    M.project = require 'project'

    keys['alt+g'] = function() M.project.goto_symbol() end
    keys['alt+o'] = function() M.project.project_quickopen() end
    keys['alt+p']= function() M.project.selectProject() end

    M.project.projects = {
        Project1 = {
            types = {}, -- File extensions to include in quickopen, empty=all
            exclude = {"/.git"}, -- Folders to exclude in quickopen
            folders = { -- Folders to find files for quickopen
                "~/dev/project1"
            },
            tagging = { -- file extension based with a default
              default = "ctags --excmd=number --sort=yes  --fields=+KS-sf -f -",
              cs = "ctags --excmd=number --sort=yes  --fields=+KS-sf -f -"
            }
        },
        BigProject2 = {
            types = {"cs","css","less","htm"},
            exclude = {"/.git"},
            folders = {
                "~/dev/project2",
                "~/dev/import/random1",
                "~/dev/import/random2"
            }
        },
        TextAdeptConf = {
            build = {},
            types = {},
            exclude = {"/.git","/.hg","/docs"},
            folders = {
                "~/.textadept"
            }
        }
    }

## Screenshots

Goto Symbol within file
![Goto Symbol](/../screenshots/gotoSymbol.png?raw=true "Goto Symbol within file")

Quick open file within project
![Quick Open](/../screenshots/quickOpen.png?raw=true "Quickopen file within project")

Goto Project
![Goto Project](/../screenshots/gotoProject.png?raw=true "Goto Project")
