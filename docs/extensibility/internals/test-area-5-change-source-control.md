---
title: 'Área de teste 5: Alterar controle do código-fonte | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], changing
- source control plug-ins, changing source control
ms.assetid: fdf09e00-108c-4d51-bbd5-72452d52a490
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ed7093d50290c4c0612faf6c7691f90e62a08267
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49847351"
---
# <a name="test-area-5-change-source-control"></a>Área de teste 5: alterar o controle do código-fonte
Essa área de plug-in de teste de controle de origem aborda alterando o controle do código-fonte por meio de **alterar controle do código-fonte** comando.  

 **Alterar controle do código-fonte** comando fornece quatro funções básicas para o usuário:  

- **Associe:**  

   Permite que um usuário estabelecer ou restabelecer um link de controle do código-fonte entre uma solução/projeto e o armazenamento de versão.  

- **Desassocie:**  

   Remove uma projeto/solução de controle de origem em uma base por conexão.  

- **Conectar/Desconecte:**  

  Alterna o estado conectado ou offline da solução controlada, que é abordado na área de 3. Para obter mais informações, consulte [área de teste 3: Fazer Check-Out / desfazer check-out](../../extensibility/internals/test-area-3-check-out-undo-checkout.md).  

## <a name="command-menu-access"></a>Acesso ao Menu de comando  
 O seguinte [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] caminho de menu de ambiente de desenvolvimento integrado é usado nos casos de teste.  

 Alterar controle do código-fonte:**arquivo**, **controle de fonte**, **alterar controle do código-fonte**.  

## <a name="test-cases"></a>Casos de teste  
 Estes são os casos de teste específicos para o **alterar controle do código-fonte** comando área de teste.  

### <a name="case-5a-bind"></a>Caso 5a: associar  
 Associação permite que o usuário adicione informações de controle do código de origem para os projetos selecionados e as soluções. Normalmente, o usuário é solicitado para identificar um projeto no controle de origem para o qual eles devem ser adicionados. O usuário não pode criar um novo projeto no controle de origem como parte dessa operação (contraste com adicionar ao controle do código-fonte).  


| Ação | Etapas de teste | Resultados esperados para verificar |
| - | - | - |
| Associar a local vazio | 1.  Criar um projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Abra **alterar controle do código-fonte** caixa de diálogo (**arquivo**, **controle de origem**, **alterar controle do código-fonte**).<br />4.  Clique em **desassociar**.<br />5.  Aceite a caixa de diálogo de aviso se ele for exibido.<br />6.  Selecione todos os itens.<br />7.  Clique em **associar**.<br />8.  Navegue até um local vazio em um repositório de controle do código-fonte.<br />9. Clique em **Okey** para fechar o **alterar controle do código-fonte** caixa de diálogo.<br />10. Clique em **continuar com estas associações** na caixa de diálogo de confirmação.<br />11. Clique em **Okey** na caixa de diálogo de aviso se ele for exibido.<br />12. Fazer check-in de tudo. Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />13. Abra a solução de controle de origem para um novo local. | `Result from Step 12:`<br /><br /> Solução e projeto são associadas a e gravados no novo destino no armazenamento de versão.<br /><br /> Arquivos de solução e projeto são check-in.<br /><br /> Hierarquia do projeto de repositório de versão corresponde à hierarquia de pastas do projeto no disco.<br /><br /> `Result from Step 13:`<br /><br /> Todos os itens de projeto são baixados. |
| Associar a local que está em sincronia com o cliente | 1.  Criar um projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Criar uma duplicata da solução e projeto no repositório de versão (compartilhar e ramificar se usando [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)]).<br />4.  Abra **alterar controle do código-fonte** caixa de diálogo (**arquivo**, **controle de origem**, **alterar controle do código-fonte**).<br />5.  Desvincule todos.<br />6.  Clique em **Okey** para fechar **alterar controle do código-fonte** caixa de diálogo.<br />7.  Reabrir **alterar controle do código-fonte** caixa de diálogo.<br />8.  Selecione tudo.<br />9. Clique em **associar**.<br />10. Navegue até o local ramificado da solução e projeto (da etapa 3)<br />11. Clique em **Okey** para fechar o **alterar controle do código-fonte** caixa de diálogo.<br />12. Obtenha mais recente recursivamente para todos os itens. | O conteúdo do arquivo depois que o get é o mesmo que antes de get. |
| Associar a local que está fora de sincronia com o cliente | 1.  Criar um projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Criar uma duplicata da solução e projeto no repositório de versão (compartilhar e ramificar se usando [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)]).<br />4.  Modificar arquivos no projeto no repositório de versão ramificado.<br />5.  Abra **alterar controle do código-fonte** caixa de diálogo (**arquivo**, **controle de origem**, **alterar controle do código-fonte**).<br />6.  Desvincule todos.<br />7.  Clique em **Okey** para fechar **alterar controle do código-fonte** caixa de diálogo.<br />8.  Reabrir **alterar controle do código-fonte** caixa de diálogo.<br />9. Selecione tudo.<br />10. Clique em **associar**.<br />11. Navegue até ramificado local para a solução e projeto.<br />12. Clique em **Okey** para fechar o **alterar controle do código-fonte** caixa de diálogo.<br />13. Aceite a caixa de diálogo de aviso se ele for exibido.<br />14. Obtenha mais recente recursiva para todos os itens. | Arquivos que foram modificados na etapa 4 também são modificados localmente. |
| Associar a solução que fosse nunca sob controle do código-fonte | 1.  Crie uma pasta vazia no controle de origem.<br />2.  Crie um projeto de cliente.<br />3.  Abra **alterar controle do código-fonte** caixa de diálogo (**arquivo**, **controle de origem**, **alterar controle do código-fonte**).<br />4.  Associe a solução local vazia no controle de origem.<br />5.  Clique em **Okey** para fechar o **alterar controle do código-fonte** caixa de diálogo.<br />6.  Clique em **continuar com estas associações** na caixa de diálogo de confirmação.<br />7.  Clique em **Okey** na caixa de diálogo de aviso se ele for exibido. | Solução é adicionada ao controle de origem.<br /><br /> Solução e projeto de check-out. |
| Cancelar Bind | 1.  Criar um projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Abra a caixa de diálogo Alterar controle do código-fonte.<br />4.  Desvincule todos.<br />5.  Clique em **Okey** botão para fechar a caixa de diálogo. Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />6.  Reabra o **alterar controle do código-fonte** caixa de diálogo.<br />7.  Associe a localização não relacionada.<br />8.  Clique em **Cancelar**. | `Result from Step 5:`<br /><br /> A solução não está mais sob controle do código-fonte<br /><br /> `Result from Step 8:`<br /><br /> A solução é ainda não em controle de origem. |

### <a name="case-5b-unbind"></a>Caso 5b: desassociar  
 Desassocie remove informações de controle de código fonte de projetos e suas soluções. A solução e projetos afetados são com base em uma combinação de seleção do usuário e como os itens foram adicionados ao controle de origem.  

|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Desassociar a solução que contém um sistema de arquivos ou o projeto da Web do IIS local e o projeto de um cliente|1.  Crie um sistema de arquivos ou o projeto da Web do IIS local.<br />2.  Adicione a solução ao controle de origem.<br />3.  Adicione um novo projeto de cliente para a solução.<br />4.  Aceite Check-Out da solução de se solicitado.<br />5.  Abra o **alterar controle do código-fonte** caixa de diálogo.<br />6.  Clique em **desassociar**.<br />7.  Clique em **OK** para fechar a caixa de diálogo.<br />8.  Tentativa de fazer check-out da solução, projeto, itens de solução, itens de projeto.|Soluções e projetos não estão sob controle de origem.<br /><br /> Comandos de menu de controle do código-fonte não aparecem.|  
|Desassociar Cancelar|1.  Criar um projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Abra o **alterar controle do código-fonte** caixa de diálogo.<br />4.  Clique em **desassociar todos**.<br />5.  Clique em **Cancelar**.|Solução estiver sob controle do código-fonte.|  

### <a name="case-5c-rebind"></a>Caso 5c: Rebind  
 Reassociar é simplesmente uma combinação de desassociar e bind — o processo de uma projeto/solução que foi anteriormente sob controle do código-fonte e foi desassociado de reassociação.  

|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Associar novamente a solução e projetos sem fechar o **alterar controle do código-fonte** caixa de diálogo|1.  Criar um projeto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Abra o **alterar controle do código-fonte** caixa de diálogo.<br />4.  Clique em **desassociar**.<br />5.  Selecione todas as linhas.<br />6.  Clique em **associar**.<br />7.  Clique em **Okey** para fechar o **alterar controle do código-fonte** caixa de diálogo.<br />8.  Se solicitado, aceite check-out.|Solução e projeto estiver sob controle do código-fonte.|  
|Reassociar projeto apenas sem fechamento **alterar controle do código-fonte** caixa de diálogo|1.  Criar um projeto.<br />2.  Adicionar apenas o projeto ao controle do código-fonte usando (arquivo de código-fonte -> controle -> adicionar projetos selecionados ao controle de origem.<br />3.  Abra a caixa de diálogo Alterar controle do código-fonte.<br />4.  Desassocie apenas o projeto.<br />5.  Vincule apenas o projeto.|Solução permanece não controlada.<br /><br /> Projeto permanece controlado.|  
|Associar novamente a solução somente sem fechamento **alterar controle do código-fonte** caixa de diálogo|1.  Criar um projeto.<br />2.  Adicione apenas a solução ao controle do código-fonte usando (**arquivo**, **controle do código-fonte**, **adicionar projetos selecionados ao controle do código-fonte**.<br />3.  Abra o **alterar controle do código-fonte** caixa de diálogo.<br />4.  Desassociar apenas a solução (não feche **alterar controle do código-fonte** caixa de diálogo.)<br />5.  Vincule apenas a solução.<br />6.  Clique em **OK** para fechar a caixa de diálogo.<br />7.  Fazer check-out de solução e itens de solução (se houver)|Solução permanece controlada.<br /><br /> Projeto permanece não controlado.|  
|Associar novamente o projeto/solução apenas no mesmo diretório|1.  Criar um projeto.<br />2.  Adicionar apenas o projeto ao controle do código-fonte usando (**arquivo**, **controle do código-fonte**, **adicionar projetos selecionados ao controle do código-fonte**.<br />3.  Feche a solução.<br />4.  Crie uma nova solução com pelo menos dois projetos.<br />5.  Adicione a solução ao controle de origem.<br />6.  Adicione o projeto criado na etapa 1 do controle de origem.<br />7.  Se solicitado, aceite o check-out da solução.<br />8.  Fazer check-in da solução inteira.<br />9. Abra o **alterar controle do código-fonte** caixa de diálogo.<br />10. Selecione o projeto adicionado (da etapa 6) e clique em **Unbind**.<br />11. Clique em **OK** para fechar a caixa de diálogo.<br />12. Se solicitado, aceite o check-out.<br />13. Reabrir **alterar controle do código-fonte** caixa de diálogo.<br />14. Selecione o projeto adicionado (da etapa 6) e clique em **associar**.<br />15. Selecione o local original.|Soluções e projetos permanecem controlados.|  

## <a name="see-also"></a>Consulte também  
 [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)