# Coordinator

The coordinator is responsible for receiving queries and samples from the
front end, and distributing them to the backend.
## Interfaces

#### Worker
```typescript
interface Worker {
    "status": "failed" | "error" | "functional"
}
```

## REST API

#### POST `/auth/login`
Request
```
{
  "username": String,
  "password": String
}
```

#### GET `/api/workers`
Return array of workers and array of WorkerId that have failed.
Response
```
{
  "workers": Array<Workers>
  "failed_workers": Array<WorkerId>
}
```

#### GET `/api/pending?worker={WorkerId}`
Returns array of samples waiting to be indexed.  
Response
```
{
  "samples": Array<SampleId>
}
```

#### GET `/api/query/status?queryId={QueryId}`
Returns status of query with Id `queryId` 
Response
```
{
  TBD
}
```

#### GET `/api/query/stream`
Subscribes user to SSE that sends updates  
Response
```
{
  TBD
}
```


#### POST `/api/query`
Request
```
{
  "username": String,
  "password": String
}
```

#### POST `/api/update`
Enqueues `samples` to be indexed on `tagetWorker`, or 
chooses a worker to send each sample to if not specified. 
Returns error with message if there is a failure to enqueue.  
Request
```
{
  "samples": Array<SampleId>,
  "targetWorker?": Array<WorkerId>
}
```