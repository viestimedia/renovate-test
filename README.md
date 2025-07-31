# renovate-test

**Update**

So it turns out that the GitHub app does NOT automatically get access to a
repository's private packages. [See this discussion](https://github.com/renovatebot/renovate/discussions/37232)
You need to create a Personal Access Token (PAT) in GitHub and add that as
a secret to Renovate and then add a `hostRules` configuration to `renovate.json`.
This repository is now an example a working setup of that.

In addition to the settings in this repository you need to create a
Personal Access Token in GitHub and [add that token as a secret in Renovate](https://docs.renovatebot.com/mend-hosted/credentials/).

**Original**

This repository demonstrates a problem with the Mend Renovate GitHub App.

The documentation for Renovate states that you do not need to add any
GitHub tokens when using the GitHub App.

This project demonstrates that with a minimal Node.js project and Renovate
using only the basic configurations, Renovate is unable to access private
packages.

In the package.json of this project, there are two packages: one private
and one public. The public package is updated often, which results in a
Renovate PR where we can see the error about the other package, the private
package, that Renovate does not have access to.

Renovate manages to create a PR with the update for the public package, but
the lock file in that PR is invalid because Renovate was unable to check the
dependencies of the private package.

This project includes a GitHub Action that runs `npm ci`, which fails
because of the invalid lock file. This simulates the standard practice
of running PR checks using `npm ci` and then building and testing the code.
