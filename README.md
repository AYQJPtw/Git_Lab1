# Git Documentation

## Working from hypertext links found on Internet.

#  Some information about git.  

In Git, the **from** -> **to** -> **into** framework is a mental model used to visualize how code moves between different branches or environments. It clarifies the flow of changes: the origin of your code (from), the specific work being reviewed (to), and the destination branch (into).

1. From (The Origin)

This is the source branch where the work currently exists (e.g., your feature-branch or dev). It represents the starting point of your code changes and contains the commits you want to migrate.

2. To (The Destination / Subject)

This is the intended target branch you are aiming to update (e.g., main or production). It represents the "destination universe" where you want the new features or bug fixes to ultimately live.

3. Into (The Action / Integration)

This defines the merging or rebasing action itself. It is the process that officially applies the code from the From branch into the To branch.For example, when submitting a pull request on platforms like GitHub, you are requesting to merge code from my-new-feature into main.

Credit:  Google  WebContent:  Google Inc.  

(trying this in another lab:   https://dev.to/michaeljota/another-git-framework-workflow-59a8)


# Git Design

Strong support for non-linear development

Git supports rapid branching and merging, and includes specific tools for visualizing and navigating a non-linear development history. In Git, a core assumption is that a change will be merged more often than it is written, as it is passed around to various reviewers. In Git, branches are very lightweight: a branch is only a reference to one commit.  Credit: Linus Torvalds creator of git.  Websource https://en.wikipedia.org/wiki/Git


Distributed development

Git gives each developer a local copy of the full development history, and changes are copied from one such repository to another. These changes are imported as added development branches and can be merged in the same way as a locally developed branch.

Compatibility with existing systems and protocols

Repositories can be published via Hypertext Transfer Protocol Secure (HTTPS), Hypertext Transfer Protocol (HTTP), File Transfer Protocol (FTP), or a Git protocol over either a plain socket or Secure Shell (ssh). Git also has a CVS server emulation, which enables the use of existing CVS clients and IDE plugins to access Git repositories. Subversion repositories can be used directly with git-svn.
Efficient handling of large projects

Torvalds has described Git as being very fast and scalable, and performance tests done by Mozilla showed that it was an order of magnitude faster diffing large repositories than Mercurial and GNU Bazaar; fetching version history from a locally stored repository can be one hundred times faster than fetching it from the remote server.

Cryptographic authentication of history

The Git history is stored in such a way that the ID of a particular version (a commit in Git terms) depends upon the complete development history leading up to that commit. Once it is published, it is not possible to change the old versions without it being noticed. The structure is similar to a Merkle tree, but with added data at the nodes and leaves. (Mercurial and Monotone also have this property.)

Toolkit-based design

Git was designed as a set of programs written in C and several shell scripts that provide wrappers around those programs. Although most of those scripts have since been rewritten in C for speed and portability, the design remains, and it is easy to chain the components together.
Pluggable merge strategies
As part of its toolkit design, Git has a well-defined model of an incomplete merge, and it has multiple algorithms for completing it, culminating in telling the user that it is unable to complete the merge automatically and that manual editing is needed.
Garbage accumulates until collected
Aborting operations or backing out changes will leave useless dangling objects in the database. These are generally a small fraction of the continuously growing history of wanted objects. Git will automatically perform garbage collection when enough loose objects have been created in the repository. Garbage collection can be called explicitly using git gc.

Periodic explicit object packing
Git stores each newly created object as a separate file. Although individually compressed, this takes up a great deal of space and is inefficient. This is solved by the use of packs that store a large number of objects delta-compressed among themselves in one file (or network byte stream) called a packfile. Packs are compressed using the heuristic that files with the same name are probably similar, without depending on this for correctness. A corresponding index file is created for each packfile, recording the offset of each object in the packfile. Newly created objects (with newly added history) are still stored as single objects, and periodic repacking is needed to maintain space efficiency. The process of packing the repository can be very computationally costly. By allowing objects to exist in the repository in a loose but quickly generated format, Git allows the costly pack operation to be deferred until later, when time matters less, e.g., the end of a workday. Git does periodic repacking automatically, but manual repacking is also possible with the git gc command.  For data integrity, both the packfile and its index have an SHA-1 checksum inside, and the file name of the packfile also contains an SHA-1 checksum. To check the integrity of a repository, run the git fsck command.

Another property of Git is that it snapshots directory trees of files. The earliest systems for tracking versions of source code, Source Code Control System (SCCS) and Revision Control System (RCS), worked on individual files and emphasized the space savings to be gained from interleaved deltas (SCCS) or delta encoding (RCS) the (mostly similar) versions. Later revision-control systems maintained this notion of a file having an identity across multiple revisions of a project. However, Torvalds rejected this concept. Consequently, Git does not explicitly record file revision relationships at any level below the source-code tree.

Downsides

These implicit revision relationships have some significant consequences:

It is slightly more costly to examine the change history of one file than the whole project. To obtain a history of changes affecting a given file, Git must walk the global history and then determine whether each change modified that file. This method of examining history does, however, let Git produce with equal efficiency a single history showing the changes to an arbitrary set of files. For example, a subdirectory of the source tree plus an associated global header file is a very common case.

Renames are handled implicitly rather than explicitly. A common complaint with CVS is that it uses the name of a file to identify its revision history, so moving or renaming a file is not possible without either interrupting its history or renaming the history and thereby making the history inaccurate. Most post-CVS revision-control systems solve this by giving a file a unique long-lived name (analogous to an inode number) that survives renaming. Git does not record such an identifier, and this is claimed as an advantage. Source code files are sometimes split or merged, or simply renamed, and recording this as a simple rename would freeze an inaccurate description of what happened in the (immutable) history. Git addresses the issue by detecting renames while browsing the history of snapshots rather than recording it when making the snapshot. (Briefly, given a file in revision N, a file of the same name in revision N − 1 is its default ancestor. However, when there is no like-named file in revision N − 1, Git searches for a file that existed only in revision N − 1 and is very similar to the new file.) However, it does require more CPU-intensive work every time the history is reviewed, and several options to adjust the heuristics are available. This mechanism does not always work; sometimes a file that is renamed with changes in the same commit is read as a deletion of the old file and the creation of a new file. Developers can work around this limitation by committing the rename and the changes separately.

Merging strategies

Git implements several merging strategies; a non-default strategy can be selected at merge time.

resolve: the traditional three-way merge algorithm.

recursive: This is the default when pulling or merging one branch, and is a variant of the three-way merge algorithm.

When there are more than one common ancestors that can be used for a three-way merge, it creates a merged tree of the common ancestors and uses that as the reference tree for the three-way merge. This has been reported to result in fewer merge conflicts without causing mis-merges by tests done on prior merge commits taken from Linux 2.6 kernel development history. Also, this can detect and handle merges involving renames.

— Linus Torvald says,
octopus: This is the default when merging more than two heads.

Data structures

Git's primitives are not inherently a source-code management system.

In many ways you can just see git as a filesystem—it's content-addressable, and it has a notion of versioning, but I really designed it coming at the problem from the viewpoint of a filesystem person (hey, kernels is what I do), and I actually have absolutely zero interest in creating a traditional SCM system.

From this initial design approach, Git has developed the full set of features expected of a traditional SCM, with features mostly being created as needed, then refined and extended over time.

Git has two data structures: a mutable index (also called stage or cache) that caches information about the working directory and the next revision to be committed; and an object database that stores immutable objects.

The index serves as a connection point between the object database and the working tree.

The object store contains five types of objects.

A blob is the content of a file. Blobs have no proper file name, time stamps, or other metadata (a blob's name internally is a hash of its content). In Git, each blob is a version of a file, in which is the file's data.

A tree object is the equivalent of a directory. It contains a list of file names, each with some type bits and a reference to a blob or tree object that is that file, symbolic link, or directory's contents. These objects are a snapshot of the source tree. (In whole, this comprises a Merkle tree, meaning that only a single hash for the root tree is sufficient and actually used in commits to precisely pinpoint to the exact state of whole tree structures of any number of sub-directories and files.)

A commit object links tree objects together into history. It contains the name of a tree object (of the top-level source directory), a timestamp, a log message, and the names of zero or more parent commit objects.

A tag object is a container that contains a reference to another object and can hold added meta-data related to another object. Most commonly, it is used to store a digital signature of a commit object corresponding to a particular release of the data being tracked by Git.

A packfile object collects various other objects into a zlib-compressed bundle for compactness and ease of transport over network protocols.
Each object is identified by a SHA-1 hash of its contents. Git computes the hash and uses this value for the object's name. The object is put into a directory matching the first two characters of its hash. The rest of the hash is used as the file name for that object.

Git stores each revision of a file as a unique blob. The relationships between the blobs can be found through examining the tree and commit objects. Newly added objects are stored in their entirety using zlib compression. This can consume a large amount of disk space quickly, so objects can be combined into packs, which use delta compression to save space, storing blobs as their changes relative to other blobs.

Additionally, Git stores labels called refs (short for references) to indicate the locations of various commits. They are stored in the reference database and are respectively.

Heads (branches): Named references that are advanced automatically to the new commit when a commit is made on top of them.

HEAD: A reserved head that will be compared against the working tree to create a commit.

Tags: Like branch references, but fixed to a particular commit. Used to label important points in history.
Commands

Frequently used commands for Git's command-line interface include.

git init, which is used to create a git repository.

git clone [URL], which clones, or duplicates, a git repository from an external URL.

git add [file], which adds a file to git's working directory (files about to be committed).

git commit -m [commit message], which commits the files from the current working directory (so they are now part of the repository's history).
A .gitignore file may be created in a Git repository as a plain text file. The files listed in the .gitignore file will not be tracked by Git.  This feature can be used to ignore files with keys or passwords, various extraneous files, and large files (which GitHub will refuse to upload).

Git references

Every object in the Git database that is not referred to may be cleaned up by using a garbage collection command or automatically. An object may be referenced by another object or an explicit reference. Git has different types of references. The commands to create, move, and delete references vary. git show-ref lists all references. Some types are:

heads: refers to an object locally,
remotes: refers to an object which exists in a remote repository,
stash: refers to an object not yet committed,
meta: e.g., a configuration in a bare repository, user rights; the refs/meta/config namespace was introduced retrospectively, gets used by Gerrit,
tags: see above.  Credit: Linus Torvalds creator of git.  Websource https://en.wikipedia.org/wiki/Git


### For the first lab.  I will create a repository in GitHub and drop files and create folder manually.  Without the use of my local Windows File Explorer.  

#
# Lab 1.  Cloning your GitHub repository on to your local pc directory new folder.  Using git bash.
  
**1.  I will make the only, new GitHub repository for step 1 called repo2.**

**2. With repo2 repository I will put new files and folder with some textual content.  As our example when transfered.**

In your local directory home pc, you will need to make a new directory from the Powershell or your terminal editor.  Use the cd command in your Powershell (command prompt) or terminal editor to get to the directory you want to put your git clone , the copied repository in GitHub to.  Now use the comamand MKDIR <yourdirectoryname>.  This new directory will be where your git clone is stored.  Use ls -a or ls -al command.  To see what is inside this directory.  Use pwd to see your current directory you are located in now. 

Using git bash, open the git bash terminal and cd to your new directory.  You can use Powershell cli command pwd, to get the full path to that directory.  Make sure your in the right directory.  Using git bash, type git init, enter.  Type git log, enter.  You should be able to use the ls -a command from Powershell to see all your repository in your local directory location new folder.  

Credit: I used this link to do just that.  https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository
  
**3. Using git bash, I will use the git clone command on repo2 repository.**

  Here is the snippet I used for the git clone command: **git clone https://(username):(token)@gitlab.example.com/tanuki/awesome_project.git**

  You will need to generate a new token from your GitHub repository.  You can find it in the <developers_settings>.
  Under your profile icon or your picture profile in the top right corner of your repository, click on Settings> developers_settings > Personal     access tokens > Fine grained tokens > And use the generate button.  Copy token paste it to some file.  As a copy.  Then put it in the (token)     space as above.  Remove these () brakets from around token from the above snippet, git clone https:// command.  You will need the @ sign, followed by the Github username account found in your browers after accessing your repository on GitHub.

Credit:  I used this link to do just that.  https://docs.gitlab.com/user/profile/personal_access_tokens/#clone-repository-using-personal-access-token  "Follow my advice above its easier, subtitute GigHub Url for the GitLab one."

**4. Using the git push command from my local File Explore folder on my pc at home.**       
using this code snippet: git push <remote> <branch>.  But I will use git push repo2 main.  

Credit: I used this link to do just that.  https://git-scm.com/docs/git-push


I was able to get the repository on GitHub down into my local computer directory.  Use GitHub Desktop to push edited files and folder up to GitHub.  
#
**I found this link is great for after completing step 4. and recommend it when working in the local directory of your pc**  https://medium.com/@nikitakharate89/git-version-control-understanding-areas-file-flow-and-undoing-changes-7529f4ff86cc
Credit: Nikitakharate.  Websource: https://medium.com  
#
# Git is only for creating a repository in your local computer directory!!!
#
#
# Lab 2.  








#
#
#
![]()
#
#
