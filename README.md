* RSyncCStation Version 2
** Introduction
Built to sync folders. See my older repository for the version 1 and real rationale.
** New in version 2
The script uses tuples to define directory and label structures, and allows for syncing specific folders at a time, each with their own specific exclude patterns. There's also the option to sync all the folders at once, starting at the first in the tuple list all the way to the last in order. Also allows for username specification in the command line and a looser, less strict argument ordering structure.
** From the comments in the file...
RSyncCStation Version 2!

Rationale:
the original rscs was quite robust, and was fairly easy to modify. That said, being written in BASH it carried over the limitations of BASH, and thus would only really allow for one directory to sync per instance of the file.

So how does it work?

To use rscs2, simply put directories in the array below. You'll note each element in the array is a tuple, with three elements. Two are strings, one is an array. The first string is the target. This should be a simple pneumonic you can type quickly and remember easily. It's the folder identifier for that path. The second argument is the path (should be a full path for compatibility and stability sake). The third argument is an array of directory-specific excluded patterns. See below for examples."""

    syncdirs = [
      ("rscs1", "/home/joe/SyncMe", []),
      ("lmms", "/home/joe/lmms", ["*.ogg", "*.wav", "*.mp3"])]; # Excludes exported audio