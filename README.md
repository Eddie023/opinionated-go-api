# wex-tag

## Overview 
This repository contains implementation that exposes APIs to Store a Purchase Transaction and Retrieve a Purchase Transaction in a Specified Countyr's Currency. 

```
API: POST {BASE_URL}/purchase

Request Body: {
    "description": "new description",
    "amount": "100.1223"
}

Response: {
    "amountInUSD": "100.12",
    "date": "2023-12-01T10:58:37.050074Z",
    "description": "new description",
    "id": "c4c1666f-2eda-49c7-99b8-635223f1330a"
}
``` 

```
API: GET {BASE_URL}/purchase/ae90db91-d278-4941-b2b0-92e3b6f666e2?country=Nepal&currency=Rupee

Response: {
    "convertedDetails": {
        "amount": "8.26608",
        "country": "'United Kingdom",
        "currency": "Pound",
        "exchangeRateDate": "2023-09-30",
        "exchangeRateUsed": "0.816"
    },
    "transactionDetails": {
        "amountInUSD": "10.13",
        "date": "2023-12-01T09:28:12.573092Z",
        "description": "new description",
        "id": "ae90db91-d278-4941-b2b0-92e3b6f666e2"
    }
}
```

### Technical Overview 
1. API Specification are described in 'openapi.yaml' file which follows OpenAPI 3.1 standard. 
2. API types are autogenerated from 'openapi.yaml' file using [oapi-codegen](github.com/deepmap/oapi-codegen/cmd/oapi-codegen) pkg. 
3. HTTP service is built using Go Chi Router. 
4. File 'pkg/api/transaction.go' contains Handler code for our two APIs
5. Package 'pkg/api/service' contains business logic required for our two APIs
6. Postgres DB is used as persistence layer and is dockerized in the codebase. 
7. [ent.go](https://entgo.io/) is used as ORM framework 

### Usage 
1. copy .env.example and create .env file with given environment variables.
1. Run "docker compose up" to initiate a postgres instance. 
2. Run "make run" command to run a go server 
3. Make curl request for new purchase transaction using "make post"
4. Get the transaction Id from output of POST request and use that to make GET request!
