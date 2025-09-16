# Deploy an Hexo based application on Clever Cloud

This project show how to deploy Hexo on Clever Cloud.

## Clever Tools setup

You need [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), a [Clever Cloud account](https://console.clever-cloud.com) and [Clever Tools to follow this tutorial](https://www.github.com/CleverCloud/clever-tools). If you don't have it installed, you can do it using npm or [your favorite package manager](https://www.clever.cloud/developers/doc/cli/install/):

```bash
npm install -g clever-tools

clever login   # Log in to your Clever Cloud account
clever profile # Check you're connected
```

## Create an application using Static runtime

Clone this project and create [a static application](https://www.clever.cloud/developers/doc/applications/static/):

```bash
git clone https://github.com/CleverCloud/HexoJS-example
cd HexoJS-example
clever create --type static
```

Find more information about Clever Tools parameters [here](https://www.clever.cloud/developers/doc/cli/applications/).

If needed, set the scaling:

```bash
clever scale --flavor pico
clever scale --build-flavor M
```

More information about Clever Tools `scale` command [here](https://www.clever.cloud/developers/doc/cli/applications/configuration/#scale-and-dedicated-build).

### Environment setup

You need to setup some environment variables:

```bash
# Define the folder where the static files are located
clever env set CC_WEBROOT "/public"

# Define commands to install dependencies and build
clever env set CC_PRE_BUILD_HOOK "npm install"
clever env set CC_BUILD_COMMAND "npm run build"
```

### Deploy !

Nothing else left to do, just deploy your application:

```bash
clever deploy
```
