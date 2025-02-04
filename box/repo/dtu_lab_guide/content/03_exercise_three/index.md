## Ex 3: Download all configuration

In this exercise, we'll see how Monaco can be used to download an existing environment's configuration. This is particularly handy when there are numerous existing custom configurations. You can download your configuration and push it into a repository, or use it as a starting point for managed configuration changes through Monaco.

### Step 1 - Create an environments file
The first step, similar to what we did in exercise one, is to create an `environments.yaml` file.

1. In Gitea, copy the contents of file 
`perform/monaco/01_exercise_one/environments.yaml` 
and paste it into 
`perform/monaco/03_exercise_three/environments.yaml` 

   > **Tip:** Both files should be identical

2. Commit the changes

### Step 2 - Download configuration
1. Open the SSH client that's connected to your VM and navigate into the directory of this exercise

    ```bash
    cd ~/perform/monaco/03_exercise_three
    ```

2. Execute the following command to pull down changes made in Gitea

    ```bash
    git pull
    ```

3. Verify that the environment variable `DT_API_TOKEN` still exists

   ```bash
   echo $DT_API_TOKEN
   ```

   If not, recreate it from the Kubernetes secret

   ```bash
   export DT_API_TOKEN=$(kubectl -n dynatrace get secret oneagent -o jsonpath='{.data.apiToken}' | base64 -d)
   ```

4. We'll use the new experimental CLI which allows us to download the Dynatrace configurations directly with Monaco. We can activate it by supplying the environment variable `NEW_CLI=true` to the `monaco` command.

   Execute the following command to get an overview of the options:

   ```bash
   NEW_CLI=true monaco
   ```

   This will result in:

   ```bash
   You are using the new CLI structure which is currently in Beta.

   Please provide feedback here:
   https://github.com/dynatrace-oss/dynatrace-monitoring-as-code/issues/45.

   We plan to make this CLI GA in version 2.0.0

   NAME:
      monaco - Automates the deployment of Dynatrace Monitoring Configuration to one or multiple Dynatrace environments.

   USAGE:
      monaco [global options] command [command options] [arguments...]

   VERSION:
      1.8.1

   DESCRIPTION:
      
      Tool used to deploy dynatrace configurations via the cli
      
      Examples:
      Deploy a specific project inside a root config folder:
         monaco deploy -p='project-folder' -e='environments.yaml' projects-root-folder
      
      Deploy a specific project to a specific tenant:
         monaco deploy --environments environments.yaml --specific-environment dev --project myProject
      

   COMMANDS:
      deploy    deploys the given environment
      download  download the given environment
      help, h   Shows a list of commands or help for one command

   GLOBAL OPTIONS:
      --help, -h  show help (default: false)
      --version   print the version (default: false)
   ```

5. We now have access to a new option to download the configuration, let's try it out with the command below:

   ```bash
   NEW_CLI=true monaco download -e=environments.yaml
   ```

   Monaco will now download the config:

   ```bash
   You are using the new CLI structure which is currently in Beta.

   Please provide feedback here:
   https://github.com/dynatrace-oss/dynatrace-monitoring-as-code/issues/45.

   We plan to make this CLI GA in version 2.0.0

   2022-10-25 11:05:47 INFO  Dynatrace Monitoring as Code v1.8.1
   2022-10-25 11:05:47 INFO  Creating base project name perform
   2022-10-25 11:05:47 INFO   --- GETTING CONFIGS for app-detection-rule-host
   2022-10-25 11:05:47 INFO   --- GETTING CONFIGS for maintenance-window
   2022-10-25 11:05:47 INFO  No elements for API maintenance-window
   2022-10-25 11:05:47 INFO   --- GETTING CONFIGS for hosts-auto-update
   2022-10-25 11:05:47 INFO   --- GETTING CONFIGS for application-mobile
   2022-10-25 11:05:47 INFO  No elements for API application-mobile
   2022-10-25 11:05:47 INFO   --- GETTING CONFIGS for application
   2022-10-25 11:05:47 INFO   --- GETTING CONFIGS for anomaly-detection-services
   2022-10-25 11:05:47 INFO   --- GETTING CONFIGS for auto-tag
   2022-10-25 11:05:47 INFO   --- GETTING CONFIGS for slo
   2022-10-25 11:05:47 INFO  No elements for API slo
   2022-10-25 11:05:47 INFO   --- GETTING CONFIGS for anomaly-detection-disks
   2022-10-25 11:05:47 INFO  No elements for API anomaly-detection-disks
   2022-10-25 11:05:47 INFO   --- GETTING CONFIGS for data-privacy
   2022-10-25 11:05:47 INFO   --- GETTING CONFIGS for custom-service-java
   2022-10-25 11:05:47 INFO  No elements for API custom-service-java
   2022-10-25 11:05:47 INFO   --- GETTING CONFIGS for synthetic-location
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for extension
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for calculated-metrics-synthetic
   2022-10-25 11:05:48 INFO  No elements for API calculated-metrics-synthetic
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for custom-service-nodejs
   2022-10-25 11:05:48 INFO  No elements for API custom-service-nodejs
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for calculated-metrics-service
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for service-detection-full-web-request
   2022-10-25 11:05:48 INFO  No elements for API service-detection-full-web-request
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for management-zone
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for anomaly-detection-metrics
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for app-detection-rule-v2
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for geo-ip-address-mappings
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for anomaly-detection-hosts
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for frequent-issue-detection
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for conditional-naming-processgroup
   2022-10-25 11:05:48 INFO  No elements for API conditional-naming-processgroup
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for calculated-metrics-application-mobile
   2022-10-25 11:05:48 INFO  No elements for API calculated-metrics-application-mobile
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for calculated-metrics-log
   2022-10-25 11:05:48 ERROR error getting client list from api calculated-metrics-log Failed to get existing configs for api calculated-metrics-log (HTTP 400)!
      Response was: {"error":{"code":400,"message":"You are using the new log monitoring solution. Old API endpoints are disabled."}}
   2022-10-25 11:05:48 ERROR error getting configs from API calculated-metrics-log %!v(MISSING)
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for kubernetes-credentials
   2022-10-25 11:05:48 INFO  No elements for API kubernetes-credentials
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for custom-service-php
   2022-10-25 11:05:48 INFO  No elements for API custom-service-php
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for alerting-profile
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for geo-ip-detection-headers
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for notification
   2022-10-25 11:05:48 INFO  No elements for API notification
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for anomaly-detection-applications
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for extension-elasticsearch
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for credential-vault
   2022-10-25 11:05:48 INFO  No elements for API credential-vault
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for allowed-beacon-origins
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for anomaly-detection-vmware
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for request-naming-service-v2
   2022-10-25 11:05:48 INFO  No elements for API request-naming-service-v2
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for failure-detection-rules
   2022-10-25 11:05:48 INFO  No elements for API failure-detection-rules
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for service-resource-naming
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for azure-credentials
   2022-10-25 11:05:48 INFO  No elements for API azure-credentials
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for conditional-naming-service
   2022-10-25 11:05:48 INFO  No elements for API conditional-naming-service
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for aws-credentials
   2022-10-25 11:05:48 INFO  No elements for API aws-credentials
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for anomaly-detection-database-services
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for synthetic-monitor
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for anomaly-detection-aws
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for content-resources
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for reports
   2022-10-25 11:05:48 INFO  No elements for API reports
   2022-10-25 11:05:48 INFO   --- GETTING CONFIGS for dashboard-v2
   2022-10-25 11:05:49 INFO   --- GETTING CONFIGS for failure-detection-parametersets
   2022-10-25 11:05:49 INFO  No elements for API failure-detection-parametersets
   2022-10-25 11:05:49 INFO   --- GETTING CONFIGS for service-detection-opaque-web-service
   2022-10-25 11:05:49 INFO  No elements for API service-detection-opaque-web-service
   2022-10-25 11:05:49 INFO   --- GETTING CONFIGS for custom-service-go
   2022-10-25 11:05:49 INFO  No elements for API custom-service-go
   2022-10-25 11:05:49 INFO   --- GETTING CONFIGS for service-detection-opaque-web-request
   2022-10-25 11:05:49 INFO  No elements for API service-detection-opaque-web-request
   2022-10-25 11:05:49 INFO   --- GETTING CONFIGS for conditional-naming-host
   2022-10-25 11:05:49 INFO  No elements for API conditional-naming-host
   2022-10-25 11:05:49 INFO   --- GETTING CONFIGS for calculated-metrics-application-web
   2022-10-25 11:05:49 INFO  No elements for API calculated-metrics-application-web
   2022-10-25 11:05:49 INFO   --- GETTING CONFIGS for service-detection-full-web-service
   2022-10-25 11:05:49 INFO  No elements for API service-detection-full-web-service
   2022-10-25 11:05:49 INFO   --- GETTING CONFIGS for application-web
   2022-10-25 11:05:49 INFO   --- GETTING CONFIGS for request-attributes
   2022-10-25 11:05:49 INFO   --- GETTING CONFIGS for custom-service-dotnet
   2022-10-25 11:05:49 INFO  No elements for API custom-service-dotnet
   2022-10-25 11:05:49 INFO  END downloading info perform
   ```

6. We can now push this content back to our git repository:

   ```bash
   git add .
   sudo git commit -m "downloaded config snapshot"
   git push
   ```

   > Tip: If you get prompted for your VM or Gitea credentials, remember that you can find them on your dashboard page.

7. Go to Gitea and inspect the newly uploaded Dynatrace config in `perform/monaco/03_exercise_three/perform`


   ![Downloaded configuration](../../assets/images/03_downloaded_config.png)

### This concludes Exercise 3, GitOps is yet another step closer!
