# Workflow


Follow git flow methodology.

## Branches

develop   - The main branch that features get merged into
feature/* - Branch from develop merge back into develop
release/* - Branch from develop, apply fixes until releaseable
hotfix/*  - Branch from master, merge into master and develop
master    - Stable codebase, merge release in

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


## Deployments

staging - when a commit is made to develop, deploy automatically
  build image with tag dev-git_hash-timestamp

pre-release - when a release is created/updated, deploy automatically
  build the release with tag semver 0.x.0-rc.1?

production - when merge request is approved, deploy automatically
  tag the release image with semver 0.x.0

