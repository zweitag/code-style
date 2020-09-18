# Purpose

This repository contains linter configs commonly used throughout our organization and for various projects.

## Why bother about code style?
The reasoning behind this is that it has many advantages to have a company-wide consistent code style:

* You spend less time wondering about how to write your code and can spend more time thinking about what you are writing
* You argue less about code style and more about important topics when reviewing code
* You are less likely to stumble upon unusual constructs, because you have likely used them yourself when reading code written by another author

Having strict guidelines moves the discussions about code style away from the daily business and improves efficiency. Nevertheless these rules have to be decided upon and – in our case – discussed by the affected developers before doing so.

## Why using linters/formatters?
Linters simply help to enforce those rules we decided to be sensible and useful. We recommend integrating them in CI/CD checks and your editor/IDE where possible!

# Mindset

Regardless of the benefits mentioned above you will still have to deal with deciding which linters to use (and why) and which rules you want to enable if the linter is configurable (and why).

A practice we want to try out currently is being less protective of styles we are just used to. Many linters and formatters update their ruleset regularly and often decide whether the rule should be enabled by default.

Whenever possible you should think about just using this default. It is more likely to reappear in other (for example open source) projects than your own customized style and makes it easier to comply.

Additionally, special rules usually mean extra lines in your configuration files, hence more effort to keep things up to date and things to worry about like structure and straightforwardness.
So try to keep the configuration as simple as possible.

# Structure

The repository root should – this readme aside – only contain sub directories for every linter or formatter for which we want a organization wide configuration.

Inside each sub directory, please include a README.md describing what this directory is and *how it can be used*. Consider linking related software like the linter itself or any editor plugins that we have confirmed to be useful.
Other than that the sub directories currently do not have any constraints; They could only host a single config file or the source of an own node_module.
If the sub directory hosts source code for a published artifact (for example a node module), please link it and briefly describe prerequisites and setup.

# Contributing

The fact that this repository is public has a few reasons:

* In projects, you might inherit a config file from a central config file living here. It would be ugly to have something like authentifaction guarding the file
* It is easier to access config files, for example for inheritance, from a CI pipeline
* It can be used also for private purposes or by people not related to zweitag

## External contributions
If you are not a member of zweitag you are of course free to use our configurations. But note that

* they might change
*  we determined the rulesets in internal discussions and *might not be open for externally requested changes*

You may of course open issues or pull requests, but please don't be disappointed if they get rejected.

## Internal contributions
If you are a member of zweitag feel free to open PRs and discuss certain decisions. If you think we reached a consensus (like, there are more people agreeing than actively disagreeing), please merge your PR.
