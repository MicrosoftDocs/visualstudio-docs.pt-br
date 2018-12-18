---
title: 'Área de teste 7: Compartilhamento | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], sharing items
- source control plug-ins, sharing items
ms.assetid: 6ec4780a-bda4-4327-bb3e-c6c9e7eabf35
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: fa74d6ff2291288a1ca0e7f17a2edb1e126f222b
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31142462"
---
# <a name="test-area-7-share"></a>Testar área 7: compartilhamento
Essa área de teste aborda itens sharing entre locais por meio de **compartilhamento** comando.  
  
 Uma operação hhare é a eliminação de duplicação aparente de arquivos e itens de pasta entre dois ou mais locais dentro de uma hierarquia de arquivo de controle de origem. Eliminação de duplicação não realmente ocorre no servidor, mas o usuário verá o mesmo arquivo em dois ou mais locais especificados. Sempre que forem feitas alterações para qualquer um dos itens compartilhados, essas alterações aparecem em todos os outros locais compartilhados.  
  
 Para pastas de compartilhamento funciona se você selecionar uma pasta pelo menos um arquivo sob controle de origem nele. O comando de compartilhamento é desabilitado nas seguintes condições:  
  
-   Se a pasta selecionada é uma pasta vazia.  
  
-   Se houver uma pasta real, mas ele não contém nenhum arquivo de controle de origem.  
  
-   Se houver uma pasta virtual, se arquivos sob controle de origem são nele ou não.  
  
-   Se houver um projeto da Web de Site remoto.  
  
## <a name="command-menu-access"></a>Acesso de Menu de comando  
 O seguinte [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] caminhos de menu do ambiente de desenvolvimento integrado são usados nos casos de teste.  
  
 Compartilhamento: **arquivo**->**controle de origem**->**compartilhamento**.  
  
## <a name="expected-behavior"></a>Comportamento esperado  
  
-   Arquivo compartilhado é exibido no local compartilhado.  
  
-   Exibindo a fonte controle versão repositório histórico mostra que os arquivos são compartilhados.  
  
-   Editar um arquivo compartilhado edita os locais do arquivo.  
  
## <a name="test-cases"></a>Casos de teste  
 Estes são os casos de teste específicos para a área de teste do compartilhamento.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Compartilhar um arquivo de um projeto carregado sob controle do código-fonte em outro projeto carregado|1.  Crie um novo projeto.<br />2.  Adicione um segundo projeto à solução.<br />3.  Crie um arquivo no segundo projeto com um nome que não está no projeto primeiro.<br />4.  Adicione a solução ao controle de origem.<br />5.  Selecione o projeto primeiro.<br />6.  Abra **compartilhamento** caixa de diálogo (**arquivo** -> **controle de origem** -> **compartilhamento**).<br />7.  Compartilhe o arquivo do projeto de segundo para o projeto primeiro.<br />8.  Aceitar **Check-Out** se solicitado.|Comportamento esperado comuns.|  
|Compartilhar um arquivo de um projeto para outro|1.  Crie um novo projeto.<br />2.  Adicione-o ao controle de origem.<br />3.  Feche a solução.<br />4.  Criar um segundo projeto (nova solução).<br />5.  Adicione a solução ao controle de origem.<br />6.  Selecione o projeto.<br />7.  Abra o **compartilhamento** caixa de diálogo (**arquivo** -> **controle de origem** -> **compartilhamento**).<br />8.  Compartilhe um arquivo do projeto previamente adicionado ao projeto aberto.<br />9. Aceitar **Check-Out** se solicitado.|Comportamento esperado comuns.|  
|Compartilhar um arquivo não faz parte do projeto do controle de origem para o projeto carregado no momento|1.  Crie um novo projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Adicione um arquivo ao controle de origem que não faz parte do projeto ou da solução.<br />4.  Selecione o projeto e abra o **compartilhamento** caixa de diálogo (**arquivo** -> **controle de origem** -> **compartilhamento**).<br />5.  Selecione um arquivo dentro de **compartilhar** caixa de diálogo que não existe no projeto atual ou da solução e compartilhá-lo.<br />6.  Aceitar **Check-Out** se solicitado.|O repositório de controle de origem executou um Get para que o arquivo agora é o local do projeto.|  
|Compartilhar arquivos dentro do mesmo projeto em uma pasta diferente|1.  Selecione **Check-out automaticamente** na **ferramentas** -> **opções** -> **controle de origem**.<br />2.  Criar um novo projeto e adicione-o ao controle de origem.<br />3.  Adicione uma pasta ao projeto.<br />4.  Adicionar um arquivo para a pasta e verifique na pasta.<br />5.  Selecione a pasta.<br />6.  Abra **compartilhamento** caixa de diálogo (**arquivo** -> **controle de origem** -> **compartilhamento**).<br />7.  Arquivo de compartilhamento na pasta selecionada.|Comportamento esperado comuns.<br /><br /> Pasta deve ser verificada com um arquivo antes de ser usada para compartilhamento.|  
|Compartilhar uma pasta para o projeto carregado — recursiva|1.  Crie um novo projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Selecione o projeto.<br />4.  Abra o **compartilhamento** caixa de diálogo (**arquivo** -> **controle de origem** -> **compartilhamento**).<br />5.  Selecione uma pasta.<br />6.  Compartilhe a pasta repetidamente para o projeto.|Comportamento esperado comuns.|  
|Compartilhar vários arquivos de um projeto para outro|1.  Crie um novo projeto com vários arquivos.<br />2.  Adicione a solução ao controle de origem.<br />3.  Feche a solução.<br />4.  Crie um novo projeto em uma solução nova.<br />5.  Adicione a solução ao controle de origem.<br />6.  Selecione o projeto.<br />7.  Abra o **compartilhamento** caixa de diálogo (**arquivo** -> **controle de origem** -> **compartilhamento**).<br />8.  Compartilhe vários arquivos de projeto criado anteriormente para o projeto aberto no momento.|Comportamento esperado comuns.|  
  
## <a name="see-also"></a>Consulte também  
 [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)