## Implementing CI/CD Workflow with GitHub Actions
### What is Continuos Integration (CI)
   Committing early and often and those committs will be tested and getting feedback of those committs that they have problems or not.

### Step 1 :
   Create ``` .github ``` Folder in the Projects Root Directory where you can create workflows for github Actions.

### Step 2 :
   Create a file with extension ``` .yml ``` where you can create rules for CI/CD workflows.
   E.g. Like when this particular workflow will start.
   (In this Demonstration workflow Starts on Pull Request from ``` test-branch ```. ) 

### Sep 3 :
   Create workflow and write rules on what scenarios that workflow should run.
   read ``` ci.yml ``` file for more details.
```yaml
   name: CI
# This workflow is triggered on pull request to the repository.
on:
  pull_request:
  # On which branch this pull request will affect.
    branches:
      - main  

jobs:
# This job will run on ubuntu virtual machine
  flutter_test:
    name: Run flutter test and analyze
    runs-on: ubuntu-latest
    steps:
    # Setup Java environment in order to build the Android app.
      - uses: actions/checkout@v2
      - uses: actions/setup-java@v1
        with:
          java-version: "12.x"
    # Setup the flutter environment.
      - uses: subosito/flutter-action@v1
        with:
          channel: "stable"  # 'dev', 'alpha', default to: 'stable'
      - run: flutter pub get # Get flutter dependencies.
      - run: flutter analyze
      - run: flutter test 
 ```