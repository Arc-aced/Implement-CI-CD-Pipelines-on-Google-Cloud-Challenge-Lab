# Implement-CI-CD-Pipelines-on-Google-Cloud-Challenge-Lab

##TASK 1

```
gcloud storage buckets create gs://${PROJECT_ID}_cloudbuild \
--project=${PROJECT_ID} \
--location=${REGION}
```
##TASK 2
```
$REGION-docker.pkg.dev/$PROJECT_ID/cicd-challenge
```
##TASK3
```
gcloud config set deploy/region $REGION
```
```
gcloud beta deploy apply \
--file=clouddeploy-config/delivery-pipeline.yaml
```
```
CONTEXTS=("cd-production" "cd-staging")
```
```
gcloud beta deploy apply \
--file=clouddeploy-config/target-cd-staging.yaml
```
```
gcloud beta deploy apply \
--file=clouddeploy-config/target-cd-production.yaml
```
##TASK 4
```
gcloud beta deploy releases create web-app-001 \
--delivery-pipeline web-app \
--build-artifacts web/artifacts.json \
--source web/
```

##TASK 5
```
gcloud beta deploy releases promote \
--delivery-pipeline web-app \
--release web-app-001 \
--quiet
```
```
gcloud beta deploy rollouts approve [xxx] \
--delivery-pipeline web-app \
--release web-app-001 \
--quiet
```
```
gcloud services enable cloudbuild.googleapis.com
```

##TASK 6
```
cd ~/cloud-deploy-tutorials/tutorials/base/web
```
```
skaffold build --interactive=false \
--default-repo $REGION-docker.pkg.dev/$PROJECT_ID/cicd-challenge \
--file-output artifacts.json
```
```
cd ..
```
```
gcloud beta deploy releases create web-app-002 \
--delivery-pipeline web-app \
--build-artifacts web/artifacts.json \
--source web/
```
##TASK 7
```
gcloud beta deploy targets rollback cd-staging \
--delivery-pipeline web-app \
--release web-app-001
```
```
gcloud beta deploy rollouts list \
--delivery-pipeline web-app \
--release web-app-001
```
