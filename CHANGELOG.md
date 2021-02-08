# Change Log

All notable changes to this project will be documented in this file.

## [1.0.7] - 2021-02-08
#### Fixed
-   Now child/router payload are correctly merged (child has priority over any parent/router).

## [1.0.6] - 2021-02-06
#### Changed
-   Updated Babel packages.
-   Updated docs.

## [1.0.5] - 2021-01-27
#### Changed
-   License changed to MIT.
-   React Router is now a dependency (before was peerDependency) because components and hooks are bypassed, so project does not have to install 'react-router' or 'react-router-dom' as dependency, every component can be imported from this library.

## [1.0.5-alpha.0] - 2021-01-27
#### Changed
-   Documentation updates. Changelog file reference in Readme.
#### Added
-   [Experimental] React Router is now a dependency (before was peerDependency) because components and hooks are bypassed, so project does not have to install 'react-router' as dependency.

## [1.0.4] - 2021-01-25
#### Changed
-   Package peer dependencies version.

## [1.0.3] - 2021-01-24
#### Added
-   Babel with React preset.
-   Building mode for create a package distribution.
#### Fixed
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
