## Conteúdos

- creating user

# creating user

## src/auth/dto/auth.credentials.dto.ts

```ts
export class AuthCredentialsDto {
  username: string;
  password: string;
}
```

## src/auth/user.repository.ts

```ts
import { Repository, Entity, EntityRepository } from "typeorm";
import { User } from "./user.entity";
import { AuthCredentialsDto } from "./dto/auth.credentials.dto";

@EntityRepository(User)
export class UserRepository extends Repository<User> {
  async signUp(authCredentialsDto: AuthCredentialsDto): Promise<User> {
    const { username, password } = authCredentialsDto;
    const user = new User();
    user.username = username;
    user.password = password;

    await user.save();

    return user;
  }
}
```

## src/auth/auth.service.ts

```ts
import { Injectable } from "@nestjs/common";
import { UserRepository } from "./user.repository";
import { InjectRepository } from "@nestjs/typeorm";
import { AuthCredentialsDto } from "./dto/auth.credentials.dto";
import { User } from "./user.entity";

@Injectable()
export class AuthService {
  constructor(
    @InjectRepository(UserRepository)
    private userRepository: UserRepository
  ) {}

  async signUp(authCredentialsDto: AuthCredentialsDto): Promise<User> {
    return this.userRepository.signUp(authCredentialsDto);
  }
}
```

## src/auth/auth.controller.ts

```ts
import { Controller, Post, Body } from "@nestjs/common";
import { AuthCredentialsDto } from "./dto/auth.credentials.dto";
import { AuthService } from "./auth.service";
import { User } from "./user.entity";

@Controller("auth")
export class AuthController {
  constructor(private authService: AuthService) {}
  @Post("/signup")
  signUp(@Body() authCredentialsDto: AuthCredentialsDto): Promise<User> {
    return this.authService.signUp(authCredentialsDto);
  }
}
```
