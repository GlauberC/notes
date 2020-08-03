## Conteúdos

- using docker to create db

# using docker to create db

```
docker run --name cursos -e POSTGRES_PASSWORD=cursos -p 5432:5432 -d postgres
```
