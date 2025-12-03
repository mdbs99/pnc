# Pascal Guide

Este documento apresenta a minha versão atualizada do guia de estilo clássico do Object Pascal, originalmente elaborado por Charlie Calvert para a Borland na época do lançamento do Delphi.

A linguagem Object Pascal é case-insensitive, característica que facilita a curva de aprendizado de iniciantes, pois, diferentemente de linguagens case-sensitive, o compilador Pascal é significativamente mais permissivo quanto à declaração da maioria dos tokens (tipos, variáveis, constantes, etc.) que compõem um programa. Entretanto, essa mesma permissividade pode resultar em inconsistências visuais do mesmo código entre diferentes unidades, além de favorecer conflitos de nomenclatura causados por ambiguidade de tokens dentro de uma mesma unidade ou entre unidades distintas.

Após mais de 25 anos de atuação profissional com Object Pascal, defini um conjunto de regras de nomenclatura baseadas em prefixos e padrões estruturais que podem ser aplicadas a qualquer tipo de projeto Pascal.

A adoção desses prefixos facilita o code completion da IDE, elimina praticamente todas as ambiguidades, melhora a legibilidade e a organização do projeto.

## Conteúdo

* [Nomenclatura e Convenções](#nomenclatura-e-convenções)
* [Estrutura](#estrutura)
* [Desenvolvimento](#desenvolvimento)

## Nomenclatura e Convenções

### Definições

- **Project**: nome do seu projeto
- **Context**: Contexto único
- **Name**: Nome/finalidade

### Tokens

- **Units (Project Context Name)**: Acme.Foo.Model, Acme.Bar.Model, Acme.Foo.Controller, Acme.Bar.EditForm
- **Interfaces (I Context Name)**: IFooModel, IBarModel, IFooController, IBarEditForm
- **Types (T Context Name)**: TFooModel, TBarModel, TFooController, TBarEditForm
- **Pointers (P Context Name)**: PFooModel, PBarModel, PFooController, PBarEditForm
- **Fields (f Name)**: fModel, fController, fEditForm
- **Arguments (a Name)**: aModel, aController, aEditForm
- **Unit Variables (v Context Name)**: vFooModel, vBarModel, vFooController, vBarEditForm
- **Local Variables (v Name)**: vModel, vController, vEditForm
- **Unit Constants (_ Context _ Name**): _FOO_VALUE, _BAR_VALUE, _FOO_BAR_VALUE
- **Local Constants (_ Name**): _VALUE, _TOKEN_VALUE
- **Local Functions (Name)**: IsValid, Execute
- **Unit Functions (Context Name)**: FooIsValid, BarExecute
- **Event Properties (On Name)**: OnEdit, OnCalculate
- **Event Implementations (Do Name)**: DoEdit, DoCalculate

### Comentários

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

### Linhas em branco

Inserir linhas em branco dentro de um método é considerado um code smell. Isso geralmente indica que o método está assumindo responsabilidades em excesso — veja meu artigo sobre isso [aqui](https://objectpascalprogramming.com/posts/linhas-em-branco-no-metodo-e-mal-cheiro/).

Evite pular linhas entre blocos de código.

### Exemplos

A seguir estão alguns links para projetos reais, atualmente em produção, que adotam — em sua maioria — a nomenclatura e as convenções de codificação apresentadas neste documento:

- **tis.ui.grid.core**: https://github.com/mdbs99/pltis_uicomponents/blob/master/src/standard/tis.ui.grid.core.pas

## Estrutura

### Declaração de Unidades

A ordem de declaração das Unidades é muito importante, seja por uma questão visual e organizacional, mas também para informar ao compilador a ordem de procura dos tokens — veja meu artigo sobre isso [aqui](https://objectpascalprogramming.com/declarando-unidades).

1. fpc/lazarus, delphi units
1. 3rd units
1. my open source units
1. project units

### Exemplos

```pascal
uses
  /// fpc/lazarus, delphi units
  Windows,
  Classes,
  SysUtils,
  Controls,
  Math,
  /// 3rd units
  mormot.core.base,
  mormot.core.data,
  mormot.core.os,
  /// my open source units
  tisstrings,
  /// project units
  tis.core.os,
  tis.core.utils,
  tis.ui.grid.controls,
  tis.ui.grid.chart;
```

### Diretórios e Arquivos

- Recomendo que os arquivos sejam nomeados em letras minúsculas, se o sistema será compilado em sistemas não-Windows.
- Cada token que compõe o nome da Unidade deve ser separado por "." (em compiladores mais atuais) ou em PascalCase (em compiladores mais antigos, exemplo Delphi 6<)
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

## Desenvolvimento

### Criação de Objetos

wip...

### Destruição de Objetos

wip...

