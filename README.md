# Bengal_meat endpoints documentation
The landing page of weight-logger is `/carcass_form` which is a form that takes carcass details including current value of carcass.After submitting the form it will log the carcass details in a database which can be fatched using `/summary/start_date/end_date` or `/summary/date` endpoints.

## Endpoints:  

### `/current` [GET]
- This is a GET request.
- It fatches current value from the indicator.
- This endpints return a json file like the following format  

Schema
```Schema
{
     "weight": number,
    "unit": str  
}
```
Example  
```json
{
    "weight": 39.4,
    "unit": "kg"
}
```
### `/summary/date`[GET]
- This is a GET request.
- It accepts a date as an input and returns the details of carcass on that particular day.
- For instance, if someone wants to access today's data, they can do so by entering the date(`/summary/14-06-2023`)summary/today's date.
- The serial number of the day's is shown by the key *`carcass_count`*.
- A json array in the following format will be returned.  

Schema
```schema

        [
        {
            "carcass_count": Integer,
            "carcass_id": String,
            "carcass_weight": Number,
            "weight_unit": String,
            "carcass_code": String,
            "supplier_id": String,
            "date_time": Date-iso-string
        }
        ....]
```
Example  
```json
[
    {
        "carcass_count": 1,
        "carcass_id": "320105",
        "carcass_weight": -49.8,
        "weight_unit": "kg",
        "carcass_code": "1110001",
        "supplier_id": "CUS100001",
        "date_time": "2023-06-14T16:09:34.342411Z"
    },
    {
        "carcass_count": 5,
        "carcass_id": "320108",
        "carcass_weight": -49.8,
        "weight_unit": "kg",
        "carcass_code": "1110002",
        "supplier_id": "CUS100001",
        "date_time": "2023-06-14T16:42:22.225898Z"
    },
    {
        "carcass_count": 6,
        "carcass_id": "320109",
        "carcass_weight": -49.8,
        "weight_unit": "kg",
        "carcass_code": "1110001",
        "supplier_id": "CUS100003",
        "date_time": "2023-06-14T16:43:07.207000Z"
    },
    {
        "carcass_count": 7,
        "carcass_id": "320110",
        "carcass_weight": -49.8,
        "weight_unit": "kg",
        "carcass_code": "1110001",
        "supplier_id": "CUS100001",
        "date_time": "2023-06-14T16:43:37.785487Z"
    }
    
]
```
### `/summary/start_date/end_date`[GET]
- This is also a GET request.
- All logged carcass details for a certain period are available at this endpoint.
- The endpoint accepts the start date and end date of the period as inputs (`/summary/14-06-2023/22-06-2023`).
- It will return a array of json like the following format  

Example
```json
[
    {
        "carcass_count": 1,
        "carcass_id": "320105",
        "carcass_weight": -49.8,
        "weight_unit": "kg",
        "carcass_code": "1110001",
        "supplier_id": "CUS100001",
        "date_time": "2023-06-14T16:09:34.342411Z"
    },
    {
        "carcass_count": 5,
        "carcass_id": "320108",
        "carcass_weight": -49.8,
        "weight_unit": "kg",
        "carcass_code": "1110002",
        "supplier_id": "CUS100001",
        "date_time": "2023-06-14T16:42:22.225898Z"
    },
    {
        "carcass_count": 6,
        "carcass_id": "320109",
        "carcass_weight": -49.8,
        "weight_unit": "kg",
        "carcass_code": "1110001",
        "supplier_id": "CUS100003",
        "date_time": "2023-06-14T16:43:07.207000Z"
    },
    {
        "carcass_count": 7,
        "carcass_id": "320110",
        "carcass_weight": -49.8,
        "weight_unit": "kg",
        "carcass_code": "1110001",
        "supplier_id": "CUS100001",
        "date_time": "2023-06-14T16:43:37.785487Z"
    },
    {
        "carcass_count": 1,
        "carcass_id": "320111",
        "carcass_weight": 0.0,
        "weight_unit": "kg",
        "carcass_code": "1110001",
        "supplier_id": "CUS100001",
        "date_time": "2023-06-17T17:24:45.215527Z"
    },
    {
        "carcass_count": 1,
        "carcass_id": "320112",
        "carcass_weight": 45.0,
        "weight_unit": "kg",
        "carcass_code": "1110001",
        "supplier_id": "CUS100001",
        "date_time": "2023-06-22T16:52:05.808772Z"
    }
]
```


