# Mitochondrium

Includes Patches from:
- https://github.com/SparklyPower/SparklyPaper/


## Building

**Applying Patches**
```bash
./gradlew applyPatches
```
**Build a Jar**
```bash
./gradlew createMojmapBundlerJar
```

## Modifying Patches 
Source: [Paper/CONTRIBUTING.md](https://github.com/PaperMC/Paper/blob/master/CONTRIBUTING.md)

This method works by temporarily resetting your `HEAD` to the desired commit to
edit it using `git rebase`.

> ❗ While in the middle of an edit, you will not be able to compile unless you
> *also* reset the opposing module(s) to a related commit. In the API's case,
> you must reset the Server, and reset the API if you're editing the Server.
> Note also that either module _may_ not compile when doing so. This is not
> ideal nor intentional, but it happens. Feel free to fix this in a PR to us!

0. If you have changes you are working on, type `git stash` to store them for
   later;
    - You can type `git stash pop` to get them back at any point.
1. Type `git rebase -i base`;
    - It should show something like
      [this](https://gist.github.com/zachbr/21e92993cb99f62ffd7905d7b02f3159) in
      the text editor you get.
    - If your editor does not have a "menu" at the bottom, you're using `vim`.  
      If you don't know how to use `vim` and don't want to
      learn, enter `:q!` and press enter. Before redoing this step, do
      `export EDITOR=nano` for an easier editor to use.
2. Replace `pick` with `edit` for the commit/patch you want to modify, and
   "save" the changes;
    - Only do this for **one** commit at a time.
3. Make the changes you want to make to the patch;
4. Type `git add .` to add your changes;
5. Type `git commit --amend` to commit;
    - **Make sure to add `--amend`** or else a new patch will be created.
    - You can also modify the commit message and author here.
6. Type `git rebase --continue` to finish rebasing;
7. Type `./gradlew rebuildPatches` in the root directory;
    - This will modify the appropriate patches based on your commits.
8. PR your modified patch file(s) back to this repository.
