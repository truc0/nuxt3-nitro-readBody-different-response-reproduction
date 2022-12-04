# Reproduction of different output of `readBody`

## Description

The output of `readBody(event)` function gives different response in `pnpm run dev -o` mode and `wrangler dev` mode.

> `wrangler dev` mode is for cloudflare worker

When running with `pnpm run dev -o`, the output of `readBody(event)` gives an JSON object, but when running with `wrangler dev`, the output of `readBody(event)` gives a buffer.

The `pnpm run dev -o` log as follow:

```js
{ hello: 'world' }
```

while the cloudflare worker version log as follow:

```js
<Buffer 7b 22 68 65 6c 6c 6f 22 3a 22 77 6f 72 6c 64 22 7d>
```

## Reproduction

Install the depencies first:

```bash
pnpm i  # you may choose npm instead
```

### Node server

```bash
pnpm run dev -o
```

### Cloudflare worker

To run the cloudflare worker version of code, you need to build nuxt first:

```bash
# docs: https://nitro.unjs.io/deploy/providers/cloudflare
NITRO_PRESET=cloudflare pnpm run build
```

Then set up dev server:

```bash
pnpx wrangler dev --local  # you may use pnpx
```

Click the button in index page to send a request to server and get output from the terminal.
