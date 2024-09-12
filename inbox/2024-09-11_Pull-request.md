---
date: 2024-09-11
tags:
    - Doc
hubs:
    - "[[git]]"
    - "[[GitHub]]"
urls:
    - https://docs.github.com/en/pull-requests
---

# Pull request 

A pull request is a proposal to merge a set of changes from one branch to into another. Collaborators can review and discuss the proposed set of changes before they integrate the changes into the main codebase.
After initializing a pull request, you'll see (on GitHub) a review page that shows a high-level overview of the changes between your branch (the compare branch) and the repository base's branch.
You can add a summary of the proposed changes, review the changes made by commits, add labels, milestones, and @mention individual contributor or teams.
Once you've created a pull request, you can push commits from your topic branch to add them to your existing request. They will appear in chronological order within the pull request and changes will be visible in "Files changed"

Other contributors can review proposed changes, add review comments, contribute to the pull request discussion and even add commits.

## Draft pull requests
When you create a pull request, you can create a pull request that is ready for review or a draft pull request. Draft pull requests can't be merged, and code owners are not automatically requested to review draft pull requests.
You can a draft PR as ready for review when you're ready to get feedback. It's possible to convert a PR to draft at any time.

## Creating a pull request

You can specify which branch you'd like to merge into when you create your pull request. It can only be opened between 2 branches that are different.
To open a pull request, you must either have write access to head of the source branch for public repo, or be member of the organization for organization-ownerd repo.
It is possible to link a pull request to an issue to show that a fix is in progress and to automatically close the issue when someone merges the PR.

### Steps

- 1: On GitHub, navigate to the main page of the repo
- 2: In the "Branch" menu, choose the branch that contains your commits
- 3: Above the list of files, in the yellow banner, click **Compare & pull request** to create a pull requets for the associated branch
- 4: Use the *base* branch  dropdown menu to select the branch you'd like to merge your changes into, then use the *compare* branch drop-down menu to choose the topic branch you made your changes in
- 5: Type a title and description for your pull request
- 6: To create a pull request that is ready for review, click **Create Pull Request**. To create a draft PR, use the drop-down and select **Create Draft Pull Request**, then click **Draft Pull Request**. If you are the member of an organization, you may need to request access to draft PR from an organization owner.


### Changing branch range and destination repo

By default, PR are based on parent repository default's branch. If default parent repo isn't correct, you can change both the parent repo and the branch with the drop-down lists. It is also possible to head and base branche with the drop-down lists to 
establish diffs between reference points.

Remember that the *base branch* is **where** changes should be applied, the *head branch* contains **what** you would like to be applied.

When you change base repo, you also change notifications for the PR. Everyone that can push to the base repo will receive an email notification and see the new PR in their dashboard.


## Request PR review

To assign a reviewer to a PR, you will need write access to the repo. You can then assign anyone with read access as a reviewer.
Organization members with write access can also assign a PR review to any person or team with read access to the repo. The requested reviewer or team will receive a notification that you asked them to review the PR. 
If you request a review from a team and code review assignment is enabled, specific members will be requested and the team will be removes as a reviewer.

You can request a review from either a suggested or specific person. Suggested reviewers are based on git blame data. If you request a review, other people with read access can still review up the PR. Once someone has reviewed the PR, and the necessary changes have been made,
you can re-request review from the same reviewer. If he does not submit a review and the PR meets the repo's mergeability requirements, you can still merge the PR.

### Steps
- 1: Under the repo name, click **Pull requests**
- 2: In the list of PR, click the PR that you'd like to ask a specific person or a team to review
- 3: To request a review from a suggested person under **Reviewers**, next to their username, click **Request**
- 4: Optionnaly, to request a PR fromm someone other than a suggested person, click **Reviewers**. If you know the name of the person or team you'd like a review from, type the username/team name, click on it to ask a review.
- 5: after the PR is reviewed and the necessary changes has been made, you can ask a reviewer to re-review the PR. Navigate to **Reviewers** in the reight side bard and in the 'looping arrows' nex to the reviewer's name.
