---
title: Empacotando e implantando soluções do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- packaging [SharePoint development in Visual Studio]
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, packaging and deploying
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6c5993f09581faf6e3cedb4c71598ea26b16b699
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49863263"
---
# <a name="package-and-deploy-sharepoint-solutions"></a>Empacotar e implantar soluções do SharePoint
  Normalmente, uma solução do SharePoint é implantada em um servidor do SharePoint usando um arquivo de pacote (. wsp) da solução. Você pode usar o Visual Studio para organizar os itens de projeto do SharePoint em recursos e criar um pacote para implantar seus recursos do SharePoint.  
  
 Este tópico fornece as seguintes informações:  
  
-   [Criando recursos e pacotes](#Creating)  
  
-   [Recursos e suporte à ferramenta de empacotamento](#Tools)  
  
-   [Implantando soluções do SharePoint](#Deploying)  
  
-   [Implantando arquivos em soluções do SharePoint](#DeployingFiles)  
  
## <a name="create-features-and-packages"></a>Criar recursos e pacotes
 Você pode usar o Visual Studio para agrupar elementos relacionados do SharePoint em um *recurso*. Por exemplo, um recurso para uma definição de lista de contatos pode incluir a instância de lista e a definição de lista. Você pode combinar esses dois elementos em um único recurso para fins de implantação. Para obter mais informações sobre recursos, consulte [bloco de construção: recursos](http://go.microsoft.com/fwlink/?LinkID=169183).  
  
 Em seguida, você pode criar um pacote de solução do SharePoint (*. wsp*) para agrupar vários recursos, site definições, assemblies e outros arquivos em um único pacote, que armazena os arquivos em um formato necessário pelo SharePoint para implantar os arquivos para o servidor. Para obter mais informações, consulte [bloco de construção: soluções](http://go.microsoft.com/fwlink/?LinkID=169186).  
  
## <a name="feature-and-packaging-tool-support"></a>Recursos e suporte de ferramenta de empacotamento
 Você pode usar as ferramentas de desenvolvimento do SharePoint no Visual Studio para organizar rapidamente os arquivos do SharePoint em recursos e pacotes de solução para facilitar a implantação. Você pode usar as ferramentas a seguir para configurar o pacote de solução e de recurso.  
  
-   Designer de recursos e o Designer de pacote.  
  
-   Gerenciador de empacotamento, uma janela de ferramentas.  
  
-   Gerenciador de soluções.  
  
### <a name="feature-designer-and-package-designer"></a>Designer de recursos e o designer de pacote
 Você pode criar recursos, definir escopos e marcar outros recursos como dependências usando o Designer de recursos. O designer também exibe o arquivo XML final que descreve cada recurso. Para obter mais informações, consulte [recursos do SharePoint criar](../sharepoint/creating-sharepoint-features.md).  
  
 Aplicar o recurso a um site específico ou um grupo de sites da Web, definindo sua *escopo* no Designer de recurso. Se um recurso é ativado para um site individual, o recurso só funciona no site da Web específico. Se um recurso é ativado para um conjunto de sites, os itens no recurso se aplicam ao conjunto de sites inteiro. Para obter mais informações, consulte [escopo elemento](http://go.microsoft.com/fwlink/?LinkID=169189).  
  
 Se o recurso depende de outros recursos, você pode definir um *dependência de ativação de recursos* para marcar os recursos dependentes antes de disponibilizar seu recurso. Uma dependência de ativação do recurso verifica se os recursos dependentes já estiverem ativados nesse escopo. Para obter mais informações, consulte [dependências de ativação e escopo](http://go.microsoft.com/fwlink/?LinkID=169190).  
  
 No Designer de pacote, você pode agrupar os elementos do SharePoint em um pacote de solução única e configurar se deseja redefinir o servidor Web durante a implantação. Para definir o tipo de servidor de implantação, use o **propriedades** janela. O designer também gera o arquivo XML que descreve o conteúdo do pacote. Para obter mais informações, consulte [pacotes de soluções do SharePoint criar](../sharepoint/creating-sharepoint-solution-packages.md).  
  
 Durante a implantação, o serviço de serviços de informações da Internet (IIS) é interrompido para copiar os arquivos de solução para o servidor do SharePoint. Usando o Designer de pacote no Visual Studio, você pode selecionar se o servidor Web deve ser reiniciado. Para configurar se a solução for implantada em um servidor Web front-end ou um servidor de aplicativos, use o **propriedades** janela. Para obter mais informações, consulte [elemento Solution (solução)](http://go.microsoft.com/fwlink/?LinkID=169191).  
  
### <a name="packaging-explorer"></a>Packaging Explorer  
 Para complementar o Designer de recursos e o Designer de pacote, você pode usar o Packaging Explorer para agrupar seus arquivos do SharePoint em recursos e pacotes. Além disso, você pode ver a exibição hierárquica de projeto do SharePoint de pacote, recursos, itens e os arquivos. O Packaging Explorer é uma janela de ferramentas que você pode usar para concluir as seguintes tarefas:  
  
- Abrir itens de projeto do SharePoint e arquivos.  
  
- Arraste e solte itens de projeto do SharePoint de um recurso para outro.  
  
- Arraste e solte itens de projeto do SharePoint e recursos de um pacote para outro.  
  
- Adicione um novo recurso a um pacote.  
  
- Abra um designer de pacote ou recurso.  
  
- Valide recursos e pacotes.  
  
  As ferramentas de desenvolvimento do SharePoint no Visual Studio tem regras de validação para ajudar a garantir que o pacote de solução está formado corretamente. Além disso, as regras de verificam se o *. wsp* arquivo da solução pode ser implantado e ativado em um servidor do SharePoint com êxito. Para obter mais informações sobre o esquema XML para os recursos, consulte [esquemas de recurso](http://go.microsoft.com/fwlink/?LinkID=169192).  
  
  Você pode adicionar o recurso personalizado e regras de validação de pacote para o sistema de projeto do SharePoint. Para obter mais informações, consulte [como: criar o recurso personalizado e o pacote de regras de validação para soluções do SharePoint](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md).  
  
  Para obter mais informações sobre o Gerenciador de pacotes, consulte [como: adicionar e remover funcionalidades e itens de um pacote usando o Packaging Explorer](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md).  
  
### <a name="solution-explorer"></a>Gerenciador de Soluções
 Você pode usar o Gerenciador de soluções para navegar e abrir os arquivos de projeto do SharePoint. Use o menu de contexto no Gerenciador de soluções para adicionar recursos, receptores de evento e recursos de recursos. Além disso, você pode abrir os Designers de recurso e os Designers de pacote para configurar os recursos e pacotes para a implantação.  
  
## <a name="deploy-sharepoint-solutions"></a>Implantar soluções do SharePoint
 Depois de personalizar os recursos e o pacote no Visual Studio, você pode criar uma *. wsp* arquivo para implantar em servidores do SharePoint. Você pode usar o Visual Studio para depurar e testar o. *wsp* somente no servidor do SharePoint no computador de desenvolvimento. Para obter mais informações sobre como implantar suas soluções do SharePoint em um servidor remoto do SharePoint, consulte [Implantando uma solução](http://go.microsoft.com/fwlink/?LinkID=169194).  
  
 Você também pode personalizar as etapas de implantação no computador de desenvolvimento. Para obter mais informações, consulte [implantar, publicar e atualizar pacotes de solução do SharePoint](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md).  
  
## <a name="deploy-files-in-sharepoint-solutions"></a>Implantar arquivos em soluções do SharePoint
 Normalmente, quando você adiciona um item de projeto do SharePoint para sua solução do SharePoint, todos os arquivos necessários estão incluídos. Arquivos que podem ser compilados (arquivos de código) são compilados no assembly de saída da solução. No entanto, talvez você também precise adicionar arquivos não compilável, por exemplo, *. XML*, *. txt*, ou arquivos de recurso para um projeto do SharePoint. Esses arquivos não são empacotados automaticamente em sua solução. Para garantir que eles são empacotados, adicione os arquivos para uma pasta mapeada ou a um item de projeto do SharePoint.  
  
 Arquivos adicionados a pastas mapeadas são copiados automaticamente para o hive do SharePoint quando a solução é implantada. Arquivos adicionados a um item de projeto do SharePoint são implantados no local especificado na **local de implantação** propriedade para cada arquivo, que é parcialmente definido com base nas **tipo de implantação** propriedade. Por padrão, o **tipo de implantação** é o valor da propriedade **NoDeployment**, que significa que o arquivo não está implementado com a solução. Você deve definir outro valor para a propriedade incluir o arquivo no pacote.  
  
 Por exemplo, para adicionar um *. XML* o arquivo para um projeto do SharePoint, execute uma destas ações:  
  
- Adicione uma pasta mapeada do SharePoint "Layouts" ao seu projeto. Isso cria nos **Gerenciador de soluções** uma pasta chamada **Layouts** que possui uma subpasta do projeto. Adicione a *. XML* arquivo para a nova subpasta. Por padrão, o arquivo é implantado para o sistema de arquivos do SharePoint *... \Template\layouts.\\\<nome da pasta >*. Para obter informações sobre como adicionar pastas mapeadas, consulte [como: adicionar e remover pastas mapeadas](../sharepoint/how-to-add-and-remove-mapped-folders.md).  
  
- Adicionar o *. XML* arquivos para a pasta de um item de projeto do SharePoint e, em seguida, altere o **tipo de implantação** propriedade do *. XML* arquivo da **NoDeployment**  para definir outro como **RootFile** ou **ElementFile**. Apropriado **tipo de implantação** configuração depende do arquivo e o projeto. Para obter mais informações sobre o **tipo de implantação** configurações de propriedade, consulte [soluções do SharePoint desenvolver](../sharepoint/developing-sharepoint-solutions.md).  
  
  Se um arquivo adicionado não se aplica a nenhum projeto específico na solução, você pode adicionar um projeto vazio do SharePoint à sua solução e, em seguida, adicionar os arquivos adicionais a ele. Outra alternativa para implantação de arquivos para o SharePoint, especialmente para o banco de dados de conteúdo, é adicionar um módulo ao projeto e, em seguida, adicione os arquivos para o módulo. Para obter mais informações, consulte [usar módulos para incluir arquivos na solução](../sharepoint/using-modules-to-include-files-in-the-solution.md).  
  
## <a name="see-also"></a>Consulte também
 [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)   
 [Compilar e depurar soluções do SharePoint](../sharepoint/building-and-debugging-sharepoint-solutions.md)  
  
