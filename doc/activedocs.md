# Automate the delivery of your API documentation using a customization of the built-in CMS

This approach to automate the delivery of the API documentation leverages the
3scale ActiveDocs repository and the built-in CMS that receives a customization
of its default documentation page (`/docs`).

## How it works

The built-in CMS receives a slight customization to generate a documentation
page containing a list of all APIs (based on the list of published ActiveDocs).

This list is stored as a JSON object in the page, JavaScript code reads this object
and generates a list of APIs with their name, description and a clickable link.

The link points to the same page with a parameter in the query string that
indicates a specific API Documentation to display.

The API list is generated from the service name and description, separated by a colon.

[![Demo of this approach](https://img.youtube.com/vi/cprtnp2NNYg/0.jpg)](https://www.youtube.com/watch?v=cprtnp2NNYg)

## Prerequesites

* 3scale account with Developer Portal
* an OpenAPI Specification, version 2.0 (3scale ActiveDocs) for each service

Currently, this module expects that Services and ActiveDocs objects will have
the same system_name (in order to match a service with an ActiveDocs).

## How to install

Replace your built-in "Documentation" page (`/docs`) in the 3scale CMS with
the [content of this file](../documentation.html).

## Usage in a CI/CD pipeline

Just create and publish an ActiveDocs object with the same system_name of its
corresponding service and the documentation will appear in the documentation
page of the Developer Portal:

```sh
curl -v -X POST "https://$TENANT-admin.3scale.net/admin/api/active_docs.json" \
     -d "access_token=$ACCESS_TOKEN" -d "name=My API" -d "system_name=my_api" \
     --data-urlencode "body=$(cat /path/to/openapi.json)"  -d "published=true"
```
