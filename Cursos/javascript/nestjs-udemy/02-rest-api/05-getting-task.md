## Conteúdos

- editing services
- using service created

# editing services

## src/tasks/tasks.service.ts

```ts
import { Injectable } from "@nestjs/common";

@Injectable()
export class TasksService {
  private tasks = [];

  getAllTasks() {
    return this.tasks;
  }
}
```

## src/tasks/tasks.controller.ts

```ts
import { Controller, Get } from "@nestjs/common";
import { TasksService } from "./tasks.service";

@Controller("tasks")
export class TasksController {
  constructor(private taskServices: TasksService) {}

  @Get()
  getAllTasks() {
    return this.taskServices.getAllTasks();
  }
}
```
