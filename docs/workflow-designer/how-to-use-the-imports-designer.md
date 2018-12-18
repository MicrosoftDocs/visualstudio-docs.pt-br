---
title: 'Designer de fluxo de trabalho - como: usar o Designer de importações'
ms.date: 11/04/2016
ms.topic: conceptual
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Presentation.View.ImportDesigner.UI
ms.assetid: 61328ab6-9b66-4e12-8630-22e30ee8c9d1
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e26dafe6d8d7e455d1977f82f96f776185a5fdb3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49845259"
---
# <a name="how-to-use-the-imports-designer"></a>Como: Use o designer imports

O designer imports permite que você inserir em namespaces para os tipos que você usará em suas expressões. Assim como o **importa** ou **usando** palavras-chave no Visual Basic e c#, especificando namespaces no designer de importações permitem que você digite simplesmente um nome de tipo em sua expressão em vez de um totalmente qualificado nome do tipo de versão.

O designer imports reage a alterações na interface do usuário e as alterações feitas quando o fluxo de trabalho é salvo. Quando o fluxo de trabalho é salvo, namespaces podem ser adicionados automaticamente ao designer imports. Eles incluem o seguinte:

- Namespaces para alguns tipos usados em declarações de variável e argumento.

- Namespaces para alguns tipos usados em expressões.

- Algumas outras namespaces necessárias para serializar o fluxo de trabalho (por exemplo, namespaces usadas por atividades personalizados soltas no fluxo de trabalho).

  Quando o fluxo de trabalho é salvo, você pode notar que algumas namespaces que você excluiu manualmente que são adicionados automaticamente ao designer imports devido à lógica descrita na lista anterior.

## <a name="to-add-a-namespace-to-the-list-of-imported-namespaces"></a>Para adicionar um namespace à lista de namespaces importados

1.  Abra um aplicativo de serviço de fluxo de trabalho WCF, o aplicativo de console do fluxo de trabalho ou o projeto de biblioteca de atividade no Visual Studio ou um aplicativo de fluxo de trabalho hospedado novamente.

2.  Clique em **importações** na parte inferior da tela principal. O designer imports aparecerá.

3.  Insira ou selecione em um namespace do controle de lista suspensa na parte superior do designer imports.

     Enquanto você digita, uma lista de namespaces válidas que correspondem aos caracteres tipados aparece.

4.  Pressione **Enter** para adicionar o namespace à lista.

5.  Se você quiser remover um namespace da lista, selecione o namespace e, em seguida, pressione a **excluir** em seu teclado. Observe que um namespace só pode ser excluída se o namespace não é válido por algum motivo, por exemplo se o assembly que contém o namespace não é referenciado pelo projeto.