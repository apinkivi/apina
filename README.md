# 🐒 APIna

Framework to build API or MCP server for any UI built for humans only. Rebuilding should be easy because UI may change and break it.

## Test Cases

The API/MCP server is missing or there are many other reasons to build it:

- [Facebook Marketplace](/test/facebook-marketplace/desktop-browser.md)
- [Google Gemini](/test/google-gemini/desktop-browser.md) AI subscription doesn't include API use.
- [Google Tasks](/test/google-tasks/desktop-browser.md) ([spec](/test/google-tasks/spec.json)) [API v1](https://developers.google.com/workspace/tasks/reference/rest) is missing (eg. recurring) functionalities.
- [tori](/test/tori/desktop-browser.md) API isn't free.

## Architecture & Workflows

- [Application Specification Schema](/schema/apina-spec.schema.json)
- [Discovery Workflows](/docs/discovery-workflows.md)

## Layers

1. *User* layer is *AI* or *App*.
2. *Interface* layer  is *MCP* or *API*.
3. Business *Logic* layer is MarkDown files.
   - May be implemented in many languages.
4. *UI* semantics layer describes controls and views.
   - Abstracts UI elements.
5. *Automation* layer is the actual implementation.
   - Component framework (eg. Material Design) and theme.


## Examine process

```mermaid
graph TD
unexamined((Unexamined<br>app))
--> os{Open source?}
-->|yes| sourceUrl[/Source code URL/]
--> clone[Clone repository]
-->|AI| techs[[Detect technologies]]
--> impls[[Select implementation]]
--> funcs[[Detect functionalities]]
--> build(((Build<br>API)))

clone -->|AI| funcs

os -->|no| web{Web<br>app?} -->|yes| appUrl[/App URL/] --> Login -->|Wappalyzer| techs
Login -->|SeleniumIDE| funcs

web -->|no| Install --> techs
Install --> dir[/Installation dir/] -->|files| techs
```

## Implemenation selection process

```mermaid
graph TD
techs((Technologies<br>detected))
--> api{API<br>docs?}
-->|yes| ktor(((1. Ktor)))
--> mobile([a. mobile])

ktor --> server([b. server])

ktor --> desktop([c. desktop])

api -->|no| clear{Clear<br>communication?}
-->|yes| ktor

clear -->|no| web{Web app?}
-->|yes| ssr{SSR?}
-->|yes| ksoup(((2. Ktor<br>+ Ksoup)))
--> mobile

ksoup --> server

ksoup --> desktop

ssr -->|no| bot{Detects bot?}
-->|no| view(((3. WebView)))
--> mobile

bot -->|no| playwright(((3. Playwright)))
--> server

playwright --> desktop

bot -->|yes| extension(((4. Extension<br>+ Robot)))
--> desktop

web -->|no| robot(((5. Robot))) --> desktop
```
