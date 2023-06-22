<table align=center border="0">
<tr>
<th>
    
![icon](https://github.com/loteque/godot-project-template/assets/69282314/9ff1f807-468a-476b-9c54-dd19b0f15aa0) 
    
</th>
<th> 

# godot-project-template
Automate Project Builds and Deployment!

</th>
</tr>
</table>

## Features:
* **GitHub pages auto-deploy**
* **itch.io auto-delivery** 
* **best practices dir stucture** 
* **_Optional_**  
  * **git-LFS** 
  * **GUT (Godot Unit Testing)**

## itch.io and GitHub pages auto deploy step by step
<details>
  <summary>Sign in to GitHub and Itch.io:</Summary>

0) Make sure you are signed in to both github and itch.io
  * https://github.com/login
  * https://itch.io/login

</details>
<details>
  <summary> Create a GitHub Personal Access Token for the project:</summary>

1) Create a [Personal Access Token](https://github.com/settings/tokens), in your GitHub user account settings, with the following permissions:
    * Contents - Read and Write
    * Metadata - Read-only
    * Pages - Read and Write
![image](https://github.com/loteque/godot-project-template/assets/69282314/7738951b-62d8-4cf2-9d2a-a7c79069109d)

</details>
<details>
  <summary>Add personal access token to repo secrets:</Summary>

2) add Personal Acess Token as a repository secret with name GH_CREDENTIALS
    * 👉 `https://github.com/<your-github-username>/<your-repository-name>/settings/secrets/actions`
![image](https://user-images.githubusercontent.com/69282314/184680197-b607040d-7a3a-4b8a-bb3d-d670d9d0d933.png)

</details>
<details>
  <summary>Set read and write permission for the workflow:</summary>

3) Make sure `read and write` permissions are set on workflows:
    * 👉 `https://github.com/<your-github-username>/<your-repository-name>/settings/actions`
![image](https://github.com/loteque/godot-project-template/assets/69282314/7e41b9a3-d075-4689-b6bb-7893e3e88eee)

</details>
<details>
  <summary>Setup GitHub Pages:</summary>

4) Setup pages for the repository:
    * 👉 `https://github.com/<your-github-username>/<your-repository-name>/settings/pages`
![image](https://github.com/loteque/godot-project-template/assets/69282314/9d1c1f01-9047-468e-8d14-e43169b4f410)

</details>
<details>
  <summary>Customize the workflow yaml to your project:</summary>

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
    
</details>
<details>
  <summary>Create a butler API token:</summary>

* Generate an [API token](https://itch.io/user/settings/api-keys) in itch.io settings

</details>
<details>
  <summary>Add Token to repo Secrets:</summary>

* add the token to yout repository secrets with name BUTLER_CREDENTIALS
    * 👉 `https://github.com/<your-github-username>/<your-repository-name>/settings/secrets/actions`
![image](https://user-images.githubusercontent.com/69282314/184680197-b607040d-7a3a-4b8a-bb3d-d670d9d0d933.png)
</details>
<details>
  <summary>Customize the deploy yaml to your project:</summary>

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
</details>


## Triggering the auto-deploy pipeline
_GitHub actions will trigger an autodeploy process when it detects a tag starting with "v", For Example:_ `v1.0.1`
<details>
  <summary>Commit as normal, push it, tag your commit, then push the tag:</summary>

* Commit your changes as normal, then tag the commit: ```git tag -a v1.0 -m "summary of release changes"```
* Push your changes with the tag: ```git push origin --tags```
* Github Actions will detect the new tag and trigger a new automated build of the game. 
* When it is done building it will auto-deploy an HTML5 Version to Github Pages.
* It will release all versions you have configured to build to Itch.io.

</details>


## GUT and git-LFS

<details>
  <summary> Optionally configure Godot Unit Testing (GUT) and/or git-LFS</summary>

## git-LFS(optional):
Before you push your first changes make sure you have git-lfs installed on your system:
https://git-lfs.github.com/
this template comes with a preconfigured .gitattributes file but feel free to add your own rules.
you must change the filename from gitattributes-template to .gitattributes

## GUT(optional):
Godot Unit Tests (GUT) is configured by default to run on pull requests to main. Tests are to be placed in res://test in either the res://test/unit or res://test/integration dirs. If you don't want to use tests just don't place tests there. For more information on GUT: https://github.com/bitwes/Gut/wiki/Quick-Start

</details>
<hr>

## _Directory structure and best practices_
* the project/asset directory is where you keep all your game art, sound, etc... It can be tracked by git-lfs
* the project/src directory is where you keep the source-code. It should not be tracked by git-lfs.
