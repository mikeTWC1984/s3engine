
# S3 Engine for Cronicle

This is updated Cronicle S3 Engine which is using version 3 of AWS SDK. Current aws-sdk (v2) package is extremly huge (150MB). This project is using @aws-sdk/client-s3 package wich is just 18MB, but you can also squeeze into about 1MB using esbuild tool!

## Setup 

### option 1 :
 
- Replace S3.js file in your current cronicle installation (opt/cronicle/node_modules/pixl-server-storage/engines/S3.js) with S3.js file from this repo
- add below packages to your cronicle:
  ```npm install @aws-sdk/client-s3 @aws-sdk/lib-storage```
- update Storage configs in your cronicle config.json using template below

### option 2 
- install esbuild tool: ```npm i esbuild -g```
- go to this project root, run command below to generate bundle:
   ```esbuild --bundle --minify --platform=node S3.js > s3.min.js```
- copy content of a bundle (s3.min.js) into S3.js on your cronicle installation (see option 1 step 1)
- update Storage params in your config.json. No need to install aws packages (those are bundled in the new file)


## Cronicle Configuration

This engine will have slighly different config then original one. Use below template to update your config.json

```json
    "Storage": {
        "engine": "S3",
        "AWS": {
            "endpoint": "http://minio:9000",
            "endpointPrefix": false,
            "forcePathStyle": true,
            "region": "us-east-1",
            "hostPrefixEnabled": false,
            "credentials": {
                "secretAccessKey": "minioadmin",
                "accessKeyId": "minioadmin"
            },
            "correctClockSkew": true,
            "maxRetries": 5,
            "httpOptions": {
                "connectTimeout": 5000,
                "timeout": 5000
            }
        },
        "S3": {
            "fileExtensions": true,
            "params": {
                "Bucket": "demo"
            }
        }
    },
```