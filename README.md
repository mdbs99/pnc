# Pascal Guide

Este documento apresenta a minha versão atualizada do guia de estilo clássico do Object Pascal, originalmente elaborado por Charlie Calvert para a Borland na época do lançamento do Delphi.

A linguagem Object Pascal é case-insensitive, característica que facilita a curva de aprendizado de iniciantes, pois, diferentemente de linguagens case-sensitive, o compilador Pascal é significativamente mais permissivo quanto à declaração da maioria dos tokens (tipos, variáveis, constantes, etc.) que compõem um programa. Entretanto, essa mesma permissividade pode resultar em inconsistências visuais do mesmo código entre diferentes unidades, além de favorecer conflitos de nomenclatura causados por ambiguidade de tokens dentro de uma mesma unidade ou entre unidades distintas.

Após mais de 25 anos de atuação profissional com Object Pascal, defini um conjunto de regras de nomenclatura baseadas em prefixos e padrões estruturais que podem ser aplicadas a qualquer tipo de projeto Pascal.

A adoção desses prefixos facilita o code completion da IDE, elimina praticamente todas as ambiguidades, melhora a legibilidade e a organização do projeto.

## Conteúdo

- [Nomenclatura e Convenções](#nomenclatura-e-convenções)
  - [Definições](#definições)
  - [Tokens](#tokens)
  - [Comentários](#comentários)
  - [Linhas em branco](#linhas-em-branco)
- [Estrutura](#estrutura)
  - [Declaração de Unidades](#declaração-de-unidades)
  - [Diretórios e Arquivos](#diretórios-e-arquivos)
    - [Nomeando Arquivos](#nomeando-arquivos)
    - [Estrutura de Diretórios](#estrutura-de-diretórios)
- [Desenvolvimento](#desenvolvimento)

## Nomenclatura e Convenções

### Definições

- **Project**: Nome do projeto
- **Module**: Nome que deve ser único por projeto
- **Function**: Nome que descreve uma funcionalidade

### Tokens

- **Units (Project Module Function)**: Acme.Foo.Model, Acme.Bar.Model, Acme.Foo.Controller, Acme.Bar.EditForm
- **Interfaces (I Module Function)**: IFooModel, IBarModel, IFooController, IBarEditForm
- **Types (T Module Function)**: TFooModel, TBarModel, TFooController, TBarEditForm
- **Pointers (P Module Function)**: PFooModel, PBarModel, PFooController, PBarEditForm
- **Fields (f Function)**: fModel, fController, fEditForm
- **Arguments (a Function)**: aModel, aController, aEditForm
- **Unit Variables (v Module Function)**: vFooModel, vBarModel, vFooController, vBarEditForm
- **Local Variables (v Function)**: vModel, vController, vEditForm
- **Unit Constants (_ Module _ Function**): _FOO_VALUE, _BAR_VALUE, _FOO_BAR_VALUE
- **Local Constants (_ Function**): _VALUE, _TOKEN_VALUE
- **Local Functions (Function)**: IsValid, Execute
- **Unit Functions (Module Function)**: FooIsValid, BarExecute
- **Event Properties (On Function)**: OnEdit, OnCalculate
- **Event Implementations (Do Function)**: DoEdit, DoCalculate
- **Enums**:
  - {SCOPEDENUMS ON} TFooBar = (A, B, C)
  - {SCOPEDENUMS OFF} TFooBar = (fbA, fbB, fbC)

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

## Estrutura

### Declaração de Unidades

A ordem de declaração das Unidades é muito importante, seja por uma questão visual e organizacional, mas também para informar ao compilador a ordem de procura dos tokens — veja meu artigo sobre isso [aqui](https://objectpascalprogramming.com/declarando-unidades).

1. fpc/lazarus, delphi units
1. 3rd units
1. my global units
1. my local units

```pascal
uses
  // fpc/lazarus, delphi units
  Windows,
  Classes,
  SysUtils,
  Controls,
  Math,
  // 3rd units
  mormot.core.base,
  mormot.core.data,
  mormot.core.os,
  // my global units
  tisstrings,
  // my local units
  tis.core.os,
  tis.core.utils,
  tis.ui.grid.controls,
  tis.ui.grid.chart;
```

### Diretórios e Arquivos

#### Nomeando Arquivos
- Recomendo que os arquivos sejam nomeados em letras minúsculas, se o sistema será compilado em sistemas não-Windows
- Cada token que compõe o nome da Unidade deve ser separado por "." quando estiver utilizando compiladores mais novos, por exemplo: `acme.bar.model.pas`; para compiladores mais antigos (como Delphi 6 e anteriores), deve-se utilizar PascalCase, por exemplo: `AcmeBarModel.pas`

#### Estrutura de Diretórios
- Dentro de `src`, existirão diretórios correspondentes a cada Module
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

