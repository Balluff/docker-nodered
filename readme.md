# About

This project provides you the [Node-RED](https://nodered.org/) data flow editor as a Docker container for using on multiple platforms.
It comes with the [Balluff](https://www.balluff.com) company style guide elements.
Also [git](https://git-scm.com/) is installed and the Node-RED project feature is enabled.

## References

- [Official Node-RED Docker container](https://github.com/node-red/node-red-docker)
- [Node-RED project feature page](https://nodered.org/docs/user-guide/projects/)
- [Customized Editor Styles](https://nodered.org/docs/configuration)

## Container usage

Start this container by the following command will pull and run it in the background.

```sh
docker run --name baluff_nodered -d -p 1880:1880 balluff/nodered:v1.0
```

If you don't enter an tag `latest` is used. But we recommend to set a tag and pull the specific version you want.

Use a volume mount binding with parameter `-v` to have the data created inside the editor available for backup etc.

```sh
# Mount binding to a local directory
docker run --name baluff_nodered -d -v /path/to/map:/home/node-red/.node-red -p 1880:1880 balluff/nodered:v1.0

# Work with a volume
docker volume create nodered_data
docker run --name baluff_nodered -d -v nodered_data:/home/node-red/.node-red -p 1880:1880 balluff/nodered:v1.0
```

## Work with Node-RED

After starting the container you can connect to the Node-RED webinterface via `http://localhost:1880` there `localhost` is available if the container runs on your local machine.
Otherwise you need to replace `localhost` with your server's IP address.

![Node-RED start page](./screens/nodered_start.png)

By default the editor is password protected - use the following data to open the editor:
- Username: `balluff`
- Password: `VuUg3vcz`

On the first start the Node-RED `projects` page welcomes you. If you want to clone a repository follow the wizard, otherwise click on `Not right now`.
You can use the project feature later.

![Node-RED project wizard](./screens/nodered_project_wizard.png)

You can install new nodes and modules inside the container via the editor webinterface.
For this click on the `3 horizontal stack bar icon` and then select `settings`. Go to the `Palette` area shows you all installed nodes in the tab.
Click on `Install` tab to add new nodes.

![Node-RED settings palette](./screens/nodered_settings_palette.png)