## Conteúdos

- query simples
- query parametrizada
- fragment
- aliases

# query simples

```
query GET_AUTHORS{
  authors{
    photo{
      url
    }
    name
    role
    description
  }
}

query GET_LANDING_PAGE{
  landingPage{
    logo{
      alternativeText
      url
    }
  }
}
```

# query parametrizada

```
query GET_AUTHOR($id: ID!){
  author(id:$id){
    id
    name
    role
    description
  }
}
```

# fragment

```
fragment imageData on UploadFile{
  alternativeText
  url
}

fragment logo on LandingPage{
  logo {
    ...imageData
  }
}

fragment header on LandingPage {
  header{
      title
      description
      button{
        label
        url
      }
      image{
        ...imageData
      }
  }
}

query GET_LANDING_PAGE{
  landingPage{
    ...logo
    ...header
  }
}
```

# aliases

```
query GET_LANDING_PAGE{
  landingPage{
    createdAt:created_at
  }
}
```
