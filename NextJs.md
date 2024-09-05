
NextRequest:
- Extends WebRequest API.
- Request() creates a new Request object.
- Request.body() returns a ReadableStream of the body.
- Request.blob() resolves it in a Blob representation of the request body.
- Similar for Request.json(), Request.formData().

Serverless Function:

- “Serverless computing” allows devs to build and deploy applications without worrying about building and deploying applications.

Project Organization Best Practices:

- In the app directory. Each folder is a route segment that is mapped to a corresponding segment in a URL path. But a route is not publicly accessible until a page.js or route.js file is added to a route segment.
- Private folders in nextjs are achieved by prefixing a folder with an underscore.
- Route groups can be created by wrapping a folder in parenthesis. This means that the folder is for organizational purposes and should not be included in the route URL path.
-   
  
Routing:

- App router is built on React Server Components (RSC)
- Each folder in a route represents a route segment. And each route segment is mapped to a segment in the url path.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeNb9X4-T0nLfZVve8weyUnuKFZkv431CyQp_p2HkUmovpgMewsBLJMZz13e2-lXSA2OTYv7OhzNjP7r7rvi8iHvOlV1RdY8gWSSS0f2XJL7699BKLbG8cu5Yg0Ru9IgAFZkGoA89vhFGNYZ8HDLu44PVmB?key=rIXjGwndUPKZeYyOaMrbaQ)
- Layout file is the shared UI for a segment and its children.
- Page file is the unique ui.
- Loading UI is the loading ui for segment and its children.
- Route is the server side api endpoint.

Server Components:

- React Server COmponents allow you to write UI that can be rendered and optionally cached on the server.
