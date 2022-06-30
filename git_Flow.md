**Workflow of Git**

The main branch is **develop**

Child branches are getting from **develop** and named with the version that are install in the factory e.g. develop_21.1

***Create a feature branch***

•	First you need to make sure **develop** (or version branch) is up to date by doing a pull (fetch / merge). 

•	Then create a feature branch of **develop** 

**Steps**

On the folder where the code is execute the following commands:
- git checkout **develop** 
- git fetch origin **develop**
- git reset --hard origin/**develop** 
- git checkout -b (feature/hotfix/improvement/fix)/BSM-XXXX-Jira-description

Note: If the feature is in a different version, the source branch is the develop_[version] branch. 

Example :

``` 
feature/BSM-42986-add-doc-with-prov-process
```

•	Make code changes locally in feature branch 

At this point to have created a feature branch locally and can start making code changes. Once you are satisfied with your code, you can commit it locally. Please include jira number in the commit message, it is mandatory to enable link between gitlab and jira (add a comment in the jira, add hyperlink to jira)  

*[JiraNumber]:message*

Example :

``` 
[BSM-42986]: add provisioning procedure
```

- git commit -m "[JiraNumber]:message" 

•	As needed (daily procedure): Interactive rebase from **develop** (or version branch) before to publish 

Before publishing your branch for code review and as otherwise needed, merge any changes from **develop** (or version branch) into your feature branch to make sure it is up to date. The rebase command will remove your commits, merge changes from **develop**, and then reapply your commits on top of the merged code. If there are any merge conflicts, you will need to address them before moving on. 

You can rebase as many times as needed. It is easier to rebase before your feature branch is published. 

- git checkout **develop** 
- git fetch origin **develop** 
- git reset --hard origin/**develop** 
- git checkout (feature/hotfix/improvement/fix)/BSM-XXXX-Jira-description 
- git rebase **develop** 

•	Publish feature branch 

Publishing your feature branch will create a remote version of your branch. This allows other users to see/checkout your branch so that they can test and code review it. 

git push origin (feature/hotfix/improvement/fix)/BSM-XXXX-Jira-description 

•	Before review and merging to **develop** (or version branch): rebase from **develop** and squash commits 

Once the feature is complete, you can then merge (only using a pull request) it back into **develop** (or version branch). 

- git checkout **develop** 
- git fetch origin **develop** 
- git reset --hard origin/**develop** 
- git checkout (feature/hotfix/improvement/fix)/BSM-XXXX-Jira-description 
- git rebase -i **develop** #pick or reword the first line, fixup the rest 
  - A VM editor is going to be opened, use [esc]+[:]+[i] to edit the commits, if there is nothing to commit, finish the edition with [esc]+[:]+[wq]
- git push -f origin (feature/hotfix/improvement/fix)/BSM-XXXX-Jira-description 

•	Merge to **develop** (or version branch) 

Once your branch is rebased, you're ready to merge your finished code only using a Pull Request. 

 