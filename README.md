# API Documentation

This repository contains the files used to build the Telephant.co.za API documentation.  Found at http://developer.telephant.co.za

The build and deploymyent process is intergrated and works like this:

When a change is committed and pushed to the main branch in this git repository (https://github.com/telephant-co-za/api-documentation.git) it triggers a Code Build pipe built on AWS.

The Code Build will use the instructions in the buildspec.yml for to launch a small linux docker container.

It will install node and some other dependencies on that little virtual machine.

Finally it will run this command:  

```redoc-cli bundle petstore.yml --output index.html```

This will build a ReDoc interface with the swagger.json file

The look and feel of Redoc is controled in the template file and integrated when the files are built.

The final step is to upload a single index.html file to a s3 bucket on AWS which is mapped on the Route 53 DNS service to http://developer.telephant.co.za

This was I can focus on the documentation in the swagger file and the rest is taken car of by the integrated build pipeline.
