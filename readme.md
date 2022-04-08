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
