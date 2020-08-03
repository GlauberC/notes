## Conteúdos

- refatoring enum status and removing model
- removing uuid

# refatoring enum status and removing model

## src/tasks/task-status.enum.ts

```ts
export enum TaskStatus {
  OPEN = "OPEN",
  IN_PROGRESS = "IN_PROGRESS",
  DONE = "DONE",
}
```

# removing uuid

```
yarn remove uuid
```
