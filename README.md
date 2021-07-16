# API Documentation

This repository contains the files used to build the Telephant.co.za API documentation found at http://developer.telephant.co.za

The build and deployment process is continuously integrated and works as follows:

* A Code Build Pipeline developed on AWS is triggered when a modification to the swagger file is committed and published to the main branch in this git repository.
* Code Build will use the instructions in the buildspec.yml file to launch a mini linux docker container, which will install node and other dependencies on the docker instance.
* Code Build will then run this command:  ```redoc-cli bundle telephant-api-documentation.yml --options.theme.colors.primary.main=orange --output index.html```
* The telephant-api-documentation.yml file will be used to create a ReDoc interface, which will output a non-dependent html file.
* The theme parameter controls Redoc's appearance, and the x-image parameters in the yaml file have been used to integrate a Telephant logo.
* Finally, the created files are stored in an AWS S3 bucket.
* The AWS Route 53 service associates the subdomain http://developer.telephant.co.za with the S3 bucket's index.html.
