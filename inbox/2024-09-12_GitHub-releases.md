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
- 1: On GitHub, naviaget to the main page of the repo
- 2: Click on **Releases** on the right of the list of files
- 3: At the top of the page, click **Draft a new release** 
- 4: To choose a tag for the release, select the **Choose a tag** dropdown menu
    - To use an existing tag, click the tag
    - To create a new tag, type a  version number for your release, then click **Create a new tag**
- 5: If you created a new tag, select the **Target** dropdown menu, then click the branch that contains the project you want to release
- 6: Optionnaly, above the description field, select the **Previous tag** dropdown menu, then select the tag that identifies the previous release.
- 7: In the "Release title" field, type a title for your release
- 8: In the "Describe this release" field, type a description for your release. If you @mention anyone in the description, the published release will include a **Contributors** section with an avatar list of all the mentioned users. Alternatively, you can automatically generate your release notes by clicking **Generate release notes**
