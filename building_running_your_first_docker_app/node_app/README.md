# Build Docker Image
1. Run from node_app directory :
   ```bash
   docker build -t <_name_> .
   ```
    OR
   Use if file is not Dockerfile
    ```bash
    docker build -t <_name_> -f <_file name other than Dockerfile_> .
   ```

# Check image
Run the below command to find the image you built in the list. 
```bash
docker images
```

# Docker Login Without 2FA:

To perform a Docker login without 2FA, you can use the following command:

```bash
docker login -u <username> -p <password>
```

Replace **<_username_>** with your Docker Hub username and **<_password_>** with your Docker Hub password. Note that using the password directly might not be secure, and it's recommended to use an access token or use the docker login command interactively, allowing you to enter your credentials securely.

# Docker Login With 2FA:

When using 2FA, you need to use a personal access token instead of your password. Follow these steps:

a. Generate a personal access token on the Docker Hub website.

b. Use the access token for the Docker login:

```bash
docker login -u <username> -p <access-token>
```

Replace **<_username_>** with your Docker Hub username and **<_access-token_>**

# Tag the Docker Image:
Before pushing the image, you need to tag it with your Docker Hub username and the desired repository name. Use the following command:

```bash
docker tag <image-id> <username>/<repository>:<tag>
```

Replace **<_image-id_>** with the ID of the Docker image you want to push, 
**<_username_>** with your Docker Hub username, **<_repository_>** with the name of your Docker Hub repository, and **<_tag_>** with a version or tag for your image.


# Push the Docker Image:
Now, push the tagged image to Docker Hub using the following command:

```bash
    docker push <username>/<repository>:<tag>
```

Replace **<_username_>**, **<_repository_>**, and **<_tag_>** with the same values used in the previous step.

After executing these commands, your Docker image should be pushed to Docker Hub. Make sure you have the necessary permissions to push images to the specified repository. If you encounter any issues, ensure that you are properly authenticated and that the image is correctly tagged.
