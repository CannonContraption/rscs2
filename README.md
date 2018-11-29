# RSyncCStation Version 2
## Introduction
Built to sync folders. This script is basically a wrapper around RSync in order to allow for quick syncing of common files. Sort of a replacement for dropbox or similar.
## Where did the name come from?
This program started out as a shell script to replace a copy of Synology CloudStation back in 2015. This was because at the time, CloudStation did not support manually triggering a sync operation. This was causing real downtime since it was being used to sync a laptop and a desktop between classes.

So, rscs was born. One raspberry pi with SSH, a copy of RSync, and a little scripting later, and a single folder could be incrementally synced rather quickly from the command line. This was really just to avoid having to type the rsync command over and over again.

This version was born out of the need to speed this process up. Originally, the script synced one directory. All of its contents was synced every time, and this wasn't always neccesarily changing files. Things like dotfiles may not have changed at all, yet they were still being checked, eating up massive amounts of time. Rewriting the whole thing in python to support targets, complete with a few extra features, made a lot of sense. That's what rscs2 is.

/history
## Basic Useage
rscs2 is built to be simple to use from a number of arguments standpoint. Note that the script needs some targets configured first, that is described in the next section.

In order to run the program, use the following pattern:

    rscs2 [options] [targets]

replace [options] with any options in this section you want to use. Replace [targets] with any targets that you want to sync to

All of the available options are described below. You may intersperse targets and options as much as you like, since the parse code does not care what order they are put.

### -r // --remote
Use the remote server rather than the local one. rscs2 includes sections for bot a default local and default remote server.

### -s (server) // --server (server)
Specify a server. This allows for temporary use of a system other than the defaults.

### -p (port) // --port (port)
Specify a port. Useful when SSH isn't on port 22 and 22 is the default, or similar situations.

### -u (username) // --username (username)
Specify a username. Useful when this doesn't match on the default and for this machine.

### --upload
Only upload incremental file changes, do not download them.

### --download
Only download incremental file changes, do not upload them.

## Specifying Targets
This is a simple affair, for the most part. rscs2 is written in python, and the program itself contains all of the configuration settings needed in order to operate. They are all well-labelled at the top of the file.

As an example, here's a simple starter target list:

    syncdirs = [
		  ("rscs1", "/home/joe/SyncMe", []),
		    ("lmms", "/home/joe/lmms", ["*.ogg", "*.wav", "*.mp3"])]; # Excludes exported audio

To add more targets, add a comma before the last ] and open a tuple.

Targets use this syntax:

    ("targetname", "/path/to/target", ["*.excluded", "*.file", "*patterns", "*.list"])

where targetname is a single word, the path to the target is a valid path on the client and server computer, and the excluded file patterns are regex expressions for files to exclude from sync operations.

# Example
## Command
rscs2 -r dotfiles school work

## Program Configuration

	syncdirs = [
	  ("dotfiles", "/home/joe/doc/dotfiles", []),
	  ("school", "/home/joe/doc/school", ["*.class", "*.o", "*.out"]), #Excludes compiled source
	  ("work", "/home/joe/doc/work", [])]

    #server parameters
	server = "192.168.0.33"
	port = "22"
	server_remote = "wykkid.awesome.dnsna.me"
	port_remote = "2000"
	username = "joe"

## Description
This invokes rscs2 and tells it to use its default remote server. From there, it tries to sync the dotfiles, school, and work targets as specified in the header of the program.
