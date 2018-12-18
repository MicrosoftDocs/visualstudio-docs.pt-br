---
title: Código de refatoração
description: Facilita a tarefa de reorganizar o código no Visual Studio para Mac usando a Análise de Código-Fonte.
author: conceptdev
ms.author: crdun
ms.date: 05/06/2018
ms.assetid: C7782BF3-016F-4B41-8A81-85FC540A1A8F
ms.openlocfilehash: 672c7547da9360ae3e278f783b160ffdaed05e03
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296457"
---
# <a name="refactoring"></a>Refatoração

Refatorar o código é uma maneira para reorganizar, reestruturar e esclarecer o código existente e garantir que o comportamento geral do código não se altere.

Refatorar produz uma base de código mais íntegra, tornando-a mais utilizável, saudável, legível e fácil de manter tanto para você quanto para qualquer outro desenvolvedor ou usuário que poderia consultar o código.

A integração do Visual Studio para Mac com o Roslyn, a plataforma de compilador .NET do software livre da Microsoft, permite realizar mais operações de refatoração.

## <a name="renaming"></a>Renomear

O comando de refatoração *Renomear* pode ser usado em qualquer identificador de código (por exemplo, um nome de classe, nome de propriedade, etc.) para localizar todas as ocorrências do identificador em questão e alterá-las. Para renomear um símbolo, clique com botão direito do mouse nele e escolha **Refatorar > Renomear** ou a associação de teclas **Cmd + R**:

![Renomear um item de menu](media/refactoring-renaming1.png)

Isso destaca o símbolo e todas as referências a ele. Quando você começar a digitar um novo nome, ele será alterado automaticamente em todas as referências no código e você poderá sinalizar a conclusão da renomeação pressionando **Enter**:

![Renomear e identificador](media/refactoring-renaming2.png)

## <a name="context-actions"></a>Ações de contexto

Ações de contexto permitem que você inspecione qualquer código C# e veja todas as possíveis opções de refatoração.

Os itens de contexto **Resolver** e **Refatorar** são combinados em um único item *Correção rápida...* que fornece todas as ações de contexto disponíveis:

![Exibir itens de contexto](media/refactoring-context-action.png)

Focalizar uma das ações de contexto fornecerá uma visualização do que será adicionado ou removido do código.

Outra opção é pressionar **Option + Enter** em qualquer lugar no seu código:

![Itens de contexto Option Enter](media/refactoring-image2a.png)

Para habilitar essas opções, você deverá selecionar *Habilitar a análise de código-fonte de arquivos abertos* nas opções de **Visual Studio para Mac > Preferências > Editor de Texto > Análise de Código-Fonte**:

![Habilitar a análise de código-fonte](media/refactoring-options.png)

Há mais de 100 ações possíveis que podem ser sugeridas, as quais são habilitadas ou desabilitadas navegando para **Visual Studio para Mac > Preferências > Análise de código-fonte > C# > Ações de Código** e marcando ou desmarcando a caixa ao lado da ação:

![Ações da Análise de código-fonte C#](media/refactoring-image3a.png)

### <a name="common-context-actions"></a>Ações de contexto comuns

Algumas das ações de contexto mais usadas são explicadas abaixo.

#### <a name="extract-method"></a>Extrair método

A operação de refatoração Extrair método permite que você crie um novo método extraindo uma seleção do código em um membro existente. Esta ação faz duas coisas:

* Cria um novo método que contém o código selecionado
* Chama o método de novo no local em que o código selecionado estava.

##### <a name="example"></a>Exemplo

1. Adicione o seguinte código:

```csharp
    class MainClass
    {

        double CalculatePyramidVolume(double baseArea, double height)
        {

            double volume = (baseArea * height) / 3;

            return volume;
        }
    }
```

2. Realce a linha `double volume = (baseArea * height) / 3;`, clique com o botão direito do mouse nela e selecione **Refatorar > Extrair método**.

3. Use as teclas de direção para selecionar onde o novo método deve ser colocado no seu código.

#### <a name="encapsulate-field"></a>Encapsular campo

A operação de Encapsular campo permite que você crie uma propriedade de um campo existente e atualiza seu código para fazer referência à propriedade recém-criada. Ao criar uma propriedade que encapsula o campo, você está cancelando a permissão de acesso direto ao seu campo público, o que significa que outros objetos não poderão modificá-lo.

Essa ação faz o seguinte:

* Altera o modificador de acesso para privado.
* Gera um getter e um setter para o campo (a menos que o campo seja somente leitura, pois nesse caso ele criará somente um getter).

## <a name="source-analysis"></a>Análise de código-fonte

A análise de código-fonte examinará o código em tempo real sublinhando possíveis erros e violações de estilo e fornecendo correções automáticas como ações de contexto.

Você pode exibir todos os resultados da análise de código-fonte para qualquer arquivo a qualquer momento exibindo a barra de rolagem à direita do editor de texto:

![Barra lateral da Análise de código-fonte](media/refactoring-image4a.png)

Se você clicar no círculo na parte superior, poderá percorrer cada sugestão, com os problemas de gravidade mais alto sendo mostrados primeiro. Focalizar um resultado ou linha individual exibirá o problema que poderá ser corrigido por meio de ações de contexto:

![Item da análise de código-fonte](media/refactoring-image5.png)

## <a name="see-also"></a>Consulte também

- [Ações rápidas (Visual Studio no Windows)](/visualstudio/ide/quick-actions)
- [Refatorar o código (Visual Studio no Windows)](/visualstudio/ide/refactoring-in-visual-studio)