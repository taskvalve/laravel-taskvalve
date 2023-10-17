# Usage

```typescript
import * as taskvalve from "https://deno.land/x/taskvalve@1.0.4/mod.ts"
import { load } from "https://deno.land/std@0.204.0/dotenv/mod.ts"

const env = await load()

const crypto = new taskvalve.DefaultCrypto(env['APP_NAME'], env['APP_KEY'])
const model = new taskvalve.model.PostgreSQL(crypto, env['DB_HOST'], env['DB_PORT'], env['DB_NAME'], env['DB_USER'], env['DB_PASS'])
const queue = new taskvalve.queue.Redis(crypto, model, env['REDIS_HOST'], env['REDIS_PORT'])

const workflow = new taskvalve.WorkflowStub(queue)

const workflowId = await workflow.start('App\\Workflows\\Simple\\SimpleWorkflow', [])

await workflow.signal(workflowId, 'setReady', [true])
```
