## Conteúdos

- install uuid
- create task service method
- post task controller method

# install uuid

```
yarn add uuid
```

# create task service method

## src/tasks/tasks.service.ts

```ts
import { Injectable } from "@nestjs/common";
import { Task, TaskStatus } from "./task.model";
import { v4 as uuidv4 } from "uuid";

@Injectable()
export class TasksService {
  private tasks: Task[] = [];

  getAllTasks(): Task[] {
    return this.tasks;
  }

  createTask(title: string, description: string): Task {
    const task: Task = {
      id: uuidv4(),
      title,
      description,
      status: TaskStatus.OPEN,
    };

    this.tasks.push(task);

    return task;
  }
}
```

# post task controller method

## src/tasks/tasks.controller.ts

```ts
import { Controller, Get, Post, Body } from "@nestjs/common";
import { TasksService } from "./tasks.service";
import { Task } from "./task.model";

@Controller("tasks")
export class TasksController {
  constructor(private taskServices: TasksService) {}

  @Get()
  getAllTasks(): Task[] {
    return this.taskServices.getAllTasks();
  }

  @Post()
  createTask(
    @Body("title") title: string,
    @Body("description") description: string
  ): Task {
    return this.taskServices.createTask(title, description);
  }
}
```
