# How To Create Modules

!!! mcbuddy "You want to learn me new tricks? Great!"

In this section, I assume you know [how to use the **@** script](usage.md). Please read it first.


## Concept

The sole purpose of the `@` script it to identify which `action` of which `module` to execute, and pass on the baton to it.

There are 4 important locations:

- **`MCBUDDY_SANCTUARY`:** The centralized location for user settings.  
  _Default: `~/.mcbuddy`_
- **`MCBUDDY_SECRETS`:** The centralized location for user‘s sensitive data.  
  _Default: `~/.__mcbuddy`_
- **`MCBUDDY_LIBRARY`:** The location where modules are installed.  
  _Value: `/usr/local/share/mcbuddy`_
- **`MCBUDDY_HOME`:** The location of mcBuddy sources.  
  _Value: `/usr/local/Cellar/mcbuddy` (as installed via Brew)_


## Module Structure

The module source directory has usually the following structure:

    <module>
    ├── actions
    │   ├── <namespace>
    │   │   ├── <action>
    │   │   └── ...
    │   ├── <action>
    │   └── ...
    ├── resources
    │   └── ...
    └── tasks
        ├── <task>
        └── ...

When a module is installed, its source directory is copied into `Library:modules/<module>`.

It can store its settings in `Sanctuary:<module>` and its sensitive data in `Forbidden City:<module>`.


## Actions

Each action is defined in a dedicated file (`action script`) located at: `<module>/actions/<action>`.


#### Execution

The first argument (`command`) is processed and removed from the arguments list (using `shift`).  
Then the `action script` is simply included (using `source`).

So the process is completely transparent for the `action script` and it can operate as if it was called directly.  
It is therefore responsible for the normal operations (e.g. handling arguments, loading dependencies).  
And it can be written in any language as long as the `action script` can be executed by the shell (Bash).


#### Arguments

The `command` is split in 2 parts stored in constants: `MODULE` and `ACTION`.

As explained in the [usage section](usage.md), if omitted, `MODULE` defaults to `core` and `ACTION` to `help`.

Namespaces are actually sub-directories.  
_Example: `<module>.foo.bar.hey` will load the `foo/bar/hey` file._


## Tasks

Tasks allow modules to perform operations at some moments during main core tasks.

# NO!  Each hook is named with a `pre-` or `post-` prefix followed by the name of the core task.  
# NO!  _Examples: `post-install`, `pre-backup`._

# NO!  Each hook is defined in a dedicated file (`hook script`) located at: `<module>/hooks/<hook>`.  
Each task is defined in a dedicated file (`task script`) located at: `<module>/tasks/<task>`.  

Generally speaking:
- I will take care to handle everything that is in `Library`, `Sanctuary` and `Forbidden City`. You must handle only what‘s outside these locations.
- You must handle the parameters that can be provided via the command-line.


### Install

@TODO: pre & post

- **Execution:**
    - On `@ modules install <module>`.
- **My Responsibilities:**
    - Copy the module source directory in the `Library`.
    - If the install is successful, call the `configure` task.
- **Your Responsibilities:**
    - Install all required packages (preferably using Brew, or any other method as needed).
    - Create and/or update settings that are not handled by the `configure` task.


### Upgrade

@TODO: pre & post


### Configure

- **Execution:**
    - Automatically after successful install.
    - On `@ modules configure <module>`.
- **Your Responsibilities:**
    - Guide the user through the configuration process, asking confirmation or input as needed.
    - Create and/or update the configuration files.


### Backup

- **Execution:**
    - On `@ backup` (backing up the whole system).
    - On `@ modules backup <module>`.
- **My Responsibilities:**
    - Perform the global backup.
- **Your Responsibilities:**
    - Prepare any file that must be included in the backup (e.g. backup databases, list installed plugins).
    - Provide the list of files/directories to include/exclude. By default everything in `Sanctuary` and `Forbidden City`.


### Uninstall

- **Execution:**
    - On `@ modules uninstall <module>`.
    - Potentially on `@ uninstall` (uninstalling mcBuddy).
- **My Responsibilities:**
    - If the uninstall is successful, I‘ll take care of deleting the module directories in `Library`, `Sanctuary` and `Forbidden City`.
- **Your Responsibilities:**
    - Remove the settings that are only related to this module.


## Resources

(e.g. configuration templates or files they need to operate).


# Best Practices

## Symlink or not?

When should you create symlinks to files (or directories) in the `Sanctuary` or `Forbidden City`?

**DO:**
- To make it transparent for the program(s) using that file.
- When it makes more sense to access the file from a given location.

**DO NOT:**
- When you have full control over the file and it‘s only used by you.
