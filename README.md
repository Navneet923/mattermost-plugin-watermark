# Mattermost Plugin Watermark
![CircleCI branch](https://img.shields.io/circleci/project/github/scottleedavis/mattermost-plugin-watermark/master.svg)

A plugin for [Mattermost](https://mattermost.com) that uses a [steganography library](https://github.com/auyer/steganography) to add a hidden string in an image that identifies an image as having been uploaded to the server.

Currently supports PNG files.  
Planned JPG support too.

##### Decode
To view the encoded message/watermark in the file, run `go run decode.go`.  For example:
```bash
$ go run decode.go assets/test.png 
This is an image that has been uploaded to Mattermost
```


##### Build
```
make
```

This will produce a single plugin file (with support for multiple architectures) for upload to your Mattermost server:

```
dist/com.example.my-plugin.tar.gz
```

There is a build target to automate deploying and enabling the plugin to your server, but it requires configuration and [http](https://httpie.org/) to be installed:
```
export MM_SERVICESETTINGS_SITEURL=http://localhost:8065
export MM_ADMIN_USERNAME=admin
export MM_ADMIN_PASSWORD=password
make deploy
```

Alternatively, if you are running your `mattermost-server` out of a sibling directory by the same name, use the `deploy` target alone to  unpack the files into the right directory. You will need to restart your server and manually enable your plugin.

In production, deploy and upload your plugin via the [System Console](https://about.mattermost.com/default-plugin-uploads).

```

### How do I build the plugin with unminified JavaScript?
Use `make debug-dist` and `make debug-deploy` in place of `make dist` and `make deploy` to configure webpack to generate unminified Javascript.
