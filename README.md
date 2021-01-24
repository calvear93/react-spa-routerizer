# [React SPA Routerizer](https://github.com/calvear93/react-spa-routerizer)

React library for application routing (based on React Router) that prevents boilerplate code.
This library eases routes definitions and routing job.
Exposes a generic Router for create base app router, some hooks and a routes service (for breadcrumbs for example).

## Structure 💡

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
├── .eslintrc.json # ESLint config
└── .prettierrc.json # Prettier config
```

-   **Router.jsx**: contains generic router logic.
-   **RouteChild.jsx**: render current route component (a.k.a. page) and updates document (browser tab) title.
-   **route.hook.js**: contains hooks like useRoutePayload for get specific route payload.
-   **route.service.js**: routes handler. Initializes routing. Calculates complete paths for nested routes and data for breadcrumbs.
-   **index.js**: exports router, hooks and routes handler/service.

## How To Use

Should be initialized with RouterProvider on App.jsx like:
```javascript
import { RouterProvider, Router } from '@calvear/react-spa-routerizer';
import AppRouter, { routes } from 'routes';

export default function App()
{
    return (
        <RouterProvider routes={ routes }>
            <Router
                loader={ <div>Cargando</div> }
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
        secured: true,
        header: 'Lista de Pokémons'
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
        secured: true
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

## Linting 🧿

Project uses two linters, for code formatting and code styling normalizing.

-   **eslint**: JavaScript and React linter with Airbnb React base config and some other additions.
-   **prettier**: optional Prettier config.

For correct interpretation of linters, is recommended to use [Visual Studio Code](https://code.visualstudio.com/) as IDE and install the plugins in .vscode folder at 'extensions.json', as well as use the config provided in 'settings.json'

## Built with 🛠️

-   [React](https://reactjs.org/)
-   [Redux Router](https://reactrouter.com/) - React most popular routing library.

## License 📄

This project is licensed under the GPL License - see [LICENSE.md](LICENSE.md) file for details.

---

⌨ by [Alvear Candia, Cristopher Alejandro](https://github.com/calvear93)
