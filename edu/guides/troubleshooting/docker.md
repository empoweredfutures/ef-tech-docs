## Docker Troubleshooting

check the your user has permission to use docker commands, if you are on linux you will likely need to follow the [post install steps](https://docs.docker.com/engine/install/linux-postinstall/)

check that you have the [vscode docker extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker), this will help you manage your containers and cleanup unused volumes

if docker is still not working try re-installing it / updating it,

you'll know when your docker is working correctly when:

- the vscode docker tab shows you info about your docker install
- running `docker version` on your cli returns successfully with the latest version info
- running `docker run hello-world` on your cli returns successfully
