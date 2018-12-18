---
title: 'Área de teste 1: Adicionar ao / abrir do controle de origem | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- source control [Visual Studio SDK], adding and opening solutions
- source control plug-ins, adding and opening solutions
ms.assetid: 5b3b5b08-5e9b-41be-ac72-c63957faed22
caps.latest.revision: 21
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 1ab1a267984f1a50cfd8e95cc8217572c0dacbcf
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51746655"
---
# <a name="test-area-1-add-toopen-from-source-control"></a>Área de teste 1: Adicionar ao / abrir do controle de origem
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Esse controle de origem plug-in de teste área abrange colocando soluções ou projetos sob controle do código-fonte e recuperá-los do controle de origem.  
  
## <a name="command-menu-access"></a>Acesso ao Menu de comando  
 O seguinte [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] caminhos de menu de ambiente de desenvolvimento integrado são usados nos casos de teste:  
  
-   Para [!INCLUDE[vsvss](../../includes/vsvss-md.md)], abra do controle de origem: **arquivo**, **abra**, **projeto**/**solução**; procure no [!INCLUDE[vsvss](../../includes/vsvss-md.md)] local.  
  
-   Para outras fonte plug-ins de controle, abrir do controle de origem: **arquivo**, **controle do código-fonte**, **abrir do controle de origem**.  
  
-   Adicionar ao controle do código-fonte: **arquivo**, **controle do código-fonte**, **adicionar solução ao arquivo de controle do código-fonte**, **controle do código-fonte**, **adicionar Projetos ao controle de origem selecionados**.  
  
-   Menu de atalho (projeto/solução), **adicionar solução ao controle do código-fonte**.  
  
-   Adicionar do controle de origem: **arquivo**, **controle do código-fonte**, **Adicionar projeto do controle do código-fonte**.  
  
-   Para [!INCLUDE[vsvss](../../includes/vsvss-md.md)], adicionar controle do código-fonte também está disponível no **arquivo**, **Add**, **projeto existente**; procure no [!INCLUDE[vsvss](../../includes/vsvss-md.md)] local.  
  
    > [!NOTE]
    >  Um caminho de um arquivo local ou um local IIS (servidor web) pode ser usado nesse teste.  
  
## <a name="expected-behavior"></a>Comportamento esperado  
  
-   Para cada tipo de projeto com suporte, um usuário deve ser capaz de "Adicionar ao" e "Aberta do" controle de origem.  
  
-   Quando um projeto é adicionado ao controle de origem, um correspondente \< *ProjectName*> vspscc (arquivo de dica de projeto) é criado. Ele contém informações de conexão e de lista do arquivo de exclusão. Não exclua esse arquivo porque ele contém informações específicas do projeto.  
  
-   Quando uma solução é adicionada ao controle do código-fonte, um correspondente \< *SolutionName*> vssscc (triplo S) de arquivo é criado. O arquivo de texto contém informações de conexão e uma lista de arquivos de exclusão, semelhante ao arquivo de dica de projeto. Esse arquivo é temporário e existe somente no banco de dados de controle de origem.  
  
-   Quando uma solução é aberta do controle do código-fonte, uma \< *SolutionName*> .vsscc (double S) arquivo que existe somente no banco de dados de controle do código-fonte, é criado localmente em um arquivo temporário. Esse arquivo contém o caminho da pasta de solução de conexão para o arquivo de solução. Esse arquivo é temporário e a cópia local é excluída quando a operação de "Abrir do controle de origem" foi concluída.  
  
-   Depois que um projeto é adicionado ao controle de origem, você pode executar as ações de controle do código-fonte nele (Check-out, Get e assim por diante).  
  
## <a name="test-cases"></a>Casos de teste  
 Estes são os casos de teste específicos para adicionar aberto na área de teste de controle de origem de / para.  
  
### <a name="case-1a-add-solution-to-source-control"></a>Caso 1a: Adicionar solução ao controle do código-fonte  
 Esse caso de teste se concentra em Adicionar soluções ao controle do código-fonte.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Adicionar a solução que contém um projeto de cliente ao controle de origem|1.  Crie um projeto de cliente.<br />2.  Adicione a solução ao controle de origem (**arquivo**, **controle do código-fonte**, **adicionar solução ao controle do código-fonte**).|Projeto/solução foi adicionado ao controle de origem.|  
|Adicionar a solução que contém um sistema de arquivos ou um projeto Web do IIS local ao controle de origem|1.  Criar um sistema de arquivos ou o projeto da Web do IIS local (use o botão Procurar para apontar para o local do projeto; o caminho determina que tipo de projeto da Web é criado).<br />2.  Adicione a solução ao controle de origem (**arquivo**, **controle do código-fonte**, **adicionar solução ao controle do código-fonte**).|Projeto/solução foi adicionado ao controle de origem.|  
|Adicionar solução contendo um projeto Web do Site remoto ao controle de origem|1.  Crie um projeto Web do Site remoto.<br />2.  Adicione a solução ao controle de origem (**arquivo**, **controle do código-fonte**, **adicionar solução ao controle do código-fonte**).<br />3.  Clique em **Okey** na caixa de diálogo de aviso de acesso do FrontPage.|Solução foi adicionada ao controle de origem.<br /><br /> Projeto de Site remoto não está sob controle do código-fonte. (Projetos de Site remoto devem ser controlados pelo seu próprio servidor IIS.)|  
|Adicionar uma solução de projeto único ao controle do código-fonte usando **adicionar projetos selecionados ao controle do código-fonte**.|1.  Crie uma solução de projeto único.<br />2.  Adicione apenas a solução ao controle de origem como uma seleção (**arquivo**, **controle do código-fonte**, **adicionar projetos selecionados ao controle do código-fonte**). Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />3.  Adicionar projeto ao controle de origem como seleção (**arquivo**, **controle do código-fonte**, **adicionar projetos selecionados ao controle do código-fonte**).<br />4.  Clique em **Sim** para adicionar o projeto no mesmo local.<br />5.  Clique em **Check-Out** na **Check-Out para edição** caixa de diálogo.|`Result from Step 2:`<br /><br /> O projeto e todos os arquivos dentro do projeto têm um check-out do indicador de controle do código-fonte e uma dica de ferramenta exibe "não está sob controle do código-fonte".<br /><br /> `Result from Step 5:`<br /><br /> Arquivo de projeto e solução estão na mesma pasta no controle de origem.|  
|Cancelar a adição de uma solução ao controle de origem|1.  Crie uma solução de projeto único.<br />2.  Tentativa de adicionar o projeto e solução ao controle de origem. Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />3.  Cancele depois que você está no sistema de controle do código-fonte.|`Result from Step 2:`<br /><br /> Caixa de diálogo de controle de origem o conjunto de projeto local é exibido apenas uma vez.<br /><br /> `Result from Step 3:`<br /><br /> Projeto Adicionar cancelado, projeto/solução não está sob controle do código-fonte e tudo que adicionar a menus de controle do código-fonte ainda estão disponíveis.|  
  
### <a name="case-1b-open-solution-from-source-control"></a>Caso 1b. Abrir solução do controle de origem  
 Esse caso de teste se concentra na abertura de soluções de controle de origem.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Abrir uma solução contendo um projeto de cliente do controle de origem|1.  Crie um projeto de cliente.<br />2.  Adicione a solução ao controle de origem.<br />3.  Feche a solução.<br />4.  Abra a solução de controle de origem para um novo local.|Solução/projeto aberto do controle do código-fonte.|  
|Abra uma solução que contém um local ou um projeto Web do IIS do controle de origem|1.  Crie um projeto de Web do IIS ou local.<br />2.  Adicione a solução ao controle de origem.<br />3.  Feche a solução.<br />4.  Abra a solução de controle de origem para um novo local.|Solução/projeto aberto do controle do código-fonte.|  
|Abrir uma solução contendo um projeto Web do Site remoto do controle de origem|1.  Crie um projeto Web do Site remoto.<br />2.  Adicione a solução ao controle de origem. Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />3.  Feche a solução.<br />4.  Abra a solução de controle de origem para um novo local.|`Result from Step 2:`<br /><br /> Web de Site remoto não está sob controle do código-fonte.<br /><br /> `Result from Step 4:`<br /><br /> Solução aberta do controle do código-fonte.<br /><br /> Projeto de Site remoto for carregado, mas não está sob controle do código-fonte.|  
  
### <a name="case-1c-add-solution-from-source-control"></a>Caso c 1: adicionar a solução de controle de origem  
 Esse caso de teste se concentra na adição de soluções de controle de origem.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Adicionar a solução vazia — uma solução de projeto único|1.  Crie uma solução de projeto único.<br />2.  Adicione a solução ao controle de origem.<br />3.  Feche a solução.<br />4.  Crie uma segunda solução vazia.<br />5.  Adicionar a solução controlada anteriormente do controle de origem (**arquivo**, **controle do código-fonte**, **Adicionar projeto do controle de origem**).|O projeto adicionado aparece no **Gerenciador de soluções** e check-in.|  
|Adicionar à solução com um único projeto — único projeto|1.  Crie uma solução com um único projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Feche a solução.<br />4.  Crie uma segunda solução vazia.<br />5.  Adicionar a solução controlada anteriormente do controle de origem (**arquivo**, **controle do código-fonte**, **Adicionar projeto do controle de origem**).|O projeto adicionado aparece no **Gerenciador de soluções** e check-in.|  
|Adicionar a solução — solução adicionada ao controle do código-fonte por seleção|1.  Crie uma solução com um projeto.<br />2.  Adicione apenas a solução ao controle de origem como seleção. Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />3.  Feche a solução.<br />4.  Crie uma nova solução.<br />5.  Adicionar a solução controlada anteriormente do controle de origem (**arquivo**, **controle do código-fonte**, **Adicionar projeto do controle de origem**).|`Result from Step 2:`<br /><br /> Projeto não está sob controle do código-fonte.<br /><br /> `Result from Step 5:`<br /><br /> Se a primeira solução tinha itens de solução, eles não podem ser adicionados do controle do código-fonte, para que eles não aparecem.<br /><br /> Projeto da solução primeiro aparece como não disponível.|  
  
## <a name="see-also"></a>Consulte também  
 [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)

