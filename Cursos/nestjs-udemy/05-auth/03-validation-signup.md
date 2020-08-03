## Conteúdos

- validation signup

# validation signup

## src/auth/dto/auth.credentials.dto.ts

```ts
import { IsString, MinLength, MaxLength, Matches } from "class-validator";

export class AuthCredentialsDto {
  @IsString()
  @MinLength(4)
  @MaxLength(20)
  username: string;

  @IsString()
  @MinLength(6)
  @MaxLength(20)
  @Matches(/((?=.*\d)|(?=.*\W+))(?![.\n])(?=.*[A-Z])(?=.*[a-z]).*$/, {
    message: "password too weak",
  })
  password: string;
}
```

## src/auth/auth.controller.ts

```ts
import { Controller, Post, Body, ValidationPipe } from "@nestjs/common";
import { AuthCredentialsDto } from "./dto/auth.credentials.dto";
import { AuthService } from "./auth.service";
import { User } from "./user.entity";

@Controller("auth")
export class AuthController {
  constructor(private authService: AuthService) {}
  @Post("/signup")
  signUp(
    @Body(ValidationPipe) authCredentialsDto: AuthCredentialsDto
  ): Promise<User> {
    return this.authService.signUp(authCredentialsDto);
  }
}
```
