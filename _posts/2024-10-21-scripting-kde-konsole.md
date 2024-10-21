---
layout: post
title: Scripting KDE Konsole
description: Automate KDE Konsole layouts and command running using dbus, exemplified with fish shell scripts.
image: 
tags:
  - fish
  - konsole
  - kde
  - dbus
  - just
  - tips
---
I finally got(took) the time to automate away the 2 seconds it takes me to set up my [Konsole][1] development layout. Given the sparse examples showing Konsole's DBus interface and its quirks in action, I thought it made sense to share my script here. 

Having recently moved from Bash to [Fish][2], I rediscovered the joy of shell scripting and added some git and [just][3] checks as well.

The following Fish function results in a three-pane window with Vim to the right taking up 65% of my screen leaving two top-to-bottom split panes showing potential information from git or just.

```fish
function git_summary -d "check if you are in a git repository and show git-related information"
    if git rev-parse --is-inside-work-tree >/dev/null 2>&1
        git status
        git worktree list
    else if test -d .git
        git worktree list
    end
end

function just_summary -d "check if a justfile exists and list the available commands"
    if test -f justfile
        just --list
    else
        echo "No justfile found"
    end
end

function dev -d "From the existing session setup a three-pane layout with git status, nvim, and just --list"
    # Setup layout
    set PRIMARY_SESSION_ID (qdbus $KONSOLE_DBUS_SERVICE /Windows/1 org.kde.konsole.Window.currentSession)

    qdbus $KONSOLE_DBUS_SERVICE /konsole/MainWindow_1 org.kde.KMainWindow.activateAction split-view-left-right > /dev/null
    set EDITOR_SESSION_ID (qdbus $KONSOLE_DBUS_SERVICE /Windows/1 org.kde.konsole.Window.currentSession)

    qdbus $KONSOLE_DBUS_SERVICE /Windows/1 org.kde.konsole.Window.setCurrentSession $PRIMARY_SESSION_ID

    qdbus $KONSOLE_DBUS_SERVICE /konsole/MainWindow_1 org.kde.KMainWindow.activateAction split-view-top-bottom > /dev/null
    set SECONDARY_SESSION_ID (qdbus $KONSOLE_DBUS_SERVICE /Windows/1 org.kde.konsole.Window.currentSession)

    # NOTE: qdbus does not appear to work with the resizeSplits method: https://invent.kde.org/utilities/konsole/-/merge_requests/932#note_837270
    gdbus call --session --dest $KONSOLE_DBUS_SERVICE --object-path /Windows/1 --method org.kde.konsole.Window.resizeSplits 0 "[35, 65]" > /dev/null

    qdbus $KONSOLE_DBUS_SERVICE /konsole/MainWindow_1 org.qtproject.Qt.QWidget.showFullScreen

    # Finally run the various commands in the right panes
    qdbus $KONSOLE_DBUS_SERVICE /Sessions/$EDITOR_SESSION_ID org.kde.konsole.Session.runCommand "nvim ."
    qdbus $KONSOLE_DBUS_SERVICE /Sessions/$PRIMARY_SESSION_ID org.kde.konsole.Session.runCommand "git_summary"

    # TODO: it seems like bash is always initiated before fish, for an unknown reason
    set FUNCTION_FILE (status --current-filename)
    qdbus $KONSOLE_DBUS_SERVICE /Sessions/$SECONDARY_SESSION_ID org.kde.konsole.Session.runCommand "fish -c 'source $FUNCTION_FILE; just_summary'"
end
```

Note that `$KONSOLE_DBUS_SERVICE` is only available from Konsole itself, some alternatives are available as per the [Konsole manual][4]. I wasn't able to get `qdbus` to work with Qt arrays so I used `gdbus`(I'm on a Gnome-based system but I prefer the syntax of `qdbus`.). It's odd that in my final panel, I need to run fish manually as my default shell is fish, I'm a little worried that there is an underlying problem. 

[1]: https://apps.kde.org/konsole/
[2]: https://fishshell.com/
[3]: https://just.systems/
[4]: https://docs.kde.org/stable5/en/konsole/konsole/scripting.html

