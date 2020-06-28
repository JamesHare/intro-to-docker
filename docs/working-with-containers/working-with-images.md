# Working with Images

So now we know how the docker run command works and how containers are based off of images.

If you are still confused at this point, think of it this way:

* Images are stopped Containers
* Containers are running Images

We already know that docker run [image name] will pull down and start a new container using the image name specified. However, we can just pull down an image without running it by using the following command:

```
docker pull [image name]
```

To pull a specific image version we can include the version in the docker pull command as follows:

```
docker pull [image name]:[version]
```

If we don't specify the image version, Docker will just pull the latest release.

Remember, you can run the docker images command to list all images that you have downloaded to your local machine:

```
docker images
```

You should take some time to get familiar with Docker Hub. I won't include much info on that here, but head over to https://hub.docker.com and take a look around. Get familiar with the UI. Remember that official images are labeled and are maintained by the teams that built the images and that they often document known security vulnerabilities on older images.

Finally, let's look at removing local images. You can remove any image that you have downloaded locally by using the following command:

```
docker rmi [image name]
```

Remember, you can also include the version number if you want to remove that particular image.