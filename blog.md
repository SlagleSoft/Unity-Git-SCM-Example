Unity3D Source Control with Git SCM
==============================


![Banner](banner.png?raw=true)


In this article we will outline how to easily and quickly setup Source Control with Unity3D using Git SCM. This is the same workflow we use not only when building with Unity but every project we do. We wanted to put this article together because there really isn't an all in one detailed How To right now.

----------


Create an account on an hosted Git Service
-------------

When working on a project in a Team Collaboration setup you have the requirement for one central location of the project source, and the ability for everyone to make their changes and sync up with the central and the other teammates. Git SCM does just that, it is an extremely powerful tool and we only touch the tip of the ice-burg in this article. Syncing the source is best done over the internet, and there are four main free solutions we would like to recommend. We will be using ***GitHub*** during the article how-to. 

> **Hosted Git Services:**

> - [GitHub](https://github.com/) --- GitHub really started the online platform we have today. We recommend this service for Open Source projects, were the source is publicly shared. 
> - [Bitbucket](https://bitbucket.org/) --- Bitbucket is another big platform that has almost equal features (and more) then GitHub. We recommend this service for Private Source project, only authorized users can view the projects. Bitbucket offers even more solutions, Ticketing (help, defects, etc), Continuous Integration and more.
> - [Visual Studio Team Services](https://www.visualstudio.com/vsts-test/) --- VSTS is an amazing platform, it could be compared to Bitbucket very closely. Similar offerings and even things BB doesn't have.
> - [Self Hosted, ex. GitLab](https://gitlab.com) --- GitLab is often called a "GitHub" clone, its software you can download and install on your own server.

GitHub and Self Hosted is usually your starting point, as projects grow they have more needs to accelerate the work flow, things like Issue Tracking and Continuous Integration. Both Bitbucket and VSTS are the next step, *BUT* you can use them as the starting point too. We recommend you try them all out, see which the team likes to the most, there are some awesome tools out there. Best thing about Source Control, is you can *"migrate"* to another service in a matter of minutes. Just Clone all your Branches locally, and Push them to the new Upstream Remote. Wait what?, don't worry you'll know how by the end of this article.

> **Note:** Bitbucket and VSTS have limits to their free packages, usually up to 5 team members until you need to purchase plans.

> **Note:** Before you read any further, go ahead and setup a free GitHub account so you can follow allow, you can use any of the other solutions if you would like, they are so similar that most matches right up. So if you need Private do Bitbucket instead, or practice with GitHub first.

#### Create a Repository on GitHub

![GitHub - Create Repository](g-make-repo.png?raw=true)

Once you make an Account login and create a Repository. You can either do personal, or make an Organization and create the repo there. The limitation for free is it has to be public when using GitHub.

![Git - Team Access](git-access.png?raw=true)

Now is a great chance to send out invites to the project you are creating. This is how other people can work on the project.


----------


Install the recommended software
-------------

There's a few tools used very commonly in the Unity workflow, and since we used them while authoring this article we decided to go ahead and promote them. Only ***Git SCM*** and ***Git LFS*** is required in order to follow along. Install each one you would like in order they are listed, if you already have one installed you can skip it. While installing each one the default selections perfectly fine, there are only a few screens we want to point out.

> **Software used:**

> - [Visual Studio](https://www.visualstudio.com/) --- A software development IDE built by Microsoft, this tool is extremely powerful. Unity allows you to write in C# *(provides the best performance)*, and you can link VS to be your script editor in Unity.
> - [Unity](https://unity3d.com/) --- Unity is game development platform, both the IDE and the Engine. It offers a free solution up to around $100k+ yearly profit.
> - [Git SCM](https://git-scm.com/) --- This is the framework required in order to start working with Git SCM. A lot is packed into this very powerful toolkit.
> - [Git LFS](https://git-lfs.github.com/) --- Git LFS is a Git module that expands it support for handling large non text based binary files. FBX Models, PSDs, etc. It's needed in order to work with Unity game projects and Source Control.
> - [SourceTree](https://www.sourcetreeapp.com/) --- SourceTree offers a nice easy to use GUI for Git, it simplifies the process even more.

#### Installing Git SCM

At the end of the install make sure to check off "Launch Git Bash". There are a few things we want to configure before we get to much future. Don't worry, you'll see another way to set these values later on. A black terminal window will open, this lets you execute commands to Git. Below are some basic identity configurations, as well as a Global Ignore file config. Go ahead and execute them in the window, replacing with your name and email.

![Git SCM - Launch Git Bash](git-bash-launch.png?raw=true)

    cd ~
    git config --global user.name "John Doe"
    git config --global user.email "johndoe@example.com"
    touch .gitignore_global
    git config --global core.excludesfile ~/.gitignore_global

#### Installing SourceTree

> **Note:** When you install SourceTree it will prompt you to login to an Atlassian account to register *(this is NOT the account you use for Source Control)*

![SourceTree - Connect an Account](st-login.png?raw=true)

Connect an Account --- If you created either a Bitbucket or GitHub account you can login now, if you created a VSTS account you can click "Skip Setup" and handle login when you Clone the first time.

![SourceTree - Install Global Ignore](st-gignore.png?raw=true)

Install global ignore file --- Click "Cancel", we already handled this set with Git SCM directly.

![SourceTree - Clone a GitHub Repository](st-repo-select.png?raw=true)

Clone a GitHub repository --- On this screen we select the repo we created on GitHub above, and define the Destination Path.

![SourceTree - Load SSH Key](st-load-ssh.png?raw=true)

Load SSH Key --- Click "Cancel", while we greatly recommend this method of authentication, it slightly falls out of the scope of this document. We do have more details about this subject at the bottom.

> **Note:** At the end of the install of SourceTree you can launch it, or open it afterwards, we will use it in a later topic below.


----------


Setup Unity Project for Source Control
-------------

In order to use Unity with Source Control a few project settings need to be changed. You can do this at the creation of the project or with an existing one.

![Unity - New Project](u-new-proj.png?raw=true)

Create a new empty Unity project, for now set the Location to the Desktop *(we will remove this when done)*. Once it opens, go ahead and save the Scene and Project.

![Unity - Project Settings](u-proj-settings.png?raw=true)

Go-to *Edit -> Project Settings -> Editor*

![Unity - Editor Settings](u-editor-settings.png?raw=true)

Set: *Version Control -> Mode = Visible Meta Files*
Set: *Asset Serialization -> Mode = Force Text*

![Unity - Delete Library Folder](u-delete-lib.png?raw=true)

Save the Project and then close Unity, now navigate to the Unity project folder and *Delete the "Library"* folder.

![Unity - Copy over Unity Source](u-copy-over.png?raw=true)

Open the folder we created when *Cloning with SourceTree*, copy the contents of the Unity project folder into the *Clone* folder. Ensure just the contents, not the root folder itself. SCM repositories are usually of one single project, rather then the full solution. So the root of the repo is the root of the location folder structure of the project.

![SourceTree - Show In Explorer](st-show-file.png?raw=true)

> **Tip:** If you need a quick way to find the *Clone* folder of a given repo, open *SourceTree* and right click on the repo in the left most list, click *"Show in Explorer"*.

> **Note:** Open the new location of the project in Unity and run, this will help show how much the outlined configuration helps when working with Git.


----------


Using SourceTree to make Your Life Easier
-------------

At this point we have all the project source files in a Local Git repo, all that remains is finalizing the configuration. Once you do this the first time you then have a base to "copy" over files to make another Git project, for example all the non-Unity files are Unity/Git templates. SourceTree will help us finish up a little quicker.

![SourceTree - Lots of Files](st-lots-files.png?raw=true)

Open up SourceTree and make sure you're on the File Status tab, you should be lots of files in the list for "Unstaged", esp if you built Unity after coping the files over above. Unity builds a lot of files that shouldn't be stored in a repo. These files are generated, so they are easily reproducible simply by opening the project in Unity. We need to ignore these files, and setup LFS.

![SourceTree - Landing UI](st-landing-ui.png?raw=true)

Across the top we have Clone, Push, Pull, Fetch, and Branch, then to the right Terminal and Settings. From the bottom middle File Status, Log History, and then Commit button on the right, with the Commit message text above. Far left pane list out the Cloned repo's, the middle pane shows File Details depending on the bottom tab states.

Go ahead and press the Terminal button to finish setting up Git with LFS support. Execute the commands below. You only need to do this Once each time a repo is created, not everytime someone Clones it.

![Bash - Repo First Time Setup](git-repo-first.png?raw=true)

    git lfs install
    touch .gitignore
    touch .gitattributes
    touch README.md
    git lfs track "*.fbx"

> **Note:** You can download these files from the [repo here](https://github.com/SlagleSoft/Unity-Git-SCM-Example)

![Git - Ignore and Attributes](g-ign-attr.png?raw=true)

The commands above created some file, go ahead and open them in your favorite text editor, such as Notepad++, we recommend you just copy the values in the files shared in the example repo above. If for some reason you can see the files, you can open them from SourceTree. These files configure Git to know about the content within the source of the project.

![Git - Unity YAML Merge](g-yaml-conf.png?raw=true)

This is an optional step, but extremely recommended. The UnityYAMLMerge is a tool that helps handle conflicts when merging files. Follow the image above to change your ".gitconfig" configuration to use the tool when needed.

![SourceTree - Less Files to Commit](st-less-files.png?raw=true)

We now have a lot less files Git will detect and track change on, you only want to check in true source files, built by the team.

![SourceTree - Commit and Push](st-push.png?raw=true)

Click on "Stage All", fill in a Commit Message, and then click Push. On the new popup, check next to "Master" and click Push. The project is now synced up to the Git SCM service and can be shared with the rest of the team.


----------


Share the Repo with the team
-------------

To work on the project, you don't have to repeat these entire steps every time on every machine by every person. Once the project is initially created into the Git SCM service all you need to do is install the needed software and have access to a service and repository. We recommend everyone to go through the entire process at least once, so they get a more in-depth idea how it all comes together.

![GitHub - Share the Repo link](gh-share-link.png?raw=true)

Login to GitHub and navigate to the project repo, you can then get the Git Clone link, click "Use HTTPS". Anyone working on the project (invited via GitHub access) has access to the link, which is used inside SourceTree when you click the "Clone" button.

![SourceTree - Fetch and Pull](st-fetch-pull.png?raw=true)

Notice the Blue Badge with the #1 on it, this shows up when you click Fetch, or automatically after a set amount of time. This number means the Upstream has changes. After changes have been Pushed to the server and you need to them locally, you use Fetch and Pull. Fetch lets you see what has changed before updating your Working Copy. Your local files are updated when you click Pull, this repeats in either direction.


----------