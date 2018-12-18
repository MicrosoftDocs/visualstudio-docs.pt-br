---
title: Página Eventos de Build, Designer de Projeto (C#)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- cs.ProjectPropertiesBuildEvents
helpviewer_keywords:
- build events
- Project Designer, Build Events page
- pre-build events
- post-build events
ms.assetid: 3fff9ae5-213c-46ea-a660-1d70acb6c922
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: fe83d3a387d2066965fe83145ddbda4e9648d36b
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31944837"
---
# <a name="build-events-page-project-designer-c"></a>Página Eventos de Build, Designer de Projeto (C#)
Use a página **Eventos de Build** do **Designer de Projeto** para especificar as instruções de configuração de build. Você também pode especificar as condições sob as quais eventos pós-build são executados. Para obter mais informações, consulte [Como especificar eventos de build (C#)](../../ide/how-to-specify-build-events-csharp.md) e [Como especificar eventos de build (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md).

## <a name="uielement-list"></a>Lista UIElement
 **Configuração** Esse controle não é editável nesta página. Para obter uma descrição desse controle, consulte [Página de Build, Designer de Projeto (C#)](../../ide/reference/build-page-project-designer-csharp.md).

 **Plataforma** Esse controle não é editável nesta página. Para obter uma descrição desse controle, consulte [Página de Build, Designer de Projeto (C#)](../../ide/reference/build-page-project-designer-csharp.md).

 **Linha de comando do evento de pré-build** Especifica os comandos a serem executados antes do início do build. Para digitar comandos longos, clique em **Editar Pré-Build** para exibir a [Caixa de Diálogo Linha de Comando de Evento de Pré-Build/Evento de Pós-Build](../../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md).

> [!NOTE]
> Eventos de pré-build não serão executados se o projeto estiver atualizado e nenhum build será disparado.


 **Linha de comando do evento de pós-build** Especifica os comandos a serem executados após o término do build. Para digitar comandos longos, clique em **Editar Pós-Build** para exibir a **Caixa de Diálogo Linha de Comando de Evento de Pré-Build/Evento de Pós-Build**.

> [!NOTE]
> Adicione uma instrução `call` antes de todos os comandos pós-build que executam arquivos .bat. Por exemplo `call C:\MyFile.bat` ou `call C:\MyFile.bat call C:\MyFile2.bat`.


 **Executar o evento de pós-build** Especifica as seguintes condições para que o evento de pós-build seja executado, conforme é mostrado na tabela a seguir.

|Opção|Resultado|
|------------|------------|
|**Sempre**|O evento de pós-build será executado independentemente de o build ser bem-sucedido.|
|**No build bem-sucedido**|O evento de pós-build será executado se o build for bem-sucedido. Assim, o evento será executado mesmo para um projeto atualizado, desde que o build seja bem-sucedido.|
|**Quando o build atualizar a saída do projeto**|O evento de pós-build só será executado quando o arquivo de saída do compilador (.exe ou .dll) for diferente do arquivo de saída anterior do compilador. Portanto, um evento de pós-build não será executado se um projeto for atualizado.|

## <a name="see-also"></a>Consulte também

- [Como especificar eventos de build (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)
- [Como especificar eventos de build (C#)](../../ide/how-to-specify-build-events-csharp.md)
- [Referência de Propriedades do Projeto](../../ide/reference/project-properties-reference.md)
- [Compilando e criando](../../ide/compiling-and-building-in-visual-studio.md)