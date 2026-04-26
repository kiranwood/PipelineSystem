
# Goal of this Pipeline

The goal of making this pipeline is to avoid having to remember to constantly make builds every single day. Instead of taking the time to remember and spend time making the build and sending it somewhere, this pipeline does it automatically for you. It uses github actions to create a build in Unity and then send the builds into another repository. All of the pipeline code can be found in `.github/workflows/deploy.yml`

## Pipeline Jobs

There are two jobs inside this workflow `Build` to build the the Unity Project and `Deploy to Github Repository` that will move the build into the repository.
The schedule time can be changed inside `- cron: "0 20 * * *" `. Although github schedules can be inconsistent and delayed at times.
Each step of the job can be seen inside github actions inside your repository. Any errors during the workflow action will display there.

### Build

**Checkout Repository**
- Checks out the project repository (current repository) in order to have access to for future steps.

**Cache Unity Library**
- Cashes the Unity Library to make building the project faster
- Can be skipped / removed but will make the build time slower

**Build Unity StandaloneWindows64**
- This creates the build. It requires an account email, password and license in order for it to work.
- It is specifically set to make a windows build. It can be changed to a different kind of build (make sure it is set up in your Unity project).

**Debug Output Structure**
- Shows the output of the build files created

**Gets current date**
- Gets the current date at the build

**Set artifact name**
- Sets a name for the artifact and the build. Uses the project name and the date to create a unique name

**Upload StandaloneWindows64 Build**
- Uploades the build as an artifact. This allows for the other job to get access to it

### Deploy

**Download build**
- Downloads the build from the artifact and moves to a folder

**Zip Build**
- Zips the build to be moved into the build repository

**Clone Build Repo**
- Clones the target repo where the builds will be going into
- If this fails, make sure to check you have set up the SSH keys properly

**Move Build into Repo**
- Moves the build into the build repository. Will overwrite the previous build if it shares the same name

**Set git config**
- Sets a user for the config. Uses the latest user that triggered / scheduled the workflow

**Push Build to Repo**
- Pushes the build to the build repo on main


