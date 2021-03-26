---
title: Barra de navegação de suporte em um serviço de linguagem herdada
description: Saiba como dar suporte à barra de navegação em um serviço de linguagem herdado. A barra de navegação na exibição do editor exibe os tipos e membros no arquivo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Navigation bar, supporting in language services [managed package framework]
- language services [managed package framework], Navigation bar
ms.assetid: 2d301ee6-4523-4b82-aedb-be43f352978e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e75103d008e65c6d2060d598e442499f38a0e322
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080652"
---
# <a name="support-for-the-navigation-bar-in-a-legacy-language-service"></a>Suporte para a barra de navegação em um serviço de linguagem herdado
A barra de navegação na parte superior da exibição do editor exibe os tipos e membros no arquivo. Os tipos são mostrados na lista suspensa à esquerda e os membros são mostrados no menu suspenso à direita. Quando o usuário seleciona um tipo, o cursor é colocado na primeira linha do tipo. Quando o usuário seleciona um membro, o cursor é colocado na definição do membro. As caixas suspensas são atualizadas para refletir o local atual do cursor.

## <a name="displaying-and-updating-the-navigation-bar"></a>Exibindo e atualizando a barra de navegação
 Para dar suporte à barra de navegação, você deve derivar uma classe da <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> classe e implementar o <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> método. Quando o serviço de linguagem recebe uma janela de código, a <xref:Microsoft.VisualStudio.Package.LanguageService> classe base cria uma instância do <xref:Microsoft.VisualStudio.Package.CodeWindowManager> , que contém o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> objeto que representa a janela de código. <xref:Microsoft.VisualStudio.Package.CodeWindowManager>Em seguida, o objeto recebe um novo <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> objeto. O <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A> método obtém um <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> objeto. Se você retornar uma instância de sua <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> classe, o <xref:Microsoft.VisualStudio.Package.CodeWindowManager> chamará o <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> método para popular as listas internas e passará seu <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> objeto para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de barras suspensas. O Gerenciador de barras suspensa, por sua vez, chama o <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.SetDropdownBar%2A> método em seu <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> objeto para estabelecer o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsDropdownBar> objeto que contém as duas barras suspensas.

 Quando o cursor se move, o <xref:Microsoft.VisualStudio.Package.LanguageService.OnIdle%2A> método chama o <xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A> método. O <xref:Microsoft.VisualStudio.Package.LanguageService.OnCaretMoved%2A> método base chama o <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> método em sua <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> classe para atualizar o estado da barra de navegação. Você passa um conjunto de <xref:Microsoft.VisualStudio.Package.DropDownMember> objetos para esse método. Cada objeto representa uma entrada na lista suspensa.

## <a name="the-contents-of-the-navigation-bar"></a>O conteúdo da barra de navegação
 A barra de navegação geralmente contém uma lista de tipos e uma lista de membros. A lista de tipos inclui todos os tipos disponíveis no arquivo de origem atual. Os nomes de tipo incluem as informações completas do namespace. Veja a seguir um exemplo de código C# com dois tipos:

```csharp
namespace TestLanguagePackage
{
    public class TestLanguageService
    {
        internal struct Token
        {
            int tokenID;
        }
        private Tokens[] tokens;
        private string serviceName;
    }
}
```

 A lista de tipos será exibida `TestLanguagePackage.TestLanguageService` e `TestLanguagePackage.TestLanguageService.Tokens` .

 A lista Membros exibe os membros disponíveis do tipo selecionado na lista tipos. Usando o exemplo de código acima, se `TestLanguagePackage.TestLanguageService` for o tipo selecionado, a lista de membros conterá os membros privados `tokens` e `serviceName` . A estrutura interna `Token` não é exibida.

 Você pode implementar a lista de membros para tornar o nome de um membro em negrito quando o cursor é colocado dentro dele. Os membros também podem ser exibidos em texto esmaecido, indicando que eles não estão dentro do escopo onde o cursor está posicionado no momento.

## <a name="enabling-support-for-the-navigation-bar"></a>Habilitando o suporte para a barra de navegação
 Para habilitar o suporte para a barra de navegação, você deve definir o `ShowDropdownBarOption` parâmetro do <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> atributo como `true` . Esse parâmetro define a propriedade <xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A>. Para dar suporte à barra de navegação, você deve implementar o <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> objeto no <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe.

 Em sua implementação do <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDropDownHelper%2A> método, se a <xref:Microsoft.VisualStudio.Package.LanguagePreferences.ShowNavigationBar%2A> propriedade for definida como `true` , você poderá retornar um <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars> objeto. Se você não retornar o objeto, a barra de navegação não será exibida.

 A opção de mostrar a barra de navegação pode ser definida pelo usuário, portanto, é possível que esse controle seja redefinido enquanto a exibição do editor está aberta. O usuário deve fechar e reabrir a janela do editor antes que a alteração ocorra.

## <a name="implementing-support-for-the-navigation-bar"></a>Implementando o suporte para a barra de navegação
 O <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> método usa duas listas (uma para cada suspensa) e dois valores que representam a seleção atual em cada lista. As listas e os valores de seleção podem ser atualizados, caso em que o <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> método deve retornar `true` para indicar que as listas foram alteradas.

 À medida que a seleção é alterada no menu suspenso tipos, a lista de membros deve ser atualizada para refletir o novo tipo. O que é mostrado na lista de membros pode ser:

- A lista de membros para o tipo atual.

- Todos os membros disponíveis no arquivo de origem, mas com todos os membros que não estão no tipo atual exibido no texto esmaecido. O usuário ainda pode selecionar os membros esmaecidos, para que eles possam ser usados para navegação rápida, mas a cor indica que eles não fazem parte do tipo selecionado no momento.

  Normalmente, uma implementação do <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> método executa as seguintes etapas:

1. Obtenha uma lista de declarações atuais para o arquivo de origem.

     Há várias maneiras de preencher as listas. Uma abordagem é criar um método personalizado em sua versão da <xref:Microsoft.VisualStudio.Package.LanguageService> classe que chama o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método com um motivo de análise personalizada que retorna uma lista de todas as declarações. Outra abordagem pode ser chamar o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método diretamente do <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> método com o motivo da análise personalizada. Uma terceira abordagem pode ser armazenar em cache as declarações na <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe retornada pela última operação de análise completa na <xref:Microsoft.VisualStudio.Package.LanguageService> classe e recuperá-la do <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> método.

2. Preencha ou atualize a lista de tipos.

     O conteúdo da lista de tipos pode ser atualizado quando a origem for alterada ou se você tiver optado por alterar o estilo de texto dos tipos com base na posição atual do cursor. Observe que essa posição é passada para o <xref:Microsoft.VisualStudio.Package.TypeAndMemberDropdownBars.OnSynchronizeDropdowns%2A> método.

3. Determine o tipo a ser selecionado na lista de tipos com base na posição atual do cursor.

     Você pode pesquisar as declarações que foram obtidas na etapa 1 para localizar o tipo que inclui a posição atual do cursor e, em seguida, Pesquisar a lista de tipos desse tipo para determinar seu índice na lista de tipos.

4. Preencha ou atualize a lista de membros com base no tipo selecionado.

     A lista de membros reflete o que é exibido atualmente na lista suspensa **Membros** . O conteúdo da lista de membros pode precisar ser atualizado se a origem tiver sido alterada ou se você estiver exibindo apenas os membros do tipo selecionado e se o tipo selecionado tiver sido alterado. Se você optar por exibir todos os membros no arquivo de origem, o estilo de texto de cada membro na lista precisará ser atualizado se o tipo selecionado no momento tiver sido alterado.

5. Determine o membro a ser selecionado na lista de membros com base na posição atual do cursor.

     Pesquise as declarações que foram obtidas na etapa 1 para o membro que contém a posição atual do cursor e, em seguida, pesquise a lista de membros desse membro para determinar seu índice na lista de membros.

6. Retorne `true` se alguma alteração tiver sido feita nas listas ou nas seleções em qualquer uma das listas.
