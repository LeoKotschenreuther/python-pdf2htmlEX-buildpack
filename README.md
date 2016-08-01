# Cloud Foundry Python Buildpack
[![CF Slack](https://s3.amazonaws.com/buildpacks-assets/buildpacks-slack.svg)](http://slack.cloudfoundry.org)


A Cloud Foundry [buildpack](http://docs.cloudfoundry.org/buildpacks/) for Python based apps.

This is based on the [Cloud Foundry Python Buildpack](https://github.com/cloudfoundry/python-buildpack).

This buildpack supports running Django and Flask apps.

This buildpack includes pdf2htmlEX which can be called as a shell command.

### Buildpack User Documentation

Official buildpack documentation can be found at http://docs.cloudfoundry.org/buildpacks/python/index.html.

### Building the Buildpack

1. Make sure you have fetched submodules

  ```bash
  git submodule update --init
  ```

1. Get latest buildpack dependencies

  ```shell
  BUNDLE_GEMFILE=cf.Gemfile bundle
  ```

1. Build the buildpack

  ```shell
  BUNDLE_GEMFILE=cf.Gemfile bundle exec buildpack-packager [ --uncached | --cached ]
  ```

1. Use in Cloud Foundry

    Upload the buildpack to your Cloud Foundry and optionally specify it by name

    ```bash
    cf create-buildpack custom_python_buildpack python_buildpack-cached-custom.zip 1
    cf push my_app -b custom_python_buildpack
    ```

### Testing
Buildpacks use the [Machete](https://github.com/cloudfoundry/machete) framework for running integration tests.

To test a buildpack, run the following command from the buildpack's directory:

```
BUNDLE_GEMFILE=cf.Gemfile bundle exec buildpack-build
```

More options can be found on Machete's [Github page.](https://github.com/cloudfoundry/machete)

### How to use pdf2htmlEX in the buildpack

pdf2htmlEX can be used as a shell command. The following example shows how to use it in a python app:
```
import os

os.system("pdf2htmlEX --data-dir ./vendor/pdf2htmlEX/data-dir/ aPdfFile.pdf anHtmlFile.html"
```
Keep in mind, every time we want to call pdf2htmlEX we need to pass the ```--data-dir``` parameter and the following directory in order to tell pdf2htmlEX where to look for the manifest and other important files. 

### Contributing

Find our guidelines [here](./CONTRIBUTING.md).

### Help and Support

Join the #buildpacks channel in our [Slack community] (http://slack.cloudfoundry.org/) if you need any further assistance.

### Reporting Issues

Open a GitHub issue on this project [here](https://github.com/cloudfoundry/python-buildpack/issues/new)

### Active Development

The project backlog is on [Pivotal Tracker](https://www.pivotaltracker.com/projects/1042066)
