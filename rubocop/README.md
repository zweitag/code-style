# Rubocop

## Summary

[Rubocop](https://github.com/rubocop-hq/rubocop) is an open source ruby gem for linting ruby code. Rules are also called cops. While ruby is a very free and forgiving language, Rubocop has various cops concerned with styling and consistency to guide a way. But at least as important are the cops concerned with writing clean, working code.

## Details
Many pitfalls you could run into are prohibited by a cop. Like [forgetting to put a variable when interpolating a string](https://docs.rubocop.org/rubocop/cops_lint.html#lintemptyinterpolation) or unintentionally using [YAML.load instead of YAML.safe_load](https://docs.rubocop.org/rubocop/cops_security.html#securityyamlload).

There are several plugins like
* [rubocop-performance](https://github.com/rubocop-hq/rubocop-performance)
* [rubocop-rails](https://github.com/rubocop-hq/rubocop-rails)
* [rubocop-rspec](https://github.com/rubocop-hq/rubocop-rspec)

which add additional rulesets concerned with the described topic.

[The documentation](https://docs.rubocop.org/rubocop/index.html) is very good and explains each cop (and a lot more) in detail.

# Our Zweitag config

The commonly usable config file is located [here](rubocop/.rubocop.yml) in this repository.

It is based on some simple principles:
1. **It should be compatible with [RuFo](https://github.com/ruby-formatter/rufo)** which we use for quick code formatting and very few neccessary style-decisions. Hence some cops are disabled.
1. Use the cops which are enabled by rubocop by default.
1. Use new cops introduced by new versions of rubocop.
1. **Exceptions should be justified and documented (in a comment).** You don't want to ask yourself in a month if it wouldn't be better to remove the exception and so on.
1. **Exceptions should be as small as possible**, meaning that if you have to turn off a rule because it makes sense for files in `db/migrate` for example, just disable it for this directory, not globally!
1. **Exceptions should be added in a structured way**:
(RuFo-) compatibilities and other justified exceptions in separate blocks. Inside of the blocks, sort the rules alphabetically and keep empty lines between namespaces to ease navigation.

## Using the Zweitag config

Projects which are generated from our rails template repository should automatically use this config. If you want to use it in an existing project (please do), add the following lines to the top of your project specific `.rubocop.yml`:
```
inherit_from:
  - https://raw.githubusercontent.com/zweitag/code-style/main/rubocop/.rubocop.yml
```
probably above other potential imports.

Since the remote file will be cached locally you can still run rubocop offline. On the other hand, you probably want to add the file or something more general like
```
# Ignore cached rubocop files
.rubocop-http*
```
to your project's `.gitignore`.

### Overwriting rules specifically for your project

Rubocop will use all rules from our shared config and override with rules set in config files imported later or directly written into your project's `.rubocop.yml`. More details on inheritance can be found in the
[rubocop documentation](https://docs.rubocop.org/rubocop/configuration.html#inheritance).

To overwrite arrays, the [inherit_mode](https://docs.rubocop.org/rubocop/configuration.html#merging-arrays-using-inherit_mode) directive should be used. This will merge the corresponding values instead of overwriting them. This is practical if, for example, you want to exclude another file without overriding (or having to repeat) centrally made exclusions:

```
inherit_mode:
  merge:
    - Exclude

AllCops:
  Exclude:
    - file.rb
```

Since rules can be overwritten you can still have project specific settings and are not forced to use exactly the configuration from this repository. But do so with care. When you enable/disable additional rules for your project, always ask yourself:
1. Is this really neccessary?
2. If so, shouldn't we all use this setting, i.e. move it from your project's config to the shared one living here?
3. If not, go to 1.

Ideally your .rubocop.yml should always be empty, except the inheritance statement.

## How do I migrate an existing project?

After following the instructions above you will most likely have lots of offenses against the new rules. Do not despair! Rubocop has a solution for this:
[Automatically generated ToDo configs](https://docs.rubocop.org/rubocop/configuration.html#automatically-generated-configuration).

By running `rubocop --auto-gen-config`, rubocop generates a new file `.rubocop_todo.yml` where all rules are disabled which your code currently violates. ***Note**: You might have to adjust your `.rubocop.yml` file because the todo.yml gets added automatically as an inheritence which sometimes crashes with manually added ancestor files like our shared config!*

You can check this file in and postpone resolving the conflicts one by one when there is time, budget and patience.

Your goal, anyway, should be removing the rubocop_todo.yml asap.

To tick off your todo list, just remove an exception from the rubocop_todo config, maybe run `rubocop -a` (or `rubocop -A`) and inspect the offending files on your own. If you don't know exactly what a cop does, you can look them up [in the documentation](https://docs.rubocop.org/rubocop/cops.html).
You might want to fix the offenses in multiple PRs to make them easier to review and revert.

This way you should either get rid of all exceptions or come to the conclusion that a cop does not fit our needs and that an exception should be added to the shared config here.
If you find that a rule is sensible but you also think a violation is justified at some point you can [disable rules in your code by a comment](https://docs.rubocop.org/rubocop/configuration.html#disabling-cops-within-source-code) (even inline comments since newer rubocop version).

# Adjusting the central config

If you feel that a rule that is currently enabled/disabled should be changed in the shared config
* because it collides with other linters or formatters (rufo for example)
* or it doesn't make sense in our circumstances (like enforcing documentation which we usually don't)
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
