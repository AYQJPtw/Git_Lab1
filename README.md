# Git Documentation

## Working from hypertext links found on Internet.

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
#
# Git is only for creating a repository in your local computer directory!!!
#
#
# Lab 2.  Using Git file merge command.  
## git-merge-file - Run a three-way file merge

Credit: I will be using this link:  https://git-scm.com/docs/git-merge-file


**SYNOPSIS**
git merge-file [-L <current-name> [-L <base-name> [-L <other-name>]]]
	[--ours|--theirs|--union] [-p|--stdout] [-q|--quiet] [--marker-size=<n>]
	[--[no-]diff3] [--object-id] <current> <base> <other>
  
**DESCRIPTION**
Given three files <current>, <base> and <other>, git merge-file incorporates all changes that lead from <base> to <other> into <current>. The result ordinarily goes into <current>. git merge-file is useful for combining separate changes to an original. Suppose <base> is the original, and both <current> and <other> are modifications of <base>, then git merge-file combines both changes.

A conflict occurs if both <current> and <other> have changes in a common segment of lines. If a conflict is found, git merge-file normally outputs a warning and brackets the conflict with lines containing <<<<<<< and >>>>>>> markers. A typical conflict will look like this:


<<<<<<< A
lines in file A
=======
lines in file B
>>>>>>> B
If there are conflicts, the user should edit the result and delete one of the alternatives.



 








#
#
#
![]()
#
#
