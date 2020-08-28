## Conteúdos

- create service
- edit controller

# create service

```
nest g service tasks --no-spec
```

# edit controller

## src/tasks/tasks.controller.ts

```ts
import { Controller } from "@nestjs/common";
import { TasksService } from "./tasks.service";

@Controller("tasks")
export class TasksController {
  constructor(private taskServices: TasksService) {}
}
```
