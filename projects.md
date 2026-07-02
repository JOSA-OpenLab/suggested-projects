# A list of suggested Python-first OSS Projects

This is a working evaluation of the Python projects pulled from the [awesome-for-beginners](https://github.com/mungell/awesome-for-beginners) list, narrowed down to the ones actually might be worth your time. I dropped any projects projects that turned out to be maintenance-mode ghost towns and kept the rest.
## What I found, in general

Beginner labels are a mess across the ecosystem as there's no standard. You'll see "good first issue" most often, but also "Easy-to-Fix" (SymPy), "level:starter" (wemake-python-styleguide), "help wanted" (opsdroid, scikit-learn), "first-contribution" (matplotlib), and "easy-pick" (Kinto). scikit-learn is the interesting outlier here: its maintainers told a contributor in a GitHub discussion that they deliberately avoid the "good first issue" label because beginner-looking issues at that scale tend to turn out more complicated than they look.

Review speed is where most of the friction lives, especially on the big scientific libraries. pandas says so directly in its own docs: a small group of people reviews everything, and that creates bottlenecks. scikit-learn requires two core developers to sign off before anything merges. ArviZ, by contrast, is small enough that its median PR turnaround is closer to a week.

The clearest differentiator between a good and a mediocre beginner experience isn't the label count, it's whether the project has built actual mentorship infrastructure. Zulip has run GSoC since 2016 and has, by its own account, over 185,000 words of contributor documentation. Oppia is in its eleventh consecutive year as a GSoC org. SymPy has done GSoC every year since 2007. PyMC runs regular office hours on Discourse. These projects treat onboarding as a real, ongoing investment, not an afterthought.

## activist ([activist-org/activist](https://github.com/activist-org/activist))

This is an open-source platform for activism organizing. Think event coordination and resource-sharing for nonprofits and grassroots groups. The stack is Vue/Nuxt with TypeScript and Tailwind on the frontend, Django on the backend, all wrapped in Docker for local dev.

**Contribution guidelines** - [CONTRIBUTING.md](https://github.com/activist-org/activist/blob/main/CONTRIBUTING.md)

The setup uses Docker Compose and there's a documented fallback path if Docker misbehaves on your machine. Issues have no formal assignment process, you just drop a comment saying you're picking something up, which is nice because it removes a round-trip before you can even start.

Community: public Matrix room at `#activist-dev`, Weblate for localization, no Discord. Community-governed, no corporate backer.

## BeeWare Briefcase ([beeware/briefcase](https://github.com/beeware/briefcase))

Briefcase takes a Python project and packages it as a real native app for macOS, Windows, Linux, iOS, Android, even web. Pure Python wrapping platform-specific toolchains (Xcode for iOS, Gradle for Android). Part of the broader BeeWare suite alongside Toga. Around 2,900 stars.

**Contribution guidelines** - [Contributing to Briefcase](https://beeware.org/contributing/guide/)

The contribution guide is split into separate paths for code and docs, which helps if you're not sure where to start. For code: install in editable mode, run tests through tox, expect near-100% line coverage. The piece that catches people off guard is the towncrier change note where every PR needs a small file in `changes/` named `<issue-id>.<type>.rst`, where type is one of feature, bugfix, doc, or removal. It's a minor bureaucratic step but the docs explain it clearly. No formal issue assignment just comment to claim.

**Review culture**

BeeWare has a community-wide reputation for being welcoming to first-timers, and Briefcase specifically maintains a [first-timer advice page](https://beeware.org/contributing/first-time-contributors/?h=first) that's worth reading before you open anything. Russell Keith-Magee (the founder) is still personally active in reviews and tends to leave detailed, patient feedback. Don't be put off if your first PR gets significant revision requests as that's the norm here, not a sign something went wrong. The review tends to be educational about the platform-specific constraints involved, which is genuinely interesting territory.

Community: active [Discord, Mastodon presence. Code of Conduct enforced](https://beeware.org/community/).

## Bokeh ([bokeh/bokeh](https://github.com/bokeh/bokeh))

Interactive data visualization library for th ebrowser. Python backend with BokehJS (TypeScript) running rendering in the browser. Volunteer-run with NumFOCUS support. Around 20,000+ stars.

**Contribution guidelines** - [Developer's Guide](https://docs.bokeh.org/en/latest/docs/dev_guide.html)

Setup is covered in the Developer's Guide and involves installing from source in a conda or virtualenv environment. The project uses pytest, mypy, and ruff, so you'll want those available. Documentation is a documented first entry point, the guide explicitly calls it out as a good starting contribution if you're not ready to dive into the TypeScript rendering internals.

**What new contributors should look for:** Focus early contributions on the Python side rather than BokehJS. TypeScript changes require understanding Bokeh's rendering model, which has a steeper learning curve. Pure Python issues (configuration, server, widgets defined in Python) are more accessible and the review path is faster.

Community: [Bokeh Discourse](https://discourse.bokeh.org/) for general support, [developer-only Slack for active contributors](https://slack-invite.bokeh.org/).

## cookiecutter ([cookiecutter/cookiecutter](https://github.com/cookiecutter/cookiecutter))

The CLI tool that scaffolds new projects from templates. Language-agnostic. The templates target any language, not just Python. Pure Python, around 25K stars, led by Audrey Roy Greenfeld.

**Contribution guidelines** - [CONTRIBUTING.md](https://github.com/cookiecutter/cookiecutter/blob/main/CONTRIBUTING.md)

The contributing docs have an explicit instruction to "be encouraging" baked into reviewer guidance, which sets the tone. The project follows the [PyPA Code of Conduct](https://www.pypa.io/en/latest/code-of-conduct/). Setup is a standard fork-and-clone with tox handling tests. There's no issue-assignment process and no requirement to open an issue before a PR for small changes. Documentation fixes and improvements to the template ecosystem are genuinely fair game to just submit. For larger features, dropping a comment first is good practice.

**What new contributors should look for:** Documentation improvements are the most reliably reviewed contribution type here.

Community: [Discord, Stack Overflow](https://github.com/cookiecutter/cookiecutter#community).

## cookiecutter-django ([cookiecutter/cookiecutter-django](https://github.com/cookiecutter/cookiecutter-django))

A production-ready Django starter template. Bootstrap 5, custom users, Celery and Flower, Docker with Traefik and Let's Encrypt, S3/GCS/Azure storage support. Around 13,500 stars, very active.

**Contribution guidelines** - [CONTRIBUTING.md](https://github.com/cookiecutter/cookiecutter-django/blob/master/CONTRIBUTING.md)

The contributing guide has been modernized to use uv as the package manager, with tox running the test suite underneath. The tests work by actually generating and building sample projects from the template, a clever approach that catches regressions that a normal unit test wouldn't. flake8 handles linting. Issues go through GitHub, not email.

**Review culture**

This project moves fast and the review culture matches. PRs for template tweaks, CI fixes, and documentation tend to get reviewed within a few days. The scope of changes is naturally limited (you're editing a template, not building complex logic) which makes PRs smaller and reviews faster. Don't expect hand-holding on Django basics as the maintainers assume you understand the framework, but they're friendly about template-specific questions.

Community: [Discord, Stack Overflow `cookiecutter-django` tag](https://github.com/cookiecutter/cookiecutter-django#community).

## DocsGPT (arc53/DocsGPT)

An open-source RAG assistant for documentation. Point it at your docs and it answers questions about them. Flask and Celery backend, React/TypeScript frontend, LangChain for retrieval, Dockerized. +18K stars.

**Contribution guidelines** - [CONTRIBUTING.md](https://github.com/arc53/DocsGPT/blob/main/CONTRIBUTING.md)

Standard Contributor Covenant Code of Conduct and CONTRIBUTING.md. The setup is Docker-first but with documented fallbacks for running the Flask backend and React frontend separately. The project has participated in Hacktoberfest, which means the maintainers have real experience handling a rush of first-time contributors.

**Review culture**

The team is active and the release cadence is healthy (v0.18.0 in June 2026). You can choose your lane, python backend (Flask routes, Celery tasks, LangChain integration) or React frontend and contribute to whichever you know better. Reviews come from the core team and tend to be practical and focused on making things work rather than on stylistic nitpicking.

**What new contributors should look for:** Join the [Discord](https://discord.gg/cpuBMp6E) before opening a PR. The maintainers are active there and it's faster to get a "yes this issue is still valid" confirmation in chat than to open a PR and wait for async feedback. Also check if your chosen issue has a related discussion thread on GitHub — some have more context than the issue body alone.

Community: [Discord](https://discord.com/invite/vN7YFfdMpj), GitHub Discussions, and a [maintained blog](https://blog.docsgpt.cloud/).

## fenn ([pyfenn/fenn](https://github.com/pyfenn/fenn))

A framework for ML/DL workflows and LLM agents. Essentially a friendlier wrapper around PyTorch with prebuilt trainers and YAML-based config management. W&B and TensorBoard hooks built in. Around 64 stars but very actively maintained.

**Contribution guidelines** - [GitHub Issues](https://github.com/pyfenn/fenn/issues)

No heavy formal process here, no pre-commit config, no mandatory linter setup, no CLA. The project is young enough that the contribution process is more "talk to the maintainer and send a PR" than a formalized workflow. That's a feature, not a bug, at this stage. MIT licensed.

**Review culture**

This is the fastest feedback loop on the entire list. The maintainer (ApusBerliozi) responds within hours, sometimes within minutes. Because the project is so young, your contribution isn't just merging into a codebase, it's shaping decisions that will matter for months.

Obvious risk: this is a new project with no multi-year track record. Come in with the understanding that it might slow down, and treat it as a low-stakes place to get reps in.

Community: [Discord](https://github.com/pyfenn/fenn#contributing)

## Jupyter Notebook (jupyter/notebook)

The classic Jupyter Notebook interface. JavaScript/TypeScript frontend talking to a Python server (jupyter_server) underneath.

**Contribution guidelines** - [CONTRIBUTING.md](https://github.com/jupyter/notebook/blob/main/CONTRIBUTING.md)

Setup is `pip install -e ".[dev]"` plus a dev-build step for the frontend assets. No formal issue claiming process just comment on an issue. The Jupyter [Code of Conduct](https://docs.jupyter.org/en/latest/community/content-community.html) applies across the whole org.

**Review culture**

Reviews come from a distributed team of maintainers across the Jupyter ecosystem. Response times are reasonable. The broader Jupyter community holds regular contributor calls and has participated in GSoC.

**What new contributors should look for:** Most of the open beginner-friendly work in this specific repo is frontend TypeScript, not Python. If you want Python-flavored issues, look at the [jupyter_server](https://github.com/jupyter-server/jupyter_server/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22) or [IPython](https://github.com/ipython/ipython/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22) repos instead, same review culture, more Python work.

Community: [Jupyter Discourse](https://discourse.jupyter.org/), regular community calls, GSoC org.

## matplotlib ([matplotlib/matplotlib](https://github.com/matplotlib/matplotlib))

The Python plotting library. Nearly every data science workflow touches it at some point. Python core with C/C++ extensions for performance, support for multiple GUI backends. NumFOCUS-affiliated.

**Contribution guidelines** - [Contributing guide](https://matplotlib.org/stable/devel/contributing.html)

PRs target main. Backports to older release branches are handled by maintainers, not contributors. The contributing docs are notably direct about expectations: your first PR doesn't need to be perfect, especially for documentation and examples, reviewers will help you get there. Draft PRs are actively encouraged even before work is complete, because early visibility leads to earlier feedback. Testing uses pytest. Linting uses pre-commit. Docs are built with Sphinx, and doc contributions are explicitly called out as valuable first contributions.

**Review culture**

The project maintains a [private "incubator" Gitter space](https://matplotlib.org/devdocs/devel/contribute.html#new-contributors) specifically for first-time contributors, moderated by core developers. This is unusual and worth using, it's a lower-stakes place to ask questions before they become problems in your PR. A [weekly community meeting](https://scientific-python.org/calendars/) posts public notes and is open to contributors. Reviews tend to be thorough, particularly on changes that affect rendering behavior or backend compatibility. The tone throughout is collaborative rather than gatekeeping.

**What new contributors should look for:** Look for the `first-contribution` label, which is used for issues that are specifically scoped for newcomers. If you're unsure about scope, post a comment on the issue before starting, maintainers are responsive to "is this still valid / is the approach I'm thinking of reasonable?" questions.

Community: [Matplotlib Discourse](https://discourse.matplotlib.org/), Gitter incubator for first-timers.

## OMRChecker ([Udayraj123/OMRChecker](https://github.com/Udayraj123/OMRChecker))

A computer vision tool that grades OMR bubble sheets. The multiple-choice answer sheets you'd scan after an exam. Pure Python built on OpenCV. Explicitly designed as a teaching tool for image processing.

**Contribution guidelines** - [CONTRIBUTING.md](https://github.com/Udayraj123/OMRChecker/blob/master/CONTRIBUTING.md)

More rigorous than most projects this size: Pylint and Black both enforced, a mandatory PR template (incomplete template = PR closed, no warnings). In exchange, you get a curated [Project Ideas List](https://github.com/users/Udayraj123/projects/2/views/1) and issues tagged by actual difficulty (Easy, Medium, Hard) rather than a single catch-all beginner label. The project is GSoC-friendly and the project ideas list is maintained with GSoC students in mind.

**Review culture**

Strict but educational. The maintainer enforces the PR template because it forces contributors to think through their change before submitting. You have to describe what the fix does, how you tested it, and whether it affects the documented behavior. If you skip the template, the PR gets closed and you reopen it properly. This can feel harsh but it means the PRs that do get reviewed are substantive. Reviews teach image-processing concepts, not just Python style.

**What new contributors should look for:** Start with beginner-labeled projects and read the PR template before you write a single line of code. Understand what you're building, why, and how you'll verify it works.

Community: [Discord](https://discord.com/invite/qFv2Vqf).

## OpenMetadata ([open-metadata/OpenMetadata](https://github.com/open-metadata/openmetadata))

A unified metadata and data-governance platform with 130+ connectors to databases, BI tools, and pipelines. Java backend, Python ingestion framework, TypeScript UI. Backed by Collate.

**Contribution guidelines** - [CONTRIBUTING.md](https://github.com/open-metadata/OpenMetadata/blob/main/CONTRIBUTING.md)

One hard requirement that catches people off guard: you must be assigned to an issue before submitting a PR. Comment requesting assignment and wait. If you open a PR without assignment, it gets closed. This is a common first-timer mistake here. Setup uses Docker for the full stack, and there's a documented local-dev guide for just the Python ingestion layer if you don't need the full Java backend running. For UI fixes, they ask for a screen recording showing the fix in action. PRs target main.

**Review culture**

There's a maintainer-pinned issue ([#27444](https://github.com/open-metadata/OpenMetadata/issues/27444), "Interested in good-first-issues? Start here! Don't see a good-first-issue that is unassigned that fits your expertise? Please reach out to me on slack!") that functions as an active onboarding thread, post a comment there or reach out on slack and maintainers will help you find something suitable. That level of hand-holding is unusual for a project this size. Reviews on the Python ingestion side are generally fast, since the Slack #contributors channel keeps things unblocked. Java and TypeScript reviews can take longer.

**What new contributors should look for:** Stay in the Python ingestion layer for your first few contributions. The `ingestion/` directory is self-contained and doesn't require the Java backend to run.

Community: [Slack workspace](https://openmetadata.slack.com/join/shared_invite/zt-408sf2zfn-oa2qF~zl2KsPQaWmg4PwsA#/shared-invite/email), [active blog](https://blog.open-metadata.org/).

## Oppia ([oppia/oppia](https://github.com/oppia/oppia))

A free online learning platform built on Google App Engine. Angular frontend, Python backend. Large codebase. In its eleventh year as a GSoC organization.

**Contribution guidelines** - [Contributing Code to Oppia Guide](https://github.com/oppia/oppia/wiki/Contributing-code-to-Oppia#setting-things-up)

The onboarding process is heavier than most: you'll need to sign a CLA, complete a getting-started guide, fill out a survey, and post an introduction in GitHub Discussions before you get assigned to a starter issue. Two-factor authentication is required on your GitHub account. It's more upfront investment than any other project on this list. The wiki has a dedicated page called ["Solve your first starter issue"](https://github.com/oppia/oppia/wiki/Solve-your-first-starter-issue).

**Review culture**

This is the most mentor-dense review culture on the list. GSoC alumni consistently describe the feedback as detailed, patient, and educational. Reviewers leave comments that explain why something should change, not just that it should. Expect multiple rounds of feedback on a first PR, particularly around Angular testing patterns and the project's own coding conventions. The contributing docs explicitly acknowledge this: "All of this is totally normal!" It's a project that takes longer to get your first contribution merged but invests more in making you a better developer in the process.

**What new contributors should look for:** Read the full getting-started wiki before touching the codebase, the process is enforced and skipping steps doesn't save time, it just means starting over. The [GitHub Discussions board](https://github.com/oppia/oppia/discussions) is active and maintainers respond there.

Community: [GitHub Discussions](https://github.com/oppia/oppia/discussions), [Oppia Community Site](https://www.oppia.org/).

## pandas ([pandas-dev/pandas](https://github.com/pandas-dev/pandas))

The dataframe library. Pure Python core with Cython underneath, NumFOCUS-backed.

**Contribution guidelines** - [Contributing to pandas](https://pandas.pydata.org/docs/development/contributing.html)

Dev setup works through conda (recommended) or pip with a requirements-dev.txt. pre-commit handles linting. PR titles need a type prefix: ENH for enhancement, BUG for bug fix, DOC for documentation. Feature branches off main. Tests-first is strongly encouraged, write a failing test before the fix, not after.

**Review culture**

pandas says this directly in its own documentation: a small group of people reviews everything, and that creates bottlenecks. The advice that follows is worth internalizing: keep PRs small, write tests first, keep CI green, and if your assigned issue goes quiet for about a week, it's fair to ask for it back. When reviews do happen, they tend to be thorough. Expect comments about test coverage, edge cases, and performance implications. Budget patience more than skill. New contributor meetings and a contributor Slack exist precisely because the async PR process is slow.

**What new contributors should look for:** The single most common ask on a beginner PR is "can you also add a test for this", get ahead of it by writing a test alongside your fix. The new [Slack channel](https://pandas.pydata.org/docs/dev/development/community.html#community-slack) is worth joining before you open a PR, not after — it's a good place to sanity-check your approach.

Community: [New-contributor meetings](https://pandas.pydata.org/docs/dev/development/community.html#new-contributor-meeting), [dev mailing list](https://groups.google.com/g/pydata), [contributor Slack](https://pandas.pydata.org/docs/dev/development/community.html#community-slack), sprint events at PyCon.

## PyMC ([pymc-devs/pymc](https://github.com/pymc-devs/pymc))

Probabilistic programming and Bayesian modeling library. Pure Python on PyTensor. NumFOCUS-backed nonprofit. Around 9,000 stars.

**Contribution guidelines** - [CONTRIBUTING.md](https://github.com/pymc-devs/pymc/blob/main/CONTRIBUTING.md)

Open a draft PR on your first commit, don't wait until you think it's done. The CONTRIBUTING.md is explicit about this because early visibility prevents wasted effort. For anything larger than a small fix, propose it in a [GitHub Discussion](https://github.com/pymc-devs/pymc/discussions) or issue first. Sometimes you'll be redirected to the pymc-experimental repo for things that aren't ready to land in core. "If a non-draft PR has no recent activity, it may be reassigned or closed." That's a real warning: don't go quiet on a PR mid-way.

**Review culture**

Reviews are patient, particularly with people who know Python but are new to Bayesian statistics specifically.

**What new contributors should look for:** Start with documentation and example notebook issues, they're the lowest-friction first contribution and the maintainers say so directly. From there, small fixes to distribution implementations are the natural next step. The [GitHub Discussions board](https://github.com/pymc-devs/pymc/discussions) is where the community is most active; post there before opening issues for things that might be questions rather than bugs.

Community: [Discourse (primary)](https://discourse.pymc.io/), [YouTube](https://www.youtube.com/c/PyMCDevelopers), [LinkedIn](https://www.linkedin.com/company/pymc/), [Mastodon](https://bayes.club/@pymc).

## pytest ([pytest-dev/pytest](https://github.com/pytest-dev/pytest))

The testing framework most of the Python world has standardized on, plus a wide ecosystem of plugins. Pure Python, around 14,300 stars, MIT.

**Contribution guidelines** - [Contributing](https://docs.pytest.org/en/stable/contributing.html)

pre-commit for style. Every change needs a changelog fragment: a file named `changelog/<issue-id>.<type>.rst` where type is one of feature, improvement, bugfix, doc, deprecation, breaking, vendor, packaging, contrib, or misc. You also add yourself to AUTHORS. PRs target main. Tests use pytest itself (which is either intuitive or circular depending on your perspective). The process is more structured than most. Changelog fragment required, AUTHORS update required, CI must pass, but the docs explain each step clearly.

**Review culture**

The structured process is a feature of the review culture, not a barrier, it means every PR that comes in is consistently formatted and easy to review. Contributors who have commit rights can merge others' reviewed PRs, which distributes the review load. There's a documented policy for stale issues and PRs so nothing quietly disappears. Reviews tend to be focused on correctness and test coverage rather than style, since pre-commit handles style automatically.

**What new contributors should look for:** The plugin ecosystem (pytest-mock, pytest-asyncio, pytest-cov, etc.) is a good on-ramp: same review culture and process, smaller codebase, narrower scope. If the core repo feels like too much to start, pick a plugin that covers something you already use.

## scrapy ([scrapy/scrapy](https://github.com/scrapy/scrapy))

A high-level web scraping and crawling framework. Pure Python (Twisted with asyncio support). Around 62,000 stars, maintained by Zyte. BSD-3-Clause.

**Contribution guidelines** - [Contributing to Scrapy](https://docs.scrapy.org/en/latest/contributing.html)

The lowest-friction process on this entire list. No issue assignment required. The docs say: "just go ahead and write a patch." No putting your name in code comments. One change per PR. pre-commit and black handle formatting (`tox -e pre-commit`). If there's already an open PR for something you think you can improve, you're explicitly invited to try.

**Review culture**

Pragmatic and fast. Maintainers pick up stalled PRs and encourage the community to do the same, it's not bad form to pick up someone else's abandoned PR. Small, focused patches are preferred, and that preference shows in how reviewers respond: clean and scoped gets faster attention than broad and ambitious. The feedback is practical, focused on whether the change is correct and doesn't break existing behavior.

Community: [Scrapy subreddit](https://www.reddit.com/r/scrapy/), [mailing list](https://groups.google.com/g/scrapy-users), [#scrapy IRC](https://docs.scrapy.org/en/latest/#getting-help), [Stack Overflow](https://stackoverflow.com/tags/scrapy) `scrapy` tag, [Discord](https://discord.com/invite/mv3yErfpvq).

## SymPy (sympy/sympy)

Pure-Python computer algebra system. Symbolic math across many domains, geometry, integrals, statistics, combinatorics, series, control theory, and more. Over 14,700 stars.

**Contribution guidelines** - [CONTRIBUTING.md](https://github.com/sympy/sympy/blob/master/CONTRIBUTING.md)

A bot called sympy-bot auto-tests every incoming PR, which catches regressions before human review. Testing runs through `bin/test` and `bin/doctest`. Style guide is in the [Documentation Style Guide](https://docs.sympy.org/dev/contributing/documentation-style-guide.html). The recommended beginner label is "Easy to Fix", but there's an important caveat from maintainers themselves: many of those labels are stale. If you find one that's been sitting untouched for a long time, comment to ask whether it's still valid before spending time on it.

**Review culture**

SymPy has done Google Summer of Code every year since 2007 and a huge share of the codebase was written by GSoC students. That legacy shows in how the [mailing list](https://groups.google.com/forum/?fromgroups#!forum/sympy) and [Gitter](https://app.gitter.im/#/room/#sympy_sympy:gitter.im) treat newcomers. Genuinely patient and used to walking first-timers through contributions. The feedback is particularly good on mathematical correctness (which is the important dimension here) and the community will push back if an implementation isn't mathematically sound, not just syntactically wrong.

**What new contributors should look for:** Filter for [Easy to Fix issues](https://github.com/sympy/sympy/issues?q=is%3Aopen+is%3Aissue+label%3A%22Easy+to+Fix%22) but check the dates and comment asking if it's still valid before starting. Pick a module you're already comfortable with mathematically. It's much easier to fix a geometry bug if you understand the geometry, not just the Python. The [mailing list](https://groups.google.com/forum/?fromgroups#!forum/sympy) is the best place to introduce yourself before your first PR.

Community: [Google Groups mailing list](https://groups.google.com/g/sympy), [Gitter](https://app.gitte  r.im/#/room/#sympy_sympy:gitter.im), GSoC every year since 2007.

## wemake-python-styleguide (wemake-services/wemake-python-styleguide)

The strictest Python linter. A flake8 plugin (with a ruff companion) that enforces strongly opinionated style rules. Around 2,900 stars, 213+ contributors, poetry-based setup.

**Contribution guidelines** - [CONTRIBUTING.md](https://github.com/wemake-services/wemake-python-styleguide/blob/master/CONTRIBUTING.md)

Poetry manages the environment. pre-commit is supported. The project uses Hacktoberfest annually, so the maintainer has experience handling first-time contributors.

**Review culture**

The maintainer (sobolevn) is personally active and fast to respond, and has very clear opinions about code quality which makes reviews educational in a distinctive way. You'll learn not just Python style but the reasoning behind specific linter rules, which is worth something as a developer. Reviews are opinionated but not dismissive. Version 1.6.2 shipped April 27, 2026.

**What new contributors should look for:** Adding a new linter rule is the most common first contribution, each rule is self-contained (its own file, its own tests), so the scope is naturally bounded. Read a couple of existing rule implementations before proposing a new one to understand the expected structure. Everything happens on GitHub; no Discord or Slack.

Community: GitHub-centric. No chat outside of GitHub issues.

## Zulip ([zulip/zulip]())

Open-source team chat, a self-hosted Slack alternative with threaded conversations. Django backend, web frontend mid-migration from JavaScript to TypeScript, Flutter mobile, Electron desktop. Apache-2.0.

**Contribution guidelines** - [Zulip Contributor Guide](https://zulip.readthedocs.io/en/latest/contributing/contributing.html)

Zulip's own contributing docs claim over 185,000 words of contributor documentation, and they mean it as a requirement, not a brag that you're expected to read it. The project has its own Git workflow built around rebasing (no merge commits ever), which takes getting used to but is explained in detail. There's an explicit AI-use policy: no unreviewed AI-generated code, communicate with intention. Issues are claimed through a bot called zulipbot.

**Review culture**

Reviews come from senior, experienced engineers and are iterative. Your first PR will likely go through several rounds, even for something small. That's intentional. Reviewers leave detailed explanations and the community at large (on [chat.zulip.org](https://chat.zulip.org)) is available to help between rounds. There are specific streams for new members (`#new members`), git help (`#git help`), environment setup (`#provision help`), and code review (`#code review`). Join all four.

**What new contributors should look for:** Read the full contribution guide before touching the codebase. Seriously. Projects this size sometimes have guides you can skim; Zulip's is one you actually need. The [chat.zulip.org](https://chat.zulip.org) server is the community's own Zulip instance, joining it is a prerequisite to being an effective contributor because that's where real-time conversation happens.

Zulip has been a GSoC org since 2016 with 10 to 20 students per summer, 900 commits merged by the 2025 cohort. Also ran Outreachy and Google Code-In historically. The upfront time investment is real; so is the return on it.

Community: [chat.zulip.org](https://chat.zulip.org) (streams: #new members, #git help, #provision help, #code review), GSoC since 2016.
