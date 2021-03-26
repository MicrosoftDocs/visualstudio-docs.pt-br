---
title: 'Área de teste 7: compartilhar | Microsoft Docs'
description: Essa área de teste do controle do código-fonte aborda o compartilhamento de itens entre locais usando o comando compartilhar para o seu plug-in de controle do código-fonte do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], sharing items
- source control plug-ins, sharing items
ms.assetid: 6ec4780a-bda4-4327-bb3e-c6c9e7eabf35
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: facfb48fbe02ff374c594f1ddadf0710c1f989d6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074347"
---
# <a name="test-area-7-share"></a>Área de teste 7: Compartilhar
Essa área de teste aborda o compartilhamento de itens entre locais por meio do comando **compartilhar** .

 Uma operação hhare é a duplicação aparente de arquivos e itens de pasta entre dois ou mais locais dentro de uma hierarquia de arquivos de controle do código-fonte. Na verdade, a duplicação não ocorre no servidor, mas o usuário vê o mesmo arquivo em dois ou mais locais especificados. Sempre que forem feitas alterações em qualquer um dos itens compartilhados, essas alterações aparecerão em todos os outros locais compartilhados.

 O compartilhamento em pastas funciona se você selecionar uma pasta com pelo menos um arquivo sob controle do código-fonte. O comando compartilhar é desabilitado sob as seguintes condições:

- Se a pasta selecionada for uma pasta vazia.

- Se houver uma pasta real, mas não contiver nenhum arquivo de controle do código-fonte.

- Se houver uma pasta virtual, se os arquivos sob controle do código-fonte estão ou não.

- Se houver um projeto Web de site remoto.

## <a name="command-menu-access"></a>Acesso ao menu de comando
 Os seguintes [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] caminhos de menu do ambiente de desenvolvimento integrado são usados nos casos de teste.

 Compartilhamento:  -> compartilhamento de **controle de origem** de arquivo -> .

## <a name="expected-behavior"></a>Comportamento esperado

- O arquivo compartilhado aparece no local compartilhado.

- A exibição do histórico do repositório de versão do controle do código-fonte mostra que os arquivos são compartilhados.

- Editar um arquivo compartilhado edita os dois locais do arquivo.

## <a name="test-cases"></a>Casos de teste
 Veja a seguir os casos de teste específicos para a área de teste de compartilhamento.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Compartilhar um arquivo de um projeto carregado no controle do código-fonte para outro projeto carregado|1. Crie um novo projeto.<br />2. Adicione um segundo projeto à solução.<br />3. Crie um arquivo no segundo projeto com um nome que não esteja no primeiro projeto.<br />4. Adicione a solução ao controle do código-fonte.<br />5. Selecione o primeiro projeto.<br />6. abrir caixa de diálogo de **compartilhamento** (compartilhamento de controle do  ->  **código-fonte** do arquivo  ->  ).<br />7. Compartilhe o arquivo do segundo projeto para o primeiro projeto.<br />8. aceitar **check-out** se solicitado.|Comportamento esperado comum.|
|Compartilhar um arquivo de um projeto para outro|1. Crie um novo projeto.<br />2. Adicione-o ao controle do código-fonte.<br />3. Feche a solução.<br />4. criar um segundo projeto (nova solução).<br />5. Adicione a solução ao controle do código-fonte.<br />6. Selecione o projeto.<br />7. Abra a caixa de diálogo **compartilhar** (compartilhamento de controle do  ->  **código-fonte** do arquivo  ->  ).<br />8. Compartilhe um arquivo do projeto adicionado anteriormente para o projeto aberto.<br />9. aceitar **check-out** se solicitado.|Comportamento esperado comum.|
|Compartilhar um arquivo que não faz parte do projeto do controle do código-fonte para o projeto atualmente carregado|1. Crie um novo projeto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. adicionar um arquivo ao controle do código-fonte que não faz parte do projeto ou da solução.<br />4. Selecione o projeto e abra a caixa de diálogo **compartilhar** (compartilhamento de controle do  ->  **código-fonte** do arquivo  ->  ).<br />5. Selecione um arquivo na caixa de diálogo de **compartilhamento** que não exista no projeto ou solução atual e compartilhe-o.<br />6. aceitar **check-out** se solicitado.|O armazenamento de controle do código-fonte realizou um get, portanto, o arquivo agora está no local local do projeto.|
|Compartilhar arquivos dentro do mesmo projeto para uma pasta diferente|1. Selecione **fazer check-out automaticamente** em **ferramentas**  ->  **Opções**  ->  **controle do código-fonte**.<br />2. Crie um novo projeto e adicione-o ao controle do código-fonte.<br />3. Adicione uma pasta ao projeto.<br />4. Adicione um arquivo à pasta e faça check-in da pasta.<br />5. Selecione a pasta.<br />6. abrir caixa de diálogo de **compartilhamento** (compartilhamento de controle do  ->  **código-fonte** do arquivo  ->  ).<br />7. Compartilhe o arquivo na pasta selecionada.|Comportamento esperado comum.<br /><br /> É necessário fazer check-in de uma pasta com um arquivo antes que ela possa ser usada para compartilhamento.|
|Compartilhar uma pasta no projeto carregado — recursivo|1. Crie um novo projeto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Selecione o projeto.<br />4. Abra a caixa de diálogo **compartilhar** (compartilhamento de controle do  ->  **código-fonte** do arquivo  ->  ).<br />5. Selecione uma pasta.<br />6. compartilhe a pasta recursivamente no projeto.|Comportamento esperado comum.|
|Compartilhar vários arquivos de um projeto para outro|1. Crie um novo projeto com vários arquivos.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Feche a solução.<br />4. Crie um novo projeto em uma nova solução.<br />5. Adicione a solução ao controle do código-fonte.<br />6. Selecione o projeto.<br />7. Abra a caixa de diálogo **compartilhar** (compartilhamento de controle do  ->  **código-fonte** do arquivo  ->  ).<br />8. Compartilhe vários arquivos do projeto criado anteriormente para o projeto aberto no momento.|Comportamento esperado comum.|

## <a name="see-also"></a>Confira também
- [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
