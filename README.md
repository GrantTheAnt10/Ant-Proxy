# Ant Proxy

A web proxy that runs entirely in the browser. Open `index.html`, type an
address, browse.

## Running it

Open `index.html`. That's it — there's no server to start.

HTTP happens inside the page using a WebAssembly client (libcurl.js) carried
over a WebSocket **Wisp** relay, with an acorn-based AST rewriter for
`location` references. Tabbed browsing and a PDF viewer are built in.

## Where traffic goes

Through a built-in pool of public Wisp relays — `definitelyscience.com`,
`nebulaproxy.io`, `wisp.mercurywork.shop` and others. The page benchmarks them
on load and remembers the fastest.

These are run by other people. Everything you browse through it, including
anything you sign into, passes through infrastructure you don't control. The
trade is deliberate: no bandwidth or CPU cost on a machine of your own, and
your IP isn't the exit for anyone else's traffic. Just don't sign into
anything you'd mind someone else seeing.

## Notes

- Font Awesome is fetched from `cdnjs.cloudflare.com` at load, so icons need
  the network and the page isn't fully offline-capable. That request happens
  before any proxying.
- Bundles acorn, libcurl.js, epoxy-tls and pdf.js. Only acorn currently carries
  its licence notice; the others' should be added before distributing this
  further.
- Not a VPN. It only covers what you load through it.
- Changing the tab's name and icon changes appearance only. It hides nothing
  from network logs or from monitoring software on a managed device.

## History

A self-hosted version that routed through a proxy you ran yourself lived here
until `243ea06`. If you want it back:

```
git show 5e5a5f4:server.js  > server.js
git show 5e5a5f4:index.html > index.html
```