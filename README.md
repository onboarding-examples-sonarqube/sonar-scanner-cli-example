## Overview

This project is an example of setting up the SonarScanner Analysis with GitHub Actions pipeline for a different languages project.  
We have multiple CI/CD Pipeline examples, one for connecting to SonarQube Server instance and the other to SonarQube Cloud instance.   

PLEASE READ OUR SONARQUBE DOCUMENTATION FOR WORKING WITH GITHUB ACTION PIPELINES  
GitHub - SonarQube Server Integration > https://docs.sonarsource.com/sonarqube-server/latest/devops-platform-integration/github-integration/introduction/  
GitHub Actions Pipelines - SonarQube Cloud > https://docs.sonarsource.com/sonarqube-cloud/getting-started/github/#ci-based-analysis 

## Important Information in Pipeline Examples
- on triggers are set to only execute on changes to specific branches and a specific directory in the project, this can be modified with whatever trigger you would want to use.
- they have shallow fetch set to 0. this is required for SonarScanner to properly analyze your project.  
- for more information on how to limit your analysis scope and parameters available, please check **SonarScanner Analysis Scope** and **SonarScanner Analysis Parameters** in the Important Links section.
- The action used for SonarScanner Analysis is **sonarqube-scan-action**, which applies for both SonarQube Server and SonarQube Cloud. But they require different parameters. Examples for both are provided.
    - SonarQube Cloud Example: sonarqube-cloud.yml  
    - SonarQube Server Example: sonarqube-server.yml 

## Important Links
SonarQube Server - GitHub Integration > https://docs.sonarsource.com/sonarqube-server/latest/devops-platform-integration/github-integration/introduction/  
SonarQube Cloud - GitHub Integration > https://docs.sonarsource.com/sonarqube-cloud/getting-started/github/  
SonarQube Server | Cloud Scan GitHub Action task > https://github.com/marketplace/actions/official-sonarqube-scan  
SonarQube Cloud Scan GitHub Action task (not used in example, but available if needed) >  https://github.com/marketplace/actions/sonarqube-cloud-scan  
SonarScanner Analysis Scope > https://docs.sonarsource.com/sonarqube-server/latest/project-administration/analysis-scope/  
SonarScanner Analysis Parameters > https://docs.sonarsource.com/sonarqube-server/latest/analyzing-source-code/analysis-parameters/  

## Example to fail the entire pipeline if Quality Gate fails
There may be situations or branches in which you will like to fail the pipeline if the SonarQube Quality Gate fails in order to stop any other steps in the pipeline.  
This can be done by adding ```sonar.qualitygate.wait=true``` 
to the **with: args: >** section in the **SonarQube Scan** task.  

Example
``` sh
    with:
        args: >
          -Dsonar.verbose=true
          -Dsonar.sources=src/
          -Dsonar.qualitygate.wait=true
```