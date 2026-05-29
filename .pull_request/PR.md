# Implement Redis Pub/Sub real-time notification worker

Adds a Redis-backed notification worker that subscribes to transaction update channels and routes user notifications via the existing NotificationRouter. Wires the worker into the job scheduler and fixes a bug in TransactionModel.updateStatus.

## Files changed
- src/workers/notificationWorker.ts (new)
- src/jobs/scheduler.ts (start worker)
- src/models/transaction.ts (bugfix)

## Testing notes
1. Ensure `REDIS_URL` points to a running Redis instance.
2. Start the app: `npm run dev`
3. Publish test messages to Redis, e.g.:
   `redis-cli PUBLISH transaction.updated '{"id":"<txId>","status":"completed"}'`

## Acceptance criteria
- Worker subscribes to transaction channels and routes notifications via `NotificationRouter`.
- Replaces DB polling for notifications, lowers DB load, and enables sub-second notifications.

## Patch apply (git)
Apply the patch locally: `git apply .pull_request/changes.patch`
