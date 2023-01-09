# java-solid




SOLID with Java




Use advanced object-oriented concept.

Writing cohesive code with the Single Responsibility principle.

Learn how to use acomplish.

Know how to deal with coupling.

Understand the benefits of encapsulation in depth.

Master solid code principles.

[freecodecamp](https://www.freecodecamp.org/portuguese/news/os-principios-solid-da-programacao-orientada-a-objetos-explicados-em-bom-portugues/)


### S - Single responsibility Principle

O método reajustarSalario() foi criado na classe ReajusteService, tornando essa classe reponsável únicamente por realizar ajustes nos salárioa dos funcionários.

O antigo método reajustarSalario foi removido da classe funcionario, tornando essa classe mais coesa.

```java
// CLASS FUNCIONARIO
public void reajustarSalario(Funcionario funcionario, BigDecimal aumento) {
  BigDecimal salarioAtual = funcionario.getSalario();
  BigDecimal percentualReajuste = aumento.divide(salarioAtual, RoundingMode.HALF_UP);
  if (percentualReajuste.compareTo(new BigDecimal("0.4")) > 0) {
    throw new ValidacaoException("Reajuste nao pode ser superior a 40% do salario!");
  } 
  BigDecimal salarioReajustado = salarioAtual.add(aumento); 
  funcionario.atualizarSalario(salarioReajustado);
}
```

### Open / Closed Principle

Foi criado uma classe para cada validação criada, e implementada a inferface de ValidacaoReajuste. Interface criada para padronizar os dados necessarios para todas as validações de reajuste de salário.
Dessa forma, cada classe de validação terá de ser alterar em sua própria classe, e se por ventura não tiver a necessidade dessa classe no projeto, ela poderá ser excluida sem o menor problema.
Com isso nós tornamos as classes mais extensíveis.
"Entidades de software (classes, módulos e funções, etc.) devem estar abertas para extensão, porém fechadas para modificação." --Bertrand Mever

```Java
public interface ValidacaoReajuste {
  void validar(Funcionario funcionario, BigDecimal aumento);
}
```

### Liskov Substitution Principle



### Interface Segregation Principle

Classes não devem ser obrigadas a implementar métodos que não irão precisar.

### Dependency Inversion Principle

Caso uma determinada implementação mude, não seremos afetados, pois dependemos apenas de sua interface.

```Java
private List<ValidacaoReajuste> validacoes;
 
public void reajustarSalarioDoFuncionario(Funcionario funcionario, BigDecimal aumento) {
  this.validacoes.forEach(v -> v.validar(funcionario, aumento));
		
	BigDecimal salarioReajustado = funcionario.getSalario().add(aumento);
	funcionario.atualizarSalario(salarioReajustado);
}
```
