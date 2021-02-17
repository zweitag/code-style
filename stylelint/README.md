# Stylelint
## Summary

[Stylelint](https://stylelint.io/) is a mighty, modern linter that helps you avoid errors and enforce conventions in your styles.
## Details
Using [Zasaf](https://github.com/zweitag/html-css-guidelines) as our in-house approach to write modular CSS with easily maintainable and scalable stylesheets, we have a very opinionated picture of what our CSS should look like. Therefore, we decided to use a zweitag-wide configuration and deviate from the standard rules. The configuration provided in this repository helps on the one hand to write better CSS and on the other hand to fulfil parts of the goals and guidelines of Zasaf.

[The stylelint documentation](https://stylelint.io/user-guide/configure) is very good and explains each rule (and a lot more) in detail.

# Our zweitag config

The commonly usable config file is located [here](/stylelint/index.js) in this repository.

It is based on some simple principles:
1. **Exceptions should be justified and documented (in a comment).** You don't want to ask yourself in a month if it wouldn't be better to remove the exception and so on.
1. **Exceptions should be as small as possible**, meaning that if you have to turn off a rule because it makes sense for files in `stylesheets/globals` for example, just disable it for this directory, not globally!

## Using the zweitag config

Projects which are generated from our rails template repository should automatically use this config. The zweitag stylelint configuration is available as a package in the [npm package-registry](tbd). If you want to use it in an existing project (please do), add the package as node module:

```sh
yarn add --dev @zweitag/stylelint-config
or
npm install --save-dev @zweitag/stylelint-config
```

Additionaly you need a `.stylelintrc.json` where you extend our global configuration:
```json
{
  "extends": "@zweitag/stylelint-config"
}
```

### Adapting the configuration to your project and handling edge cases
Situations will arise where you have to deactivate stylelint rules for certain cases. This can be done with the help of the comment ignore syntax, but ensure to disable only the specific rules:
```js
// stylelint-disable-next-line [rules] -- comment
```
or
```js
// stylelint-disable-line [rules] -- comment
```
or
```js
// stylelint-disable [rules] -- comment
.block {
  width: 100px;
}
// stylelint-enable [rules]
```
There is a more detailed documentation on the [stylelint docs](https://stylelint.io/user-guide/ignore-code) available.

In some cases, some rules must also be overriden or deactivated project-wide. To do this, you can simply override a rule in your `.stylelintrc.json`. If it makes sense to adapt the rule for all projects, you are welcome to create a pull request for the central configuration in this repository.

If you just want to ignore some specific files, you can create a `.stylelintignore` including the common globs-patterns for the files to be ignored.

## How do I migrate an existing project?
As you are migrating an existing project, there is a `--fix` option, auto-correcting simple errors and code smells. In case you don't want to migrate the whole project at once, you can use the [comment ignore syntax](#Adapting-the-configuration-to-your-project-and-handling-edge-cases) or the `.stylelintignore` to handle larger code smells when there is time and budget.

# Adjusting the central config

If you feel that a rule that is currently enabled/disabled should be changed in the shared config
* it doesn't make sense in our circumstances (like enforcing documentation which we usually don't)
* or it does make absolutely no sense whatsoever
* ...

please feel free to discuss the rule
* in the office
* during hack teams
* on slack
* in a github issue or a github pull request
* ...

and eventually create a pull request that does the following:
* enables/disables the rule(s) or adds exceptions regarding files in the config file
* adds a comment directly beside or beneath the exception explaining why it exists
* probably links some more resources or reasons for the decision (e.g. a slack conversation) on the pull request (not in the config)

---

Last but not least, feel free to also discuss and adjust this readme.
