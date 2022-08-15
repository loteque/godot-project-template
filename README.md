# godot-project-template
### (some configuration required) features: best practices dir stucture, git-LFS, itchio auto-delivery, ghpages auto-deploy

## git-LFS:
Before you push your first changes make sure you have git-lfs installed on your system:
https://git-lfs.github.com/
this template comes with a preconfigured .gitattributes file but feel free to add your own rules.

## itchio and ghpages auto deploy:
you will need to generate a key for both itch.io and github.
Save them with the following variable names in your repository settings:
* GH_CREDENTIALS
* BUTLER_CREDENTIALS
![image](https://user-images.githubusercontent.com/69282314/184680197-b607040d-7a3a-4b8a-bb3d-d670d9d0d933.png)



You will need to set some Global variables at the top of the following yaml files
* .github/workflows/godot-ci.yml
* .github/workflows/publish-to-itchio.yml

## directory structure and best practices

* the import directory is where you keep all your working files like .psd .krita .blender etc... It is track by git-lfs.
* the project/asset directory is where you keep all your game art, sound, etc... It is tracked by git-lfs
* the project/src directory is where you keep all your user created source-code.
* the documentation directory is a directory where you can store design docs, wiki rough drafts, etc...
