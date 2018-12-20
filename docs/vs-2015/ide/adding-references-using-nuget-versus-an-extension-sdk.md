---
title: Adicionando referências usando o NuGet versus um SDK de Extensão | Microsoft Docs
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
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
ms.assetid: 2175581e-83cb-444c-bb52-cc1fca8ea196
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 031b582665abeb14f705725c7bee97f272bd5ab4
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49235801"
---
# <a name="adding-references-using-nuget-versus-an-extension-sdk"></a>Adicionando referências usando o NuGet versus um SDK de Extensão
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível fornecer um pacote de consumo em projetos do Visual Studio usando a extensão do NuGet para Visual Studio ou um SDK (Software Development Kit). Ao descrever as similaridades e diferenças entre os dois mecanismos, este tópico pode ajudá-lo a escolher o melhor para sua tarefa.  
  
-   O NuGet é um sistema de gerenciamento de pacotes de software livre que simplifica o processo de incorporação de bibliotecas em uma solução de projeto. Para obter mais informações, consulte [NuGet Overview (Visão geral do NuGet)](http://go.microsoft.com/fwlink/?LinkId=254877).  
  
-   Um SDK é uma coleção de arquivos que o Visual Studio trata como um único item de referência. A caixa de diálogo **Gerenciador de Referências** lista todos os SDKs relevantes para o projeto que está aberto quando você exibe essa caixa de diálogo. Quando você adiciona um SDK a um projeto, é possível acessar todo o conteúdo desse SDK por meio do IntelliSense, da **Caixa de Ferramentas**, dos designers, do **Pesquisador de Objetos**, do MSBuild, da implantação, da depuração e do empacotamento. Para obter mais informações sobre SDKs, consulte [Creating a Software Development Kit (Criando um Software Development Kit)](../extensibility/creating-a-software-development-kit.md).  
  
## <a name="which-mechanism-should-i-use"></a>Qual mecanismo devo usar?  
 A tabela a seguir ajuda a comparar os recursos de referência de um SDK com os recursos de referência do NuGet.  
  
|Recurso|Suporte do SDK|Anotações do SDK|Suporte do NuGet|Anotações do NuGet|  
|-------------|-----------------|---------------|-------------------|-----------------|  
|O mecanismo referencia uma entidade e, em seguida, todos os arquivos e funcionalidades estarão disponíveis.|S|Você adiciona um SDK usando a caixa de diálogo **Gerenciador de Referências** e todos os arquivos e funcionalidades estarão disponíveis durante o fluxo de trabalho de desenvolvimento.|S||  
|O MSBuild consome automaticamente os assemblies e os arquivos de metadados do Windows (.winmd).|S|As referências no SDK são automaticamente passadas para o compilador.|S||  
|O MSBuild consome automaticamente os arquivos .h ou .lib.|S|O arquivo *SDKName*.props informa ao Visual Studio como configurar o diretório do Visual C++ e assim por diante, para consumo automático do arquivo .h ou .lib.|N||  
|O MSBuild consome automaticamente os arquivos .js ou .css.|S|No **Gerenciador de Soluções**, é possível expandir o nó de referência do SDK do JavaScript para mostrar arquivos .js ou .css individuais e, em seguida, gerar marcações `<source include/>` arrastando esses arquivos para seus arquivos de origem. O SDK dá suporte ao F5 e à configuração automática do pacote.|S||  
|O MSBuild adiciona automaticamente o controle na **Caixa de Ferramentas**.|S|A **Caixa de Ferramentas** pode consumir SDKs e mostrar controles nas guias especificadas.|N||  
|O mecanismo dá suporte ao VSIX (Instalador do Visual Studio para extensões).|S|O VSIX tem um manifesto e uma lógica especiais para criar pacotes do SDK|S|O VSIX pode ser inserido em outro programa de instalação.|  
|O **Pesquisador de Objetos** enumera as referências.|S|O **Pesquisador de Objetos** obtém automaticamente a lista de referências em SDKs e as enumera.|N||  
|Os arquivos e links são automaticamente adicionados à caixa de diálogo **Gerenciador de Referências** (links de ajuda e assim por diante, preenchimento automático)|S|A caixa de diálogo **Gerenciador de Referências** enumera os SDKs automaticamente, juntamente com links de ajuda e a lista de dependências do SDK.|N|O NuGet fornece sua própria caixa de diálogo **Gerenciar Pacotes do NuGet**.|  
|O mecanismo dá suporte a várias arquiteturas.|S|Os SDKs podem distribuir várias configurações. O MSBuild consome os arquivos apropriados para cada configuração de projeto.|N||  
|O mecanismo dá suporte a várias configurações.|S|Os SDKs podem distribuir várias configurações. Dependendo da arquitetura de projeto, o MSBuild consome os arquivos apropriados para cada arquitetura de projeto.|N||  
|O mecanismo pode especificar "não copiar."|S|Dependendo se os arquivos são soltos na pasta \redist ou \designtime, é possível controlar quais arquivos devem ser copiados no pacote do aplicativo de consumo.|N|Você declara quais arquivos devem ser copiados no manifesto do pacote.|  
|O conteúdo é exibido nos arquivos localizados.|S|Documentos XML localizados em SDKs são incluídos automaticamente para obter uma melhor experiência do tempo de design.|N||  
|O MSBuild dá suporte ao consumo de várias versões de um SDK simultaneamente.|S|O SDK dá suporte ao consumo de várias versões simultaneamente.|N|Isso não está referenciando. Não é possível ter mais de uma versão de arquivos NuGet em seu projeto de cada vez.|  
|O mecanismo dá suporte à especificação de estruturas de destino, versões do Visual Studio e tipos de projeto aplicáveis.|S|A caixa de diálogo **Gerenciador de Referências** e a **Caixa de Ferramentas** mostram apenas os SDKs aplicáveis a um projeto para que os usuários possam escolher mais facilmente os SDKs apropriados.|Y (parcial)|O Pivot é a estrutura de destino. Não há nenhuma filtragem na interface do usuário. No momento da instalação, ela pode retornar um erro.|  
|O mecanismo dá suporte à especificação de informações de registro para WinMDs nativos.|S|É possível especificar a correlação entre o arquivo .winmd e o arquivo .dll em SDKManifest.xml.|N||  
|O mecanismo dá suporte à especificação de dependências em outros SDKs.|S|O SDK apenas notifica o usuário; o usuário ainda deverá instalá-las e referenciá-las manualmente.|S|O NuGet as extrai automaticamente; o usuário não é notificado.|  
|O mecanismo integra-se a conceitos [!INCLUDE[win8_appstore_long](../includes/win8-appstore-long-md.md)] como o manifesto do aplicativo e a ID do Framework.|S|O SDK deve aprovar conceitos específicos do [!INCLUDE[win8_appstore_short](../includes/win8-appstore-short-md.md)] para que o empacotamento e o F5 funcionem corretamente com os SDKs disponíveis no [!INCLUDE[win8_appstore_short](../includes/win8-appstore-short-md.md)].|N||  
|O mecanismo integra-se aos pipelines de depuração de aplicativo para aplicativos [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)].|S|O SDK deve aprovar conceitos específicos do [!INCLUDE[win8_appstore_short](../includes/win8-appstore-short-md.md)] para que o empacotamento e F5 funcionem corretamente com os SDKs disponíveis no [!INCLUDE[win8_appstore_short](../includes/win8-appstore-short-md.md)].|S|O conteúdo do NuGet se torna parte do projeto. Nenhuma consideração F5 especial é necessária.|  
|O mecanismo se integra aos manifestos do aplicativo.|S|O SDK deve aprovar conceitos específicos do [!INCLUDE[win8_appstore_short](../includes/win8-appstore-short-md.md)] para que o empacotamento e F5 funcionem corretamente com os SDKs disponíveis no [!INCLUDE[win8_appstore_short](../includes/win8-appstore-short-md.md)].|S|O conteúdo do NuGet se torna parte do projeto. Nenhuma consideração F5 especial é necessária.|  
|O mecanismo implanta os arquivos de não referência (por exemplo, implante a estrutura de testes na qual os testes de aplicativos [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] serão executados).|S|Se você soltar os arquivos na pasta \redist, eles serão implantados automaticamente.|S||  
|O mecanismo adiciona automaticamente os SDKs da plataforma no IDE do Visual Studio.|S|Se você soltar o SDK do [!INCLUDE[win8](../includes/win8-md.md)] ou do Windows Phone em um local específico com um layout específico, o SDK será automaticamente integrado a todos os recursos do Visual Studio.|N||  
|O mecanismo dá suporte a um computador de desenvolvedor limpo. (Ou seja, não é necessária nenhuma instalação e a simples recuperação do controle do código-fonte funcionará.)|N|Como você referencia um SDK, é necessário verificar fazer check-in na sua solução e no SDK separadamente. É possível fazer check-in do SDK nos dois locais de não Registro padrão dos quais o MSBuild itera SDKs (para obter detalhes, consulte [Creating a Software Development Kit (Criando um Software Development Kit](../extensibility/creating-a-software-development-kit.md))). Como alternativa, se um local personalizado for composto dos SDKs, será possível especificar o código a seguir no arquivo de projeto:<br /><br /> `<PropertyGroup>    <SDKReferenceDirectoryRoot>C:\MySDKs</SDKReferenceDirectoryRoot>   </PropertyGroup>`<br /><br /> Em seguida, faça check-in dos SDKs nesse local.|S|É possível fazer check-out da solução e o Visual Studio reconhece imediatamente e age nos arquivos.|  
|É possível ingressar a uma grande comunidade existente de autores de pacotes.|N/D|A comunidade é nova.|S||  
|É possível ingressar em uma grande comunidade existente de consumidores de pacotes.|N/D|A comunidade é nova.|S||  
|É possível ingressar em um ecossistema de parceiros (galerias personalizadas, repositórios e assim por diante).|N/D|Os repositórios disponíveis incluem a Galeria do Visual Studio, o Centro de Download da Microsoft e [!INCLUDE[win8_appstore_long](../includes/win8-appstore-long-md.md)].|S||  
|O mecanismo se integra a servidores de build de integração contínua para criação e consumo de pacotes.|S|O SDK deve passar o local com check-in (propriedade SDKReferenceDirectoryRoot) na linha de comando para o MSBuild.|S||  
|O mecanismo dá suporte a versões do pacote estáveis e de pré-lançamento.|S|O SDK dá suporte à adição de referências a várias versões.|S||  
|O mecanismo dá suporte à atualização automática para pacotes instalados.|S|Se fornecido como VSIX ou como parte de atualizações automáticas do Visual Studio, o SDK oferece notificações automáticas.|S||  
|O mecanismo contém um arquivo .exe autônomo para criar e consumir pacotes.|S|O SDK contém MSBuild.exe.|S||  
|O check-in dos pacotes pode ser feito no controle de versão.|S|Não é possível fazer check-in fora do nó Documentos, o que significa que o check-in dos SDKs da Extensão não pode ser feito. O tamanho do SDK da Extensão pode ser grande.|S||  
|É possível usar uma interface do PowerShell para criar e consumir pacotes.|Y (consumo), N (criação)|Não há ferramentas para a criação de um SDK. Consumo está sendo executado o MSBuild na linha de comando.|S||  
|É possível usar um pacote de símbolos para o suporte à depuração.|S|Se você soltar arquivos .pdb no SDK, os arquivos são selecionados automaticamente.|S||  
|O mecanismo dá suporte a atualizações automáticas do gerenciador de pacotes.|N/D|O SDK é revisado com o MSBuild.|S||  
|O mecanismo dá suporte a um formato de manifesto leve.|S|O SDKManifest.xml dá suporte a muitos atributos, mas geralmente um pequeno subconjunto é necessário.|S||  
|O mecanismo está disponível para todas as edições do Visual Studio.|S|O SDK dá suporte a todas as edições do Visual Studio, desde o Visual Studio Express até o [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)].|S|O NuGet dá suporte a todas as edições do Visual Studio Express, do Express até o [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)].|  
|O mecanismo está disponível para todos os tipos de projeto.|N|O SDK dá suporte a aplicativos do [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] a partir do [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)].|N|É possível examinar uma lista de projetos permitidos.|  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando referências em um projeto](../ide/managing-references-in-a-project.md)



