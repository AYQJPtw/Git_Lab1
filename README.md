# Git Documentation

## Working from hypertext links found on Internet.

### For the first lab.  I will create a repository in GitHub and drop files and create folder manually.  Without the use of my local Windows File Explorer.  


  
**1.  I will make the second new GitHub repository for step 1 called repo2.**

**2. With repo2 repository I will put new files and folder with some textual content.  As our example when transfered.**
  
**3. Using git bash, I will use the git clone command on repo2 repository.**

  Here is the snippet I used for the git clone command: **git clone https://(username):(token)@gitlab.example.com/tanuki/awesome_project.git**

  You will need to generate a new token from your GitHub repository.  You can find it in the <developers_settings>.
  Under your profile icon or your picture profile in the top right corner of your repository, click on Settings> developers_settings > Personal     access tokens > Fine grained tokens > And use the generate button.  Copy token paste it to some file.  As a copy.  Then Put it in the <token>     space as above.  Remove these <> brakets from from the above example git clone https:// command.  You will need the @ sign, followed by the       Github username account found in your browers after accessing your repository on GitHub.

  
  
  I used this link to do just that.  https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository

**4.  Using**

In your local directory home pc, you will need to make a new directory from the Powershell or your terminal editor.  Use the cd command in your Powershell (command prompt) or terminal editor to get to the directory you want to put your git clone , the copied repository in GitHub to.  Now use the comamand MKDIR <yourdirectoryname>.  This new directory will be where your git clone is stored.  Use ls -a or ls -al command.  To see what is inside this directory.  Use pwd to see your current directory you are located in now. 

Using git bash, open the git bash terminal and cd to your new directory.  You can use Powershell cli command pwd, to get the full path to that directory.  Make sure your in the right directory.  Using git bash, type git init, enter.  Type git log, enter.  You should be able to use the ls -a command from Powershell to see all your repository in your local directory location new folder.  

Credit: I used this link to do just that.  https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository
  
**5. Using the git push command from my local File Explore folder on my pc at home.**       
using this code snippet: git push <remote> <branch>.  But I will use git push repo2 main.  

Credit: I used this link to do just that.  https://git-scm.com/docs/git-push


I was able to get the repository on GitHub down into my local computer directory.  Use GitHub Desktop to push edited files and folder up to GitHub.  
#
#
# Git is only for creating a repository in your local computer directory!!!
#
#
#


 








#
#
#
![]()
#
#
