# React SPA Routerizer

React library for application routing (based on React Router) that prevents boilerplate code.
This library eases routes definitions and routing job.
Exposes a generic Router for create base app router, some hooks and a routes service (for breadcrumbs for example).

## Structure 📋

```bash
├── README.md
├── LICENCE.md
├── CHANGELOG.md
├── .vscode/ # Visual Studio shared development config
├── src/
│   ├── router/
│   │   ├── components/
│   │   │   ├── RouteChild.jsx # handle page rendering
│   │   │   ├── Router.jsx # handle Switch and Route definitions
│   │   │   └── RouterProvider.jsx # initializes router.service
│   │   ├── router.hook.js # library hooks
│   │   └── router.service.js # handle current routes
│   └── index.js
├── package.json
├── jsconfig.js
├── .babelrc
├── .eslintrc.json
└── .prettierrc.json
```

-   **Router.jsx**: contains generic router logic.
-   **RouteChild.jsx**: render current route component (a.k.a. page) and updates document (browser tab) title.
-   **route.hook.js**: contains hooks like useRoutePayload for get specific route payload.
-   **route.service.js**: routes handler. Initializes routing. Calculates complete paths for nested routes and data for breadcrumbs.
-   **index.js**: exports router, hooks and routes handler/service.

## How To Use 💡

Should be initialized with RouterProvider on App.jsx like:
```javascript
import { RouterProvider, Router } from '@calvear/react-spa-routerizer';
import routes from 'routes'; // your routes definition JSON

export default function App()
{
    return (
        <RouterProvider routes={ routes }>
            <Router
                loader={ <div>Loading</div> }
                DefaultChild={ () => <div>Page Not Found</div> }
            />
        </RouterProvider>
    );
}
```

### Routes format are shown below:

```javascript
{
    key: 'unique-id',
    title: 'Main Page',
    path: '/',
    Layout: LayoutComponent,
    Child: PageComponent,
    payload: {
        ...
    }
}
```

- **key**: any unique string for route.
- **title**: title shown in tab browser.
- **path**: relative path of route.
- **Layout**: optional. Layout component.
- **Child**: Route/Page component.
- **payload**: optional. The payload defined for route. May be accessed with useRoutePayload hook.

### Routers format are shown below:

```javascript
{
    key: 'unique-id',
    path: '/',
    Layout: LayoutComponent,
    DefaultChild: NotFoundPage,
    payload: {
        ...
    },
    routes: [
        ...
    ]
}
```

- **key**: any unique string for router.
- **title**: optional. Title for nested routes, shown in tab browser.
- **path**: base path for nested routes.
- **Layout**: optional. Layout component for every child.
- **DefaultChild**: default component on no one defined route.
- **payload**: optional. The payload defined for router. May be accessed with useRoutePayload hook.
    Will be merged with low priority with child payload.
- **routes**: array of sub-routes.

#### Example:

```javascript
import { lazy } from 'react';

// layouts container.
const Layouts = {
    Card: lazy(() => import('layouts/card'))
};

// pages container.
const Pages = {
    Main: lazy(() => import('pages/main')),
    Detail: lazy(() => import('pages/detail')),
    UserProfile: lazy(() => import('pages/user-profile')),
    UserEdit: lazy(() => import('pages/user-edit'))
};

export default [
    {
        key: 'main-page',
        title: 'Main Page',
        path: '/',
        Layout: Layouts.Card,
        Child: Pages.Main,
        payload: {
            header: 'List of Items'
        }
    },
    {
        key: 'detail-page',
        title: 'Detail Page',
        path: '/detail/:name',
        Layout: Layouts.Card,
        Child: Pages.Detail
    },
    {
        key: 'user-router',
        path: '/user',
        Layout: Layouts.Card,
        DefaultChild: () => <div>Page Not Found</div>,
        payload: {
            header: 'User Page'
        },
        routes: [
            {
                key: 'user-profile',
                title: 'User Profile',
                path: '/profile',
                Child: Pages.UserProfile
            },
            {
                key: 'user-edit',
                title: 'User Edit',
                path: '/edit',
                Child: Pages.UserEdit
            }
        ]
    }
];
```

### Hooks

Library has some hooks for eases route state management.

- **useRoutePayload**: returns current route payload.

For this route definition:

```javascript
...

export default [
    {
        key: 'main-page',
        title: 'Main Page',
        path: '/',
        Child: Pages.Main,
        payload: {
            title: 'Main Page'
        }
    },
    ...
];
```

We can access to it's payload, at '/' path, as below:

```javascript
import { useRoutePayload } from '@calvear/react-spa-routerizer';

export default function MainPage()
{
    const { title } = useRoutePayload();

    return (
        <div id='main-page'>
            <h1>{title}</h1>
        </div>
    );
}
```

- **useQueryParams**: returns URL query parameters.

- **useHashValue**: returns URL hash value.

- **useRouteState**: returns current route state, from React Router.

Also, this library exports every hook from 'react-router' - see [React Router Hooks](https://reactrouter.com/web/api/Hooks) for more information.

- **useRouteState**: gives you access to the history instance that you may use to navigate.

- **useLocation**: returns the location object that represents the current URL.

- **useParams**: useParams returns an object of key/value pairs of URL parameters.

- **useRouteMatch**: attempts to match the current URL in the same way that a <Route> would.

## Linting 🧿

Project uses ESLint, for code formatting and code styling normalizing.

-   **eslint**: JavaScript and React linter with Airbnb React base config and some other additions.
-   **prettier**: optional Prettier config.

For correct interpretation of linters, is recommended to use [Visual Studio Code](https://code.visualstudio.com/) as IDE and install the plugins in .vscode folder at 'extensions.json', as well as use the config provided in 'settings.json'

## Changelog 📄

For last changes see [CHANGELOG.md](CHANGELOG.md) file for details.

## Built with 🛠️

-   [React](https://reactjs.org/) - the most fabulous JavaScript framework.
-   [React Router](https://reactrouter.com/) - React most popular routing library.

## License 📄

This project is licensed under the MIT License - see [LICENSE.md](LICENSE.md) file for details.

---

⌨ by [Alvear Candia, Cristopher Alejandro](https://github.com/calvear93)
