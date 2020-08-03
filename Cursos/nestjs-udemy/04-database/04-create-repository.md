## Conteúdos

- Creating repository

# Creating repository

## src/tasks/task.repository.ts

```ts
import { Repository, EntityRepository } from "typeorm";
import { Task } from "./task.entity";

@EntityRepository(Task)
export class TaskRepository extends Repository<Task> {}
```

## src/tasks/tasks.module.ts

```ts
import { Module } from "@nestjs/common";
import { TasksController } from "./tasks.controller";
import { TasksService } from "./tasks.service";
import { TypeOrmModule } from "@nestjs/typeorm";
import { TaskRepository } from "./task.repository";

@Module({
  imports: [TypeOrmModule.forFeature([TaskRepository])],
  controllers: [TasksController],
  providers: [TasksService],
})
export class TasksModule {}
```
