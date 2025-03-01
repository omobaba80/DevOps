# Linux Concepts for Beginners

## 1. Unix and Linux Difference

*   **Unix:**
    *   **What it is:** A pioneering operating system developed at Bell Labs in the late 1960s and early 1970s. Designed for multi-user, multi-tasking, and portability.
    *   **Key Characteristics:**
        *   Command-line interface (CLI) focused.
        *   Hierarchical file system.
        *   "Everything is a file."
        *   Small, single-purpose tools.
    *   **Examples:** macOS, Solaris, HP-UX.
    *   **Proprietary:** Unix is a trademarked name.
*   **Linux:**
    *   **What it is:** A Unix-like, open-source operating system kernel created by Linus Torvalds in 1991.
    *   **Key Characteristics:**
        *   Shares core principles with Unix.
        *   Open-source and customizable.
        *   Huge community support.
    *   **Examples:** Ubuntu, Fedora, Debian, CentOS, RHEL, Android.
    *   **Open Source:** Linux kernel and many distributions are free.
*   **Key Difference (Simplified):** Unix is the original blueprint; Linux is a successful, open-source implementation.

## 2. Linux Filesystem Structure

Hierarchical tree structure, starting with the root directory (`/`).

*   `/` (root): Top-level directory.
*   `/bin`: Essential *bin*ary programs (commands).
*   `/boot`: Files needed to boot the system.
*   `/dev`: *Dev*ice files.
*   `/etc`: System-wide configuration files.
*   `/home`: Home directories of individual users.
*   `/lib`: Shared *lib*raries.
*   `/media`: Mount points for removable media.
*   `/mnt`: Temporary mount points.
*   `/opt`: *Opt*ional software packages.
*   `/proc`: Virtual filesystem (process and kernel info).
*   `/root`: Home directory of the root user.
*   `/sbin`: Essential *s*ystem *bin*aries (system administration).
*   `/srv`: Data for *s*e*rv*ices.
*   `/tmp`: *Temp*orary files.
*   `/usr`: *U*ser *s*ystem *r*esources (programs, libraries, etc.).
    *   `/usr/bin`: Most user commands.
    *   `/usr/lib`: Libraries for `/usr/bin`.
    *   `/usr/local`: Locally installed software.
    *   `/usr/sbin`: System administration binaries (non-essential).
    *   `/usr/share`: Architecture-independent data.
*   `/var`: *Var*iable data files (logs, etc.).
    *   `/var/log`: System log files.

**Example:** `/home/yourusername/mydoc.txt`

## 3. Basic Linux / Unix Commands

*   **`pwd`** (print working directory): Current location.
    ```bash
    pwd
    ```

*   **`ls`** (list): List files and directories.
    ```bash
    ls
    ls -l
    ls -a
    ls -la
    ls -lh
    ls -t
    ls -r
    ```

*   **`cd`** (change directory): Move to a different directory.
    ```bash
    cd /home/myuser/documents
    cd documents
    cd ..
    cd ~
    cd -
    cd
    ```

*   **`mkdir`** (make directory): Create a directory.
    ```bash
    mkdir mynewdir
    mkdir -p mynewdir/subdir1/subdir2
    ```

*   **`rmdir`** (remove directory): Delete an *empty* directory.
    ```bash
    rmdir myemptydir
    ```

*   **`rm`** (remove): Delete files or directories.  **BE CAREFUL!**
    ```bash
    rm myfile.txt
    rm -r mydirectory
    rm -f myfile.txt
    rm -rf mydirectory
    ```

*   **`cp`** (copy): Copy files or directories.
    ```bash
    cp myfile.txt mybackup.txt
    cp -r mydir mybackupdir
    cp *.txt mytxtfiles/
    ```

*   **`mv`** (move): Move or rename files/directories.
    ```bash
    mv oldname.txt newname.txt
    mv myfile.txt /tmp
    mv mydir /tmp
    ```

*   **`touch`**: Create an empty file or update timestamp.
    ```bash
    touch newfile.txt
    touch existingfile.txt
    ```

*   **`cat`** (concatenate): Display file contents.
    ```bash
    cat myfile.txt
    cat file1.txt file2.txt > combined.txt
    ```

*   **`less`**: View file content page by page.
    ```bash
    less verylargefile.txt
    ```

*   **`head`**: Display the beginning of a file.
    ```bash
    head myfile.txt
    head -n 20 myfile.txt
    ```

*   **`tail`**: Display the end of a file.
    ```bash
    tail myfile.txt
    tail -n 5 myfile.txt
    tail -f mylogfile.log
    ```

*   **`echo`**: Print text.
    ```bash
    echo "Hello, world!"
    echo $HOME
    ```

*   **`man`** (manual): Display command manual pages.
    ```bash
    man ls
    man cp
    ```

* **`clear`** : Clears the terminal.

## 4. Changing File Permissions and Ownership

*   **Permissions:** Control access (read, write, execute).
    *   **`r` (read):** View contents/list directory contents.
    *   **`w` (write):** Modify file/create, delete files in directory.
    *   **`x` (execute):** Run file/access directory.
*   **User Categories:**
    *   **`u` (user/owner):** File owner.
    *   **`g` (group):** Group associated with the file.
    *   **`o` (others):** All other users.
*   **`chmod`** (change mode): Change permissions.
    *   **Symbolic Mode:**
        ```bash
        chmod u+x myfile.sh
        chmod go-r myfile.txt
        chmod a+rw myfile.txt
        chmod g=rx myfile.txt
        ```
    *   **Numeric Mode:**
        ```bash
        chmod 755 myfile.sh  # rwxr-xr-x
        chmod 644 myfile.txt # rw-r--r--
        chmod 600 myfile.txt # rw-------
        ```
*   **`chown`** (change owner): Change owner and/or group.
    ```bash
    chown newuser myfile.txt
    chown newuser:newgroup myfile.txt
    chown :newgroup myfile.txt
    chown -R newuser:newgroup mydir
    ```
* **`chgrp`** (change group): Used to change only group of a file or directory.
    ```bash
        chgrp newgroup myfile.txt
    ```

## 5. Types of Links: Soft and Hard Links

*   **Links:** Pointers to files.
*   **Hard Links:**
    *   Another name for the same data (same inode).
    *   Share inode number.
    *   Deleting one doesn't delete data (until all links gone).
    *   No directory hard links.
    *   No cross-filesystem links.
    *   `ln` (without `-s`).
    ```bash
    touch original.txt
    ln original.txt hardlink.txt
    ls -li
    rm original.txt
    cat hardlink.txt
    ```

*   **Soft Links (Symbolic Links):**
    *   File pointing to another file/directory (by path).
    *   Different inode numbers.
    *   Deleting original breaks the link.
    *   Can link to directories.
    *   Can link across filesystems.
    *   `ln -s`.
    ```bash
    touch original.txt
    ln -s original.txt softlink.txt
    ls -li
    rm original.txt
    cat softlink.txt
    ls -l softlink.txt
    ```

## 6. Filter Commands

Process input (stdin) and send to output (stdout).  Used in pipelines (`|`).

*   **`grep`** (global regular expression print): Search for patterns.
    ```bash
    grep "error" mylogfile.log
    grep -i "error" mylogfile.log
    grep -v "info" mylogfile.log
    grep -c "error" mylogfile.log
    grep -n "error" mylogfile.log
    grep -r "pattern" /path/to/search
    grep "^error" mylogfile.log
    grep "error$" mylogfile.log
    ```

*   **`sort`**: Sort lines.
    ```bash
    sort myfile.txt
    sort -r myfile.txt
    sort -n numbers.txt
    sort -k2 file.txt
    ```

*   **`uniq`**: Report/omit repeated lines (often with `sort`).
    ```bash
    sort myfile.txt | uniq
    sort myfile.txt | uniq -c
    ```

*   **`wc`** (word count): Count lines, words, characters.
    ```bash
    wc myfile.txt
    wc -l myfile.txt
    wc -w myfile.txt
    wc -c myfile.txt
    ```

*   **`cut`**: Extract sections from lines.
    ```bash
    cut -d, -f1 myfile.csv
    cut -c1-10 myfile.txt
    ```

*   **`tr`** (translate): Translate/delete characters.
    ```bash
    tr 'a-z' 'A-Z' < myfile.txt
    tr -d '0-9' < myfile.txt
    ```
## 7. Simple and Advanced Filter commands.
*   **Simple filter commands**: These perform basic text manipulation:
    *   `head`: Displays the beginning of a file.
    *   `tail`: Displays the end of a file.
    *   `grep`: Filters lines matching a pattern.
    *   `wc`: Counts lines, words, and characters.
    *   `sort`: Sorts lines of text.
    *    `cut`: Extracts sections from lines.
    *   `tr`: Translates or deletes characters.
*   **Advanced filter commands:** These offer more complex text processing capabilities, often involving regular expressions and scripting:
  *   **`sed`** (Stream Editor): A powerful command for performing text transformations on a stream of text. It's often used for substitutions, deletions, insertions, and more complex pattern-based manipulations.
    ```bash
    sed 's/old/new/' myfile.txt       # Replace "old" with "new" on each line (first occurrence only)
    sed 's/old/new/g' myfile.txt      # Replace all occurrences of "old" with "new"
    sed '1,5d' myfile.txt            # Delete lines 1 through 5
    sed '/pattern/d' myfile.txt      # Delete lines matching "pattern"
    sed -n '2p' myfile.txt           # Print only the second line (-n suppresses default output)
    sed -i 's/foo/bar/g' myfile.txt # Edit the file in-place (-i), replacing "foo" with "bar" globally
    ```

 *  **`awk`**: A versatile programming language designed for text processing.  It's particularly good at working with structured data (like CSV files or tabular output). `awk` treats each line of input as a record and divides each record into fields.

    ```bash
    awk '{print $1}' myfile.txt       # Print the first field of each line
    awk '{print $2, $1}' myfile.txt    # Print the second and first fields, in that order
    awk -F',' '{print $3}' myfile.csv # Use a comma as the field separator (-F) and print the third field
    awk '$1 > 10 {print $2}' myfile.txt # Print the second field only if the first field is greater than 10
    awk '{sum += $1} END {print sum}' numbers.txt  # Calculate the sum of the numbers in the first field
    awk '/pattern/ {print $0}' myfile.txt # Print entire lines ($0) matching "pattern" (similar to grep)
    ```

## 8. Start and Stop Services

*   **System V init (SysVinit):** Older systems, less common now.
    *   `/etc/init.d/` directory contains scripts.
    *   `service <service_name> start|stop|restart|status`
    ```bash
    sudo service apache2 start  # Start Apache web server
    sudo service mysql stop     # Stop MySQL database server
    sudo service ssh restart    # Restart SSH server
    sudo service nginx status   # Check status of Nginx
    ```

*   **systemd:** The modern standard, used by most current distributions.
    *   `systemctl` is the primary command.
    ```bash
    sudo systemctl start apache2.service   # Start Apache
    sudo systemctl stop mysql.service      # Stop MySQL
    sudo systemctl restart ssh.service     # Restart SSH
    sudo systemctl status nginx.service    # Check status
    sudo systemctl enable apache2.service  # Enable Apache to start on boot
    sudo systemctl disable mysql.service   # Disable MySQL from starting on boot
    sudo systemctl is-enabled sshd.service # Check if a service is enabled
    ```
    The `.service` suffix is often optional.

*   **Upstart:**  Used by some older Ubuntu versions (largely replaced by systemd).
    *   `initctl` command (or `start`, `stop`, `restart`, `status` directly).
    ```bash
    sudo start apache2  # Or: sudo initctl start apache2
    sudo stop mysql     # Or: sudo initctl stop mysql
    sudo status ssh     # Or: sudo initctl status ssh
    ```

## 9. Find and Kill Processes

*   **`ps`** (process status): Lists running processes.
    ```bash
    ps aux          # Show all processes for all users (detailed view)
    ps -ef          # Another common way to show all processes
    ps aux | grep nginx  # Find processes related to Nginx
    ```
* **`top`**: dynamic real-time view of running processes.
```bash
    top
