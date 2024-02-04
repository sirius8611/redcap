---
layout: default
title: API Documentation 
nav_order: 7
---
# API Usage

REDCap is a fairly complete program, which comes with an extensive API and API documentation. In order to check out the API documentation, you can visit the link:

- https://{yourURL}/api/help

in which the API documentation will be displayed.

However, there is another way to access the API documentation. After creating a project, there is a button called "API" and "API Playground" that can lead you to the API

## Example of using REDCap API to pull the data from a project to poewrBI visualisation.
```M
let
    url = "https://{yourdomain}/api/",
    body = "token={your_project_token}&content=record&action=export&format=csv&type=flat&csvDelimiter=&rawOrLabel=raw&rawOrLabelHeaders=raw&exportCheckboxLabel=false&exportSurveyFields=false&exportDataAccessGroups=false&returnFormat=json",
    data = Web.Contents(url,
    [ 
        Headers = [#"Content-Type"="application/x-www-form-urlencoded", #"Accept" = "application/json"],
        Content=Text.ToBinary(body)
    ]
    ),
    Source = Csv.Document(data)
in
    Source
```