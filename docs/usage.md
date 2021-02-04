# Usage

!!! mcbuddy "Easy, just call `@` to shout me your orders."

```bash
@ COMMAND [ARGUMENTS]...
```

`@` is just a gateway to actions provided by modules.  
`COMMAND` identifies the module and its action to execute.  
`ARGUMENTS` are simply passed to the action.


## Commands

`COMMAND` is usually of the form `MODULE.ACTION` (separated by a dot).

- For simplicity, actions of the `core` module (i.e. mcBuddy itself) can be executed without mentioning the `MODULE` part.
- If the `ACTION` part is omitted (i.e. `MODULE.`, with a trailing dot), it defaults to `help`.
- Modules can group actions together in namespaces.

!!! example "Examples"
    - No module: `@ upgrade` is the same as `@ core.upgrade`.
    - No action: `@` is `@ core.help`, and `@ ssh.` is the same as `@ ssh.help`.
    - Namespaces: `python.versions.available`.


## Arguments

`ARGUMENTS` are specific to the command. And as for all command-line tools…

For gateway actions, the arguments **must** be the same as the real command (**unless really good** reasons). Otherwise, our recommandations are the following…

Arguments can be of 3 forms, usually specified on the command-line in that order:

- **Flag:** An option without value, acting like a boolean.
- **Named:** A “key=value” information.
- **Positional:** A value that must be specified at a given place.

Flag and named arguments are usually handled in 2 forms:

- **Short:** A single alpha-numeric character, preferably lowercase, preceeded by `-` (a single short dash).
- **Long:** A lowercase alpha-numeric-dash-case word, preceeded by `--` (a double short dash).

!!! example "Examples"
    - Flags: `-q`, `--quiet`, `-V`, 
    - Named: `-s :`, `--separator=":"`, `src="/path/to/"`.
    - `@ module.action -q --separator=":" 42 "a string value" "/path/to/"*`


## Modules

As said, the `@` command is just a gateway to actions provided by modules.

Check the [modules](modules.md) section for more details. Or see [how to create one](how-to-create-modules.md).
