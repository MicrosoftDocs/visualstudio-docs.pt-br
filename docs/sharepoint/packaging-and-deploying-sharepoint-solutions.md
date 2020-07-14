---
title: Empacotando e implantando soluções do SharePoint | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- packaging [SharePoint development in Visual Studio]
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, packaging and deploying
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9a4bf3394cf47b4f355fbe6a330ff5374e2da1c9
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015591"
---
# <a name="package-and-deploy-sharepoint-solutions"></a>Empacotar e implantar soluções do SharePoint
  Normalmente, uma solução do SharePoint é implantada em um servidor do SharePoint usando um arquivo de pacote de solução (. wsp). Você pode usar o Visual Studio para organizar seus itens de projeto do SharePoint em recursos e criar um pacote para implantar seus recursos do SharePoint.

 Este tópico fornece as seguintes informações:

- [Criar recursos e pacotes](#create-features-and-packages)

- [Suporte a ferramentas de recurso e empacotamento](#feature-and-packaging-tool-support)

- [Implantar soluções do SharePoint](#deploy-sharepoint-solutions)

- [Implantar arquivos em soluções do SharePoint](#deploy-files-in-sharepoint-solutions)

## <a name="create-features-and-packages"></a>Criar recursos e pacotes
 Você pode usar o Visual Studio para agrupar elementos relacionados do SharePoint em um *recurso*. Por exemplo, um recurso para uma definição de lista de contatos pode incluir a instância de lista e a definição de lista. Você pode combinar esses dois elementos em um único recurso para fins de implantação. Para obter mais informações sobre recursos, consulte [bloco de construção: recursos](/previous-versions/office/developer/sharepoint-2010/ee537350(v=office.14)).

 Em seguida, você pode criar um pacote de solução do SharePoint (*. wsp*) para agrupar vários recursos, definições de site, assemblies e outros arquivos em um único pacote, que armazena os arquivos em um formato necessário ao SharePoint para implantar os arquivos no servidor. Para obter mais informações, consulte [bloco de construção: soluções](/previous-versions/office/developer/sharepoint-2010/ee537008(v=office.14)).

## <a name="feature-and-packaging-tool-support"></a>Suporte a ferramentas de recurso e empacotamento
 Você pode usar as ferramentas de desenvolvimento do SharePoint no Visual Studio para organizar rapidamente seus arquivos do SharePoint em recursos e pacotes de solução para facilitar a implantação. Você pode usar as ferramentas a seguir para configurar o recurso e o pacote de solução.

- Designer de recursos e designer de pacotes.

- O Packaging Explorer, uma janela de ferramentas.

- Gerenciador de Soluções.

### <a name="feature-designer-and-package-designer"></a>Designer de recursos e designer de pacotes
 Você pode criar recursos, definir escopos e marcar outros recursos como dependências usando o designer de recursos. O designer também exibe o arquivo XML final que descreve cada recurso. Para obter mais informações, consulte [criar recursos do SharePoint](../sharepoint/creating-sharepoint-features.md).

 Aplique o recurso a um site ou grupo de sites específico definindo seu *escopo* no designer de recursos. Se um recurso for ativado para um site da Web individual, o recurso só funcionará nesse site específico. Se um recurso for ativado para um conjunto de sites, os itens no recurso se aplicarão a todo o conjunto de sites. Para obter mais informações, consulte [escopo do elemento](/previous-versions/office/developer/sharepoint-2010/ms476615(v=office.14)).

 Se seu recurso depender de outros recursos, você poderá definir uma *dependência de ativação de recurso* para marcar os recursos dependentes antes de disponibilizar o recurso. Uma dependência de ativação de recurso verifica se os recursos dependentes já estão ativados nesse escopo. Para obter mais informações, consulte [dependências e escopo de ativação](/previous-versions/office/developer/sharepoint-2010/aa543162(v=office.14)).

 No designer de pacotes, você pode agrupar elementos do SharePoint em um único pacote de solução e configurar se deseja redefinir o servidor Web durante a implantação. Para definir o tipo de servidor de implantação, use a janela **Propriedades** . O designer também gera o arquivo XML que descreve o conteúdo do pacote. Para obter mais informações, consulte [criar pacotes de solução do SharePoint](../sharepoint/creating-sharepoint-solution-packages.md).

 Durante a implantação, o serviço de Serviços de Informações da Internet (IIS) é interrompido para copiar os arquivos de solução para o servidor do SharePoint. Usando o designer de pacotes no Visual Studio, você pode selecionar se o servidor Web deve ser reiniciado. Para configurar se a solução for implantada em um servidor Web front-end ou um servidor de aplicativos, use a janela **Propriedades** . Para obter mais informações, consulte [elemento de solução (solução)](/previous-versions/office/developer/sharepoint-2010/ms412929(v=office.14)).

### <a name="packaging-explorer"></a>Gerenciador de empacotamento
 Para complementar o designer de recursos e o designer de pacotes, você pode usar o Gerenciador de pacotes para agrupar os arquivos do SharePoint em recursos e pacotes. Além disso, você pode ver a exibição hierárquica do pacote, recursos, itens de projeto do SharePoint e arquivos. O Gerenciador de empacotamento é uma janela de ferramentas que você pode usar para concluir as seguintes tarefas:

- Abra arquivos e itens de projeto do SharePoint.

- Arraste e solte itens de projeto do SharePoint de um recurso para outro.

- Arraste e solte itens e recursos de projeto do SharePoint de um pacote para outro.

- Adicione um novo recurso a um pacote.

- Abra um designer de recursos ou de pacotes.

- Valide recursos e pacotes.

  As ferramentas de desenvolvimento do SharePoint no Visual Studio têm regras de validação para ajudar a garantir que o pacote de solução esteja formado corretamente. Além disso, as regras verificam se o arquivo da solução *. wsp* pode ser implantado e ativado com êxito em um servidor do SharePoint. Para obter mais informações sobre o esquema XML para recursos, consulte [esquemas](/previous-versions/office/developer/sharepoint-2010/ms414322(v=office.14))de recursos.

  Você pode adicionar regras de validação de pacote e recurso personalizado ao sistema de projeto do SharePoint. Para obter mais informações, consulte [como criar regras personalizadas de validação de pacotes e recursos para soluções do SharePoint](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md).

  Para obter mais informações sobre o Gerenciador de pacotes, consulte [como adicionar e remover recursos e itens para um pacote usando o Gerenciador de empacotamento](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md).

### <a name="solution-explorer"></a>Gerenciador de Soluções
 Você pode usar Gerenciador de Soluções para navegar e abrir os arquivos do projeto do SharePoint. Use o menu de contexto no Gerenciador de Soluções para adicionar recursos, receptores de eventos de recurso e recursos de recurso. Além disso, você pode abrir os designers de recursos e os designers de pacote para configurar os recursos e pacotes para implantação.

## <a name="deploy-sharepoint-solutions"></a>Implantar soluções do SharePoint
 Depois de personalizar os recursos e o pacote no Visual Studio, você pode criar um arquivo *. wsp* para implantar nos servidores do SharePoint. Você pode usar o Visual Studio para depurar e testar o. *WSP* somente no servidor do SharePoint no computador de desenvolvimento. Para obter mais informações sobre como implantar suas soluções do SharePoint em um servidor remoto do SharePoint, consulte [implantando uma solução](/previous-versions/office/developer/sharepoint-2010/aa544500(v=office.14)).

 Você também pode personalizar as etapas de implantação no computador de desenvolvimento. Para obter mais informações, consulte [implantar, publicar e atualizar pacotes de solução do SharePoint](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md).

## <a name="deploy-files-in-sharepoint-solutions"></a>Implantar arquivos em soluções do SharePoint
 Normalmente, quando você adiciona um item de projeto do SharePoint à sua solução do SharePoint, todos os arquivos necessários são incluídos. Os arquivos que podem ser compilados (arquivos de código) são incorporados ao assembly de saída da solução. No entanto, você também pode adicionar arquivos não compiláveis, por exemplo, *. xml*, *. txt*ou arquivos de recurso, a um projeto do SharePoint. Esses arquivos não são empacotados automaticamente em sua solução. Para garantir que eles sejam empacotados, adicione os arquivos a uma pasta mapeada ou a um item de projeto do SharePoint.

 Os arquivos adicionados às pastas mapeadas são copiados automaticamente para o hive do SharePoint quando a solução é implantada. Os arquivos adicionados a um item de projeto do SharePoint são implantados no local especificado na propriedade **local de implantação** para cada arquivo, que é parcialmente definido com base na Propriedade do **tipo de implantação** . Por padrão, o valor da Propriedade do **tipo de implantação** é **NoDeployment**, o que significa que o arquivo não é implantado com a solução. Você deve definir outro valor para a propriedade para incluir o arquivo no pacote.

 Por exemplo, para adicionar um arquivo *. xml* a um projeto do SharePoint, execute uma destas ações:

- Adicione uma pasta mapeada de "layouts" do SharePoint ao seu projeto. Isso cria em **Gerenciador de soluções** uma pasta denominada **layouts** que tem uma subpasta para o projeto. Adicione o arquivo *. xml* à nova subpasta. Por padrão, o arquivo é implantado no sistema de arquivos do SharePoint em *.. \\\TEMPLATE\LAYOUTS \<Folder Name> *. Para obter informações sobre como adicionar pastas mapeadas, consulte [como adicionar e remover pastas mapeadas](../sharepoint/how-to-add-and-remove-mapped-folders.md).

- Adicione o arquivo *. xml* à pasta de um item de projeto do SharePoint e, em seguida, altere a propriedade **tipo de implantação** do arquivo *. xml* de **NoDeployment** para outra configuração, como **RootFile** ou **ElementFile**. A configuração apropriada do **tipo de implantação** depende do arquivo e do projeto. Para obter mais informações sobre as configurações de Propriedade do **tipo de implantação** , consulte [desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md).

  Se um arquivo adicionado não se aplicar a qualquer projeto específico na solução, você poderá adicionar um projeto do SharePoint vazio à sua solução e, em seguida, adicionar os arquivos adicionais a ele. Outra alternativa para implantar arquivos no SharePoint, especialmente no banco de dados de conteúdo, é adicionar um módulo ao projeto e, em seguida, adicionar os arquivos ao módulo. Para obter mais informações, consulte [usar módulos para incluir arquivos na solução](../sharepoint/using-modules-to-include-files-in-the-solution.md).

## <a name="see-also"></a>Consulte também
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
- [Compilar e depurar soluções do SharePoint](../sharepoint/building-and-debugging-sharepoint-solutions.md)
