---
title: Página Eventos de Build, Designer de Projeto (C#) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- cs.ProjectPropertiesBuildEvents
helpviewer_keywords:
- build events
- Project Designer, Build Events page
- pre-build events
- post-build events
ms.assetid: 3fff9ae5-213c-46ea-a660-1d70acb6c922
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 5a73978bf78c26914e7ee6b21c27f1eb2e7682ea
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49223062"
---
# <a name="build-events-page-project-designer-c"></a>Página Eventos de Build, Designer de Projeto (C#)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Use a página **Eventos de Build** do **Designer de Projeto** para especificar as instruções de configuração de build. Você também pode especificar as condições sob as quais eventos pós-build são executados. Para obter mais informações, consulte [Como especificar eventos de build (C#)](../../ide/how-to-specify-build-events-csharp.md) e [Como especificar eventos de build (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md).  
  
## <a name="uielement-list"></a>Lista UIElement  
 **Configuração**  
 Esse controle não é editável nesta página. Para obter uma descrição desse controle, consulte [Página de Build, Designer de Projeto (C#)](../../ide/reference/build-page-project-designer-csharp.md).  
  
 **Plataforma**  
 Esse controle não é editável nesta página. Para obter uma descrição desse controle, consulte [Página de Build, Designer de Projeto (C#)](../../ide/reference/build-page-project-designer-csharp.md).  
  
 **Linha de comando do evento de pré-build**  
 Especifica comandos serem executados antes do início do build. Para digitar comandos longos, clique em **Editar Pré-Build** para exibir a [Caixa de Diálogo Linha de Comando de Evento de Pré-Build/Evento de Pós-Build](../../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md).  
  
> [!NOTE]
>  Eventos de pré-build não serão executados se o projeto estiver atualizado e nenhum build será disparado.  
  
 **Linha de comando de evento de pós-build**  
 Especifica comandos a serem executados após o fim do build. Para digitar comandos longos, clique em **Editar Pós-Build** para exibir a **Caixa de Diálogo Linha de Comando de Evento de Pré-Build/Evento de Pós-Build**.  
  
> [!NOTE]
>  Adicione uma instrução `call` antes de todos os comandos pós-build que executam arquivos .bat. Por exemplo `call C:\MyFile.bat` ou `call C:\MyFile.bat call C:\MyFile2.bat`.  
  
 **Executar o evento de pós-build**  
 Especifica as condições a seguir para o evento de pós-build ser executado, conforme mostrado na tabela a seguir.  
  
|Opção|Resultado|  
|------------|------------|  
|**Sempre**|O evento de pós-build será executado independentemente de o build ser bem-sucedido.|  
|**No build bem-sucedido**|O evento de pós-build será executado se o build for bem-sucedido. Assim, o evento será executado mesmo para um projeto atualizado, desde que o build seja bem-sucedido.|  
|**Quando o build atualizar a saída do projeto**|O evento de pós-build só será executado quando o arquivo de saída do compilador (.exe ou .dll) for diferente do arquivo de saída anterior do compilador. Portanto, um evento de pós-build não será executado se um projeto for atualizado.|  
  
## <a name="see-also"></a>Consulte também  
 [Como especificar eventos de build (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)   
 [Como especificar eventos de build (C#)](../../ide/how-to-specify-build-events-csharp.md)   
 [Referência de propriedades do projeto](../../ide/reference/project-properties-reference.md)   
 [Compilando e criando](../../ide/compiling-and-building-in-visual-studio.md)



