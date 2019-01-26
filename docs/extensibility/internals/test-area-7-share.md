---
title: 'Área de teste 7: Compartilhamento | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], sharing items
- source control plug-ins, sharing items
ms.assetid: 6ec4780a-bda4-4327-bb3e-c6c9e7eabf35
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2efaad276eec2030b062be5f6508ec9603dcbf89
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55040691"
---
# <a name="test-area-7-share"></a>Área de teste 7: Compartilhar
Essa área de teste aborda itens de compartilhamento entre locais por meio de **compartilhamento** comando.  
  
 Uma operação de hhare é a eliminação de duplicação aparente de arquivos e itens de pasta entre dois ou mais locais dentro de uma hierarquia de arquivo de controle do código-fonte. Eliminação de duplicação não realmente ocorre no servidor, mas o usuário verá o mesmo arquivo em dois ou mais locais especificados. Sempre que forem feitas alterações para qualquer um dos itens compartilhados, essas alterações aparecem em todos os outros locais compartilhados.  
  
 Em pastas de compartilhamento funciona se você selecionar uma pasta pelo menos um arquivo sob controle do código-fonte nela. O comando de compartilhamento é desabilitado nas seguintes condições:  
  
-   Se a pasta selecionada é uma pasta vazia.  
  
-   Se há uma pasta real, mas não contém nenhum arquivo de controle de origem.  
  
-   Se houver uma pasta virtual, sejam arquivos sob controle do código-fonte nela ou não.  
  
-   Se houver um projeto Web do Site remoto.  
  
## <a name="command-menu-access"></a>Acesso ao Menu de comando  
 O seguinte [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] caminhos de menu de ambiente de desenvolvimento integrado são usados nos casos de teste.  
  
 Compartilhe: **Arquivo**->**controle de fonte**->**compartilhamento**.  
  
## <a name="expected-behavior"></a>Comportamento esperado  
  
-   Arquivo compartilhado é exibido em um local compartilhado.  
  
-   Exibindo o código-fonte controle versão store histórico mostra que os arquivos são compartilhados.  
  
-   Editar um arquivo compartilhado edita os locais do arquivo.  
  
## <a name="test-cases"></a>Casos de teste  
 Estes são os casos de teste específicos para a área de teste do compartilhamento.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Compartilhar um arquivo de um projeto carregado no controle de origem para outro projeto carregado|1.  Crie um novo projeto.<br />2.  Adicione um segundo projeto à solução.<br />3.  Crie um arquivo no segundo projeto com um nome que não está no primeiro projeto.<br />4.  Adicione a solução ao controle de origem.<br />5.  Selecione o projeto primeiro.<br />6.  Abra **compartilhamento** caixa de diálogo (**arquivo** -> **controle de origem** -> **compartilhamento**).<br />7.  Compartilhe o arquivo de projeto de segundo para o primeiro projeto.<br />8.  Aceite **Check-Out** se solicitado.|Comportamento esperado comuns.|  
|Compartilhar um arquivo de um projeto para outro|1.  Crie um novo projeto.<br />2.  Adicioná-lo ao controle de origem.<br />3.  Feche a solução.<br />4.  Criar um segundo projeto (nova solução).<br />5.  Adicione a solução ao controle de origem.<br />6.  Selecione o projeto.<br />7.  Abra o **compartilhamento** caixa de diálogo (**arquivo** -> **controle de origem** -> **compartilhamento**).<br />8.  Compartilhe um arquivo de projeto adicionado anteriormente para o projeto aberto.<br />9. Aceite **Check-Out** se solicitado.|Comportamento esperado comuns.|  
|Compartilhar um arquivo não faz parte do projeto do controle de origem para o projeto carregado no momento|1.  Crie um novo projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Adicione um arquivo ao controle do código-fonte que não faz parte do projeto ou solução.<br />4.  Selecione o projeto e abra o **compartilhamento** caixa de diálogo (**arquivo** -> **controle de origem** -> **compartilhamento**).<br />5.  Selecione um arquivo dentro de **compartilhar** caixa de diálogo que não existe dentro do projeto atual ou da solução e compartilhá-lo.<br />6.  Aceite **Check-Out** se solicitado.|O repositório de controle do código-fonte executou um Get, portanto, o arquivo agora é o local do projeto.|  
|Compartilhamento de arquivos dentro do mesmo projeto para uma pasta diferente|1.  Selecione **Check-out automaticamente** na **ferramentas** -> **opções** -> **controle do código-fonte**.<br />2.  Criar um novo projeto e adicioná-lo ao controle do código-fonte.<br />3.  Adicione uma pasta ao projeto.<br />4.  Adicione um arquivo para a pasta e fazer check-in na pasta.<br />5.  Selecione a pasta.<br />6.  Abra **compartilhamento** caixa de diálogo (**arquivo** -> **controle de origem** -> **compartilhamento**).<br />7.  Compartilhar o arquivo na pasta selecionada.|Comportamento esperado comuns.<br /><br /> Pasta deve ser marcada com um arquivo nela antes que ele pode ser usado para compartilhamento.|  
|Compartilhar uma pasta para o projeto carregado — recursiva|1.  Crie um novo projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Selecione o projeto.<br />4.  Abra o **compartilhamento** caixa de diálogo (**arquivo** -> **controle de origem** -> **compartilhamento**).<br />5.  Selecione uma pasta.<br />6.  Compartilhe pasta recursivamente no projeto.|Comportamento esperado comuns.|  
|Compartilhar vários arquivos de um projeto para outro|1.  Crie um novo projeto com vários arquivos.<br />2.  Adicione a solução ao controle de origem.<br />3.  Feche a solução.<br />4.  Crie um novo projeto em uma nova solução.<br />5.  Adicione a solução ao controle de origem.<br />6.  Selecione o projeto.<br />7.  Abra o **compartilhamento** caixa de diálogo (**arquivo** -> **controle de origem** -> **compartilhamento**).<br />8.  Compartilhe vários arquivos do projeto criado anteriormente para o projeto aberto no momento.|Comportamento esperado comuns.|  
  
## <a name="see-also"></a>Consulte também  
 [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)