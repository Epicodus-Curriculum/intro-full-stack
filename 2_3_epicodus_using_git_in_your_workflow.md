We’ve covered a lot of information about why we use Git and how to manage repositories on GitHub. Now it's time to put it all together by discussing exactly how to use Git in your workflow and best practices when using Git.


### List of most relevant git commands

This is a list of all the git commands we have used so far.

* `git init`
    * Initializes a `.git` repository in your project. 
    * Required only once per project. 
    * Tracks changes made in the project.
    * If deleted local project history is lost. Hopefully you have a remote version of your project on GitHub you can clone in this event. 

* `git status`
    * Tells you the status of files: untracked, tracked (unmodified, modified, staged).
    * Use frequently; especially after the `git add` command and before making a commit.

* `git diff name-of-file`
    * Allows you to see what changes were made to a modified file. 

* `git add name-of-file` `or `git add .`
    * Adds files to be committed. 
    * The `.` represents all files. Use it to add all modified files to staged.
    * Can also add multiple files but not all by leaving space between file names. Such as `git add name-of-file1 name-of-file2` etc.

* `git commit -m “commit message here”`
    * Used to take a snapshot of your project as it currently is at that moment in time.
    * Becomes part of your project's commit history.

* `git log`
    * Allows you to view commit history in the terminal.
    * `--oneline` is an option for the `git log` command. `git log --oneline` just lists the commit ids and messages. 

* `git remote add origin url-to-remote-repo` or `git remote add your-initials url-to-remote-repo`

    * “origin” is the typical default name for urls to remote repos.
    * “Your-initials” represents renaming “origin” to your initials though you can rename origin to whatever you like. Useful to rename origin when working with other people. 

*  `git push origin main` or `git push your-initials main`
    * Adds changes from local repository to remote repository on GitHub.
    * Recommend pushing changes at the end of each workday. 

**New commands!**

* `git commit --amend -m “new message for most recent commit”`
    * `--amend` is an option for the `git commit` command
    * Modifies the most recent commit message.
* `git rebase -i HEAD~n`
    * Allows you to bulk modify older commit messages. 
    * “n” represents the number of commits you want to edit starting from the first.
    * See GitHub Docs: [Changing the message of older or multiple commit messages](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/changing-a-commit-message#amending-older-or-multiple-commit-messages) under “Amending older or multiple versions”.


## Co-Author Commit Trailers

GitHub uses your commit history to create a collection called **GitHub contributions** in your GitHub profile page. As a brand new user to GitHub, your contributions will be sparse. That's okay, you’ll make lots of commits in the future.

One reason to commit regularly while at Epicodus is that sometimes employers will look at your GitHub contribution calendar as evidence of experience.

For example, here are contributions of two graduates from the same Epicodus cohort. Their commits begin in January and end in May


Graduate 1:

![more](https://i.imgur.com/TVgdR9P.png)


Graduate 2:

![less](https://i.imgur.com/r1yhqKW.png)


Graduate 1 made more commits than Graduate 2 while in the program. While the number of commits is not an indicator of meaningful work, having a spotty commit history or no commits will look bad for your coding portfolio, aka your GitHub account.

The takeaway here is to commit regularly as part of your workflow.

However, what about when pair programming remotely? Only the person who has the project on their computer can make commits and they end up as the only author on the commit.

We can fix that using a co-author **commit trailer**.

Using a co-author commit trailer looks like this:

```
git commit -m “Add styled box to heading

Co-authored-by: firstName lastName <emailAddress>
```

The spacing is important. This is what it will look like in your terminal before hitting Enter:

![commit trailer](https://i.imgur.com/idXXTnz.png)

	
The `firstName`, `lastName`, and `<emailAddress>` should be the information your pair uses for their GitHub account. You can include additional co-authors by adding them to a new line in the commit message.

Using `git log` you should see:

![git log commit trailer](https://i.imgur.com/qz7YaSi.png)	


Finally, after pushing to the remote repository, you should see that this commit has a link to both author's GitHub accounts.

Here is further documentation about [creating commits with mulitple authors](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/creating-a-commit-with-multiple-authors).

Be aware that it may take time for the **GitHub contributions** to appear on your profile page but if they are not showing up after a few days then troubleshoot using this doc: [Why are my contributions not showing up on my profile?](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/managing-contribution-settings-on-your-profile/why-are-my-contributions-not-showing-up-on-my-profile)


## 	Fixing past commit history

If you forget to co-author a commit, that is no problem. It is relatively easy to go back and alter commit history on your **local** repository.


Use the git command:


```
git rebase -i HEAD~n
``` 
 
`n` represents the number of commits you want to edit, starting from the most recent comment. For example, if I wanted to edit the last 4 commits, I use `git rebase -i HEAD~4`

Git should open a new file in VS Code.


>Note!  
>If VS Code doesn’t open and instead git wants you to make edits in your terminal, then revisit this lesson [Git configurations](https://www.learnhowtoprogram.com/introduction-to-programming/getting-started-with-intro-to-programming/git-configurations) and make sure VS code is set up as Git's default editor.


![rebase first menu](https://i.imgur.com/AFwFUEV.png)


VS code should open a edit window that looks something like the image above. At the top is the commit history of the project. Below are instructions for options available. The list is in ascending order; the red circle is next to the most recent commit made in the commit history. The red underlined words are what we feel are the most relevant options for you at this time. (Though play around with them all!)

`pick` is just leave the commit as is.
`reword` means to use the commit but edit the message.
`squash` is to use the commit but meld it into the previous commit (the one next above in the list). This is helpful if you forget to include a minor edit in a commit. You can make another commit and then meld the two.

Do use the options, replace the word `pick` with any of the option names. Such as: 

![rebase commands](https://i.imgur.com/g0GTcqi.png)


Then save and close the edit window. A new edit window will appear in VS code. The first thing Git wants us to resolve is the `squash` command. We want to combine the very first and second commit into one. In this new edit window, Git is giving us an opportunity to edit the commit message if we please.


![rebase squash](https://i.imgur.com/WyT9zT7.png)

(The last few letters of "languages" is in red because that commit message is a bit too long.)

For this example this is how we chose to combine the commit messages.

![combine rebase](https://i.imgur.com/wjFCGOj.png)
        

When you are happy with the commit message, save and close the edit window. 

Since we also chose to use the `reword` command on another commit, the edit window will open again. This time we are not combining commits, just editing the commit message of a single commit.

![reword rebase](https://i.imgur.com/N7j3TLd.png)
        

This time we added our co-author commit trailer. When we are done we again save and close the file.

![reword cocommit](https://i.imgur.com/8aNy8XR.png)

Using `git log` we can see our new local commit history. It looks like we forgot to add a co-author commit trailer to all commits. No problem, we can just run `git rebase` again!

![final rebase result](https://i.imgur.com/zyFpCKc.png)


## Git Best Practices

Just like with any list of best practices, your standards might change depending on circumstances or on the company you work with in the future. The following are Git best practices based on convention and what practices we know to help beginners create good habits.


### When to make commits

Typically, you make a commit when any of the following are true:

1. When a new feature or functionality is added to your project.
2. When a bug (an error) is fixed.
3. When we reach a stopping point or have been stuck for a long time.

A long period of time may pass before any of these situations are true. For the sake of making it a habit to commit while you are learning, we recommend making a commit at least every 30 minutes.


When understanding when to make a commit, there aren't really any hard rules. However, there is definitely the problem of committing too much or not enough. It is more of a problem to not commit enough. Here are some common scenarios:


Scenario 1:  
    “Ava and Eli are pair programming. Since Ava and Eli are new to using Git, they decide to set up a timer and make a commit every 30 minutes. However, when it is time to commit, Ava and Eli feel like they haven’t made any meaningful progress. Ava and Eli use the abbreviation WIP (Work in Progress) at the start of the commit message along with a brief description of progress made so far.”

Scenario 2:  
    “Ava has been coding for a long time and making really great progress. However, Ava has forgotten to make commits the entire time. A lot of work has been done but it has no accompanying commit history. Ava has 5 modified files in her project. She could make 1 commit for all 5 files. Instead Ava decides to make 1 commit for each file, resulting in 5 commits. This was the better choice because Ava can more clearly describe the change to each file in separate commit messages. 5 commits also better reflects the amount of work Ava has done more so than 1 commit.



Scenario 3:  
    “Eli spots several errors in their code. Eli is more experienced so they quickly know how they will fix the errors. Eli could fix all the errors and then make 1 commit. Instead, Eli decides to fix 1 error at a time then make a commit. This was a better choice because Eli can include a commit message for every error. Now Eli has a more robust commit history. If Eli encounters a similar error in the future, they can more easily reference their commit history.

Scenario 4:  
“Nick has completed a new feature in his project. He has added a form to his website that prompts visitors to fill out a fun quiz. Proud of his work, Nick makes a commit. However, just after Nick makes a commit, he notices he accidentally left out the last question in the quiz. Nick adds the question and makes another commit.”


          


### When writing commit messages

1. **Commits messages should be brief; generally 50 characters or less.**  
Commit messages are intended to be brief so they can be easily referenced. When looking through a big list of commit messages (such as when using `git log --oneline`)  you don’t want to have to read lengthy paragraphs of information. 


For example, if you make a really long commit message, on GitHub the message will be cut off. You would have to click the `...` icon to see the whole message. That's annoying!

![too long commit](https://lh3.googleusercontent.com/u/0/docs/ADP-6oFm7MjERRPAdzt3FQy-Robl-C0CsQ6hDfY8rZ5qO-1pomPQpKSFFqV5Lt487wjrO6AQ1hje5Ozb9SkdaimlJIJBKy0IXrEgx2kCMUr7wMKt7rndVcZXgRNC4u3jCMmMAZ95vkuOaH2WmR-xQo_anuA1Qrgxn1lwupqAxXXZslB570UGaiLezb1tLPxZgLy9KvQW3uRSAAecSQqgpAQesRYE6PkpBJ7mUyE39iexSxsz75goD9STw-0XHAeVoIEWnnrywf4gF0UjOGlbYOiXGiAZtz4l9bmqBA1_RNX0IvtUOJfWZD5ZW22sXffi9PrDU3PafcGp-iOY8u5Au2eF0UnE2X_4r76XiAO4RnlpBapXKmSwWPKOyR2TI1k38RxVEhBJMiHm75nL_sxDLM8J12PXX8xCx-oUwv95DGSWW8pwEIvHYenItRsSln50LS5Ex_RTBPzgDjP0ZKUsd5ms9nGD0v6Igqt6TqRrtc5RpqLtLA6HEllVUAYuitv3w3qqBM90cL1xbJKuuYx3db6X6mWE5U2z8JPb2wyDZUm0IVJ_bhYQOWIgzHYY9uB7yaB3VuOmzgu0M-HIXfds_aPiQGdBB2Gz5BCwYaiA3IoFAobWB0O5HgIGhKF1Pvj2T8yF6KdoVXTBvOPq6sISzavcjAUe0A6eBLyREGlG8Jphq2YG7etdCz0OqFhspc1Rk395e6IFuh7tL-SIIMiwQDMQGr6f5DxFL_oTjueHGq_1r_D-LQMS67vOr4yaSGuHm3X_sCex1wIJ1yVQ2f1pxIz6Wz6sCychYBqDTmQ_aI0jZm68dSKPB1_C6iyBzXlImCMoVyWR63I9Sa9aKw5XDycJggQW3AL0ZllOQQDcxwxB4tt1omF7Rq-djVOhmEgzXuR5oK9j4p8QFWqgynJPc_n5f0eUu0_-YRJqtjS23_v9LPD8vWdL5jxzaqhZwfK5bNk32NTk0yreiMtGpHlmfVDBI-LqcCg_Nww1TD5OktlrMKyXTHkRkWzmEzaNHCK8RWHYtKH_MscugdASsmBmcjR5Dq43moU_8WuN8iZ4Ag)


If you are not sure how to condense your commit message, that might be a sign your commit should be broken down to make several smaller commits.


2. **Start a commit message with a present tense verb.**  
In the English language, a verb is a word used to describe an action, state or occurrence. These are examples of present tense verbs: fix, add, adjust, create, remove, delete, move, update.  

Starting a commit message with a present tense verb is generally considered best practice. That's to say, you’re going to see exceptions and other conventional standards out there. 

3. Can use labels WIP (work in progress) or BUGFIX at start of commit message.  
This is an exception to the previous guideline. Using the WIP label is helpful when making regular commits to show progress but you haven’t finished anything yet. Using the label BUGFIX is helpful to more easily reference your commit history.

These are examples of good commits messages:

``` 
"Add personal bio to home page"
"Add green and gold styling to navbar"
"Add styled box to heading"
"Add radio buttons to favorite color form"
"Add README that lists completed features"
"Update README to include project setup instructions"
"Create hide function to hide form on sign up"
"Write temp method to track current temperature"
"WIP: updating navbar to add styles"
"WIP: trying to fix bug in addMoney function"
"WIP working on logic for Record class"
"Fix typos in favorite things list"
"BUGFIX: Fix overlapping text box on home page"
```

The following are examples of bad commit messages:

All of these commits are too vague
```
"Update styles"
"Fix bug"
"Add forms"
"Add business logic"
```

These commits are too long and too detailed.
```
"Add sidebar with a bulleted list of how to say hello in English, French, Kinyarwanda, Japanese, German, Spanish, and Pig Latin."
"Add sidebar, navbar, page content, and complete styles for all pages plus add user interface code.
```
These commits are too wordy and don’t start with a present tense verb. With exceptions for using WIP (work in progress) or BUGFIX. 
```
“It will add favorite things list”
“I added a info form to the front page”
“We completed writing setup instructions in README
```

## Git workflow

Your Git workflow will change over time; especially when you start your next job after Epicodus. 


### When pair programming remotely:

Let's say Ava and Eli are pair programming:

1. Ava creates a project directory on her computer. She initializes Git in the top level directory of the project using `git init`.
2. Ava starts **VS Code Live Share** and **VS Code Live Server** so Eli can participate in pair programming.  

3. Ava and Eli pair program as usual, switching between being the driver and being the navigator.
4. Regardless of who is the driver, only Ava can access her terminal to use git commands. When it is time to commit, Ava uses the following git commands: 
    * `git add name-of-file` 

    * 
    ```
    git commit -m “brief message

    Co-authored-by: Firstname Lastname emailAddress”
    ```
    Ava includes Eli's information as a commit trailer in the commit message so Eli gets credit.  

    Ava repeats this step as necessary throughout the pair programming session. 

5. Ava and Eli are done pair programming or have come to a good stopping point. Ava creates a remote repository on her GitHub account. Ava then connects her remote repository to her local repository using `git remote add origin url-of-remote-repo` in the top level directory of the project. 

6. Ava then pushes all changes from her local repository to her remote repository using `git push origin main`.

    Ava repeats this step periodically if additional changes have been made to her local repository.

7. Eli forks Ava's remote repository so a copy is on their GitHub account. If Ava and Eli continue to pair program on the same project, Eli can sync additional changes to their forked repository from the original via GitHub.


### When working independently:

1. Create a new project on your computer. Initialize Git in the top level directory of the project using `git init` 

2. Start **VS Code Live Server 
**
3. Work as usual and make regular commits. When it is time to commit:
    * `git add name-of-file` 

    * `git commit -m “brief message”`

    Repeat this step as necessary to commit.

4. When at a good spotting point, create a remote repository on your GitHub account. Connect your remote repository to your local repository using `git remote add origin url-of-remote-repo` in the top level directory of the project. 

5. Push changes to your remote repository using `git push origin main`. Repeat this step periodically.
