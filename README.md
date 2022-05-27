# darpa-software-examples
Examples, templates and resources for facilitating writing sharable and scalable software

## Introduction

This guide is intended for teams taking part in DARPA's program. It tackles a case which is more specific than general problem of writing good software, so please keep this in mind while reading – this is not necessarily set of best practices, but rather set of practices that we find best suited for organizations participating in this program. 

Our goal here is to define a set of guides and tools that will help minimize the friction for collaboration and integration betwen projects.

Here's the characteristic of the teams and projects involved:
- Teams come from various organizations
- They write software that other teams might need to integrate with
- Some projects might have only a single developer, while other have many
- People involved are usually domain experts, not software engineers
- We're at the forefront of science and engineering, so the scope of the projects is deemed to change.

Therefore, we tried to come up with solutions that will be:
- Accessible 
- Low friction
- Automated
- Flexible

Most of the guide is written with Python in mind and assume using GitHub for storing code. If that's not the case for you, the solutions can almost certainly be adapted to other languages/tools.

## List of resources

### GitHub workflows
In the `.github` directory, you can find the files listed below. They don't require any extra setup, they just need to be present in the right place, exactly as in this repository. These are just basic versions of the files that you can use, feel free to customize to fit your needs!
- Pull request template – when present, all the pull requests are created with this template. It also contains a checklist, so that you don't forget to, e.g.: document the changes you've introduced.
- Issues templates – when present, allow you to create new issues with one of two templates. The goal is to streamline communication, as the person creating issue will be prompted to include necessary info.
- Workflows for style – when present, it will automatically run a workflow checking for style issues, in this case whenever there's a push or pull request to a `main` branch.
- Workflows for tests – when present, it will automatically run a workflow running tests, in this case whenever there's a push or pull request to a `main` branch.

### GitHub – branch protection rules

Another thing that you might want to configure are branch protection rules at GitHub. This will allow you to put some restriction on the `main` (or any other) branch that will help you introduce code reviews into the project, ensure quality and save you from some unpleasant git situations.

You need to have admin privileges for the repository to be able to enable these features.

What to do:

1. Go to Settings
2. Branches (left pane)
3. "Add Rule"
4. Type in the name of the branch you want in the textbox at the top
5. Select options

Here is a set of options that we use for our projects at Zapata (some options are visible only after you click "parent option" first):
- "Require a pull request before merging" with 1 required approval
- "Require status checks to pass before merging" + "Require branches to be up to date before merging" . Then in the search box you need to type in the names of the workflows you want to pass (they need to be already on the `main` branch, otherwise they won't show up!). I remember encountering case when they didn't show up, but I'm not sure exactly what was the reason. If you encounter such case, please let [me](michal.stechly@zapatacomputing.com) know.

Enabling this option will result in:
- No-one being able to push directly to `main` – all the code on `main` needs to go through pull requests.
- Style checks and tests will have to pass before someone will be able to merge their pull request.
- At least one person will need to review and accept pull request before merging.
- Admins will be able to override these settings.

### pre-commit-hooks
[Pre-commit](https://pre-commit.com/) is a useful tool which allows you to run certain checks every time you want to commit something in your git repository. Contrary to the GitHub workflows, it runs the tests on your local machine, every time you run `git commit`. We've included an example of such file, for the instructions how to set it up, please refer to [the documentation](https://pre-commit.com/). If you're using both GitHub workflows and pre-commit hooks, it's important to make sure all the settings and versions of the libraries are the same, otherwise it might lead to frustrating debugging session.


### gitignore
Gitignore is a very useful file which tells git which files it should never commit. Your project might automatically generate `__pycache__` directories that you don't want to commit. In such case, you can just put `__pycache__/` into the `.gitignore` file and you can safely run `git add .` without risking of them accidentally being added there.

You can find a sample file in this repository or use [this tool](https://www.toptal.com/developers/gitignore) to generate one.


## Versioning

Versioning your software is really important, as it allows others to use it reliably.
The most common system for versioning is [Semantic Versioning (SemVer)](https://semver.org/).


Some people don't want to release a new version of their package until they feature they want to release is polished and fully developed. However, this is not a good strategy, as it might lead to very rare, irregular releases. 

A couple of good rules of thumb when it comes to releasing:

- It's better to release to often rather than too seldom
- Automate as much of the process as possible (TODO: provide some materials)
- If your project is still in very experimental phase, use major zero version (see below)

### Major zero version

SemVer documentation has an interesting case which works very well with for projects in the early stages:

> 4. Major version zero (0.y.z) is for initial development. Anything MAY change at any time. The public API SHOULD NOT be considered stable.

So basically, if you don't want to promise anything to your users, you can just use major version zero, in such cases no rules apply. This is a good way to get acquainted with SemVer while at the same time communicate to your users clearly what's the stage of your project.
Some notable QC projects that use 0 as their major version are [Qiskit](https://github.com/Qiskit/qiskit) or [CirQ](https://github.com/quantumlib/Cirq). 



## TODOs

Here are items that we would like to see more materials on but we haven't yet found time to add them.

- Templates for testing
- Guide on "how to write tests for experimental stage scientific software"
- Guide to setting up your IDE properly
- List of good reading resources
- Materials on style 
- More info on automatic style checkers

