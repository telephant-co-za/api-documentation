# API Documentation

This repository contains the files used to build the Telephant.co.za API documentation.  Found at http://developer.telephant.co.za

The build and deploymyent process is intergrated and works like this:

* When a change is committed and pushed to the main branch in this git repository (https://github.com/telephant-co-za/api-documentation.git) it triggers a Code Build Pipeline built on AWS.
* The Code Build will use the instructions in the buildspec.yml file to launch a small linux docker container.
* It will install node and some other dependencies on that virtual machine.
* Finally it will run this command:  ```redoc-cli bundle telephant-api-documentation.yml --options.theme.colors.primary.main=orange --output index.html```
* This will build a ReDoc interface with the telephant-api-documentation.yml file and output a non-dependent html file
* The look and feel of Redoc is controlled by the theme parameter and a Telephant logo has been integrated using the x-image parameters in the yaml file.
* The final step is to upload a few files to a S3 bucket on AWS which is mapped on the Route 53 DNS service to http://developer.telephant.co.za
* The file api_spec is where the actually editing of the API documentation occurs.  It uses the API Blueprint format.  I found this easier than YAML to edit.
* I use the the tool found at https://www.apimatic.io/ to convert the Blueprint file to YAML.  This is a manual process currently.

With this code build pipeline in place I can focus on the API technicalities.  This pipeline was also learnings for deployment of the components like static site, SPA and API.
