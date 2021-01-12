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
    data: number|boolean|string|Array<any>|object|null
    error: null|string
}
```

Unsuccessful operations will be returned with the appropriate HTTP status codes ([status code references](https://www.steveschoger.com/status-code-poster/img/status-code.png)).

Error messages will be translated and human-readable. They will be constructed with the understanding that they can and will be displayed to computer-illiterate users.

API endpoints on an apex domain will follow this format: `DOMAIN/api/VERSION/ENDPOINT`

API endpoints on an API subdomain will follow this format: `api.DOMAIN/VERSION/ENDPOINT`

### Example Controller 

```php
// Example endpoint: api/v1/products/<id:\d+>
function exampleControllerAction(int $id)
{
    $response = [
        "success" => false,
        "data" => null,
        "error" => null,
    ];

    $this->requireAcceptsJson();
    $method = $this->getRequestMethod();
    $data = $this->getRequestBody();
    $user = $this->getUser();

    switch ($method)
    {
        case "POST":
            if ($user->can("products:update"))
            {
                $response = ProductServiceClass->updateProductById($id, $data);
            }
            else
            {
                $this->setResponseStatus(401);
                $respose["error"] = "You do not have permission to update this product.";
            }
            break;
        case "DELETE":
            if ($user->can("products:delete"))
            {
                $response = ProductServiceClass->deleteProductById($id);
            }
            else
            {
                $this->setResponseStatus(401);
                $respose["error"] = "You do not have permission to delete this product.";
            }
            break;
        case "GET":
            $response = ProductServiceClass->getProductById($id);
            break;
        default:
            $this->setResponseStatus(405);
            $respose["error"] = "Invalid method type: " . $method;
            break;
    }

    return $this->respondAsJson($response);
}
```