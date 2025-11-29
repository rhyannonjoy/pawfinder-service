---
layout: page
title: Contribution Guide
permalink: /docs/overview/contribution-guide/
---

## Contribution guide

Documentation improvements are always welcome. Contributions
must benefit PawFinder users. Create
[an issue](https://github.com/rhyannonjoy/pawfinder-service/issues) and or
make [a pull request](https://github.com/rhyannonjoy/pawfinder-service/pulls).

### Pull request tips

1. Fork this repository to a personal [GitHub](https://github.com) account.
2. Build a local copy of the documentation from the fork.
3. Install [Vale](https://vale.sh/) in the development environment.
4. If using [VS Code](https://code.visualstudio.com/download),
install extensions [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint) and
[Vale VS Code](https://marketplace.visualstudio.com/items?itemName=ChrisChinchilla.vale-vscode).
5. Test all changes locally before submitting a pull request.
6. Pull requests must not require more content to function.
7. Ideally, pull requests should address an existing issue,
but this isn't required.
8. Don't submit pull requests with lint or Vale errors in
the content or code examples.

### Troubleshooting

**Documentation build fails locally**\
Revisit the [Tutorial Requirements](tutorial-requirements.md).
Make sure all software requirements installed correctly. For
example, ensure [Node.js](https://nodejs.org/en/download)
and [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)
are up to date. Run `npm install` in the fork directory,
then attempt the build again. If using [json-server](https://www.npmjs.com/package/json-server), ensure the version is at least 0.17.4.

**Vale or markdownlint extensions don't appear in VS Code**\
Install the extensions from [the Visual Studio Code marketplace](https://marketplace.visualstudio.com/VSCode). Reload the VS Code window
(`Ctrl+R` on Windows/Linux, `Cmd+R` on Mac) after installation.

**Vale reports errors but the content appears correct**\
Check the `.vale.ini` configuration file in the repository root.
Use `vale .` to run Vale from the command line and observe
detailed error output.

**Pull request marked as having lint errors**\
Run `npm run lint` locally to identify errors before submission. Most formatting issues can be auto-fixed with `npm run lint:fix`.

**Changes don't appear after pushing to GitHub**\
GitHub Pages can take a few minutes to rebuild and deploy.
Wait a few minutes, then refresh the site. Clear the browser cache
(`Ctrl+Shift+Delete` on Windows/Linux,`Cmd+Shift+Delete on Mac`)
if changes still don't appear.

### Related topics

- [Tutorial Requirements](tutorial-requirements.md)
- [Authentication Guide](authentication-guide.md)
- [Quickstart Guide](quickstart-guide.md)
- [API Index](../api-reference/api-index.md)
