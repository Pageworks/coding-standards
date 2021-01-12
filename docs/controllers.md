# Controllers

Controllers are allowed to do the following:

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

Unsuccessful operations will be returned with the appropriate HTTP status codes ([status code references](https://www.steveschoger.com/status-code-poster/img/status-code.png)).

Error messages will be translated and human readable. They will be constructed with the understanding that they can and will be displayed to computer illiterate users.

API endpoints on an apex will follow this format: `DOMAIN/api/VERSION/ENDPOINT`

API endpoints on an API subdomain will follow this format: `api.DOMAIN/VERSION/ENDPOINT`

