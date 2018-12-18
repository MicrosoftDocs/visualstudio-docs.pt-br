---
title: Designer de fluxo de trabalho - navegue e selecione uma caixa de diálogo de tipo do .NET
ms.date: 11/04/2016
ms.topic: conceptual
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- TypeBrowser.UI
- ActivityTypeResolver.UI
ms.assetid: 864b60b6-a070-4e5c-aa5b-a25341b57ea6
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 686969c233f50dd1df743590206966183be48da9
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39513192"
---
# <a name="browse-and-select-a-net-type-dialog-box"></a>Procurar e selecione uma caixa de diálogo de tipo do .NET

No **propriedades** designers como o designer variável, quando você seleciona, caixas de diálogo ou janela **procurar tipos** de uma lista de tipos de dados, é o **procurar e selecione um tipo .NET** caixa de diálogo (conhecida na forma abreviada, como o tipo "navegador"). Na caixa de diálogo, você pode escolher um tipo de um modo de exibição de árvore de assemblies e de projetos.

Esta caixa de diálogo é empregada em um número de cenários do usuário, incluindo o seguinte:

-   Ao definir o tipo de uma variável ou um argumento.

-   Ao selecionar um tipo para uma atividade genérico.

-   Para adicionar uma captura na atividade de <xref:System.Activities.Statements.TryCatch> .

> [!NOTE]
> O navegador do tipo pode exibir tipos de jagged array Visual Basic, mas não tipos de matriz multidimensional. Ver [matrizes denteadas](http://go.microsoft.com/fwlink/?LinkId=195226) e [matrizes multidimensionais](http://go.microsoft.com/fwlink/?LinkId=195227) para obter detalhes.

## <a name="selecting-a-value-or-reference-type-from-the-type-browser"></a>Selecionando um tipo de valor ou tipo de referência de navegador de tipo

### <a name="to-select-a-value-or-reference-type-from-the-type-browser"></a>Para selecionar um valor ou uma referência digite de navegador de tipo

1.  No **nome do tipo** , digite o nome do tipo que você deseja usar.

2.  Realize um dos seguintes procedimentos:

    -   Depois que o nome do tipo que você deseja usar aparece na árvore na **nome do tipo** caixa, clique duas vezes o tipo para selecioná-lo.

    -   Tipo suficiente caracteres na **nome do tipo** caixa para identificar exclusivamente o tipo que você deseja usar e, em seguida, pressione enter para selecionar o tipo

### <a name="to-select-a-generic-type-from-the-type-browser"></a>Para selecionar um tipo genérico de navegador de tipo

1.  No **nome do tipo** caixa, digite o nome do tipo que você deseja usar.

2.  Depois que o nome do tipo que você deseja usar aparece na árvore na **nome do tipo** caixa, clique no tipo para selecioná-lo para causar caixas suspensas aparecem.

     Selecione o tipo que você deseja usar para fechar o genérico caixas de lista suspensa e, em seguida, clique em **Okey**.

## <a name="types-displayed-in-the-type-browser"></a>Tipos exibidos no navegador de tipo

Os tipos exibidos no navegador do tipo podem variar dependendo de como o navegador de tipo foi iniciado. Se o navegador de tipo foi iniciado em um projeto de fluxo de trabalho dentro de **vs2010**, por padrão, todos os tipos em assemblies referenciados e referenciou projetos são mostrados. Se o navegador de tipo foi iniciado fora de um **vs2010** (como em um aplicativo de fluxo de trabalho rehosted ou em um arquivo de fluxo de trabalho autônomo), sistema de projeto, por padrão, os tipos de todos os assemblies carregados no AppDomain são mostradas .

No navegador de tipo pode ser filtro por desenvolvedores do designer de atividade. Para quaisquer atividades determinada, você pode ver apenas um subconjunto dos tipos. Por exemplo, na atividade de <xref:System.Activities.Statements.TryCatch> , somente os tipos derivados de <xref:System.Exception> são mostrados no navegador do tipo.

## <a name="filtering-search-results-in-the-type-browser"></a>Resultados de pesquisa de filtragem no navegador de tipo

A lista de tipos na **nome do tipo** caixa obtém mais curta, conforme você digita mais caracteres para localizar uma correspondência. Somente há suporte para os tipos cujo nome totalmente qualificado começa com a cadeia de caracteres que você digitou ou tipos cujo nome curto começa com a cadeia de caracteres que você digitou aparecem na lista filtrada.

Por exemplo:

1.  Digitação **operação** corresponde a <xref:System.OperationCanceledException> mas não <xref:System.InvalidOperationException>. Para corresponder <xref:System.InvalidOperationException>, inicie digite System.I ou inválido.

2.  Digitação **genérico** corresponde a <xref:System.GenericUriParser> mas não tipos no <xref:System.Collections.Generic> namespace. Para procurar por tipos no <xref:System.Collections.Generic> namespace, digite o nome totalmente qualificado do namespace.

## <a name="selecting-a-service-contract-using-the-type-browser-dialog"></a>Selecionando um contrato de serviço usando a caixa de diálogo de navegador de tipo

Ao selecionar um tipo de contrato de serviço, o navegador do tipo mostra somente os tipos que têm o atributo de <xref:System.ServiceModel.ServiceContractAttribute> .

## <a name="see-also"></a>Consulte também

- [Usando os designers de atividade](../workflow-designer/using-the-activity-designers.md)