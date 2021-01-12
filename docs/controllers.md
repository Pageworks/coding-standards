# Controllers

Controllers are allowed to the the following:

1. Handle request types (GET, PUT, POST, etc).
1. Validate request headers.
1. Validate user permissions.
1. Call service functions.
1. Respond to requests.

Controllers are **not allowed** to do the following:

1. Perform business logic.

Controllers returning JSON will respond with the following pattern:

```typescript
interface {
	success: boolean
	data: number|boolean|string|Array<any>|object
	error: null|string
}
```

Unseccussful operations will be returned with the approporite HTTP status codes ([status code reference](https://www.steveschoger.com/status-code-poster/img/status-code.png)).

Error messages will be translated and human readable. They will constructed with the understanding that they can and will be displayed to computer illiterate users.

API endpoints will follow this format: `/api/VERSION/ENDPOINT_NAME`

