## SOLID

Solid é um acrônimo que representa cinco princípios de design de software orientado a objetos que visam criar sistemas mais compreensíveis, flexíveis e de fácil manutenção. Cada letra de SOLID representa um princípio. 

- S -> Single Responsibility Principle (Principio de responsabilidade única)
- O -> Open/Closed Principle (Principio de Aberto/Fechado)
- L -> Liskov Substitution Principle (Principio de Substituição de Liskov)
- I -> Interface Segregation Principle (Principio de Segregação de Interface)
- D -> Dependency Inversion Principle (Principio da Inversão de Dependência)

## Single Responsibility Principle

*Cada classe deve ter uma única responsabilidade ou motivo para mudar*

```csharp

    public class RelatorioServico
    {
        public void GerarRelatorio(string dados)
        {
            // Gera o relatorio
        }
    }

    public class RelatorioRepositorio
    {
        public void SalvarRelatorio(string relatorio)
        {
            // Salva o relatório no banco de dados
        }
    }

    // Separando as responsabilidades de geração e salvamento do relatório
```

## Open/Closed Principle

Classes devem estar abertas para extensão, mas fechada para modificação

```csharp

    public abstract class Forma
    {
        public abstract double CalcularArea();
    }

    public class Retangulo : Forma
    {
        public double Largura { get; set; }
        public double Altura { get; set; }

        public override double CalcularArea()
        {
            return Largura * Altura;
        }
    }

    public class Circulo : Forma
    {
        public double Raio { get; set; }

        public override double CalcularArea()
        {
            return Math.PI * Raio * Raio;
        }
    }

    // Adicionar novas formas não requer modificação nas classes existentes
```

## Liskov Substituition Principle

Objetos de uma classe derivada devem ser substituíveis por objetos de classe base sem alterar o comportamento correto do programa.

```csharp

    public class Pato
    {
        public virtual void Quack()
        {
            Console.WriteLine("Quack!");
        }
    }

    public class PatoDeBorracha : Pato
    {
        public override void Quack()
        {
            Console.WriteLine("Squeak!");
        }
    }

    // Pato de borracha pode substituir Pato sem problemas

    Pato pato = new PatoDeBorracha();
    pato.Quack(); // Output: Squeak!
```

## Interface Segregation Principle 

Clientes não devem ser forçados a depender de interfaces que não utilizam

```csharp

    public interface IImpressora
    {
        void Imprimir();
    }

    public interface IScanner
    {
        void Scanear();
    }

    public class Impressora : IImpressora
    {
        public void Imprimir()
        {
            // Implementação da impressão
        }
    }

    public class Scanner : IScanner
    {
        public void Scanear()
        {
            // Implementação da scanner
        }
    }

    // As classes não precisam implementar métodos que não usam
```

## Dependency Inversion Principle

Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações.

```cs

    public interface IRepositorio
    {
        void Adicionar(string dado);
    }

    public class RepositorioSql: IRepositorio
    {
        public void Adicionar (string dado)
        {
            // Implementação para adicionar no banco de dados SQL
        }
    }

    public class Servico
    {
        private readonly IRepositorio _repositorio;

        public Servico(IRepositorio repositorio)
        {
            _repositorio = repositorio;
        }

        public void Executar(string dado)
        {
            _repositorio.Adicionar(dado);
        }
    }

    // A classe Servico depende da abstração IRepositorio, não da implementação específica
```

## Exemplos Incorretos para cada um dos princípios

### Single Responsability Principle

```cs

    public class Relatorio
    {
        public void GerarRelatorio(string dados)
        {

        }

        public void SalvarRelatorio(string relatorio)
        {

        }

        public void EnviarEmailRelatorio(string email, string relatorio)
        {

        }
    }

    // A classe tem multiplas responsabilidades: gerar, salvar e enviar o relatório
```

### Open/Closed Principle

```cs
public class CalculadoraDeArea
{
    public double CalcularAreaRetangulo(double largura, double altura)
    {
        return largura * altura;
    }

    public double CalcularAreaCirculo(double raio)
    {
        return Math.PI * raio * raio;
    }
}

// Para adicionar novas formas como um triangulo é necessário modificar a classe CalculadoraDeArea
```

## Liskov Substituition Principle

```cs
public class Pato
{
    public virtual void Quack()
    {
        Console.WriteLine("Quack!");
    }
}

public class PatoDeBorracha : Pato
{
    public override void Quack()
    {
        throw new NotImplementedException("Pato de borracha não faz quack!");
    }
}

// PatoDeBorracha não pode substituir Pato de forma segura, pois lança uma exceção ao chamar Quack.
```

### Interface Segregation Principle

```cs

public interface IMultifuncional
{
    void Imprimir();
    void Scanear();
    void EnviarFax();
}

public class Impressora : IMultifuncional
{
    public void Imprimir()
    {
        // Implementação da impressão
    }

    public void Scanear()
    {
        throw new NotImplementedException();
    }

    public void EnviarFax()
    {
        throw new NotImplementedException();
    }
}

// A impressora é forçada a implementar métodos que não utiliza
```

### Dependency Inversion Principle

```cs

public class Servico
{
    private readonly RepositorioSql _repositorio;

    public Servico()
    {
        _repositorio = new RepositorioSql();
    }

    public void Executar(string dado)
    {
        _repositorio.Adicionar(dado);
    }
}

public class RepositorioSql
{
    public void Adicionar(string dado)
    {
        // Implementação para adicionar no banco de dados SQL
    }
}

// A classe servico depende diretamente da implementação concreta de RepositorioSql dificultando a troca de repositórios ou o teste unitário
```