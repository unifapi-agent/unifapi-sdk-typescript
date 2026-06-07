# @unifapi/sdk

TypeScript SDK for the [UnifAPI](https://unifapi.com) public-data API.

UnifAPI gives agents and applications one HTTP surface for public-data workflows
such as KOL pricing, creator research, social listening, competitive
intelligence, and market research.

> This package is generated from the UnifAPI OpenAPI spec with
> [`@hey-api/openapi-ts`](https://heyapi.dev). Do not edit `src/` by hand — it is
> regenerated from the spec and force-pushed on each release.

## Install

```bash
npm install @unifapi/sdk
# or: pnpm add @unifapi/sdk
```

The package has no runtime dependencies — the fetch client is bundled.

## Usage

Every operation is a tree-shakeable function named `<method><Path>` (for example
`getHackerNewsMaxItem`, `postBrowserMarkdown`, `getXUsersByUsername`). Request and
response types ship from the same import.

```ts
import { client, getHackerNewsMaxItem } from "@unifapi/sdk";

// Configure the API key once. baseUrl defaults to https://api.unifapi.com.
client.setConfig({ auth: () => process.env.UNIFAPI_API_KEY });

const { data, error } = await getHackerNewsMaxItem();
if (error) throw error;
console.log(data);
```

Pass a request body or query/path params through the typed `options` argument:

```ts
import { postBrowserMarkdown } from "@unifapi/sdk";

const { data } = await postBrowserMarkdown({
  body: { url: "https://example.com" },
});
```

You can also scope configuration to a single call instead of the shared client:

```ts
await getHackerNewsMaxItem({
  baseUrl: "https://api.unifapi.com",
  auth: () => process.env.UNIFAPI_API_KEY,
});
```

## Auth

UnifAPI authenticates with a workspace API key sent as a Bearer token:

```http
Authorization: Bearer $UNIFAPI_API_KEY
```

Create a key from the UnifAPI dashboard at `https://api.unifapi.com/sign-in`.

## MCP

For agent clients, prefer the hosted MCP server:

```text
https://mcp.unifapi.com
```

It lets an agent discover operations, inspect schemas, and call live public-data
APIs through `list_operations`, `get_operation`, and `call_api`.

## Links

- Developer resources: `https://unifapi.com/developers`
- OpenAPI: `https://unifapi.com/openapi.json`
- Docs: `https://docs.unifapi.com`
- MCP registry manifest: `https://unifapi.com/server.json`
