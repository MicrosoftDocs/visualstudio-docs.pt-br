---
title: Argumentos da linha de comando para o Gerenciador de Conteúdo da Ajuda | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3aa9890a-1147-42ba-adea-17935d184038
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 5ac0d333f8103f6904bce517397a73cc010b1d36
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49873403"
---
# <a name="command-line-arguments-for-the-help-content-manager"></a>Argumentos da linha de comando para o Gerenciador de Conteúdo da Ajuda
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode especificar como implantar e gerenciar conteúdo da Ajuda local usando argumentos de linha de comando para o Gerenciador de Conteúdo da Ajuda (HlpCtntmgr.exe). Você deve executar scripts para essa ferramenta de linha de comando com permissões de administrador, e você não pode executar esses scripts como um serviço. Você pode realizar as seguintes tarefas usando esta ferramenta:  
  
- Adicionar ou atualizar o conteúdo da ajuda local de um disco ou da nuvem.  
  
- Remova o conteúdo da ajuda local.  
  
- Mova o repositório de conteúdo local da Ajuda.  
  
- Adicionar, atualizar, remover ou mover o conteúdo da ajuda local silenciosamente.  
  
  Sintaxe:  
  
```  
HlpCtntmgr.exe /operation Value /catalogname CatalogName /locale Locale /sourceuri InstallationPoint  
```  
  
 Por exemplo:  
  
```  
hlpctntmgr.exe /operation install /catalogname VisualStudio14 /locale en-us /sourceuri d:\productDocumentation\HelpContentSetup.msha  
```  
  
## <a name="switches-and-arguments"></a>Opções e argumentos  
 A tabela a seguir define as opções e os argumentos que você pode usar a ferramenta de linha de comando para o Gerenciador de Conteúdo da Ajuda:  
  
|Alternar|Necessário?|Arguments|  
|------------|---------------|---------------|  
|/operation|Sim|-   **Instalar** – adiciona livros de fonte de instalação especificada ao repositório de conteúdo local.<br />     Esta opção requer o argumento /booklist ou o argumento /sourceURI, ou ambos. Se você não especificar o argumento /sourceURI, o URI do Visual Studio padrão será usado como a origem da instalação. Se você não especificar o argumento /booklist, todos os livros em /sourceUri serão instalados.<br />-   **Desinstalar** – remove os livros especificado do repositório de conteúdo local.<br />     Esta opção requer o argumento /booklist ou o argumento /sourceURI.  Se você especificar o argumento /sourceURI, todos os livros serão removidos e o argumento /booklist será ignorado.<br />-   **Mover** – move o repositório local para o caminho que você especificar. O caminho local padrão de armazenamento é definido pela configuração da ajuda em %PROGRAMDATA%<br />     Esta opção requer os argumentos /locationPath e /catalogName. Mensagens de erro serão registradas no log de eventos se você especificar um caminho que não é válido ou se não houver espaço livre na unidade para manter o conteúdo.<br />-   **Atualizar** – atualiza os tópicos alterados desde que foram instalados ou atualizados mais recentemente.<br />     Esta opção requer o argumento /sourceURI.|  
|/catalogName|Sim|Especifica o nome do catálogo de conteúdo.|  
|/locale|Não|Especifica a localidade do produto que é usada para exibir e gerenciar conteúdo para a instância atual do visualizador da Ajuda. Por exemplo, você especifica para `EN-US` inglês - Estados Unidos.<br /><br /> Se você não especificar uma localidade, a localidade do sistema operacional será usada. Se essa localidade não puder ser determinada, `EN-US` será usado.<br /><br /> Se você especificar uma localidade que não seja válida, uma mensagem de erro será registrada no log de eventos.|  
|/e|Não|Promove o Gerenciador de Conteúdo a Ajuda a Privilégios administrativos se o usuário atual possuir credenciais administrativas.|  
|/sourceURI|Não|Especifica a URL da qual o conteúdo é instalado (serviço API) ou o caminho para o arquivo de conteúdo de instalação (.msha). O URL pode apontar para o grupo de produtos (nó a nível superior) ou para livros do produto (nó a nível folha) em um ponto de extremidade de estilo do Visual Studio 2010. Não é necessário incluir uma barra (/) no final do URL. Se você incluir uma barra à barra, ela será manipulado apropriadamente.<br /><br /> Uma mensagem de erro é colocada no log de eventos se você especificar um arquivo não localizado, não válido ou não acessível ou se uma conexão com a Internet não está disponível ou é interrompida quando o conteúdo está sendo gerenciado.|  
|/vendor|Não|Especifica o fornecedor para o conteúdo do produto que será removido (por exemplo, `Microsoft`). O argumento padrão para essa opção é Microsoft.|  
|/productName|Não|Especifica o nome do produto para os livros que serão removidos. O nome do produto é identificado nos arquivos helpcontentsetup.msha ou books.html que são enviados com o conteúdo. Você pode remover os livros de apenas um produto de cada vez. Para remover livros de vários produtos, você deve executar várias instalações.|  
|/booklist|Não|Especifica os nomes dos livros a serem gerenciados, separados por espaços. Os valores devem corresponder aos nomes de livro conforme listado na mídia de instalação.<br /><br /> Se você não especificar esse argumento, todos os livros recomendados para o produto especificado em /sourceURI serão instalados se a origem da instalação estiver no formato [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)].<br /><br /> Se o nome de um livro contém um ou mais espaços, coloque-o entre aspas duplas (") para que a lista seja delimitada apropriadamente.<br /><br /> Mensagens de erro serão registradas se você especificar um /sourceURI que não é válido ou não é alcançável.|  
|/skuId|Não|Especifica a unidade de manutenção de estoque (SKU) do produto da fonte de instalação, e filtra os livros que a opção de /SourceURI identifica.|  
|/membership|Não|-   **Mínimo** – instala um conjunto mínimo de conteúdo de Ajuda com base na SKU especificada usando a opção /skuId. O mapeamento entre o SKU e o conteúdo é exposto no serviço API.<br />-   **Recomendado** – instala um conjunto recomendado de livros para a SKU especificada usando o argumento /skuId. A origem de instalação é o serviço API ou .MSHA.<br />-   **Completo** – instala todo o conjunto de livros para a SKU que você especifica usando o argumento /skuId. A origem de instalação é o serviço API ou .MSHA.|  
|/locationpath|Não|Especifica a pasta padrão para o conteúdo da Ajuda local. Você deve usar essa opção para instalar ou mover apenas o conteúdo. Se você especificar esta opção, também deverá especificar a opção /silent.|  
|/silent|Não|Instala ou remove conteúdo da Ajuda sem avisar o usuário ou sem exibir qualquer IU, incluindo o ícone na área de notificação de status. A saída é registrada em um arquivo no diretório %Temp%. **Importante:** para instalar o conteúdo silenciosamente, use arquivos .cab assinados digitalmente, não arquivos .mshc.|  
|/launchingApp|Não|Define o aplicativo e o contexto de catálogo quando o Visualizador da Ajuda é iniciado sem o aplicativo pai. Os argumentos para essa opção são *CompanyName*, *ProductName* e *VersionNumber* (por exemplo, `/launchingApp Microsoft,VisualStudio,11.0`).<br /><br /> Isso é necessário para a instalação do conteúdo com o parâmetro /silent.|  
|/wait *Seconds*|Não|Interrompe operações de instalação, desinstalação e atualização. Se uma operação já está em andamento para o catálogo, o processo esperará até o número determinado de segundos para continuar. Use 0 para aguardar indefinidamente.|  
|/?|Não|Lista as opções e suas descrições para a ferramenta de linha de comando do Gerenciador de Conteúdo da Ajuda.|  
  
### <a name="exit-codes"></a>Códigos de saída  
 Quando você executa a ferramenta de linha de comando para o Gerenciador de Conteúdo da Ajuda em modo silencioso, ela retorna os seguintes códigos de saída:  
  
```  
Success = 0,  
  
FailureToElevate = 100  
InvalidCmdArgs = 101,  
FailOnFetchingOnlineContent = 110,  
FailOnFetchingContentFromDisk = 120,  
FailOnFetchingInstalledBooks = 130,  
NoBooksToUninstall = 200,  
NoBooksToInstall = 300,  
FailOnUninstall = 400,  
FailOnInstall = 500,  
FailOnMove = 600,  
FailOnUpdate = 700,  
FailOnRefresh = 800,  
Cancelled = 900,  
Others = 999,  
ContentManagementDisabled = 1200,  
OnlineHelpPreferenceDisabled = 1201  
UpdateAlreadyRunning = 1300 – (Signals that the update didn't run because another was in progress.)  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Guia do administrador do Help Viewer](../ide/help-viewer-administrator-guide.md)   
 [Substituições do Gerenciador de Conteúdo da Ajuda](../ide/help-content-manager-overrides.md)



