## Anteater - CI / CD Gate Check Framework

Anteater is an open framework to prevent the unwanted merging of
nominated strings, filenames, binaries, depreciated functions, staging
enviroment code / credentials etc. Anything that can be specified with
regular expression syntax, can be sniffed out by anteater.

You tell anteater exactly what you don't want to get merged, and
anteater looks after the rest.

Any false positives are easily negated by using the same RegExp
framework to cancel out the false match.

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

```yaml
apprun:
  regex: app\.run\s*\(.*debug.*=.*True.*\)
  desc: "Running flask in debug mode could potentially leak sensitive data"
```

Anteater also works with filenames:

For Example:

```bash
jenkins\.plugins\.publish_over_ssh\.BapSshPublisherPlugin\.xml``
```

Or even..

```bash
- \.pypirc
- \.gem\/credentials
- aws_access_key_id
- aws_secret_access_key
- LocalSettings\.php
```

If any binaries are found, IP address (public) and URLs, they will be
scanned with the Virus Total API (unless whitelisted by you).

```bash
INFO - Found what I believe is a URL: <script src = "https://coin-hive.com/lib/coinhive.min.js"></script><script>
INFO - Rate limit clear
INFO - Report found, job complete for https://coin-hive.com/lib/coinhive.min.js
ERROR - https://coin-hive.com/lib/coinhive.min.js  is recorded as a malicious site by ADMINUSLabs
ERROR - https://coin-hive.com/lib/coinhive.min.js  recorded as a malware site by Yandex Safebrowsing
ERROR - Full report available here: https://www.virustotal.com/#/url/2a6ae27b9692354ebbb693594f3aca910dc3b0418063c69859bd80bca8a6a8c6/detection
```

Why RegExp and not AI / Machine Learning / Blockchain etc
---------------------------------------------------------

The fact is that near on everyone knows regular expressions
and if they don't, its not to challenging to learn. Regular
expressions can also be universally applied to all different
languages, scripts, config files etc.

Anteater is not reliant on a project being Java or Python or
any specific language, so its not limited to needing a certain
abstract syntax tree or the compiler of a specific language.

Its made for a DevOps world, where code is in the form of bash
scripts, jinja2, groovy templates, yaml / json files source code
and developers can check in any sort of file type or content.

For a deeper overview, its best to consult the [docs](http://anteater.readthedocs.io/en/latest/)
