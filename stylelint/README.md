# Stylelint
## Summary

[Stylelint](https://stylelint.io/) is a mighty, modern linter that helps you avoid errors and enforce conventions in your styles.
## Details

[The documentation](https://stylelint.io/user-guide/configure) is very good and explains each rule (and a lot more) in detail.

# Our zweitag config

The commonly usable config file is located [here](/stylelint/index.js) in this repository.

It is based on some simple principles:
1. **Exceptions should be justified and documented (in a comment).** You don't want to ask yourself in a month if it wouldn't be better to remove the exception and so on.
1. **Exceptions should be as small as possible**, meaning that if you have to turn off a rule because it makes sense for files in `stylesheets/globals` for example, just disable it for this directory, not globally!

## Using the zweitag config

Projects which are generated from our rails template repository should automatically use this config. If you want to use it in an existing project (please do), add the package as node module:

```sh
yarn add --dev zweitag-stylelint-config
npm install --save-dev zweitag-stylelint-config
```

### Overwriting rules specifically for your project


## How do I migrate an existing project?

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
* enables/disables the cop(s) or adds exceptions regarding files in the config file
* adds a comment directly beside or beneath the exception explaining why it exists
* probably links some more resources or reasons for the decision (e.g. a slack conversation) on the pull request (not in the config)

---

Last but not least, feel free to also discuss and adjust this readme.
