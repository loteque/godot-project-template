# godot-project-template
### (some configuration required) features: best practices dir stucture, git-LFS, itchio auto-delivery, ghpages auto-deploy

## git-LFS(optional):
Before you push your first changes make sure you have git-lfs installed on your system:
https://git-lfs.github.com/
this template comes with a preconfigured .gitattributes file but feel free to add your own rules.
you must change the filename from gitattributes-template to .gitattributes

## itchio and ghpages auto deploy:
you will need to generate a key for both itch.io and github.
Save them with the following variable names in your repository settings:
* GH_CREDENTIALS
* BUTLER_CREDENTIALS


Setup GH_CREDENTIALS and github pages:
1) Create a Personal Access Token, in account settings, with the following permissions:
  * Contents - Read and Write
  * Metadata - Read-only
  * Pages - Read and Write
![image](https://github.com/loteque/godot-project-template/assets/69282314/7738951b-62d8-4cf2-9d2a-a7c79069109d)


2) add Personal Acess Token as a repository secret with name GH_CREDENTIALS
![image](https://user-images.githubusercontent.com/69282314/184680197-b607040d-7a3a-4b8a-bb3d-d670d9d0d933.png)


3) Make sure `read and write` permissions are set on workflows:
![image](https://github.com/loteque/godot-project-template/assets/69282314/7e41b9a3-d075-4689-b6bb-7893e3e88eee)


4) Setup pages for the repository:
![image](https://github.com/loteque/godot-project-template/assets/69282314/9d1c1f01-9047-468e-8d14-e43169b4f410)


You will need to set some Global variables at the top of the following yaml files
* .github/workflows/godot-ci.yml 
* .github/workflows/publish-to-itchio.yml

## How to trigger the auto-deploy pipeline
* GitHub actions will trigger an autodeploy process when it detects a tag starting with "v", For Example: ```v1.0.1```
* Commit your changes as normal, then tag the commit: ```git tag -a v1.0 -m "summary of release changes"```
* Push your changes with the tag: ```git push origin --tags```
* Github Actions will detect the new tag and trigger a new automated build of the game. 
* When it is done building it will auto-deploy an HTML5 Version to Github Pages.
* It will release all versions you have configured to build to Itch.io.

## directory structure and best practices
* the import directory is where you keep all your working files like .psd .krita .blender etc... It is track by git-lfs.
* the project/asset directory is where you keep all your game art, sound, etc... It is tracked by git-lfs
* the project/src directory is where you keep all your user created source-code.
* the documentation directory is a directory where you can store design docs, wiki rough drafts, etc...
