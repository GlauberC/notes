## Conteúdos

- testing update task status

# testing update task status

## src/tasks/tasks.service.spec.ts

```ts
import { Test } from "@nestjs/testing";
import { TasksService } from "./tasks.service";
import { TaskRepository } from "./task.repository";
import { GetTasksFilterDto } from "./dto/get-tasks-filter.dto";
import { TaskStatus } from "./task-status.enum";
import { NotFoundException } from "@nestjs/common";
import { CreateTaskDto } from "./dto/create-task.dto";

const mockUser = { id: 12, username: "Test user" };

const mockTaskRepository = () => ({
  getTasks: jest.fn(),
  findOne: jest.fn(),
  createTask: jest.fn(),
  delete: jest.fn(),
});

describe("TasksServices", () => {
  let tasksService;
  let taskRepository;

  beforeEach(async () => {
    const module = await Test.createTestingModule({
      providers: [
        TasksService,
        { provide: TaskRepository, useFactory: mockTaskRepository },
      ],
    }).compile();

    tasksService = await module.get<TasksService>(TasksService);
    taskRepository = await module.get<TaskRepository>(TaskRepository);
  });

  describe("getTasks", () => {
    it("gets all tasks from the repository", async () => {
      taskRepository.getTasks.mockResolvedValue("someValue");
      expect(taskRepository.getTasks).not.toHaveBeenCalled();

      const filters: GetTasksFilterDto = {
        status: TaskStatus.IN_PROGRESS,
        search: "Some search query",
      };
      const result = await tasksService.getTasks(filters, mockUser);
      expect(taskRepository.getTasks).toHaveBeenCalled();
      expect(result).toEqual("someValue");
    });
  });

  describe("getTaskById", () => {
    it("calls taskRepository.findOne() and successfully retrieve and return the task", async () => {
      const mockTask = {
        title: "Teste task",
        description: "Test desc",
      };
      taskRepository.findOne.mockResolvedValue(mockTask);

      const result = await tasksService.getTaskById(1, mockUser);
      expect(result).toEqual(mockTask);
      expect(taskRepository.findOne).toHaveBeenCalledWith({
        where: {
          id: 1,
          userId: mockUser.id,
        },
      });
    });
    it("throws an error as task is not found", () => {
      taskRepository.findOne.mockResolvedValue(null);
      expect(tasksService.getTaskById(1, mockUser)).rejects.toThrow(
        NotFoundException
      );
    });
  });
  describe("createTask", () => {
    it("calls taskRepository.createTask and return a created task", async () => {
      const createTaskDto: CreateTaskDto = {
        title: "Some task",
        description: "Some description",
      };
      expect(taskRepository.createTask).not.toHaveBeenCalled();
      taskRepository.createTask.mockResolvedValue("someTask");
      const result = await tasksService.createTask(createTaskDto, mockUser);
      expect(taskRepository.createTask).toHaveBeenCalledWith(
        createTaskDto,
        mockUser
      );
      expect(result).toEqual("someTask");
    });
  });
  describe("deleteTask", () => {
    it("calls taskRepository.delete to delete a task", async () => {
      taskRepository.delete.mockResolvedValue({ affected: 1 });
      expect(taskRepository.delete).not.toHaveBeenCalled();
      await tasksService.deleteTask(1, mockUser);
      expect(taskRepository.delete).toHaveBeenCalledWith({
        id: 1,
        userId: mockUser.id,
      });
    });
    it("throws an error as task could not be found", () => {
      taskRepository.delete.mockResolvedValue({ affected: 0 });
      expect(taskRepository.delete).not.toHaveBeenCalled();

      expect(() => tasksService.deleteTask(1, mockUser)).rejects.toThrow(
        NotFoundException
      );
    });
  });
  describe("updateTaskStatus", () => {
    it("updates a task status", async () => {
      const saveMethod = jest.fn().mockResolvedValue(true);

      tasksService.getTaskById = jest.fn().mockResolvedValue({
        status: TaskStatus.OPEN,
        save: saveMethod,
      });
      expect(tasksService.getTaskById).not.toHaveBeenCalled();
      expect(saveMethod).not.toHaveBeenCalled();
      const result = await tasksService.updateTaskStatus(
        1,
        TaskStatus.DONE,
        mockUser
      );
      expect(tasksService.getTaskById).toHaveBeenCalled();
      expect(saveMethod).toHaveBeenCalled();
      expect(result.status).toEqual(TaskStatus.DONE);
    });
  });
});
```
