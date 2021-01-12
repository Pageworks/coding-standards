# Controllers

Controllers are allowed to the the following:

- Handle request types (GET, PUT, POST, etc).
- Validate request headers.
- Validate user permissions.
- Call service functions.
- Respond to requests.

Controllers are **not allowed** to do the following:

- Perform business logic.

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

