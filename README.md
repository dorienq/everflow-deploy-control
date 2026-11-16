# EverFlow deployment control

This public repository is the reviewer-gated deployment boundary for the private
`dorienq/everflow-automations` application.

A release request is a tag matching `release-*`. The tag commit contains a
`release.json` file with the tested image, source commit, and source workflow
run. The `preflight` job validates those fields and fails closed unless the
`production-approval` environment has at least one required reviewer and
administrator bypass is disabled. The `deploy` job then waits for approval
before deploying the prebuilt image with Fly.

This repository contains no application source, customer data, or deploy token
in version control. The Fly token is stored only as a repository secret. The
release request copies the tested `fly.toml` from the private release commit so
the deployment keeps the production volume, HTTP service, and machine settings
in sync with the application release.
