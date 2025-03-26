## Overview

This project is an example of setting up the SonarScanner Analysis with GitHub Actions pipeline for a different languages project.  
We have multiple CI/CD Pipeline examples, one for connecting to SonarQube Server instance and the other to SonarQube Cloud instance.   

**PLEASE READ OUR SONARQUBE DOCUMENTATION FOR WORKING WITH GITHUB ACTION PIPELINES**  
[GitHub - SonarQube Server Integration](https://docs.sonarsource.com/sonarqube-server/latest/devops-platform-integration/github-integration/introduction/)  
[GitHub Actions Pipelines - SonarQube Cloud](https://docs.sonarsource.com/sonarqube-cloud/advanced-setup/ci-based-analysis/github-actions-for-sonarcloud/)

## Important Information in Examples
- On triggers are set to only execute on changes to specific branches and a specific directory in the project, this can be modified with whatever trigger you would want to use.
- They have shallow fetch set to 0. this is required for SonarScanner to properly analyze your project.  
- For more information on how to limit your analysis scope and parameters available, please check **SonarScanner Analysis Scope** and **SonarScanner Analysis Parameters** in the Important Links section.
- The action used for SonarScanner Analysis is `sonarqube-scan-action`, which applies for both SonarQube Server and SonarQube Cloud. But they require different parameters. Examples for both are provided.
    - SonarQube Cloud Example: [sonarqube-cloud.yml](.github/workflows/sonarqube-cloud.yml)  
    - SonarQube Server Example: [sonarqube-server.yml](.github/workflows/sonarqube-server.yml)
- The version being used for `sonarqube-scan-action` is `v5`, major version is being used in order to not have to change the version constantly and with setting the version this way it will always use the latest version from the `v5` version. Ex, if v5 set and latest is `v5.1.0`, it will use this latest and if it changes to `v5.2.0`, it will automatically use that one when it gets added.
- For both `sonar.projectKey` and `sonarprojectName`, we are using the following `$(echo ${{ github.repository }} | cut -d'/' -f1)-gh_$(echo ${{ github.repository }}` as naming convention. This results in `OrgName-gh_RepoName`.  
- Please make sure you have set up your `SONAR_TOKEN` and `SONAR_HOST_URL` secrets or variables. In the command used, `SONAR_TOKEN` is set up as a secret and `SONAR_HOST_URL` is set a variable. If set up differently please change the prefix in the respective parameter.   

## Important Links
[SonarQube Server - GitHub Integration](https://docs.sonarsource.com/sonarqube-server/latest/devops-platform-integration/github-integration/introduction/)  
[SonarQube Cloud - GitHub Integration](https://docs.sonarsource.com/sonarqube-cloud/getting-started/github/)  
[SonarQube Server | Cloud Scan GitHub Action task](https://github.com/marketplace/actions/official-sonarqube-scan)  

[SonarScanner Analysis Scope](https://docs.sonarsource.com/sonarqube-server/latest/project-administration/analysis-scope/)  
[SonarScanner Analysis Parameters](https://docs.sonarsource.com/sonarqube-server/latest/analyzing-source-code/analysis-parameters/)  

[Languages SonarScanner Analysis Extra Information](https://docs.sonarsource.com/sonarqube-server/latest/analyzing-source-code/languages/overview/)  
[Test Coverage](https://docs.sonarsource.com/sonarqube-server/latest/analyzing-source-code/test-coverage/overview/)  

## Example to Fail the Pipeline on Quality Gate Failure
In certain situations, you may want to halt/fail the pipeline if the SonarQube Quality Gate fails, preventing subsequent steps from executing.  
This can be achieved by adding `sonar.qualitygate.wait=true` to the `with: args: >` section in the **SonarQube Analysis** task.  

Example:
``` sh
    with:
        args: >
          -Dsonar.verbose=true
          -Dsonar.sources=src/
          -Dsonar.qualitygate.wait=true
```

__**For more examples please check:**__
[Onboarding Examples](https://github.com/sonar-solutions/Onboarding-Examples-List)
