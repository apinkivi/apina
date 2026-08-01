# 🐒 APIna

Build API for any UI

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
--> web{Web app?}
-->|yes| ssr{SSR?}
-->|yes| ktor(((Ktor +<br>Ksoup)))
--> mobile([Mobile])

ktor --> server([Server])

ktor --> desktop([Desktop])

ssr -->|no| driver{WebDriver<br>allowed?} -->|yes| selenium(((Selenium))) --> server
selenium --> desktop

driver -->|no| extension(((Extension<br>+ Robot))) --> desktop

web -->|no| robot(((Robot))) --> desktop
```
