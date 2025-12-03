This work-in-progress documentation repository contains notes about how Mnemian™ (https://mnemian.net) handles data retrieved from AtoM. 

## Documentation Folders
- `/mapping-atom-to-ric/` contains an overview of our methodology, and individual files detailing how we process each field returned by AtoM API endpoints. 

## Retrieval from AtoM

Mnemian currently uses these existing AtoM API endpoints:
- `GET /api/informationobjects`*
- `GET /api/informationobjects/<slug>`

***Note:** We have modified the `informationobjects` API to return the `id` and `parent_id` of each record. We have done this so that we can reconstruct the information hierarchy, and then retrieve a set of child descriptions for each top-level record by using the `id` as a filter parameter.

### Example:
```
/api/informationobjects "topLod=1"
```
Returns:
```json
{ "total":7,
  "results":[
    {
      "reference_code":"Ref code",
      "slug":"slug",
      "title":"Title of first record",
      "repository":"Name or Repository",
      "level_of_description":"Collection",
      "creators":["Name of creator"],
      "creation_dates":["Creation date"],
      "id":4189,
      "parent_id":1
    },
    {
      "reference_code":"Ref code",
      "slug":"slug",
      "title":"Title of second record",
      "repository":"Name or Repository",
      "level_of_description":"Collection",
      "creators":["Name of creator"],
      "creation_dates":["Creation date"],
      "id":6294,
      "parent_id":1
    }
    ...etc. 
]}
```

### New API endpoints...

We have built two new API endpoints in AtoM, for `actor` and `repository` data.  Links will be added here once those are published.  We intend to offer them to the AtoM project for inclusion in a future release of AtoM.
