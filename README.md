# Udemy_GithubActionsTheCompleteGuide
This repository contains exercises included in Github Actions - The Complete Guide course in Udemy.
link : https://www.udemy.com/course/github-actions-the-complete-guide/learn/lecture/34120940#overview

Section 07 - Controlling Workflow & Job Execution
=================================================
- L91 Working with Special Conditional Functions 
    - failure function is added into Upload test report step in test job and report is observed, and can be downloaded, on github after previous Test code step failed.

- L92 Conditional Jobs
    - Usage of if condition at job level: wrote some dummy message on terminal if one of the existing jobs have failed or not. 
        report:
            # this job write a message and github context on terminal if any existing job fails
            needs: [lint,deploy]
            if: failure()
            runs-on: ubuntu-latest
            steps:
            - name: Output Information
                run: |
                echo "Something went wrong"
                echo "${{ github }}" 

- L95 understanding and using matrix stragety
    - run the same job with different configurations (operating system, node-version etc)
        jobs:
            build:
                continue-on-error: true
                strategy:
                    matrix:
                        node-version: [12,14,16]
                        operating-system: [ubuntu-latest,windows-latest]
                        include:
                            - node-version: 18
                            operating-system: ubuntu-latest
                        exclude:
                            - node-version: 12
                            operating-system: windows-latest

- L96 Including and Excluding Values (Matrix Strategy)
    - how to include or exclude specific configurations to/from matrix
        jobs:
            build:
                continue-on-error: true
                strategy:
                    matrix:
                        node-version: [12,14,16]
                        operating-system: [ubuntu-latest,windows-latest]
                        include:
                            - node-version: 18
                            operating-system: ubuntu-latest
                        exclude:
                            - node-version: 12
                            operating-system: windows-latest

- L97 Saving Time & Code with Reusable workflows
    - how to use another workflow inside a worfklow
        deploy:
        needs: build
        uses: ./.github/workflows/reusable_workflow.yml