# HackCheck-ts

Official NodeJS library for the [hackcheck.io](https://hackcheck.io) API

- [HackCheck-ts](#hackcheck-ts)
  - [Installation](#installation)
  - [Quick start](#quick-start)
  - [Getting your api key](#getting-your-api-key)
  - [Other examples](#other-examples)

## Installation

```sh-session
# NPM
npm i hackcheck

# PNPM
pnpm i hackcheck

# Yarn
yarn add hackcheck
```

## Quick start

Example usage

```ts
import { HackCheckClient } from "hackcheck";

async function main() {
  const hc = new HackCheckClient("MY_API_KEY");

  const response = await hc.search({
    field: "email",
    query: "example@example.com",
  });

  console.log(response.results);
}

main();
```

## Getting your api key

1. Visit https://app.hackcheck.io/profile
2. Add your IP address in the "Authorized IP Addresses" text area and click Update
3. Copy your API key

## Other examples

<details>
<summary>Breach Monitors</summary>

```ts
import { HackCheckClient } from "hackcheck";

async function main() {
  const hc = new HackCheckClient("MY_API_KEY");

  const monitors = await hc.getMonitors();

  console.log(monitors.asset_monitors);
  console.log(monitors.domain_monitors);

  // Getting a monitor by its id
  let myAssetMonitor = await hc.getAssetMonitor("...");

  console.log(myAssetMonitor.status);
  console.log(myAssetMonitor.asset);

  // Updating a monitor
  myAssetMonitor = await hc.updateAssetMonitor("...", {
    asset: "example@example.com",
    asset_type: "email",
    notification_email: "notify-me@domain.com",
  });

  console.log(myAssetMonitor);
}

main();
```

</details>

<details>
<summary>Filtering databases</summary>

```ts
import { HackCheckClient } from "hackcheck";

async function main() {
  const hc = new HackCheckClient("MY_API_KEY");

  // This will only yield results from "website.com" and "website.org"
  const response = await hc.search({
    field: "email",
    query: "example@example.com",
    filter: {
      type: "use",
      databases: ["website.com", "website.org"],
    },
  });

  console.log(response.results);
}

main();
```

</details>

<details>
<summary>Checking if a query exists</summary>

```ts
import { HackCheckClient } from "hackcheck";

async function main() {
  const hc = new HackCheckClient("MY_API_KEY");

  // Returns true if the query is found
  const exists = await hc.check({
    field: "email",
    query: "example@example.com",
  });

  console.log(exists);
}

main();
```

</details>
