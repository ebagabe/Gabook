## Entity Framework

O EF é um ORM (Object-Relational Mapping). Foi desenvolvido pela Microsoft. Ele permite que os desenvolvedores trabalhem com dados relacionais usando objetos .NET, eliminando a necessidade de grande parte do código SQL de baixo nivel que seria necessário de outra forma.

- *Modelos de Dados*: O EF permite criar um modelo de dados a partir de um banco de dados existente (Database First), criar um banco de dados a partir de um modelo de dados (Model First) ou definir o modelo de dados por meio de classes de código (Codigo First)

- *Consulta de dados*: Com EF, é possivel consultar dados usando LINQ (Language Integrated Query), que permite escrever consultas usando a sintaxe de linguagem de programação .NET, gerando uma integração mais fluida e intuitiva

- *Trabalhando com Objetos*: Permite que os desenvolvedores trabalhem com dados como objetos de domínio, usando as mesmas técnicas e padrões usados em outros aspectos do desenvolvimento de software orientado a objetos.

- *Migrações*: O EF oferece suporte a migrações de banco de dados, permitindo que os desenvolvedores atualizem a estrutura do banco de dados de forma incremental, sincronizando as mudanças no modelo de dados com o banco de dados físico.

- *Lazy Loading e Eager Loading*: Suporta lazy loading, onde os dados relacionados são carregados sob demanda, e eager loading, onde os dados relacionados são carregados antecipadamente, oferecendo flexibilidade na maneira como os dados são recuperados.

## Como instalar para SQL Server (Visual Studio)

No Visual Studio basta seguir: Ferramentas -> Gerenciador de Pacotes do Nugget -> Gerenciar Pacotes do Nugget para Solução:

- Na aba de Procurar busca por `Entity Framework` e selecione `Microsoft.EntityFrameworkCore.SqlServer` e instale no seu projeto.

- Para criar um contexto (Conexao com banco de dados), você deve utilizar o nome da sua aplicação + Context: `NomeDaAplicacaoContext.cs`

```cs
using Microsoft.EntityFrameworkCore;

public class NomeDaAplicacaoContext : DbContext
{
    private string connectionString = "Server=<host>,<port>;Database=<DataBaseName>;User Id=<NomeDeUser>;Password=<Senha>;Encrypt=False;";

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer(connectionString);
    }
}
```