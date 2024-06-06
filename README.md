# **godot-project-template**
### (support: Godot 4.2.2 stable)

### Features:
* **GitHub pages auto-deploy**
* **itch.io auto-delivery** 
* **best practices dir stucture** 
* **_Optional_**  
  * **git-LFS** 
  * **GUT (Godot Unit Testing)**

## itch.io and GitHub pages auto deploy step by step
    
- [ ] **Sign in to GitHub and Itch.io:**

    0) Make sure you are signed in to both github and itch.io
        * https://github.com/login
        * https://itch.io/login

- [ ] **Create a GitHub Personal Access Token for the project:**

    1) Create a [Personal Access Token](https://github.com/settings/tokens), in your GitHub user account settings, with the following permissions:
        * Contents - Read and Write
        * Metadata - Read-only
        * Pages - Read and Write
![image](https://github.com/loteque/godot-project-template/assets/69282314/7738951b-62d8-4cf2-9d2a-a7c79069109d)

- [ ] Add personal access token to repo secrets:</Summary>

    2) add Personal Acess Token as a repository secret with name GH_CREDENTIALS
        * 👉 `https://github.com/<your-github-username>/<your-repository-name>/settings/secrets/actions`
![image](https://user-images.githubusercontent.com/69282314/184680197-b607040d-7a3a-4b8a-bb3d-d670d9d0d933.png)

- [ ] Set the read and write permissions for the workflow:

    3) Make sure `read and write` permissions are set on workflows:
        * 👉 `https://github.com/<your-github-username>/<your-repository-name>/settings/actions`
![image](https://github.com/loteque/godot-project-template/assets/69282314/7e41b9a3-d075-4689-b6bb-7893e3e88eee)

- [ ] Setup GitHub Pages:

    4) Setup pages for the repository:
        * 👉 `https://github.com/<your-github-username>/<your-repository-name>/settings/pages`
![image](https://github.com/loteque/godot-project-template/assets/69282314/9d1c1f01-9047-468e-8d14-e43169b4f410)

- [ ] Customize the workflow yaml to your project:</summary>

    5) Edit the .github/workflows/godot-ci.yml file:
        * 👉 `https://github.com/<your-github-username>/<your-repository-name>/blob/main/.github/workflows/godot-ci.yml`
        ```yaml
        name: "godot-ci export"
        on: 
          push:
            tags:
              - "v*"
    
        env:
        👉  GODOT_VERSION: X.x    #your-godot-version probably "3.5"
        👉  EXPORT_NAME: string   #the-name-of-your-project
        ```
        * After the godot-ci workflow completes you will find your game at <your-username>.github.io/<your-repos-name>
    

- [ ] Create a butler API token:

    * Generate an [API token](https://itch.io/user/settings/api-keys) in itch.io settings

- [ ] Add Token to repo Secrets:

    * add the token to yout repository secrets with name BUTLER_CREDENTIALS
        * 👉 `https://github.com/<your-github-username>/<your-repository-name>/settings/secrets/actions`
![image](https://user-images.githubusercontent.com/69282314/184680197-b607040d-7a3a-4b8a-bb3d-d670d9d0d933.png)

- [ ] Customize the deploy yaml to your project:

    * Edit .github/workflows/publish-to-itchio.yml
        * 👉 `https://github.com/<your-github-username>/<your-repository-name>/blob/main/.github/workflows/publish-to-itchio.yml`
        ```yaml
        name: "publish to itch.io"
        on:
          release:
          types: [published]

        env:
        👉  ITCH_USER: your_itchio_username       #<your-user-name>.itch.io
        👉  ITCH_GAME: the_url_stub_of_your_game  #<your-user-name>.itch.io/<the-url-stub>

        ```


## Triggering the auto-deploy pipeline
_GitHub actions will trigger an autodeploy process when it detects a tag starting with "v", For Example:_ `v1.0.1`
### Commit as normal, push it, tag your commit, then push the tag:###

* Commit your changes as normal, then tag the commit: ```git tag -a v1.0 -m "summary of release changes"```
* Push your changes with the tag: ```git push origin --tags```
* Github Actions will detect the new tag and trigger a new automated build of the game. 
* When it is done building it will auto-deploy an HTML5 Version to Github Pages.
* It will release all versions you have configured to build to Itch.io.


## GUT and git-LFS

### Optionally configure Godot Unit Testing (GUT) and/or git-LFS

### git-LFS(optional):
Before you push your first changes make sure you have git-lfs installed on your system:
https://git-lfs.github.com/
this template comes with a preconfigured .gitattributes file but feel free to add your own rules.
you must change the filename from gitattributes-template to .gitattributes

### GUT(optional):
Godot Unit Tests (GUT) is configured by default to run on pull requests to main. Tests are to be placed in res://test in either the res://test/unit or res://test/integration dirs. If you don't want to use tests just don't place tests there. For more information on GUT: https://github.com/bitwes/Gut/wiki/Quick-Start


### _Directory structure and best practices_
* the project/asset directory is where you keep all your game art, sound, etc... It can be tracked by git-lfs
* the project/src directory is where you keep the source-code. It should not be tracked by git-lfs.
