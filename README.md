# OpenSource

[Vale](https://vale.sh) styles for an open-source project's community files.

`Readme` checks a README against the
[`standard-readme`](https://github.com/RichardLitt/standard-readme) spec: a
title, a one-line description, the required sections in order, and an
install command a reader can copy. `Contributing` checks that a contributing
guide tells a newcomer what they need: how to set up the project, how to run
the tests, how to submit a change, where the code of conduct is, and where
to start. `Welcoming` reads both, for words that make a newcomer feel shut
out.

Each style also looks for the way its file usually goes wrong. A README
turns into a manual, with an Install or Usage section that runs for pages
and a table of every flag. A contributing guide lists rules and never says
how to begin.

Works on [Markdown](https://docs.vale.sh/formats/markdown) files named
`README.md` and `CONTRIBUTING.md`.

## Install

Requires Vale 3.23.0 or later. OpenSource builds on
[Std](https://github.com/vale-cli/Std), the standard library its
`Gendered` rule extends. Sync pulls Std in, and it stays present without
being enabled.

```ini
StylesPath = styles
Packages = https://github.com/jdkato/opensource/releases/latest/download/OpenSource.zip
```

```console
$ vale sync
```

To pin a version, use a release URL instead:
`https://github.com/jdkato/opensource/releases/download/v0.1.0/OpenSource.zip`.

Vale doesn't know which kind of file it is reading, so the package's config
chooses a style by file name, wherever the file is:

```ini
[**/README.md]
BasedOnStyles = Readme, Welcoming

[**/CONTRIBUTING.md]
BasedOnStyles = Contributing, Welcoming
```

Nothing needs to be repeated in your own config. A `[*.md]` section of yours
still applies to these files too.

| Style | Reads | What it checks |
| ----- | ----- | -------------- |
| `Readme` | `README.md` | The checkable parts of the `standard-readme` spec, and a README that is turning into a manual. |
| `Contributing` | `CONTRIBUTING.md` | What a contributing guide tells a newcomer, and setup written as numbered steps. |
| `Welcoming` | both | Words that call a step easy, gendered terms, and phrasing that blames the reader. |

## Rules

| Style | Rule | Flags | Level |
| ----- | ---- | ----- | ----- |
| `Readme` | `Title` | a first heading that isn't level 1 | warning |
| | `Description` | a section heading straight after the title and badges | warning |
| | `DescriptionLength` | a description whose first sentence runs to 120 characters | warning |
| | `Install` | no Install section | warning |
| | `Usage` | no Usage section | warning |
| | `Contributing` | no Contributing section | warning |
| | `License` | no License section | warning |
| | `Order` | Install, Usage, and Contributing out of order | warning |
| | `LicenseLast` | a section after License | warning |
| | `InstallCode` | an Install section with no code block and no link | warning |
| | `LongSection` | an Install or Usage section of more than 600 words | suggestion |
| | `OptionTable` | more than six table rows of command-line flags | suggestion |
| `Contributing` | `Setup` | nothing on setting up the project | warning |
| | `Tests` | nothing on running the tests | warning |
| | `PullRequest` | nothing on submitting a change | warning |
| | `CodeOfConduct` | no link to a code of conduct | warning |
| | `FirstStep` | nothing on where a newcomer can start | suggestion |
| | `Steps` | a setup section with no numbered list and no link | suggestion |
| | `Imperative` | `You should install Go.` in a numbered step | suggestion |
| `Welcoming` | `Dismissive` | `simply`, `obviously`, `of course`, `everyone knows`, `just run`, `it's easy` | suggestion |
| | `Gendered` | `guys`, `you guys`, and Std's gendered terms | suggestion |
| | `Blame` | `RTFM`, `as already stated`, `will be closed without comment`, `low-effort PRs` | suggestion |

Every rule file starts with a comment that says what it checks, and links to
the section of the guidance it follows. Structure and presence are warnings,
since the sources require them. The heuristics and the `Welcoming` rules are
suggestions, because only the writer can say whether the alert applies.

Section names are matched leniently. Installation, Getting started, Quick
start, Setup, and Building count as Install. Examples, How to use, Getting
started, Configuration, and Documentation count as Usage. Contribute and
Development count as Contributing, and Licence, Copyright, and Terms of use
as License. A heading can start with an emoji. `Order` reads headings at the
top level the sections appear at, and skips fenced code.

A footer of links or badges below the License section is fine; only another
heading is flagged. `Dismissive` leaves a word in quotes alone, along with
the senses that aren't dismissive: `just as`, `just now`, `easy to read`,
`will simply be`.

## Configuration

Levels and limits are settings, so you can change them without editing the
rule:

```ini
[**/README.md]
BasedOnStyles = Readme, Welcoming
Readme.LongSection[condition] = "> 1000"
Readme.Usage = NO
Welcoming.Dismissive = NO
```

A documentation repository has no code to install, and the spec makes
Install and Usage optional for one; turn those two rules off.

## What it does not check

Whether the title matches the package name, whether the description
matches the package manager's, broken links, whether a table of contents
covers every section, and whether the License section names an SPDX
identifier. Section presence reads headings, so a README that installs in
a paragraph with no heading is reported as missing one. `Order` doesn't
place the optional sections, and a heading Vale doesn't recognize is
skipped.

`Contributing` checks that each topic comes up, not that it is explained
well. A guide that says "run the tests" without the command passes.

## Sources

- The [`standard-readme` specification](https://github.com/RichardLitt/standard-readme/blob/main/spec.md)
  (MIT): every `Readme` rule except `LongSection` and `OptionTable`.
- The Good Docs Project's
  [templates](https://gitlab.com/tgdp/templates) (MIT No Attribution): the
  README guide's
  [best practices](https://gitlab.com/tgdp/templates/-/blob/main/readme/guide_readme.md#readme-best-practices)
  for `LongSection` and `OptionTable`, and its
  [instructions](https://gitlab.com/tgdp/templates/-/blob/main/readme/guide_readme.md#about-the-instructions-for-using-project-section)
  for `Imperative`; the contributing guide's
  [ground rules](https://gitlab.com/tgdp/templates/-/blob/main/contributing-guide/guide_contributing-guide.md#about-the-ground-rules-section),
  [environment setup](https://gitlab.com/tgdp/templates/-/blob/main/contributing-guide/guide_contributing-guide.md#about-the-environment-setup-section),
  and [contribution workflow](https://gitlab.com/tgdp/templates/-/blob/main/contributing-guide/guide_contributing-guide.md#about-the-contribution-workflow-section)
  for `CodeOfConduct`, `Steps`, and `PullRequest`.
- The [Open Source Guides](https://opensource.guide):
  [Writing your contributing guidelines](https://opensource.guide/starting-a-project/#writing-your-contributing-guidelines)
  for `Setup` and `Tests`;
  [How you write affects your brand](https://opensource.guide/starting-a-project/#how-you-write-and-code-affects-your-brand-too)
  for `Dismissive` and `Gendered`; and
  [Make people feel welcome](https://opensource.guide/building-community/#make-people-feel-welcome)
  for `FirstStep` and `Blame`. Content based on
  [github.com/github/opensource.guide](https://github.com/github/opensource.guide)
  used under the [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/)
  license.

The messages are this package's own words. The thresholds, 600 words for
`LongSection` and six rows for `OptionTable`, are this package's; the
sources ask for a short README but name no number.

## Development

`./test.sh` runs each rule's own cases with `vale test --coverage`, then
checks the READMEs and contributing guides under `fixtures/` against the
golden files in `testdata/`, and requires their rewrites in
`fixtures/clean/` to pass clean. Each fixture sits in its own directory
under its real name, since the config picks a style by file name, and some
rules need a file of their own: a README with no Install section can't also
have one with no code block. `./test.sh -u` rewrites the golden files. The
script expects a Std checkout beside this repository, or `STD` pointing at
its `Std` directory.

## License

MIT; see [LICENSE](LICENSE).
