# Litmus Portal Dvelopment Environment Setup for Okteto cloud

This directory contains setup guide to start developing Litmus Portal on Okteto cloud. 

## Instructions

- STEP-1: Export your GitHub username to an environment variable.

  ```
  OKTETO_NAMESPACE=“<GitHub username>” 
  ```

- STEP-2: Enter `okteto-dev-env-setup` folder and obtain the Litmus Portal development manifest using the given template.

  ```
  sed s/%OKTETO_NAMESPACE%/$OKTETO_NAMESPACE/g litmus-portal-dev-manifest-template.yml > litmus-portal-dev-manifest.yml
  ```

- STEP-3: Update this readme file by replacing the `%GITHUB_USERNAME%` variable in STEP-7.

  ```
  sed s/%GITHUB_USERNAME%/$OKTETO_NAMESPACE/g README.md > README.md
  ```

- STEP-4: Go to root folder of this repository then add, commit and push these changes to your GitHub.

  ```
  cd ../..
  git add .
  git commit -s -m "Obtained development manifest and updated README"
  git push
  ```

- STEP-5: Install Okteto CLI
  
  For MAC/Linux:

  ```
  curl https://get.okteto.com -sSfL | sh
  ```

  or

  ```
  brew install okteto
  ```

  For Windows:

  Download the binary executable from [here](https://downloads.okteto.com/cli/okteto.exe) and add it to your `$PATH` environment variable.

- STEP-6: Create an Okteto account and login to Okteto cloud using the CLI.

  ```
  okteto login
  ```

- STEP-7: Click the button below to deploy litmus-portal on Okteto cloud and start developing.
  
  [![Develop Litmus Portal on Okteto](https://okteto.com/develop-okteto.svg)](https://cloud.okteto.com/deploy?repository=https://github.com/%GITHUB_USERNAME%/litmus)

- STEP-8: Go to specific component folders i.e. authentication, cluster-agents/subscriber, graphql-server, tools/self-deployer or frontend then run okteto up before manking changes to the code.

  ```
  cd ..
  cd frontend
  okteto up
  ```

- STEP-9: Run okteto build and push after making the code changes to get them reflected on deployed litmus-portal component.

  ```
  okteto build -t okteto.dev/litmusportal-frontend:ci .
  okteto push --name frontend -t $OKTETO_NAMESPACE/itmusportal-frontend:ci
  ```

- STEP-10: Raise a pull request to [litmuschaos/litmus](https://github.com/litmuschaos/litmus) after deleting the generated development manifest file `litmus-portal-dev-manifest.yml` in `litmus-portal/okteto-dev-env-setup` folder of `litmus` repository.