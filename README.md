# How to use multiple SSH keys for different git accounts


Create different public key
---------------------------
create a different ssh key for each account (GitHub, GitLab, ...)

    $ ssh-keygen -t rsa -C "your_email@youremail.com" -f ~/.ssh/github-github_user_name
    $ ssh-keygen -t rsa -C "your_email@youremail.com" -f ~/.ssh/gitlab-gitlab_user_name
  
for example, 2 key pais created as follows:

#### Key pair 1:

    ~/.ssh/github-github_user_name
    ~/.ssh/github-github_user_name.pub
  
#### Key pair 2:

    ~/.ssh/gitlab-gitlab_user_name
    ~/.ssh/gitlab-gitlab_user_name.pub


Add the private keys
--------------------
all cached keys can be deleted before

    $ ssh-add -D

If you get the following error:
__**Could not open a connection to your authentication agent.**__


add these two keys as following

    $ ssh-add ~/.ssh/github-github_user_name
    $ ssh-add ~/.ssh/gitlab-gitlab_user_name


Modify the ssh config file
--------------------------
create the config file if it does not exist and open it using a text editor (vi / vim / gedit / nano...)

    $ cd ~/.ssh/
    $ touch config
    $ vim config

add all the accounts

    #github-github_user_name account
    Host gh-github_user_name
        HostName github.com
        User github_user_name
        IdentityFile ~/.ssh/github-github_user_name

    #gitlab-gitlab_user_name account
    Host gh-gitlab_user_name
        HostName gitlab.com
        User gitlab_user_name
        IdentityFile ~/.ssh/gitlab-gitlab_user_name


Check the saved keys
--------------------
finally, check the saved keys

    $ ssh-add -l

if the ssh keys don't show up, run:

    $ ssh-add ~/.ssh/github-github_user_name
    $ ssh-add ~/.ssh/gitlab-gitlab_user_name

one of the following methods (A or B) is used

### A) Make the config global
the git username and email can be set globally and then use the normal flow to push the code

while working with GitHub

    $ git config --global user.name "github_user_name"
    $ git config --global user.email "your_email@youremail.com"

while working with GitLab

    $ git config --global user.name "gitlab_user_name"
    $ git config --global user.email "your_email@youremail.com"

### B) Clone the repository and modify the git configuration
clone the repository

    $ git clone git@github.com:github_user_name/repo.git repo-github_user_name

if <code>repo-github_user_name</code> is not defined at then end of the command, the folder name will be same as the <code>repo</code> name.

enter the repository folder and modify the git configuration locally

    $ cd repo-github_user_name
    $ git config user.name "gibhub_user_name"
    $ git config user.email "your_email@gmail.com"

    $ cd repo-gitlab_user_name
    $ git config user.name "giblab_user_name"
    $ git config user.email "your_email@gmail.com" 

then use normal flow to push the code

    $ git add .
    $ git commit -m "your comments"
    $ git push

## Credits
This is a customized version of [Multiple SSH Keys settings for different GitHub account](https://gist.github.com/jexchan/2351996) documented by [jexchan](https://gist.github.com/jexchan)


## Misc
Follow Mohammad: [LinkedIn](https://www.linkedin.com/in/alaamjadi/), [Twitter](https://twitter.com/AlaAmjadi)
