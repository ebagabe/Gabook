## DAL e DAO

Se você já ouviu falar em DAO escrito com a letra "o", pode se perguntar qual a diferença entre esta escrita e a de DAL com "l". Sim, são diferentes

- DAO (Data Access Object)
- DAL (Data Access Layer)

O DAL é a camada de acesso a dados que promove a abstração desses dados e vai emitir todos os comandos de SELECT, INSERT, UPDATE e DELETE de maneira separada da lógica das classes do projeto e independente da fonte de dados, enquanto o DAO é um objeto de banco de dados que representa um banco aberto.

Basicamente, o DAL representa a estrutura de acesso aos dados, independente do tipo de banco utilizado, e o DAO é o objeto que representa o acesso a uma fonte de dados específica. 

## Documentações sugeridas:

- [Data Access Layers](https://learn.microsoft.com/en-us/aspnet/web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs)
- [Data Access Object](https://learn.microsoft.com/pt-br/cpp/mfc/dao-classes?view=msvc-170)