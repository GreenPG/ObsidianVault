---
date: 2024-09-12
tags:
    - Doc
hubs:
    - "[[GitHub]]"
urls:
    - https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases
---

# GitHub releases 

Releases are deployable software iterations you can package and make available for a wider audience to download and use.
They are based on Git tag, which mark a specific point in your repository's history. A tag date and the associated release date since they can be created at different times.
Only people with write access to a repo can manage releases.
You can manually create release notes while managing a release, or you can automatically generate release notes from a default template,or customize your own release notes template.

GitHub automatically include links to download a zip file and tarball containig the contents of the repo at the points of the tag of creation.

If a release fixes a security vulnerability, you should publish a security advisory in your repo. GitHub reviews each published scecurity advisory and may use it to send Dependabot alerts to affected repo.
You can view **Dependents** tab of the dependency graph to see which repo and packages depend on code in your repository, and may threfore be affected by a new release.

## Release management

You can create new releases with release note, @mentions of contributors, and links to binary files, as well as edit or delete existing releases. You can also create, modify and delete releases by using the Releases API.
You can also publish an action from a specific release in GitHub Marketplace.
You can choose wheter Git Large File Storage object are included int ZIP files and tarballs that GitHub creates for each release.

### Creating a release
- 1: On GitHub, navigate to the main page of the repo
- 2: Click on **Releases** on the right of the list of files
- 3: At the top of the page, click **Draft a new release** 
- 4: To choose a tag for the release, select the **Choose a tag** dropdown menu
    - To use an existing tag, click the tag
    - To create a new tag, type a  version number for your release, then click **Create a new tag**
- 5: If you created a new tag, select the **Target** dropdown menu, then click the branch that contains the project you want to release
- 6: Optionally, above the description field, select the **Previous tag** dropdown menu, then select the tag that identifies the previous release.
- 7: In the "Release title" field, type a title for your release
- 8: In the "Describe this release" field, type a description for your release. If you @mention anyone in the description, the published release will include a **Contributors** section with an avatar list of all the mentioned users. Alternatively, you can automatically generate your release notes by clicking **Generate release notes**
- 9: Optionally, to include binary files such as compiled programs in your release, drag and drop or manually select files in the binary box
- 10: Optionally, to notify users that the release is not ready for production and may be unstable, select **This is a pre-release**
- 11: Optionally, select **Set as latest release**. If you do not select this option, the latest relase label will automatically be assigned based on semantic versioning.
- 12: Optionally, if GitHub Discussions is enabled for the repo, creates a discussion for the release
    - Select **Create a discussion for this release**
    - Select the **Category** dropdown menu, then click a category for the release discussion
- 13: If you're ready to publicize your release, click **Publish release**. To work on the release later, click **Save draft**. You can then view your published or draft releases in the releases feed for your repo.

### Editing a release
- 1: On GitHub, navigate to the main page of the repo
- 2: Click on **Releases** on the right of the list of files
- 3: Next to the release you want to edit, click on the edit button
- 4: Edit the details for the release in the form, then click **Update release**. If you add or remove any @mentions of GitHub users in the description, those users will be added or removed from the avatar list in the **Contributors** section of the release.

### Deleting a release
- 1: On GitHub, navigate to the main page of the repo
- 2: Click on **Releases** on the right of the list of files
- 3: On the right side of the page, next to the release you want to delete, click on the delete button
- 4: Click **Delete this release*
