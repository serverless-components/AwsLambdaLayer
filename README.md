# AWS Lambda Layer

Easily provision Layers for AWS Lambda using [Serverless Components](https://github.com/serverless/components).

&nbsp;

1. [Install](#1-install)
2. [Create](#2-create)
3. [Configure](#3-configure)
4. [Deploy](#4-deploy)

&nbsp;


### 1. Install

```console
$ npm install -g @serverless/components
```

### 2. Create


```console
$ mkdir my-layer && cd my-layer
```

in the case of a nodejs layer, the directory should look something like this:


```
|- code
  |- index.js     # the root of your library
  |- package.json # the main property should point to index.js in this example
|- serverless.yml

```

### 3. Configure

```yml
# serverless.yml

name: my-layer
stage: dev

myLayer:
  component: "@serverless/aws-lambda-layer"
  inputs:
    name: my-layer
    description: My Serverless Layer
    code: ./code
    regoin: us-east-1
    runtimes: [ 'nodejs8.10' ] # the default is undefined (aka. all runtimes supported)

    # a path prefix to all the files that would be included in the package
    # this example would package a valid node dependency
    # since this is the path expected by aws
    prefix: nodejs/node_modules

    # if you'd like to include any files outside the codebase
    include:
      - ../external/file.js 

    # specifying an existing deployment bucket would optimise deployment speed
    # by using accelerated multipart uploads
    bucket: my-deployment-bucket
```

### 4. Deploy

```console
AwsLambdaLayer (master)$ components

  myLayer › outputs:
  name:  'my-layer'
  description:  'My Serverless Layer'
  arn:  'arn:aws:lambda:us-east-1:552760238299:layer:my-layer:1'


  29s › dev › my-layer › done

AwsLambdaLayer (master)$

```
For a real world example of how this component could be used, [take a look at how the AwsLambda component is using it](https://github.com/serverless-components/AwsLambda/blob/master/serverless.js#L64-L77).

&nbsp;

### New to Components?

Checkout the [Serverless Components](https://github.com/serverless/components) repo for more information.
