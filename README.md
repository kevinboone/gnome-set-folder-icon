# gnome-set-folder-icon

## What is this?

`gnome-set-folder-icon` is a simple script that searches one or more
directories for a file that denotes an icon to be used when displaying the
directory in a Gnome file manager (e.g., Nautilus). If such a file is found,
the script uses the `gio` command to set it as the folder icon.

Many audio players that handle album cover art add a file to the directory that
contains the audio files, with one of a number of conventional filenames. The
Cablibre e-book utility also does so. However, you can add any image to any
directory, and use it as the folder icon.

The filenames that are tested are all combinations of the names 'cover',
'folder', 'Folder', and '.folder', and the extensions '.png', '.jpg', and
'.gif'. It is easy to add to these names (or remove from them) by editing the
values of `NAMES` nd `EXTS` in the script.

It's possible to use the Nautilis "Properties" function to select an icon
for a specific directory. The purpose of this utility is to speed things
up, when there might be hundreds of directories.

## Usage

    $ gnome-set-folder-icon {directory 1} {directory 2}...

The script accepts relative directory paths, but Gnome expects full pathnames
for both the directory and the icon file, so they have to be expanded.  The
utility will cope with spaces in filenames but, because it is just a shell
script, it's difficult to guarantee that every odd combination of characters in
a directory name will be handled correctly. 

## Processing directories recursively

`gnome-set-folder-icon` does not recurse directories. If you want to scan
a whole tree of directories, you can do it like this: 

    $ find {dir} -type d -exec gnome-set-folder-icon "{}" \;

## Notes

The usage of the `gio` command for this application is:

    $ gio set -t string {dir} metadata::custom-icon file://[icon_path]

This utility does not add or modify any data in the specified directory -- it
only sets gnome metadata attribute `custom-icon`. It follows that any changes
made are only for a specific user. 

To revert to the default icon for a specific directory, unset the `custom-icon`
attribute like this: 

    $ gio set -t unset {dir} metadata::custom-icon

# Legal and author

`gnome-set-folder-icon` was written by Kevin Boone, and released into the
public domain. Do whatever you like with it, with my compliments.

