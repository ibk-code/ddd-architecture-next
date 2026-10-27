The app uses the Next.js App Router. Pages and layouts in `app/` are Server Components by default, and route segments can stream.

## Where code goes

Add a route under `app/`. Keep the components, hooks, and styles used by that route next to it.

`components/` is for UI shared by more than one route. Do not create it for a single screen.

`public/` holds static assets such as images and icons.

Shared helpers that are not tied to one route can live in `lib/` once they exist. Server-side data access belongs in a Server Component, a route handler under `app/api/`, or a small module in `lib/` that those call. Do not add a root `Api/` folder or a browser client that every page calls.

Do not add a global client store. Use server data, the URL, or cookies. Add a client store only when several client components must share state that does not belong in the URL. Keep hooks next to the client components that use them.

When a request needs a redirect, rewrite, or header change, add `proxy.ts`. It runs on the Node.js runtime.

## Styling

Tailwind CSS is the styling system. `app/globals.css` is the only Tailwind entry. It imports the global partials:

- `css/abstracts/_variable.css` for tokens
- `css/base/_base.css` and `css/base/_typography.css` for element defaults
- `css/utils/helper.css` for shared helper classes

Route-specific styles stay with that route. Tailwind preflight is the CSS reset.

## Data and request APIs

`fetch` is not cached unless the call sets a cache option. In a page, layout, or route handler, await `params`, `searchParams`, `cookies()`, `headers()`, and `draftMode()` before reading them.

## Runtime

The app targets Node.js 24 or newer. See `package.json` for the Next.js, React, TypeScript, and Tailwind versions.
