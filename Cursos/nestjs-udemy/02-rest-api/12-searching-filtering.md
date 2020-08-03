## Conteúdos

- createDto
- change getAllTasks to getTasks and editing

# createDto

## src/tasks/dto/get-tasks-filter.dto.ts

```ts
import { TaskStatus } from "../task.model";

export class GetTasksFilterDto {
  status: TaskStatus;
  search: string;
}
```

# change getAllTasks to getTasks and editing

## src/tasks/tasks.service.ts

```ts
import { Injectable, Get } from "@nestjs/common";
import { Task, TaskStatus } from "./task.model";
import { v4 as uuidv4 } from "uuid";
import { CreateTaskDto } from "./dto/create-task.dto";
import { GetTasksFilterDto } from "./dto/get-tasks-filter.dto";

@Injectable()
export class TasksService {
  private tasks: Task[] = [];

  getAllTasks(): Task[] {
    return this.tasks;
  }

  getTasksWithFilters(filterDto: GetTasksFilterDto): Task[] {
    const { status, search } = filterDto;

    let tasks = this.getAllTasks();

    if (status) {
      tasks = tasks.filter((task) => task.status === status);
    }
    if (search) {
      tasks = tasks.filter(
        (task) =>
          task.title.includes(search) || task.description.includes(search)
      );
    }
    return tasks;
  }

  getTaskById(id: string): Task {
    return this.tasks.find((task) => task.id === id);
  }

  createTask(createTaskDto: CreateTaskDto): Task {
    const { title, description } = createTaskDto;

    const task: Task = {
      id: uuidv4(),
      title,
      description,
      status: TaskStatus.OPEN,
    };

    this.tasks.push(task);

    return task;
  }

  deleteTask(id: string): void {
    this.tasks = this.tasks.filter((task) => task.id !== id);
  }

  updateTaskStatus(id: string, status: TaskStatus): Task {
    const task = this.getTaskById(id);

    task.status = status;

    return task;
  }
}
```

## src/tasks/tasks.controller.ts

```ts
import {
  Controller,
  Get,
  Post,
  Body,
  Param,
  Delete,
  Patch,
  Query,
} from "@nestjs/common";
import { TasksService } from "./tasks.service";
import { Task, TaskStatus } from "./task.model";
import { CreateTaskDto } from "./dto/create-task.dto";
import { GetTasksFilterDto } from "./dto/get-tasks-filter.dto";

@Controller("tasks")
export class TasksController {
  constructor(private taskServices: TasksService) {}

  @Get()
  getTasks(@Query() filterDto: GetTasksFilterDto): Task[] {
    if (Object.keys(filterDto).length) {
      return this.taskServices.getTasksWithFilters(filterDto);
    } else {
      return this.taskServices.getAllTasks();
    }
  }

  @Get("/:id")
  getTaskById(@Param("id") id: string): Task {
    return this.taskServices.getTaskById(id);
  }

  @Post()
  createTask(@Body() createTaskDto: CreateTaskDto): Task {
    return this.taskServices.createTask(createTaskDto);
  }

  @Delete("/:id")
  deleteTask(@Param("id") id: string): void {
    this.taskServices.deleteTask(id);
  }

  @Patch("/:id/status")
  updateTaskStatus(
    @Param("id") id: string,
    @Body("status") status: TaskStatus
  ): Task {
    return this.taskServices.updateTaskStatus(id, status);
  }
}
```
