![CruiserFlow Logo](CruiserFlow.png)

***CruiserFlow*** is a simple and straightforward Git Workflow for web software projects with a small team size (~ 12 individuals or less) and regular interpersonal communication. It is designed for and integrates very nicely with single small teams in which every individual knows every other individual, communication occurs on a regular basis and trustful joint ownership of the projects is universally shared.

CruiserFlow is also very suitable for a highly agile fast iterating Scrum approach with weekly sprints, standardized tools and technology and code that is run directly without further centralized post-commit code-processing like automated upstream compilation, transpilation, minification, testing, container procedures or similarly complex and centralized pre-deploy tasks.

CruiserFlow makes potentially required rollbacks trivially easy and tracks every release verbatim while giving individual developers maximum freedom and agency to organize their work environment and track their individual setups in their own branches as desired.

***

## Details

### **CruiserFlow** Branches

* **release**
    * no direct commits allowed, only merges
    * every merge & push to the upstream "**release**" branch automatically deploys to staging and has a one-click deploy to live/production
    * every commit in **release** represents an actual release; it’s up to the individual developer merging to test and ensure this before merging his code
    * web-ready media assets directly used and referenced in live code may be tracked in this branch but excluding BLOBs that are too large to justify being tracked by keeping them in **/workbin** is recommended and encouraged
    * this branch must **_not_** contain any purely development related code or asset
    * this branch does **_not_** track the **/tools**, **/workbin** or **/docs** directories
    * **release** must be rollback-ready, meaning that the previous commit in **release** should run simply by being (re-)deployed; commits in **release** all must be deployable by non-expert individuals and non-developers
* **develop-[developers_name]**
    * Every developer has this **_single_** individual upstream branch to which they commit and push frequently (multiple times a day). This branch should closely track the critical aspects of the individual’s current state of work. The developer should not lose any more than 1 or 2 hours of work should their current state of work be lost due to error or disaster. Only the individual developer is allowed to merge from their branch to **release**. Anything that the developer deems useful for their work may go here, including own scripts, individual post-pull and pre-commit tooling, local configs, etc.
    * It is the individual developer’s responsibility to keep "**release**" clean of their personal development setup and correctly prepare and process code that they want to merge into "**release**" and to use individual tooling to ensure this
    * commit messages must contain useful information of the work done regularly; no more than 5 commits in a row may have generic phrases such as "**minor change**," "**cleanup**," "**sync commit**," etc.
    * bloating this branch with binary files such as media-workfiles, original images in print resolution, and other BLOBs is not allowed
    * commits must be logically **separated** by feature or task
    * commits that are merged into **release** must contain useful information on the updates contained
    * the individual developer may add **additional** entries to **.gitignore** in coordination with **their** peers if **/workbin** doesn’t suffice for technical reasons
    * the developer may tag commits as they desire, as long as their personal tags don’t collide with universal tags the team has agreed on
* **junior-[developers_name]** (optional, as required)
    * same as **develop-…**, but **junior** may not merge; a developer has to pull from **junior-…** and merge into **release**
* **testing** (optional branch)
    * no direct commits allowed, only merges
    * **testing** is an optional branch that deploys to **its** own host automatically upon merge and allows for user-testing individual **features** that aren’t decided upon yet
    * in **testing** all bets are off; **testing** may be deleted and **re-branched** from **release** or some **individual’s** own **develop** branch

***

### **CruiserFlow** Directories

* **/workbin**
    Apart from usually gitignored files and directories, the project’s /workbin directory in root is **_universally ignored_** across all branches in a CruiserFlow project. /workbin is meant for individual developers‘ temporary workfiles such as large BLOBs, taking notes, project related messages, etc. Archiving (subsets of) this directory – if necessary – is the *individual developer’s responsibility* but shouldn’t be generally required.
* **/tools**
    Tooling code and scripts go here; **/tools** must **_not_** be tracked in **release**
* **/docs**
    documentation in editor-readable format goes here (.txt, .md, etc.); proprietary file formats are prohibited; **/docs** must **_not_** be tracked in **release**
* **/dist** or **/deploy** (optional directory) a directory of this sort may be tracked in "**release**" and gitignored everywhere else if deemed sensible

***

## Further local branches and individual clones

Every individual may have as many branches, working copies, or repo-copies as they deem necessary in their individual workspace locally and is encouraged to do so in order to solve specific problems or prevent pushing prohibited branches to upstream.

However, they are **_not_** allowed to push these other branches upstream and nothing mission-critical may solely be stored and tracked in such a branch. It is up to the individual developer to ensure that upstream information and configuration is removed/disabled in additional personal clones to prevent accidental upstream pushing.
