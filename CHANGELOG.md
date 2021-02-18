# Change Log

All notable changes to this project will be documented in this file.

## [1.0.10] - 2021-02-18
-   Changed minimum React version to 16.13.1.
-   eslint-radar instead of eslint-sonarjs.

## [1.0.9] - 2021-02-10
-   Fix payload mergin priority.

## [1.0.8] - 2021-02-09
-   Fix when no route payload defined.

## [1.0.7] - 2021-02-08
-   Now child/router payload are correctly merged (child has priority over any parent/router).

## [1.0.6] - 2021-02-06
-   Updated Babel packages.
-   Updated docs.

## [1.0.5] - 2021-01-27
-   License changed to MIT.
-   React Router is now a dependency (before was peerDependency) because components and hooks are bypassed, so project does not have to install 'react-router' or 'react-router-dom' as dependency, every component can be imported from this library.

## [1.0.5-alpha.0] - 2021-01-27
-   Documentation updates. Changelog file reference in Readme.
-   [Experimental] React Router is now a dependency (before was peerDependency) because components and hooks are bypassed, so project does not have to install 'react-router' as dependency.

## [1.0.4] - 2021-01-25
-   Package peer dependencies version.

## [1.0.3] - 2021-01-24
-   Babel with React preset.
-   Building mode for create a package distribution.
-   React import modern preset in Babel.

## [1.0.0] - 2021-01-24
-   Handles declarative JSON routing.
-   Routing generic component. RouteChild.jsx for render a page with optional
    layout and Router.jsx for rendering boilerplate generalize.
-   RouterProvider.jsx HOC for initialize application routes.
-   Routes payload declaration. Payload logic consist of a data package
    for inject in routes depending of current path.
-   Hooks for React: useRouteState, useHashValue, useQueryParams and
    useRoutePayload.
