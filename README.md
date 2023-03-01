# Bengal_meat endpoints documentation
Weight-logger fatches current weight from a weight indicator through the `/current` endpoint and after confirmation of this value through `/confirm` endpoint it will log the value in a database which can be fatched using `/summary/start_date/end_date` or `/summary/date` endpoints.

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
### `/confirm` [POST]
- It is a POST request.
- After fatching current value API user needs to confirm the value to log it in the database.
- Only logged values in the database are included in the `/summary` endpoints (described below).  
- If the value is not confirmed by anyone then it will not be stored in the database.
- The endpoint takes a json object as follwoing. like the same format the `/current` endpoint response.    

Schema
```schema
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
- It accepts a date as an input and returns the logged weight indicator values that were verified on that particular day.
- For instance, if someone wants to access today's data, they can do so by entering the date summary/today's date.
  summary/today's_date.
- The serial number of the day's confirmed weights is shown by the key *`weight_count`*.
- A json array in the following format will be returned.  

Schema
```schema

        [
        {
            "weight_count": Integer,
            "date_time": Date-iso-string,
            "weight": Number,
            "unit": String
        }
        ....]
```
Example  
```json
[
    {
        "weight_count": 1,
        "date_time": "2023-02-27T15:28:22.743773Z",
        "weight": 99.0,
        "unit": "kg"
    },
    {
        "weight_count": 2,
        "date_time": "2023-02-27T15:29:35.329487Z",
        "weight": 95.8,
        "unit": "kg"
    },
    {
        "weight_count": 3,
        "date_time": "2023-02-27T15:55:40.056865Z",
        "weight": 95.8,
        "unit": "kg"
    }
]
```
### `/summary/start_date/end_date`[GET]
- This is also a GET request.
- All logged values for a certain period are available at this endpoint.
- The endpoint accepts the start date and end date of the period as inputs.
- It will return a array of json like the following format  

Example
```json
[
    {
        "weight_count": 1,
        "date_time": "2023-02-27T15:28:22.743773Z",
        "weight": 99.0,
        "unit": "kg"
    },
    {
        "weight_count": 2,
        "date_time": "2023-02-27T15:29:35.329487Z",
        "weight": 95.8,
        "unit": "kg"
    },
    {
        "weight_count": 3,
        "date_time": "2023-02-27T15:55:40.056865Z",
        "weight": 95.8,
        "unit": "kg"
    },
    {
        "weight_count": 1,
        "date_time": "2023-03-01T12:21:01.197357Z",
        "weight": 13.6,
        "unit": "kg"
    },
    {
        "weight_count": 2,
        "date_time": "2023-03-01T12:21:14.434483Z",
        "weight": 84.8,
        "unit": "kg"
    }
]
```


