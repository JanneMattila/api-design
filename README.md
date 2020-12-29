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

## Links

[Microsoft REST Guidelines](https://github.com/microsoft/api-guidelines)
