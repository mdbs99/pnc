# Pascal Naming Conventions

Este documento apresenta a minha versão atualizada do guia de estilo clássico do Object Pascal, originalmente elaborado por Charlie Calvert para a Borland na época do lançamento do Delphi.

A linguagem Object Pascal é case-insensitive, característica que facilita a curva de aprendizado de iniciantes, pois, diferentemente de linguagens case-sensitive, o compilador Pascal é significativamente mais permissivo quanto à declaração da maioria dos tokens (tipos, variáveis, constantes, etc.) que compõem um programa. Entretanto, essa mesma permissividade pode resultar em inconsistências visuais do mesmo código entre diferentes unidades, além de favorecer conflitos de nomenclatura causados por ambiguidade de tokens dentro de uma mesma unidade ou entre unidades distintas.

Após mais de 25 anos de atuação profissional com Object Pascal, defini um conjunto de regras de nomenclatura baseadas em prefixos e padrões estruturais que podem ser aplicadas a qualquer tipo de projeto Pascal.

A adoção desses prefixos facilita o code completion da IDE, elimina praticamente todas as ambiguidades, melhora a legibilidade e a organização do projeto.

## Nomenclatura

### Definições

- **Project**: nome do seu projeto
- **Context**: Contexto único
- **Name**: Nome/finalidade

### Tokens

- **Units (Project Context Name)**: Acme.Foo.Model, Acme.Bar.Model, Acme.Foo.Controller, Acme.Bar.EditForm
- **Interfaces (I Context Name)**: IFooModel, IBarModel, IFooController, IBarEditForm
- **Tipos (T Context Name)**: TFooModel, TBarModel, TFooController, TBarEditForm
- **Ponteiro (P Context Name)**: PFooModel, PBarModel, PFooController, PBarEditForm
- **Fields (f Name)**: fModel, fController, fEditForm
- **Arguments (a Name)**: aModel, aController, aEditForm
- **Unit Variables (v Context Name)**: vFooModel, vBarModel, vFooController, vBarEditForm
- **Local Variables (v Name)**: vModel, vController, vEditForm
- **Unit Constants (_ Context _ Name**): _FOO_VALUE, _BAR_VALUE, _FOO_BAR_VALUE
- **Local Constants (_ Name**): _VALUE, _TOKEN_VALUE
- **Event Properties (On Name)**: OnEdit, OnCalculate
- **Event Implementations (Do Name)**: DoEdit, DoCalculate

## Comentários

- Sempre acima dos tipos e métodos, devem iniciar com "///" a descrição principal
- Linhas opcionais, com detalhes, devem ser iniciadas por "// -"
- Se a linha da descrição principal ou detalhe for muito longa, quebre o texto a próxima linha
```pascal
  /// adapter for a node
  TTisNodeAdapter = object
    Offset: Cardinal;
    Grid: TTisGrid;
    procedure Init(aGrid: TTisGrid);
    /// return aNode Data pointer
    // - use this method if you need a PTisNodeData local variable,
    // as it will be a little faster then GetData
    function GetDataPointer(aNode: PVirtualNode): Pointer;
```

## Diretórios e Arquivos

- Todos os arquivos devem ser nomeados em letras minúsculas
- Dentro de `src`, irão existir diretórios para cada Context; como esses diretórios são únicos, assim também será um Context por todo o projeto
```
acme
  bin
  doc
  src
    bar
      acme.bar.model.pas
      acme.bar.edit.form.pas
    foo
      acme.foo.model.pas
      acme.foo.controller.pas
```

## Exemplos reais

Abaixo alguns links de projetos reais, em produção, que utilizam (em sua maioria) a nomenclatura descrita:

- **tis.ui.grid.core**: https://github.com/mdbs99/pltis_uicomponents/blob/master/src/standard/tis.ui.grid.core.pas
