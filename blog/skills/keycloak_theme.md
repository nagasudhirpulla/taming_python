# Customize Keycloak appearance with themes

-   Themes can be used to change the look of Keycloak pages.
-   The built-in themes of keycloak can be extended to just modify the required elements of built-in theme. For example we can change the logo, colors, text etc.
-   If a independent new theme from scratch is required to be developed, it can be extended from the in-built ‘base’ theme of Keycloak.
-   If just minor tweaks are intended to be done, the new theme can be extended from the existing keycloak theme.


## Parts of a theme

-   A theme can have 4 parts: Login, Account, Admin, Email for customization of login page, account page, admin page and email content respectively

## Change Theme in Keycloak
* In the Keycloak admin console, go to Realm settings and select the "Themes" tab.
* Here the theme for login, account, admin and email can be changed.

![keycloak_theme_settings.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_theme_settings.png?raw=true)
## Create a Keycloak theme

-   In the keycloak installation folder, go to themes folder and create a new folder with the theme name.
-   For example, to create a new theme named “acme”, create a new folder named “acme” in the themes folder of Keycloak folder.

## Anatomy of a new theme folder
* Inside the new theme folder there can be one or more folders named 'login', 'admin', 'account', 'email'.
* The theme for the respective parts can be defined in these folders.
* In this new 'acme' theme example, we will create folders for login admin and account.
* The final folder structure of this example would be as follows

```
    acme
    ├───account
    │   │   theme.properties
    │   │
    │   └───resources
    │       │   favicon.svg
    │       │   logo.svg
    │       │
    │       └───css
    │               styles.css
    │
    ├───admin
    │   │   theme.properties
    │   │
    │   └───resources
    │       │   favicon.svg
    │       │   logo.svg
    │       │
    │       └───css
    │               styles.css
    │
    └───login
        │   theme.properties
        │
        ├───messages
        │       messages_en.properties
        │
        └───resources
            ├───css
            │       styles.css
            │
            └───img
                    favicon.ico
                    keycloak-bg.png
                    keycloak-logo-text.png
```
### theme.properties file
* This file defines the theme type
* The `theme.properties` file of login folder of acme theme in this example is as follows

```bash
parent=keycloak
import=common/keycloak

styles=css/login.css css/styles.css
``` 

* `parent` means the parent theme from which the theme is being extended from.
*  `import` is used to define the parent theme folder to import resources from.
* `styles` is used to define the css files to be used in the theme. Note that we have defined only styles.css file. But we need to also mention the css file path being used in parent theme also. Hence the value of `styles` is kept as `css/login.css css/styles.css` . Multiple css file paths should be separated by a space and the order should start from parent files to child files since the file paths in the right override the file paths in the left.
*   `scripts` - JavaScript files can also be added to theme using `script`. This can be used add additional JavaScript code to browser 

## View existing keycloak themes for inspiration

- In the lib\lib\main\ folder of keycloak installation folder, keycloak theme jar files can be found.
- Use a tool like 7zip or winrar to see the files inside the jar file.
- In the jar file with name like `org.keycloak.keycloak-themes-24.0.2.jar`, the login and email theme files of “keycloak” and the "base" theme can be found. These themes can be used to extend the login and email theme types in the new theme.
- In the jar file with name like `org.keycloak.keycloak-admin-ui-24.0.2.jar`, the admin theme files of “keycloak-v2” theme can be found.
- In the jar file with name like `org.keycloak.keycloak-account-ui-24.0.2.jar`, the account theme files of “keycloak-v3” theme can be found.


## References

-   Official documentation on Keycloak themes - [https://www.keycloak.org/docs/24.0.2/server_development/#_themes](https://www.keycloak.org/docs/24.0.2/server_development/#_themes)
-   [https://www.mastertheboss.com/keycloak/how-to-create-a-custom-keycloak-theme/](https://www.mastertheboss.com/keycloak/how-to-create-a-custom-keycloak-theme/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NTAxMDY1MDIsLTE4MjI5NjAzMDAsLT
ExNTkxNDg4NjIsLTE3MTIwNTk1NSwzMTU1NzgxMjcsMTQwOTkx
MTgwMl19
-->