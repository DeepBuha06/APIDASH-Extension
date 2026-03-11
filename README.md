# API Dash - VS Code Extension PoC

A Proof of Concept VS Code extension that brings API Dash's core capabilities into VS Code.

## Features Demonstrated

- **Send HTTP Requests** - GET, POST, PUT, DELETE, PATCH with headers, params, and body
- **Code Generation** - Generate code in Python (requests), JavaScript (fetch), and cURL using the same Nunjucks templates as API Dash (identical `{{ }}` syntax as Jinja)
- **Sidebar** - TreeView showing saved requests with method icons
- **Response Viewer** - Status badge, response time, size, formatted body, and headers
- **Theme Support** - Automatic VS Code theme integration via CSS variables
- **Persistence** - Requests saved to VS Code globalState

## How This Relates to API Dash

This PoC demonstrates that API Dash's core features can work as a VS Code extension:

| API Dash (Dart/Flutter) | PoC (TypeScript/VS Code) |
|---|---|
| `jj.Template(tmpl).render(data)` (Jinja) | `nunjucks.renderString(tmpl, data)` (Nunjucks) |
| `HttpRequestModel` (Freezed) | `RequestModel` (TypeScript interface) |
| Riverpod providers | `vscode.EventEmitter` + callbacks |
| Hive storage | `context.globalState` |
| Flutter widgets | Webview HTML/CSS/JS |
| `dart:http` / better_networking | axios |

The codegen templates are **identical** between API Dash and this extension. The `{{ }}` syntax works in both Jinja (Dart) and Nunjucks (TypeScript).

## Run Locally

1. Open this folder in VS Code
2. Run `npm install`
3. Press `F5` to launch the extension in a debug window
4. Click the API Dash icon in the Activity Bar (left sidebar)
5. Click `+` to create a new request
6. Enter a URL and click Send

## Project Structure

```
src/
├── extension.ts              Entry point
├── http_client.ts            HTTP client (axios)
├── models/
│   └── request_model.ts      Data models
├── codegen/
│   ├── codegen.ts            Generator manager
│   ├── python_requests.ts    Python code gen (ported from API Dash)
│   ├── js_fetch.ts           JavaScript code gen (ported from API Dash)
│   └── curl.ts               cURL code gen (ported from API Dash)
├── sidebar/
│   └── request_tree_provider.ts   Sidebar TreeView
└── webview/
    └── request_panel.ts      Webview panel manager
media/
├── request_editor.css        UI styles (VS Code theme variables)
├── request_editor.js         UI logic
└── icon.svg                  Activity Bar icon
```
