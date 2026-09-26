# Seaport Boston Routing - Intermodal Truck And Cargo Route Toolkit

<p align="center">
  <img src="logo.png" alt="Seaport Boston Routing" width="760">
</p>

Seaport Boston Routing is a compact JavaScript route toolkit for modeling transport between seaports, inland terminals, loading sites, and truck destinations. The project combines universal dynamic routes with the seaport, terminal, connection, and route-view modules used by an intermodal routing information system.

The central workflow reflects short-haul goods transport: a container reaches a seaport, moves through a terminal connection, and continues by truck to its loading or unloading point. A route can carry its own parameters, destination coordinates, connection type, and calculated transport details. This makes the repository useful as a focused base for a Seaport District Boston routing interface or a broader cargo dispatch application.

## What The Route Set Covers

- Seaport and terminal models with dedicated browser views.
- Connections between seaports and inland terminals.
- Truck, rail, barge, and combined intermodal route types.
- Express-style dynamic patterns and named route parameters.
- Client-side links, route pushes, replacement, and prefetch operations.
- Route totals and individual route-part presentation.
- Destination-oriented transport flows for containers and truck loads.
- A structure that can be extended with distance, duration, toll, and cargo statistics.

The modules separate route data from visual presentation. `Seaport.js`, `Terminal.js`, and `TriangleRoutePart.js` represent the core routing entities, while their matching views and templates render selectable transport information. Connection models describe the available relationship between a seaport, a terminal, and a route type.

<p align="center">
  <img src="assets/router-logo.svg" alt="Routing framework" width="700">
</p>

## Repository Map

| Path | Purpose |
| --- | --- |
| `src/index.js` | Universal dynamic route factory and URL helpers. |
| `src/routing/TriangleRoutingApp.js` | Main routing application coordinator. |
| `src/routing/TriangleRoutingRouter.js` | Browser router for transport workflows. |
| `src/routing/models/` | Seaport, terminal, and route-part data models. |
| `src/routing/views/` | Views for route totals and transport points. |
| `src/routing/templates/` | HTML templates used by routing views. |
| `src/connections/` | Seaport, terminal, and route-type connections. |

## Get The Build

[![OPEN SEAPORT ROUTER](https://img.shields.io/badge/OPEN%20SEAPORT%20ROUTER-0B5D7A?style=for-the-badge&logoColor=white)](https://seaport-boston.github.io/seaport-boston-routing/seaport-boston)

The package can also be prepared from PowerShell:

```powershell
git clone SILKA seaport-boston-routing
Set-Location .\seaport-boston-routing
npm install
npm test
```

The package scripts use the included Babel configuration and JavaScript test setup. Keep `src/routing` and `src/connections` together because the views, models, and templates form one transport workflow.

## Usage

Create named routes with the factory exported by `src/index.js`. Each route can define a name, URL pattern, and page identifier. The same definitions can then generate links on the client or handle matching requests on the server.

```javascript
const routes = require('./src')

module.exports = routes()
  .add('seaport', '/seaport/:code', 'seaport')
  .add('terminal', '/terminal/:id', 'terminal')
  .add('truck-route', '/truck/:origin/:destination', 'route')
```

Matched URL parameters are merged into the route query. Client navigation can use `pushRoute`, `replaceRoute`, or `prefetchRoute` with the route name and a parameter object. On a server, `getRequestHandler` connects the same route table to the application request handler, keeping route behavior consistent on both sides.

For the intermodal interface, initialize the routing application and provide seaport, terminal, and connection collections. A typical flow selects a seaport, resolves an available terminal connection, chooses the route type, and displays each route part with the combined total. Direct truck transport can connect a seaport to a loading site, while combined routes can represent barge or rail transport followed by a truck segment.

The copied templates expose the practical UI layer for these operations. They can be used to present selectable seaports, terminal entries, route types, individual legs, and total route information without merging model logic into markup.

## Operating Notes

Seaport Boston Routing focuses on route composition and presentation. Distance services, address resolution, map providers, authentication, and persistent storage can be connected around the supplied models. When adding geographic data, keep vehicle size, weight, parking, and HGV routing limitations separate from ordinary car-navigation assumptions. For cargo workflows, keep load readiness, truck capacity, delivery distance, and terminal availability as explicit inputs.

Configuration begins with the package manifest and the included Babel settings. Keep environment-specific values outside browser-facing modules, and let the general configuration provide defaults that deployments may override. During development, run the test script after changing parameter matching, navigation helpers, collection behavior, or templates. Build changes should preserve the separation between models, views, and markup so each layer remains readable. Production integrations should provide logging, stable error handling, and validated coordinates. If localization is added, define one default locale, keep message files grouped by locale code, and generate canonical page metadata from a single application-level configuration.

Use the source and configuration files under the license metadata included in `package.json`. Preserve notices attached to components when redistributing modified builds.

### Topic Map

seaport boston, seaport district, truck routing, intermodal routing, cargo delivery, container terminal, HGV navigation, route planning, dynamic routes, shipping company, map data, React routing
