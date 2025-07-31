# renovate-test

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
