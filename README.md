# k8s-from-private-docker-registry
This is a project to deploy a container from an image in your private docker registry.

1. Build the app with the Dockerfile in the **my-app-n-dockerfile** repository.
2. Upload it to dockerhub
3. Login to dockerhub from your cli
4. Run `cat .docker/config.json` to get the authentication values.
5. Convert the file's content to base64
6. Enter the values in the `data` section of the **docker-secret.yaml** file
7. Run the **docker-secret.yaml** file
8. Next, run the **my-app-deployment** file with the container image from your registry to deploy it to your k8s cluster.

Note that the `spec.template.spec.imagePullSecrets` value in the deployment file is what facilitates
the successful connection to your docker private repository.
The `spec.template.spec.containers.imagePullPolicy` parameter is set to "Always",
so k8s always pulls the image from your private repository when needed.
