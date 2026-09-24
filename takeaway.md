# Understanding Our CI Pipeline

**What is CI and why do we use it?**
Continuous Integration (CI) is an automated process that helps us make sure our code changes are safe and work correctly. Instead of manually testing and building the app every time someone writes new code, the CI pipeline does it for us automatically in the cloud. This catches bugs early and saves us a lot of time.

**What triggers the pipeline?**
I learned that the pipeline runs automatically whenever someone pushes new code to the `main` branch or creates a pull request pointing to `main`. There is also a manual trigger, meaning we can click a button on GitHub to run the pipeline ourselves whenever we need to.

**How the jobs work together**
Our pipeline has two main jobs: `test` and `build`. They depend on each other. The `test` job runs first. If all the tests pass, the pipeline moves on to the `build` job. If any test fails, the entire pipeline stops right there, and the build job will not run.

**What the Test Job does**
This job spins up a fresh Ubuntu environment. It first downloads our source code and installs Python version 3.12. Then, it uses pip to install all the external packages we need, which are listed in `requirements.txt`. Once the environment is fully set up, it runs `pytest` to execute all our automated tests.

**What the Build Job does**
Because jobs run in isolated environments, the build job also has to download the code and set up Python 3.12 again. After that, it makes our `build.sh` script executable and runs it to build the application. Finally, it takes the newly created `build` folder and uploads it to GitHub as an artifact named `calculator-build`. This artifact allows us to download the final, built files after the pipeline finishes.
