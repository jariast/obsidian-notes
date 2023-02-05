# Code Snippet Auto-complete
I was having a really odd issue with the code snippets e.g `clog` `clg`, they were not showing up in occasions and other times they will fail to show up at all.

After disabling a bunch of extensions without luck, I decide to reinstall VS Code. On Mac, after you delete the App from the Applications folder, and follow [these instructions](https://code.visualstudio.com/docs/setup/uninstall), I only deleted the `Code` folder inside App Support. It's of note that the `$HOME` directory is located in `Users/juanarias`.

Deleting only the above folder, means that we only deleted the user settings, but kept all the Extensions, after reinstalling VS Code, the Auto-Complete was working again, which points to an User Settings issue and not an Extension issue.