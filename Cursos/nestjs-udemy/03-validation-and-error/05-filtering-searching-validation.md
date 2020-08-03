## Conteúdos

- searching and filtering status validation

# searching and filtering status validation

## src/tasks/dto/get-tasks-filter.dto.ts

```ts
import { TaskStatus } from "../task.model";
import { IsOptional, IsIn, IsNotEmpty } from "class-validator";

export class GetTasksFilterDto {
  @IsOptional()
  @IsIn([TaskStatus.DONE, TaskStatus.OPEN, TaskStatus.IN_PROGRESS])
  status: TaskStatus;

  @IsOptional()
  @IsNotEmpty()
  search: string;
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
  UsePipes,
  ValidationPipe,
} from "@nestjs/common";
import { TasksService } from "./tasks.service";
import { Task, TaskStatus } from "./task.model";
import { CreateTaskDto } from "./dto/create-task.dto";
import { GetTasksFilterDto } from "./dto/get-tasks-filter.dto";
import { TaskStatusVallidationPipe } from "./pipes/task-status-validation.pipe";

@Controller("tasks")
export class TasksController {
  constructor(private taskServices: TasksService) {}

  @Get()
  getTasks(@Query(ValidationPipe) filterDto: GetTasksFilterDto): Task[] {
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
  @UsePipes(ValidationPipe)
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
    @Body("status", TaskStatusVallidationPipe) status: TaskStatus
  ): Task {
    return this.taskServices.updateTaskStatus(id, status);
  }
}
```
