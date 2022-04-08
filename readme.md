# 3MF ZIP Uncompressed

This is an experiment in seeing whether repacking a 3MF OPC ZIP archive into a
new archive with "store" compression (uncompressed) will make the changes to the
3MF file diffable and make the whole file a better fit for version control.

The process is as follows:

- Start a new project in PrusaSlicer with default settings
- Right-click the print bed and select Add Shape > Box with default dimensions
- Save the project as `box.3mf`
- Run `unzip box.3mf -d box` to extract the 3MF OPC ZIP into a directory `box`
- Run `zip -r box -0 box` to create a new archive, `box.zip` with no compression
- Turn off the lock next to the box properties Scale and Size
- Scale the box up twice the size by setting `50` for its Size on the Z axis
- Save the project again under the same name
- Delete the `box` directory to not clash with the `unzip` command
- Run `unzip box.3mf -d box` again to generate a new extraction of the project
- Run `zip -r box -0 box` to update the archive with no compression

At this point, VS Code will detect the ZIP archive is a binary file and will not
diff it. It can be forced to view it using the default text editor, but even in
that case it will not attempt to diff it.

GitHub will show the file as binary and will not offer a way to force-diff it.
It does offer a link to view the raw file, but it downloads the file instead of
diffing or at least viewing it in the browser.

Since Git detects binary files not by extension, but by a slice of the file's
contents, it will always reject ZIP files because their extension is binary and
further textual content (due to the store compression mode) will not make a
difference.

It is possible to coerce Git into viewing textual diffs of binary files, but at
this point, we've strayed too far off the default path and it will give more
trouble than it is worth.

The conclusion, then, is that 3MF cannot be version controlled easily even by
repacking with no compression. It's best to stick with unpacking the 3MF into a
directory and versioning the contents of the directory. Or to use textual STL.
