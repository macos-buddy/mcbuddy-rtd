# DocsMk

Template and CLI tool to manage a standalone [MkDocs](https://www.mkdocs.org/) documentation.


## Install

**Prerequisites:** Python 3, Git, Bash.

In your project folder, clone this project (or fork it first)…

```
git clone git@github.com:ppo/docsmk.git
./docsmk/docsmk install
```

#### This will

- Create a Python3 virtualenv (`python3 -m venv ./docsmk/.venv`).
- Install the required pip packages (see `requirements.txt`).
- Create the documentation directory (`./docs`); unless it already exists.

#### Remark

If you plan to keep it versioned, don't forget to either:

1) Delete the .git directory of this project:

```
rm -fr ./docsmk/.git
```

2) Change it to your repository:

```
cd docsmk
git remote set-url origin git@example.com:<YOU>/<YOUR_REPO>.git
```


## Usage

```
Usage: docsmk [COMMAND=serve]

  serve      Run the local server to preview the documentation.
  build      Build the documentation.
  clean      Remove the build directory.
  install    Create a virtualenv and install pip packages.
  upgrade    Upgrade the pip packages.
  uninstall  Remove the virtualenv.
  help       Show this usage.
```


## Deployment

### Read The Docs

1. Move the `.readthedocs.yml` file to the root of your repository. No modifications required.
2. Import your project via [your dashboard on RTD](https://readthedocs.org/dashboard/).
3. That's it! The building process starts automatically.
   Click on “your documentation is building” to follow its progress.


**Known Problem:**

If you don't see the projects of an organization in RTD, you've to explicitely grant them access
to that organization.
See [Requesting organization approval for OAuth Apps](https://docs.github.com/en/github/setting-up-and-managing-your-github-user-account/requesting-organization-approval-for-oauth-apps).
_([information found here](https://github.com/readthedocs/readthedocs.org/issues/2044#issuecomment-405940573))_


**Documentation:**

- [Importing Your Documentation](https://docs.readthedocs.io/en/stable/intro/import-guide.html)
- [Configuration File](https://docs.readthedocs.io/en/stable/config-file/index.html)
- [Incoming Webhooks and Automation](https://docs.readthedocs.io/en/stable/webhooks.html)


## License

This project is licensed under the [MIT License](https://choosealicense.com/licenses/mit/).  
See the [LICENSE](./LICENSE) file for details.
