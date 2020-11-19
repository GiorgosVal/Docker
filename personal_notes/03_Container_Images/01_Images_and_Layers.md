# Points to remember
[About storage drivers](https://docs.docker.com/storage/storagedriver/)
## Images and Layers
- A Docker image is built up from a series of layers.
- Each layer represents an instruction in the image’s Dockerfile.
- Each layer except the very last one is read-only.
- Each layer is only a set of differences from the layer before it. The layers are stacked on top of each other.
## Container and Layers
- When a new container is created, a new writable layer is added on top of the underlying layer.
- All writes to the container that add new or modify existing data are stored in this writable layer.
- Multiple containers can share access to the same underlying image and yet have their own data state.

![](https://docs.docker.com/storage/storagedriver/images/sharing-layers.jpg)

*Source: [docker hub](https://docs.docker.com/storage/storagedriver/)*

## Copy-On-Write
If a file or directory exists in a lower layer within the image, and another layer (including the writable layer) needs read access to it, it just uses the existing file. The first time another layer needs to modify the file (when building the image or running the container), the file is copied into that layer and modified.

---
`docker image history <image>`<br/>
Shows the history of the image layers. Every image starts with a blank layer (scratch). Every set of changes that happens after that on the file system, in the image, is another layer.
>**Example:**
>`docker image history nginx:latest`<br/>

---
`docker image inspect <image>`<br/>
Returns the metadata of an image.
>**Example:**
>`docker image inspect nginx:latest`<br/>