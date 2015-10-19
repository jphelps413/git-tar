# git-tar

A simple script to tar up and compress a git repository for archival
purposes. Typically used before attempting to tinker with the more arcane
git commands which have the ability to open rabbit holes, thus spending
hours researching how to undo an "Oops!"

This script taps into git's ability to be extended by placing an
executuable version of git-tar in your PATH. Once this is in place git will
treat it as a subcommand, meaning if you type this anywhere in a git
repository:

    git tar

the script will do the following:

  - Verify the presence of a $GITAR subdirectory for storing the tarballs.

  - Verify the presence of a list of exclusions in $GITAR/AAA_TarExcludes.
    This file will be created with commonly ignored extensions if it does
    not exist. One day I plan to make this smarter.

  - Locate the top of the repository and tar its contents into the $GITAR
    directory by building up a file name in the form of:
    ```
       $GITAR/<repository_name>/<YYYYMMDD-hhmmss>.tar
    ```

  - Finally, the tarball will be compressed using bzip2 by default, or xz
    if it is available on the system. This operation is performed in the
    background since it can sometimes be a rather lengthy process.

# install

Simply clone and then add git-tar to a subdirectory that the shell searches
for executables. Also make certain the file permissions are set to 0555 to
ensure that it is executable.
