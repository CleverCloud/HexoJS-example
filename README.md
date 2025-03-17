#HEXOJS EXAMPLE

This project show how to deploy hexoJS on Clever Cloud.

### Create the app

At the root of the project :

```bash
clever login
```

Log in the UI and close it. Then create your Python application and PostgreSQL add-on :

```bash
clever create --type node --region par HexoJS-app
```

More information on parameters [HERE](https://www.clever-cloud.com/doc/clever-tools/create/).

If needed, you can set the scaling :

```bash
clever scale --min-flavor pico --max-flavor pico
clever scale --min-instances 1 --max-instances 1
```

More information on scaling [HERE](https://www.clever-cloud.com/doc/clever-tools/manage/).

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

Nothing else left to do, just go on and deploy your app :

```bash
clever deploy
```


