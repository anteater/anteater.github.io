# Anteater - CI / CD Gate Check Framework

Anteater is an open framework to prevent the unwanted merging of
nominated strings, filenames, binaries, depreciated functions, staging
enviroment code / credentials etc. Anything that can be specified with
regular expression syntax, can be sniffed out by anteater.

You tell anteater exactly what you don't want to get merged, and
anteater looks after the rest.

If anteater finds something, it exits with a non-zero code which in turn
fails the build of your CI tool, with the idea that it would prevent a pull
request merging. Any false positives are easily negated by using the
same RegExp framework to cancel out the false match.

Entire projects may also be scanned also, using a recursive directory
walk.

With a few simple steps it can be easily implemented into a CI / CD
workflow with tooling such as [Travis CI](https://travis-ci.org/),
[CircleCI](https://circleci.com/), [Gitlab CI/CD](https://about.gitlab.com/features/gitlab-ci-cd/)
and [Jenkins](https://jenkins.io/).

All strings are entered into a simple YAML format, making it easy to
maintain your own list or share one with others.

Why would I want to use this?
-----------------------------

Anteater has many uses, and can easily be bent to cover your own
specific needs.

First, as mentioned, it can be set up to block strings and files with a
potential security impact or risk. This could include private keys, a
shell history, aws credentials etc.

It is especially useful at ensuring that elements used in a staging /
development enviroment don't find there way into a production
enviroment.

Let's take a look at some examples:

```
apprun:
  regex: app\.run\s*\(.*debug.*=.*True.*\)
  desc: "Running flask in debug mode could potentially leak sensitive data"
```

Anteater also works with filenames:

For Example:

``jenkins\.plugins\.publish_over_ssh\.BapSshPublisherPlugin\.xml``

Or even..

```
- \.pypirc
- \.gem\/credentials
- aws_access_key_id
- aws_secret_access_key
- LocalSettings\.php
```

If any binaries are found, IP address (public) and URLs, they will be
scanned with the Virus Total API (unless whitelisted by you).

For a deeper overview, its best to consult the [docs](http://anteater.readthedocs.io/en/latest/)

