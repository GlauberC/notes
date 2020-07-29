## Conteúdos

- create a model

# create a model

## src/tasks/task.model.ts

```ts
export interface Task {
  id: string;
  title: string;
  description: string;
  status: TaskStatus;
}

export enum TaskStatus {
  OPEN = "Open",
  IN_PROGRESS = "IN_PROGRESS",
  DONE = "DONE",
}
```

## src/tasks/tasks.service.ts

```ts
import { Injectable } from "@nestjs/common";
import { Task } from "./task.model";

@Injectable()
export class TasksService {
  private tasks: Task[] = [];

  getAllTasks(): Task[] {
    return this.tasks;
  }
}
```

## src/tasks/tasks.controller.ts

```ts
import { Controller, Get } from "@nestjs/common";
import { TasksService } from "./tasks.service";
import { Task } from "./task.model";

@Controller("tasks")
export class TasksController {
  constructor(private taskServices: TasksService) {}

  @Get()
  getAllTasks(): Task[] {
    return this.taskServices.getAllTasks();
  }
}
```
