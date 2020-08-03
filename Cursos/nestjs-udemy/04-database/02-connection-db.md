## Conteúdos

- Install Typeorm and Pg libraries
- configure typeorm

# Install Typeorm and Pg libraries

```
yarn add @nestjs/typeorm typeorm pg
```

# configure typeorm

## src/config/typeorm.config.ts

```ts
import { TypeOrmModuleOptions } from "@nestjs/typeorm";

export const typeOrmConfig: TypeOrmModuleOptions = {
  type: "postgres",
  host: "localhost",
  port: 5432,
  username: "postgres",
  password: "cursos",
  database: "nestjstaskmanagement",
  entities: [__dirname + "/../**/*.entity.{js,ts}"],
  synchronize: true,
};
```

## src/app.module.ts

```ts
import { Module } from "@nestjs/common";
import { TasksModule } from "./tasks/tasks.module";
import { TypeOrmModule } from "@nestjs/typeorm";
import { typeOrmConfig } from "./config/typeorm.config";

@Module({
  imports: [TasksModule, TypeOrmModule.forRoot(typeOrmConfig)],
})
export class AppModule {}
```
