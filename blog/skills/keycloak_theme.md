# Customize Keycloak appearance with themes

-   Themes can be used to change the look of Keycloak pages
-   The built-in themes of keycloak can be extended to just modify the required elements of built-in theme. For example we can change the logo, colors, text etc.
-   If a independent new theme from scratch is required to be developed, it can be extended from the in-built ‘base’ theme of Keycloak
-   If just minor tweaks are intended to be done, the new theme can be extended from the existing keycloak theme

## Create a Keycloak theme

-   In the keycloak installation folder, go to themes folder and create a new folder with the theme name.
-   For example, to create a new theme named “acme”, create a new folder named “acme” in the themes folder of Keycloak folder

## Change Theme in Keycloak
* In the Keycloak admin console, go to Realm settings and select the "Themes" tab
* Here the theme for login, account, admin and email can be changed.

![keycloak_theme_settings.png](https://github.com/nagasudhirpulla/taming_python/blob/master/blog/skills/assets/img/keycloak_theme_settings.png?raw=true)

## Parts of a theme

-   A theme can have 4 parts: Login, Account, Admin, Welcome, Email for customization of login page, account page, welcome page and email content respectively

## Components of a theme

## References

-   Official documentation on Keycloak themes - [https://www.keycloak.org/docs/24.0.2/server_development/#_themes](https://www.keycloak.org/docs/24.0.2/server_development/#_themes)
-   [https://www.mastertheboss.com/keycloak/how-to-create-a-custom-keycloak-theme/](https://www.mastertheboss.com/keycloak/how-to-create-a-custom-keycloak-theme/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk0OTIyNTAwMCwxNDA5OTExODAyXX0=
-->