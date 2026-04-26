# Pipelines System

**PG29 Pipelines**

## About the Project

This project is to make a simple pipeline system to address and solve a common problem.

### What I did:

I decided to create a pipeline to create unity builds from a unity project and post them in a separate github repository. It is scheduled to happen once a day. 

### How to use pipeline:

This project contains an Unity Project to serve as an example of the pipeline working. The repository it sends the build to is https://github.com/kiranwood/TestingBuilds. The original source code for the pipeline is found in `.github/workflows/deploy.yml`.

## How to add pipeline to own unity project

**Step 1** Check your unity project build settings. Make sure it is set to windows and is using the correct scene.

**Step 2** Make sure your github repository root is the Unity Project.

**Step 3** Download `.github/workflows/deploy.yml` from inside the repo.

**Step 4** Create a folder named `.github` and inside create another folder called `workflows`. Add the `deploy.yml` file downloaded.

**Step 5** Create a repository to hold your builds.

**Step 6** Enter the command line. Type in `ssh-keygen -t ed25519 -C "your_email@gmail.com"` to create a SSH key.

**Step 7** Inside the repository that will have all the builds, go to the settings. Inside the Deploy Keys add in a with your public SSH key.

**Step 8** Go to your repository settings. Inside secrets and variables add in the following:

**Secrets**
- `DEPLOY_KEY` : The private SSH key used to connect to the public SSH to have access to the repo
- `UNITY_EMAIL` : The email if your Unity Account
- `UNITY_LICENSE` : The license of your Unity Account
- `UNITY_PASSWORD` : The password to your unity account

**Variables**
- `BUILD_PROJECT_NAME` : The name of your project build. All the build folder names will include this
- `BUILD_REPOSITORY` : The repository written as "username/repo-name"

**Step 9** Push your github changes. Check inside your repository actionns. There should be an action labeled `Build and Deploy StandaloneWindows64`. When clicked there should also be an option to run the workflow. Use this to test to make sure your workflow is functioning. Github actions will show the workflow steps and logs in real time.

**Extra** More details of the individual steps of this pipeline can be found inside `Docs/Documentation.md`