[Python projects](../../README.md)

<a id="historical-workflow-configuration"></a>

# Archived Audio8D Workflow — History and Current Project

The archived `audio8d-release.yml` records the release configuration for the former `8D/` application in this examples repository.

> **In this guide:** [Understand the details](#guide-understand-the-archive) · [Check the limits](#guide-plan-a-replacement-deliberately) · [Find the current project](#guide-find-the-current-project)

<a id="guide-find-the-current-project"></a>

## Find the current project

Audio8D now lives in the [8D audio converter repository](https://github.com/gcfernando/8d-audio-converter). Its [application guide](https://github.com/gcfernando/8d-audio-converter#readme) describes current source setup and packaging.

<a id="guide-understand-the-archive"></a>

## Understand the archive

The original workflow is preserved byte-for-byte here. Its old `8D/` working directory is no longer present in this repository. GitHub discovers active workflow files directly under `.github/workflows/`, so this historical copy cannot be dispatched or triggered by a tag.

<a id="guide-plan-a-replacement-deliberately"></a>

## Plan a replacement deliberately

Review the current Audio8D packaging guide before creating a replacement workflow. The archive is historical evidence, not a supported release entry point.
