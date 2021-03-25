---
title: 'Área de teste 1: Adicionar To-Open do controle do código-fonte | Microsoft Docs'
description: Esta área de teste de plug-in de controle de origem aborda a colocação de soluções ou projetos sob controle do código-fonte e sua recuperação no controle do código-fonte.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], adding and opening solutions
- source control plug-ins, adding and opening solutions
ms.assetid: 5b3b5b08-5e9b-41be-ac72-c63957faed22
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 174834dde4c049bcb1b3fd8bc2eb8e82166d01d4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078676"
---
# <a name="test-area-1-add-toopen-from-source-control"></a>Área de teste 1: Adicionar/abrir do controle do código-fonte
Esta área de teste de plug-in de controle de origem aborda a colocação de soluções ou projetos sob controle do código-fonte e sua recuperação no controle do código-fonte.

## <a name="command-menu-access"></a>Acesso ao menu de comando
 Os seguintes [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] caminhos de menu do ambiente de desenvolvimento integrado são usados nos casos de teste:

- Para o [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] , abra do controle do código-fonte: **arquivo**, **abrir**, solução de **projeto** / ; examine o [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] local.

- Para outros plug-ins de controle de origem, abra do controle do código-fonte: **arquivo**, **controle do código-fonte**, **Abrir do controle do código-** fonte.

- Adicionar ao controle do código-fonte: **arquivo**, **controle do código-fonte**, **Adicionar solução ao arquivo de controle do código-** fonte, **controle de origem**, **adicionar projetos selecionados ao controle do código-fonte**

- Menu de atalho (projeto/solução), **Adicionar solução ao controle do código-fonte**.

- Adicionar do controle do código-fonte: **arquivo**, **controle do código-fonte**, **Adicionar projeto do controle do código-** fonte.

- Para o [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] , adicionar do controle do código-fonte também está disponível em **arquivo**, **Adicionar**, **projeto existente**; examinar o [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] local.

  > [!NOTE]
  > Um caminho de um arquivo local ou um IIS local (servidor Web) pode ser usado neste teste.

## <a name="expected-behavior"></a>Comportamento esperado

- Para cada tipo de projeto com suporte, um usuário deve ser capaz de "adicionar ao" e "abrir de" controle de origem.

- Quando um projeto é adicionado ao controle do código-fonte, um \<*ProjectName*> arquivo. vspscc correspondente (arquivo de dica de projeto) é criado. Ele contém informações de conexão e lista de arquivos de exclusão. Não exclua este arquivo porque ele contém informações específicas para o projeto.

- Quando uma solução é adicionada ao controle do código-fonte, um \<*SolutionName*> arquivo. vssscc (Triple S) correspondente é criado. O arquivo de texto contém informações de conexão e uma lista de arquivos de exclusão, semelhante ao arquivo de dica de projeto. Esse arquivo é temporário e existe somente no banco de dados de controle do código-fonte.

- Quando uma solução é aberta do controle do código-fonte, um \<*SolutionName*> arquivo. vsscc (duplo S) que existe somente no banco de dados de controle do código-fonte, é criado localmente em um arquivo temporário. Esse arquivo contém o caminho da pasta de conexão da solução para o arquivo de solução. Esse arquivo é temporário e a cópia local é excluída quando a operação "abrir do controle do código-fonte" for concluída.

- Depois que um projeto é adicionado ao controle do código-fonte, você pode executar qualquer ação de controle do código-fonte nele (fazer check-out, Get e assim por diante).

## <a name="test-cases"></a>Casos de teste
 Veja a seguir os casos de teste específicos para a área de teste adicionar a/abrir do controle do código-fonte.

### <a name="case-1a-add-solution-to-source-control"></a>Caso 1a: Adicionar solução ao controle do código-fonte
 Esse caso de teste se concentra em Adicionar soluções ao controle do código-fonte.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Adicionar solução que contém um projeto de cliente ao controle do código-fonte|1. criar um projeto de cliente.<br />2. Adicione a solução ao controle do código-fonte (**arquivo**, **controle do código-fonte**, **Adicionar solução ao controle do código-fonte**).|Solução/projeto foi adicionado ao controle do código-fonte.|
|Adicionar solução que contém um sistema de arquivos ou projeto Web local do IIS ao controle do código-fonte|1. Crie um sistema de arquivos ou um projeto Web local do IIS (use o botão procurar para apontar para o local do projeto; o caminho determina que tipo de projeto Web é criado).<br />2. Adicione a solução ao controle do código-fonte (**arquivo**, **controle do código-fonte**, **Adicionar solução ao controle do código-fonte**).|Solução/projeto foi adicionado ao controle do código-fonte.|
|Adicionar solução que contém um projeto Web do site remoto ao controle do código-fonte|1. criar um projeto Web de site remoto.<br />2. Adicione a solução ao controle do código-fonte (**arquivo**, **controle do código-fonte**, **Adicionar solução ao controle do código-fonte**).<br />3. clique em **OK** na caixa de diálogo aviso de acesso do FrontPage.|A solução foi adicionada ao controle do código-fonte.<br /><br /> O projeto de site remoto não está no controle do código-fonte. (Os projetos de site remoto devem ser controlados de seu próprio servidor IIS.)|
|Adicione uma única solução de projeto ao controle do código-fonte usando **adicionar projetos selecionados ao controle do código-fonte**.|1. Crie uma única solução de projeto.<br />2. Adicione apenas a solução ao controle do código-fonte como uma seleção (**arquivo**, **controle do código-fonte**, **adicionar projetos selecionados ao controle do código-fonte**). Se essa etapa for concluída com sucesso, continue na próxima etapa.<br />3. Adicionar projeto ao controle do código-fonte como seleção (**arquivo**, **controle do código-fonte**, **adicionar projetos selecionados ao controle do código-fonte**).<br />4. clique em **Sim** para adicionar o projeto ao mesmo local.<br />5. clique em **fazer check-out** na caixa **de diálogo fazer check-out para editar** .|`Result from Step 2:`<br /><br /> O projeto e todos os arquivos dentro do projeto têm um indicador de controle do código-fonte extraído e uma dica de ferramenta exibe "não está sob controle do código-fonte".<br /><br /> `Result from Step 5:`<br /><br /> O projeto e o arquivo de solução estão na mesma pasta no controle do código-fonte.|
|Cancelar a adição de uma solução ao controle do código-fonte|1. Crie uma única solução de projeto.<br />2. tentativa de Adicionar projeto e solução ao controle do código-fonte. Se essa etapa for concluída com sucesso, continue na próxima etapa.<br />3. cancele depois que você estiver no sistema de controle do código-fonte.|`Result from Step 2:`<br /><br /> A caixa de diálogo Definir controle de origem do local do projeto é exibida apenas uma vez.<br /><br /> `Result from Step 3:`<br /><br /> O projeto adicionado cancelado, projeto/solução não está sob controle do código-fonte e todos os menus adicionar ao controle do código-fonte ainda estão disponíveis.|

### <a name="case-1b-open-solution-from-source-control"></a>Caso 1B. Abrir solução do controle do código-fonte
 Esse caso de teste se concentra na abertura de soluções do controle do código-fonte.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Abrir uma solução que contém um projeto de cliente do controle do código-fonte|1. criar um projeto de cliente.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Feche a solução.<br />4. Abra a solução do controle do código-fonte para um novo local.|Solução/projeto aberto do controle do código-fonte.|
|Abrir uma solução que contém um projeto Web local ou IIS do controle do código-fonte|1. Crie um projeto Web local ou IIS.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Feche a solução.<br />4. Abra a solução do controle do código-fonte para um novo local.|Solução/projeto aberto do controle do código-fonte.|
|Abrir uma solução que contém um projeto Web de site remoto do controle do código-fonte|1. criar um projeto Web de site remoto.<br />2. Adicione a solução ao controle do código-fonte. Se essa etapa for concluída com sucesso, continue na próxima etapa.<br />3. Feche a solução.<br />4. Abra a solução do controle do código-fonte para um novo local.|`Result from Step 2:`<br /><br /> A Web do site remoto não está no controle do código-fonte.<br /><br /> `Result from Step 4:`<br /><br /> Solução aberta do controle do código-fonte.<br /><br /> O projeto de site remoto está carregado, mas não está no controle do código-fonte.|

### <a name="case-1c-add-solution-from-source-control"></a>Caso 1C: Adicionar solução do controle do código-fonte
 Esse caso de teste se concentra em Adicionar soluções do controle do código-fonte.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Adicionar à solução vazia — uma única solução de projeto|1. Crie uma única solução de projeto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Feche a solução.<br />4. Crie uma segunda solução vazia.<br />5. Adicione a solução controlada anteriormente do controle do código-fonte (**arquivo**, **controle do código-fonte**, **Adicionar projeto do controle do código-fonte**).|O projeto adicionado aparece na **Gerenciador de soluções** e é feito check-in.|
|Adicionar à solução com um único projeto — único projeto|1. Crie uma solução com um único projeto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Feche a solução.<br />4. Crie uma segunda solução vazia.<br />5. Adicione a solução controlada anteriormente do controle do código-fonte (**arquivo**, **controle do código-fonte**, **Adicionar projeto do controle do código-fonte**).|O projeto adicionado aparece na **Gerenciador de soluções** e é feito check-in.|
|Adicionar à solução — solução adicionada ao controle do código-fonte por seleção|1. Crie uma solução com um projeto.<br />2. Adicione apenas a solução ao controle do código-fonte como seleção. Se essa etapa for concluída com sucesso, continue na próxima etapa.<br />3. Feche a solução.<br />4. Crie uma nova solução.<br />5. Adicione a solução controlada anteriormente do controle do código-fonte (**arquivo**, **controle do código-fonte**, **Adicionar projeto do controle do código-fonte**).|`Result from Step 2:`<br /><br /> O projeto não está no controle do código-fonte.<br /><br /> `Result from Step 5:`<br /><br /> Se a primeira solução tiver itens de solução, eles não poderão ser adicionados do controle do código-fonte, portanto, eles não aparecerão.<br /><br /> O projeto da primeira solução aparece como indisponível.|

## <a name="see-also"></a>Confira também
- [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
