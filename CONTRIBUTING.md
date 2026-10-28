# Contributing

Use [repository issues](https://github.com/gcfernando/python-projects-and-examples/issues) for reproducible problems and focused suggestions. Check existing reports first. Use [private security reporting](SECURITY.md) for vulnerabilities.

## Before making a change

Read the [project overview](README.md), [documentation index](documentation.md) and [repository standards](REPOSITORY_STANDARDS.md). Keep changes focused and preserve attribution, prerequisites, supported versions and existing public links.

## Project-specific validation

Follow the selected example's guide and install dependencies in an isolated environment. State the Python version, platform and required services or hardware. Run tools only against systems and data you are authorized to use. There is no shared dependency set for every example.

## Documentation and repository checks

Use UTF-8, LF line endings and a final newline for repository metadata. Use one level-one title, hierarchical headings, fenced code blocks with a language where useful and blank lines around headings and lists. Preserve two-space Markdown hard breaks and stable anchors. Match relative link paths exactly, including case.

Run `python .github/scripts/check_repository.py` with Python 3.12 or later from the repository root, then run the existing checks relevant to the changed project. Review rendered Markdown and any published-page changes. Report checks actually performed and remaining limitations.

## Pull requests

Describe the concrete problem and resulting behavior, affected files, relevant versions and validation. Explain configuration, dependency, compatibility or licensing changes. Do not include credentials, private data or generated build output.
