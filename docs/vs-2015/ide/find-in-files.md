---
title: Localizar nos Arquivos | Microsoft Docs
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
- vs.findreplace.findinfiles
- vs.findinfiles
helpviewer_keywords:
- objects [Visual Studio], finding
- text searches, replacing text
- objects [Visual Studio], searching for
- Find and Replace window, Find in Files tab
- text searches, Find and Replace window
- documents, searching
- files, searching
- Find in Files tab, Find and Replace window
ms.assetid: 989e0737-46d7-4474-8453-fad52a74669d
caps.latest.revision: 45
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4529b44014b209bdef1fc919ac413b61d77407c1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49902133"
---
# <a name="find-in-files"></a>Localizar em Arquivos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Localizar nos arquivos * * permite pesquisar um conjunto de arquivos especificado. As correspondências encontradas e as ações executadas são listadas na janela **Localizar Resultados** selecionada em **Opções de resultado**.  
  
 É possível usar qualquer um dos métodos a seguir para exibir **Localizar nos Arquivos** na janela **Localizar e Substituir**.  
  
### <a name="to-display-find-in-files"></a>Para exibir Localizar nos Arquivos  
  
1. Na barra de menus, escolha **Editar**, **Localizar e Substituir**.  
  
2. Escolha **Localizar nos Arquivos**.  
  
   Para cancelar uma operação de localização, pressione CTRL + BREAK.  
  
> [!NOTE]
>  A ferramenta Localizar e Substituir não pesquisa diretórios com o conjunto de atributos `Hidden` ou `System`.  
  
## <a name="find-what"></a>Localizar  
 Para pesquisar uma nova cadeia de caracteres de texto ou expressão, especifique-a na caixa. Para pesquisar qualquer uma das 20 cadeias de caracteres mais pesquisadas recentemente, abra a lista e escolha a cadeia de caracteres que você deseja pesquisar. Escolha o botão **Construtor de Expressões** adjacente se você desejar usar uma ou mais expressões regulares na cadeia de caracteres de pesquisa. Para obter mais informações, consulte [Usando expressões regulares no Visual Studio](../ide/using-regular-expressions-in-visual-studio.md).  
  
## <a name="look-in"></a>Examinar  
 A opção escolhida na lista suspensa **Examinar** determina se **Localizar nos Arquivos** pesquisa apenas em arquivos ativos ou em todos os arquivos armazenados em determinadas pastas. Selecione um escopo da pesquisa na lista ou clique no botão **Procurar (...)** para exibir a caixa de diálogo **Escolher Pastas de Pesquisa** e insira seu próprio conjunto de diretórios. Também é possível digitar um caminho diretamente na caixa **Examinar**.  
  
> [!WARNING]
>  Com as opções **Solução Inteira** ou **Projeto Atual**, os arquivos de projeto e de solução não são pesquisados. Se você deseja examinar arquivos de projeto, escolha uma pasta de pesquisa.  
  
> [!NOTE]
>  Se a opção **Examinar** selecionada fizer com que você pesquise um arquivo do qual você fez check-out do controle do código-fonte, apenas a versão desse arquivo que tiver sido baixada em seu computador local será pesquisada.  
  
## <a name="include-subfolders"></a>Incluir subpastas  
 Especifica que as subpastas da pasta **Examinar** serão pesquisadas.  
  
## <a name="find-options"></a>Opções de busca  
 É possível expandir ou recolher a seção **Localizar opções**. As opções a seguir podem ser marcadas ou desmarcadas:  
  
 Diferenciar maiúsculas de minúsculas  
 Quando selecionada, uma pesquisa **Localizar Resultados** diferenciará maiúsculas de minúsculas  
  
 Coincidir palavra inteira  
 Quando selecionadas, as janelas **Localizar Resultados** retornarão apenas correspondências de palavras inteiras.  
  
 Usar Expressões Regulares  
 Se essa caixa de seleção estiver marcada, será possível usar notações especiais para definir padrões de texto a serem correspondidos nas caixas de texto **Localizar** ou **Substituir por**. Para obter uma lista dessas notações, consulte [Usando expressões regulares no Visual Studio](../ide/using-regular-expressions-in-visual-studio.md).  
  
 Procurar nestes tipos de arquivos  
 Essa lista indica os tipos de arquivos a serem pesquisados nos diretórios **Examinar**. Se esse campo estiver em branco, todos os arquivos nos diretórios **Examinar** serão pesquisados.  
  
 Selecione qualquer item na lista para inserir uma cadeia de caracteres de pesquisa pré-configurada que localizará arquivos desses tipos específicos.  
  
## <a name="result-options"></a>Opções de resultado  
 É possível expandir ou recolher a seção **Opções de resultado**. As opções a seguir podem ser marcadas ou desmarcadas:  
  
 Janela Localizar Resultados 1  
 Quando selecionada, os resultados da pesquisa atual substituirão o conteúdo da janela **Localizar Resultados 1**. Esta janela é aberta automaticamente para exibir os resultados da pesquisa. Para abrir essa janela manualmente, selecione **Outras Janelas** no menu **Exibir** e escolha **Localizar Resultados 1**.  
  
 Janela Localizar Resultados 2  
 Quando selecionada, os resultados da pesquisa atual substituirão o conteúdo da janela **Localizar Resultados 2**. Esta janela é aberta automaticamente para exibir os resultados da pesquisa. Para abrir essa janela manualmente, selecione **Outras Janelas** no menu **Exibir** e escolha **Localizar Resultados 2**.  
  
 Exibir apenas nomes de arquivos  
 Exibe uma lista de arquivos que contém correspondências de pesquisa em vez de exibir as próprias correspondências de pesquisa.  
  
 Acrescentar resultados  
 Acrescenta os resultados da pesquisa aos resultados da pesquisa anterior.  
  
## <a name="see-also"></a>Consulte também  
 [Localizando e substituindo texto](../ide/finding-and-replacing-text.md)   
 [Substituir nos Arquivos](../ide/replace-in-files.md)   
 [Comandos do Visual Studio](../ide/reference/visual-studio-commands.md)



