- Get current project ID
    ```shell
    export PROJECT_ID=$(gcloud info --format='value(config.project)')
    export BUCKET=${PROJECT_ID}-ml
    ```
- 