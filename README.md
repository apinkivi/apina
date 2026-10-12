# 🐒 APIna

Build API for any UI

## Layers

1. *User* layer is *AI* or *App*.
2. *Interface* layer  is *MCP* or *API*.
3. Business *Logic* layer is MarkDown files.
   - May be implemented in many languages.
4. *UI* semantics layer describes controls and views.
   - Abstracts UI elements.
5. *Automation* layer is the actual implementation.
   - Component framework (eg. Material Design) and theme.


## Commands

- `gradlew dependencyUpdates --no-configuration-cache --no-parallel -Dorg.gradle.warning.mode=none` - Report updates
- `gradlew wrapper --gradle-version 9.7.0-rc-3 --distribution-type all` - Update Gradle wrapper
- `gradlew spotlessApply --no-configuration-cache` - Format Kotlin source

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
