## Conteúdos

- update
- update parametrizado
- create
- delete

# update

```
mutation UPDATE_AUTHOR{
  updateAuthor(
    input: {
      where:{
         id:1
      }, data:{
        name: "Willian Justen"
      }
    }
  ){
    author{
      id
      name
      role
    }
  }
}
```

# update parametrizado

```
mutation UPDATE_AUTHOR($id: ID!, $data: editAuthorInput){
  updateAuthor(input: {where:{ id:$id }, data:$data}){
    author{
      id
      name
      role
    }
  }
}
```

# create

```
mutation CREATE_AUTHOR {
  createAuthor(
    input: {
      data: {
        name: "Glauber Carvalho"
        role: "Desenvolvedor"
        description: "Um cara bem legal"
      }
    }
  ) {
    author {
      id
      name
      role
    }
  }
}

```

# delete

```
mutation DELETE_AUTHOR {
  deleteAuthor(
    input: {
      where:{id: 5}
    }
  ) {
    author {
      id
    }
  }
}

```
