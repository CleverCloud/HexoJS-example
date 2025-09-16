# Deploy an Hexo based application on Clever Cloud

This project show how to deploy Hexo on Clever Cloud.

## Clever Tools setup

You need [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), a [Clever Cloud account](https://console.clever-cloud.com) and [Clever Tools to follow this tutorial](https://www.github.com/CleverCloud/clever-tools). If you don't have it installed, you can do it using npm or [your favorite package manager](https://www.clever.cloud/developers/doc/cli/install/):

```bash
npm install -g clever-tools

clever login   # Log in to your Clever Cloud account
clever profile # Check you're connected
```


```bash
clever create --type node --region par HexoJS-app
```

Find more information about Clever Tools parameters [here](https://www.clever.cloud/developers/doc/cli/applications/).

If needed, you can set the scaling :

```bash
clever scale --flavor pico
clever scale --build-flavor M
```

More information about Clever Tools `scale` command [here](https://www.clever.cloud/developers/doc/cli/applications/configuration/#scale-and-dedicated-build).

### Environment setup

You need to setup one Environment variable :

```bash
clever env set CC_PRE_BUILD_HOOK "npm install hexo-cli -g"
```

Optionally, if you want the command `hexo genrate` to be launched at every deployment to automatically generate the static file, you can also add :

```bash
clever env set CC_POST_BUILD_HOOK "hexo genrate"
```

### Modify hexo server configuration

The hexoJS server launch is configured in the `package.json` in the `scripts/start` field.  
This example is set to use the command :

```bash
hexo server --port 8080 --static
```

Listening on port 8080 is necessary to deploy on Clever Cloud. 
The `--static` option means only static page generated with `hexo generate` are shown. You can remove this option if you want.

### Deploy !

Nothing else left to do, just deploy your application:

```bash
clever deploy
```
