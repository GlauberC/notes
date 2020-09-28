# Conteúdos

- Criando primeiro controlador
- Criando model

### Criando primeiro controlador

- src/main/java/com---.api.controller/ClienteController.java

```java
package com.algaworks.osworks.api.controller;

import java.util.Arrays;
import java.util.List;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import com.algaworks.osworks.domain.model.Cliente;

@RestController()
public class ClienteController {

	@GetMapping("/clientes")
	public List<Cliente> listar() {
		var cliente1 = new Cliente();
		var cliente2 = new Cliente();

		cliente1.setId(1L);
		cliente1.setNome("João");
		cliente1.setTelefone("84987654321");
		cliente1.setEmail("joao@emai.com");

		cliente2.setId(2L);
		cliente2.setNome("Paula");
		cliente2.setTelefone("84987654322");
		cliente2.setEmail("paula2@emai.com");

		return Arrays.asList(cliente1, cliente2);

	}
}


```

### Criando model

- src/main/java/com---.domain.model/Cliente.java

```java
package com.algaworks.osworks.domain.model;

public class Cliente {
	private Long id;
	private String nome;
	private String email;
	private String telefone;


	public Long getId() {
		return id;
	}
	public void setId(Long id) {
		this.id = id;
	}
	public String getNome() {
		return nome;
	}
	public void setNome(String nome) {
		this.nome = nome;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public String getTelefone() {
		return telefone;
	}
	public void setTelefone(String telefone) {
		this.telefone = telefone;
	}

}

```
