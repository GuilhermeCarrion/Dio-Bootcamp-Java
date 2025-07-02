## Primeiro contato com o Spring Boot

---
A estrutura do projeto conta com três classes:  
- Classe principal **PrimeirosPassosApplication ->** inicia o Spring Boot;  
- A **Calculadora ->** um componente com a lógica (Receber dois números e soma-los);  
- E o **MyApp ->** executa o código principal e usa a Calculadora.  

---
### PrimeiroPassosApplication.java
```Java
 @SpringBootApplication
 public class PrimeiroPassosApplication{
    public static void main(String[] args){
        SpringApplication.run(PrimeiroPassosApplication.class, args);
    }
 }
 ```
💡 **Explicação**

O que acontece aqui é que a anotação "@SpringBootApplication" faz o Spring:

- Escanear todas as classes.
- Identificar os componentes(@Component, @Service, ...).
- Criar os objetos(beans) automaticamente.

E "SpringApplication.run(...)" inicia a aplicação Spring.

---
### Calculadora.java
```Java
@Component
public class Calculadora {
    public int somar(int numero1, int numero2) {
        return numero1 + numero2;
    }
}
```
💡 **Explicação**

- Com o "@Component", o Spring registra a classe Calculadora como um bean.  
- Ele irá criar uma única instância da Calculadora e guardá-la no container.  
- Sendo assim a classe fica pronta para ser injetada em qualquer aplicação.


---
### MyApp.java
```Java
@Component
public class MyApp implements CommandLineRunner {
    @Autowired
    private Calculadora calculadora;

    @Override
    public void run(String... args) {
        System.out.printf("O resultado é " + calculadora.somar(19, 20));
    }
}
```
💡 **Explicação**

- Como possui a anotação "@Component", o Spring também cria e gerencia essa aplicação.  
- A anotação "@Autowire" injeta automaticamente a instância da Calculadora aqui. E isso se chama **Injeção de Dependência**.  
- Como está implementado "CommandLineRunner", o método "run" será executado automaticamente assim que aplição for iniciada.  
