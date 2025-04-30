# API Design

Some ideas how you can plan and design your APIs faster
by quickly prototyping them first.

## Rapid prototyping your APIs

If you want to playaround with your API design, you
can use tools like [JSON Server](https://github.com/typicode/json-server)
to quickly try them out.

JSON Server is used for creating following prototyping examples under `src` folder:

| Folder                                           | Description                                                            |
|--------------------------------------------------|------------------------------------------------------------------------|
| [api-operations](src/api-operations)             | Try different API operations such as GET, POST, DELETE and PATCH       |
| [async](src/async)                               | Play with long running operations API design                           |
| [auth](src/auth)                                 | See different kind of authentication options for your APIs             |
| [callback](src/callback)                         | Play with API which requires callback functionality                    |
| [entity-design](src/entity-design)               | Play with different entity design options                              |
| [internal-vs-external](src/internal-vs-external) | Compare the entity design when exposing internal and external entities |
| [media-types](src/media-types)                   | Identify the media types that you plan to use in your APIs             |
| [paths](src/paths)                               | Play with different path segmenting that you might use in your APIs    |
| [versioning](src/versioning)                     | Try version and revision concepts to map to you API requirements       |

You can try them out yourself. Just first clone this repo to your local machine and
open this workspace in Visual Studio Code. 
Then navigate to the approriate folder and run following command:

```
json-server --watch db.json --routes routes.json
```

Then you can execute the different API calls using `usage.http`
using the Visual Studio Code [Rest Client extension](https://marketplace.visualstudio.com/items?itemName=humao.rest-client).

## Use TypeSpec

[TypeSpec](https://typespec.io/)

[OpenAPI Generator](https://github.com/OpenAPITools/openapi-generator)

```typescript
import "@typespec/http";

using Http;
@service(#{ title: "Widget Service" })
namespace DemoService;

model Widget {
  id: string;
  weight: int32;
  color: "red" | "blue";
}

model WidgetList {
  items: Widget[];
}

@error
model Error {
  code: int32;
  message: string;
}

model AnalyzeResult {
  id: string;
  analysis: string;
}

@route("/widgets")
@tag("Widgets")
interface Widgets {
  /** List widgets */
  @get list(): WidgetList | Error;
  /** Read widgets */
  @get read(@path id: string): Widget | Error;
  /** Create a widget */
  @post create(@body body: Widget): Widget | Error;
  /** Update a widget */
  @patch update(@path id: string, @body body: Widget): Widget | Error;
  /** Delete a widget */
  @delete delete(@path id: string): void | Error;

  /** Analyze a widget */
  @route("{id}/analyze") @post analyze(@path id: string): AnalyzeResult | Error;
}
```

```powershell
npm install @openapitools/openapi-generator-cli -g
npm install -g @typespec/compiler

tsp init
tsp compile .

openapi-generator-cli generate -i tsp-output/schema/openapi.yaml -g aspnetcore -o tsp-output/src
```

Snippet from the generate server code:

```csharp
namespace Org.OpenAPITools.Controllers
{ 
  [ApiController]
  public class WidgetsApiController : ControllerBase
  { 
    [HttpPost]
    [Route("/widgets/{id}/analyze")]
    [ValidateModelState]
    [SwaggerOperation("WidgetsAnalyze")]
    [SwaggerResponse(statusCode: 200, type: typeof(AnalyzeResult), description: "The request has succeeded.")]
    [SwaggerResponse(statusCode: 0, type: typeof(Error), description: "An unexpected error response.")]
    public virtual IActionResult WidgetsAnalyze([FromRoute (Name = "id")][Required]string id)
    { /* ... */ }
  }
}
```

## Links

[Microsoft REST Guidelines](https://github.com/microsoft/api-guidelines)

[JSONschema.net](https://jsonschema.net)

[The OpenAPI Specification Repository](https://github.com/OAI/OpenAPI-Specification)
