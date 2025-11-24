# @resonatehq/cloudflare

`@resonatehq/cloudflare` is the official binding to deploy Distributed Async Await, Resonate's durable execution framework, to [Cloudflare Workers](https://workers.cloudflare.com). Run long-running, stateful applications on short-lived, stateless infrastructure.

**Examples:**

- [Durable Countdown]()
- [Durable, Recursive Research Agent]()

## Architecture

When the Durable Function awaits a pending Durable Promise (for example on `yield* context.rpc()` or `context.sleep`), the Cloudflare Workers function **terminates**. When the Durable Promise completes, the Resonate Server resumes the Durable Function by invoking the Cloudflare Workers function again.

```ts
function* factorial(context: Context, n: number): Generator {
  if (n <= 0)  { 
    return 1;
  }
  else {
    return n * (yield* context.rpc(factorial, n - 1));
  }
}
```

Illustration of executing `factorial(2)` on Cloudflare Workers:

![Resonate on Serverless](./public/resonate.svg)

## Quick Start

```bash
npm install @resonatehq/cloudflare
```

See [Cloudflare Workers documentation](https://developers.cloudflare.com/workers/) to learn how to develop and deploy Cloudflare Workers and see Resonate's Cloudflare Workers examples for a step by step tutorial:

- [Durable Countdown](https://github.com/resonatehq-examples/example-countdown-cloudflare-ts)
- [Durable, Recursive Research Agent](https://github.com/resonatehq-examples/example-openai-deep-research-agent-cloudflare-ts)
