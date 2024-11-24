Definição: OOP é o estilo de programação que utiliza `classes` como elemento principal para a construção de um software.

Classe é um estrutura de programação que descreve as características e comportamento de um objeto.

Objeto é um elemento criado e colocado na memória para ser utilizado em um software. O processo de criar um objeto é chamado de `Instanciação`.

Modelos de programação: Orientada a Objetos, Estruturada, Orientada a Eventos e Orientada a Aspectos.

Programação estruturada:

- `Comando 1`
- `Comando 2`
- `Comando 3`
- `Comando 4`

```
Scanner sc = new Scanner(System.in);

System.out.print("Enter a number: ")

int number = sc.nexInt();

System.out.println("-")

System.out.println("Você digitou: " + number)

sc.close()
```

Programação Orientada a Objetos:

Classes e Objetos
- Classe: É um modelo ou estrutura que define as propriedades (atributos) e comportamentos (métodos) de um objeto.
- Objeto: É um instância de uma classe, representando uma entidade específica.

```java
class Person {

	// Atributos
	String name;
	int age;

	// Método
	void greeting() {
		System.out.println("Olá, meu nome é " + name + " e eu tenho " + age + " anos de idade.");
	}
}


public class Main {
	public static void main(String[] args) {
		// Criando objetos
		Person person = new Person();
		person.name = "Wilder";
		person.age = 21;

		// Chamando o método greeting.
		person.greeting();
	}
}
```


Abstração
- Destaca os aspectos essenciais de uma entidade e oculta os detalhes desnecessários.
- Abstração é o processo de focar nos processos principais e não na implementação real.
- A abstração é útil para construir sistemas complexos, separando as funcionalidades em partes menores.
- A implementação concreta deve ser feita apenas quando o problema a ser resolvido estiver totalmente compreendido.


Encapsulamento
- Protege os dados internos de uma classe, permitindo acesso controlado por meio de métodos públicos (getters e setters)
- O motorista não precisa saber como o motor funciona, mas apenas interagir com o carro por meio de ações simples, como ligar, desligar e acelerar. O motor é uma parte interna do carro, e seus detalhes devem ser "escondidos" do motorista.
- É o ato de ocultar detalhes da implementação e tornar público apenas o necessário para a classe realizar as tarefas para as quais foi criada.

```java
class Person {
	private String name;
	private int age;

	// Getter para name
	public String getName() {
		return name;
	}

	// Setter para name
	public void setName(String name) {
		this.name = name;
	}

	// Getter para age
	public int getAge() {
		return age;
	}

	// Setter para age com validação
	public void setAge(int age) {
		if (age >= 0) {
			this.age = age;
		} else {
			System.out.println("Erro: Idade inválida!");
		}
	}
}

public class Main {
	public static void main(String[] args) {
		Person person = new Person();
		person.setName("Wilder");
		person.setAge(-21);
		person.setAge(21);

		System.out.println("Nome: " + person.getName() + ", Idade: " + person.getAge() + " anos");
	}
}
```


Herança
- Permite que um classe (subclasse) herde atributos e métodos de outra classe (superclasse).
- Classes abstratas (abstract)construídas para servir de base para outras classes. Não podem ser instanciadas diretamente.

Imagine um sistema para gerenciar diferentes tipos de funcionários em uma empresa. Há um **funcionário genérico**, mas alguns têm características específicas, como gerentes e desenvolvedores.

```java
class Employee {
	protected String name;
	protected double salary;

	public Employee(String name, double salary) {
		this.name = name;
		this.salary = salary;
	}

	public void displayDetails() {
		System.out.println("Funcionário: " + name + ", Salário: R$ " + salary);
	}
}

class Manager extends Employee {
	private double bonus;

	public Manager(String name, double salary, double bonus) {
		super(name, salary); // Chama o construtor da classe base
		this.bonus = bonus;
	}

	public void displayDetails() {
		System.out.println("Gerente: " + name + ", Salário: R$ " + salary + ", Bônus: R$ " + bonus);
	}
}

class Developer extends Employee {
	private String language;

	public Developer(String name, double salary, String language) {
		super(name, salary);
		this.language = language;
	}

	public void displayDetails() {
		System.out.println("Desenvolvedor: " + name + ", Salário: R$ " + salary + ", Linguagem: " + language);
	}
}


public class Main {
	public static void main(String[] args) {
		Employee employee = new Employee("William", 3000.00);
		Manager manager = new Manager("Stephane", 8000.00, 2000.00);
		Developer developer = new Developer("Wilder", 5000.00, "Java");

		employee.displayDetails();
		manager.displayDetails();
		developer.displayDetails();
	}
}
```

Sistema de pagamento onde diferentes métodos de pagamento (como boleto e cartão) herdam de uma classe abstrata.

```java
abstract class Payment {
	protected double value;

	public Payment(double value) {
		this.value = value;
	}

	// Método abstratos (sem implementação)
	public abstract void makePayment();

	public void displayValue() {
		System.out.println("Valor do pagamento: R$ " + value);
	}
}

// Subclasse Boleto
class PaymentSlip extends Payment {
	public PaymentSlip(double value) {
		super(value);
	}

	@Override
	public void makePayment() {
		System.out.println("Pagamento de R$ " + value + " realizado via Boleto.");
	}
}

// Subclasse Cartão

class Card extends Payment {
	public Card(double value) {
		super(value);
	}

	@Override
	public void makePayment() {
		System.out.println("Pagamento de R$ " + value + " realizado via Cartão.");
	}
}


public class Main {
	public static void main(String[] args) {
		// Usando abstração para ocultar detalhes específicos
		Payment payment = new PaymentSlip(500.00);
		Payment payment2 = new Card(200.00);

		payment.displayValue();
		payment.makePayment();
		
		System.out.println("-");
		
		payment2.displayValue();
		payment2.makePayment();
	}
}
```


Polimorfismo
- Um método ou objeto pode se comportar de maneiras diferentes dependendo do contexto.

Imagine um sistema para processar pagamentos de diferentes tipos de contas: **Cartão de Crédito**, **Conta Corrente** e **Carteira Digital**. Cada um tem uma forma diferente de processar o pagamento.

```java
abstract class Payment {
	protected double value;

	public Payment(double value) {
		this.value = value;
	}

	public abstract void processPayment();
}

class CreditCard extends Payment {
	private String cardNumber;

	public CreditCard(double value, String cardNumber) {
		super(value);
		this.cardNumber = cardNumber;
	}

	@Override
	public void processPayment() {
		System.out.println("Pagamento de R$ " + value + " processado no Cartão de Crédito: " + cardNumber);
	}
}

class CurrentAccount extends Payment {
	private String accountNumber;

	public CurrentAccount(double value, String accountNumber) {
		super(value);
		this.accountNumber = accountNumber;
	}

	public void processPayment() {
		System.out.println("Pagamento de R$ " + value + " debitado da Conta Corrente: " + accountNumber);
	}
}

class DigitalWallet extends Payment {
	private String email;

	public DigitalWallet(double value, String email) {
		super(value);
		this.email = email;
	}

	public void processPayment() {
		System.out.println("Pagamento de R$ " + value + " realizado pela Carteira Digital: " + email);
	}
}


public class Main {
	public static void main(String[] args) {
		// polimorfismo: usando a classe base para referenciar diferentes tipos de pagamentos.
		Payment[] payments = new Payment[3];
		payments[0] = new CreditCard(100.50, "2143-6587-8967-4523");
		payments[1] = new CurrentAccount(250.75, "896745-1");
		payments[2] = new DigitalWallet(75.00, "developer.wilder@gmail.com");

		for (Payment payment : payments) {
			System.out.println("-");
			payment.processPayment();
		}
	}
}
```
