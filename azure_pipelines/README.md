# Azure Pipelines

## General
This is the first try at Azure Pipelines. Please contact Cloudnet if you are using Azure Pipelines and want to improve this example.

## TODO
- Figure out how to reuse the code for test and production deploys using the same pipeline.
- Documentation of configuration settings in Azure

## Access to the Cloudnet server
To upload the final results to Cloudnet, a deployment ssh key is needed. Add the private key as a secret file in the Azure library. Send the public part to Cloudnet to be added as a deployment key.

To make sure we are communicating with the correct server, we add the SSH fingerprint to the start script. The SSH fingerprint for the Cloudnet server is obtained with the following command:

    ssh-keyscan cXXXX.cloudnet.cloud

## Deployment folder on Cloudnet
This deployment process will replace the existing release folder on the server, so please make your app does not save data in the deployment folder. Any local storage should be saved outside the release folder.

With WordPress, you will want to symlink the uploads-folder to avoid having the uploads cleaned out at every release.

## Folder rotation at deploy
1. If there is an old release in release.old, it will be removed
2. The new release will be prepared in the release.new folder
3. If evrything goes well, the service is stopped, folders renamed and the service started again to make the interruption as short as possible while making sure that no user will access a half-baked release.
4. The previous release will be saved in release.old for reference until the next deploy.

## Site configuration
This example uses a .env settings file in ../shared relative to the target folder. A symlink is re-created after each deploy to this file.

