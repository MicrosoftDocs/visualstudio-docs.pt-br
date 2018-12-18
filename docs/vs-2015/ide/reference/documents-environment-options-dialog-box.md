---
title: Caixa de diálogo Documentos, Ambiente, Opções | Microsoft Docs
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
- VS.Environment.Documents
- VS.ToolsOptionsPages.Environment.Documents
- VS.ToolsOptionsPag.Environment.Documents
helpviewer_keywords:
- Documents Environment Options dialog box
- defaults, directories
- error messages, customizing
- files [Visual Studio], default options
- files [Visual Basic], auto-loading modified
- windows, customizing environment
- in-memory editing
- folders [Visual Studio], specifying where Open File goes
- Open File dialog box
- windows, enabling re-use of current
- notifications, files changed
- files [Visual Studio], displaying in Solution Explorer
- default directories
- read-only files, editing
- Options dialog box, showing Miscellaneous Files
- directories [Visual Studio], IDE environment options
- Options dialog box, Documents page
- warnings, files changed
- Solution Explorer, displaying files in
ms.assetid: 4e3ccf1b-cd68-4db6-9470-710c911b47fc
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ad1e397b67d04b8e8233a568b675eaf24a29bf59
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49246201"
---
# <a name="documents-environment-options-dialog-box"></a>Caixa de diálogo Documentos, Ambiente, Opções
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Use esta página da caixa de diálogo **Opções** para controlar a exibição de documentos no IDE (ambiente de desenvolvimento integrado) e gerenciar alterações externas em documentos e arquivos. É possível acessar essa caixa de diálogo clicando em **Opções** no menu **Ferramentas** e selecionando **Documentos** no nó **Ambiente**. Se **Documentos** não aparecer na lista, selecione **Mostrar todas as configurações** na caixa de diálogo **Opções**.  
  
> [!NOTE]
>  As opções disponíveis nas caixas de diálogo e os nomes os locais dos comandos de menu que você vê podem diferir do que é descrito na Ajuda, dependendo de suas configurações ativas ou da edição. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
 **Reutilizar a janela do documento atual, se tiver sido salva**  
 Quando selecionado, fecha o documento atual se ele tiver sido salvo e abre um novo documento na mesma janela. Se o documento atual não tiver sido salvo, ele permanecerá aberto e o novo documento será aberto em uma janela separada. Quando essa opção está desmarcada, novos documentos sempre são abertos em janelas separadas.  
  
 Se você executar operações de recortar e colar em vários documentos com pouca frequência e desejar minimizar o número de documentos e janelas abertas em seu espaço de trabalho, tente esta opção.  
  
 **Detectar quando o arquivo foi alterado fora do ambiente**  
 Quando essa opção é selecionada, uma mensagem notifica você imediatamente sobre alterações em um arquivo aberto que foram feitas por um editor fora do IDE. A mensagem permite recarregar o arquivo do armazenamento.  
  
 **Carregar alterações automaticamente, se tiverem sido salvas**  
 Quando **Detectar quando o arquivo foi alterado fora do ambiente** está selecionado e um arquivo aberto no IDE é alterado fora do IDE, uma mensagem de aviso é gerada por padrão. Se essa opção estiver habilitada, nenhum aviso será exibido e o documento será recarregado no IDE para acompanhar alterações externas.  
  
 **Permitir a edição de arquivos somente leitura; avisar ao tentar salvar**  
 Quando essa opção é habilitada, você pode abrir e editar um arquivo somente leitura. Quando tiver terminado, você deve usar o comando **Salvar como** para salvar o arquivo com um novo nome se quiser salvar um registro de suas alterações.  
  
 **Abrir arquivo usando o diretório do documento ativo no momento**  
 Quando selecionada, essa opção especifica que a caixa de diálogo **Abrir Arquivo** deve exibir o diretório do documento ativo. Quando essa opção está desmarcada, a caixa de diálogo **Abrir Arquivo** exibe o diretório que foi usado para abrir um arquivo pela última vez.  
  
 **Verificar terminações de linha consistentes ao carregar**  
 Selecione esta opção para que o editor verifique as terminações de linha em um arquivo e exiba uma caixa de mensagem se forem detectadas inconsistências na forma como as terminações de linha estão formatadas.  
  
 **Exibir aviso quando a opção de desfazer global for modificar arquivos editados**  
 Selecione esta opção para exibir uma caixa de mensagem quando o comando **Desfazer Global** for reverter alterações de refatoração feitas em arquivos que também foram alterados após a operação de refatoração. Retornar um arquivo ao seu estado pré-refatoração pode descartar alterações feitas posteriormente no arquivo.  
  
 **Mostrar arquivos diversos no Gerenciador de Soluções**  
 Selecione esta opção para exibir o nó **Arquivos Diversos** no **Gerenciador de Soluções**. Arquivos diversos são arquivos que não estão associadas um projeto ou solução, mas podem aparecer no **Gerenciador de Soluções** por questões de conveniência.  
  
> [!NOTE]
>  Selecione esta opção para habilitar o comando **Exibir no Navegador** no menu **Arquivo** para documentos da Web não incluídos no aplicativo Web ativo.  
  
 **\<** *n* **> itens salvos no projeto de arquivos diversos**  
 Especifica o número de arquivos a persistir na pasta **MiscellaneousFiles** do **Gerenciador de Soluções**. Esses arquivos são listados mesmo que não estejam mais abertos em um editor. É possível especificar qualquer número inteiro entre 0 e 256. O número padrão é 0.  
  
 Por exemplo, se você definir essa opção como 5 e tiver 10 arquivos diversos abertos, quando você fechar todos os 10 arquivos, os 5 primeiros ainda aparecerão na pasta **Arquivos Diversos**.  
  
 **Salvar documentos como Unicode quando os dados não puderem ser salvos em página de código**  
 Selecione esta opção para fazer com que arquivos que contêm informações incompatíveis com a página de código selecionada sejam salvos como Unicode por padrão.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Opções do Ambiente](../../ide/reference/environment-options-dialog-box.md)   
 [Arquivos Diversos](../../ide/reference/miscellaneous-files.md)   
 [Localizando e substituindo texto](../../ide/finding-and-replacing-text.md)



