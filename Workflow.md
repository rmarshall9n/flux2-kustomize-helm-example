# Workflow


Follow git flow methodology.

## Branches

develop   - The main branch that features get merged into
feature/* - Branch from develop merge back into develop
release/* - Branch from develop, apply fixes until releaseable
hotfix/*  - Branch from master, merge into master and develop
master    - Stable codebase, merge release in

## Environments

staging - most recent changes on develop branch
pre-release - release branch for testing
production - most stable code from master

## Flow

1. Start new feature/* from develop
1. When feature is finished, merge back into develop
1. Continue adding features until ready to cut a release
1. Create release/* from develop
1. Continue adding commits until stable
1. Merge release/* into master
1. If a fix is required, create hotfix/* from master
1. Merge the fix back into master and into develop

## Pipelines

feature/*
  - All feature branches run QA process
  - Should merge develop before running tests
  - Should not merge into develop if not up to date with develop
  - Should not merge if missing reviews
  - Requires re-review if new changes are pushed since last review
  - Should merge automatically if everything passes

develop - Run non-critical/slow processes

release/*
  - All release branches run QA process
  - Run non-critical/slow processes
  - Should merge master before running tests
  - Should not merge into master if not up to date with master
  - Should not merge if missing reviews
  - Requires re-review if new changes are pushed since last review
  - Should merge automatically if everything passes

hotfix/*
  - All hotfix branches run QA process
  - Run non-critical/slow processes?
  - Should merge master before running tests
  - Should not merge into master if not up to date with master
  - Should not merge if missing reviews
  - Requires re-review if new changes are pushed since last review
  - Should merge automatically into master if everything passes
  - Should create feature branch/MR to merge into develop

master
  - When merged, notify about release
  - When merged, build charts

## Deployments

staging - when a commit is made to develop, deploy automatically
  build image with tag dev-git_hash-timestamp

pre-release - when a release is created/updated, deploy automatically
  build the release with tag semver 0.x.0-rc.1?

production - when merge request is approved, deploy automatically
  tag the release image with semver 0.x.0




