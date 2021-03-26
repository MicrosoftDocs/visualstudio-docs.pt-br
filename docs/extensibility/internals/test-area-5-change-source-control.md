---
title: 'Área de teste 5: alterar controle do código-fonte | Microsoft Docs'
description: Esta área de teste de plug-in de controle de origem aborda a alteração do controle do código-fonte usando o comando alterar controle do código-fonte.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], changing
- source control plug-ins, changing source control
ms.assetid: fdf09e00-108c-4d51-bbd5-72452d52a490
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 44647781b8f7605a59fba5d9249b6a7165c0e27e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073398"
---
# <a name="test-area-5-change-source-control"></a>Área de teste 5: Alterar controle do código-fonte
Esta área de teste de plug-in de controle de origem aborda a alteração do controle do código-fonte por meio do comando **alterar controle do código-fonte** .

 O comando **alterar controle do código-fonte** fornece quatro funções básicas para o usuário:

- **Associa**

   Permite que um usuário estabeleça ou restabeleça um link de controle do código-fonte entre uma solução/um projeto e o repositório de versão.

- **Desassociar**

   Remove um projeto/solução do controle do código-fonte em uma base por conexão.

- **Conectar/desconectar:**

  Alterna o estado conectado ou offline da solução controlada, que é abordada na área 3. Para obter mais informações, consulte [área de teste 3: fazer check-out/desfazer check-out](../../extensibility/internals/test-area-3-check-out-undo-checkout.md).

## <a name="command-menu-access"></a>Acesso ao menu de comando
 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] caminho de menu do ambiente de desenvolvimento integrado a seguir é usado nos casos de teste.

 Alterar controle de origem:**arquivo**, **controle do código-fonte**, **alterar controle do código-** fonte.

## <a name="test-cases"></a>Casos de teste
 Veja a seguir os casos de teste específicos para a área de teste alterar comando do **controle do código-fonte** .

### <a name="case-5a-bind"></a>Caso 5a: associar
 A ligação permite que o usuário adicione informações de controle do código-fonte aos projetos e soluções selecionados. Normalmente, o usuário é solicitado a identificar um projeto no controle do código-fonte ao qual eles devem ser adicionados. O usuário não pode criar um novo projeto no controle do código-fonte como parte dessa operação (compare com adicionar ao controle do código-fonte).

| Ação | Etapas de teste | Resultados esperados para verificar |
| - | - | - |
| Associar a um local vazio | 1. Crie um projeto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Abra a caixa de diálogo **alterar controle do código-fonte** (**arquivo**, **controle do código-fonte**, **alterar controle do código-fonte**).<br />4. clique em **desassociar**.<br />5. caixa de diálogo aceitar aviso se aparecer.<br />6. selecionar todos os itens.<br />7. clique em **associar**.<br />8. Navegue até um local vazio em um armazenamento de controle do código-fonte.<br />9. clique em **OK** para fechar a caixa de diálogo **alterar controle do código-fonte** .<br />10. clique em **continuar com estas associações** na caixa de diálogo de confirmação.<br />11. clique em **OK** na caixa de diálogo de aviso se aparecer.<br />12. faça o check-in de tudo. Se essa etapa for concluída com sucesso, continue na próxima etapa.<br />13. Abra a solução do controle do código-fonte para um novo local. | `Result from Step 12:`<br /><br /> A solução e o projeto são associados e gravados no novo destino no repositório de versão.<br /><br /> Os arquivos da solução e do projeto são verificados.<br /><br /> A hierarquia de projeto de repositório de versão corresponde à hierarquia de pastas do projeto em disco.<br /><br /> `Result from Step 13:`<br /><br /> Todos os itens de projeto são baixados. |
| Associar ao local que está em sincronia com o cliente | 1. Crie um projeto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Crie uma duplicata da solução e do projeto no repositório de versão (compartilhamento e ramificação, se estiver usando [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] ).<br />4. Abra a caixa de diálogo **alterar controle do código-fonte** (**arquivo**, **controle do código-fonte**, **alterar controle do código-fonte**).<br />5. desassociar tudo.<br />6. clique em **OK** para fechar a caixa de diálogo **alterar controle do código-fonte** .<br />7. reabra a caixa de diálogo **alterar controle do código-fonte** .<br />8. selecionar tudo.<br />9. clique em **associar**.<br />10. Navegue até o local de ramificação da solução e do projeto (da etapa 3)<br />11. clique em **OK** para fechar a caixa de diálogo **alterar controle do código-fonte** .<br />12. obter o mais recente recursivamente para todos os itens. | O conteúdo do arquivo após Get é o mesmo que antes do get. |
| Associar ao local que está fora de sincronia com o cliente | 1. Crie um projeto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Crie uma duplicata da solução e do projeto no repositório de versão (compartilhamento e ramificação, se estiver usando [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] ).<br />4. modificar arquivos no projeto ramificado no repositório de versão.<br />5. Abra a caixa de diálogo **alterar controle do código-** fonte (**arquivo**, **controle do código-fonte**, **alterar controle do código-fonte**).<br />6. desassociar tudo.<br />7. clique em **OK** para fechar a caixa de diálogo **alterar controle do código-fonte** .<br />8. abrir novamente a caixa de diálogo **alterar controle do código-fonte** .<br />9. selecionar tudo.<br />10. clique em **associar**.<br />11. Navegue até o local de ramificação para solução e projeto.<br />12. clique em **OK** para fechar a caixa de diálogo **alterar controle do código-fonte** .<br />13. caixa de diálogo de aviso de aceitação se aparecer.<br />14. obter os mais recentes recursivos para todos os itens. | Os arquivos que foram modificados na etapa 4 também são modificados localmente. |
| Associar solução que nunca foi sob controle do código-fonte | 1. Crie uma pasta vazia no controle do código-fonte.<br />2. criar um projeto de cliente.<br />3. Abra a caixa de diálogo **alterar controle do código-fonte** (**arquivo**, **controle do código-fonte**, **alterar controle do código-fonte**).<br />4. associe a solução ao local vazio no controle do código-fonte.<br />5. clique em **OK** para fechar a caixa de diálogo **alterar controle do código-fonte** .<br />6. clique em **continuar com estas associações** na caixa de diálogo de confirmação.<br />7. clique em **OK** na caixa de diálogo de aviso se ela aparecer. | A solução é adicionada ao controle do código-fonte.<br /><br /> A solução e o projeto são submetidos a check-out. |
| Cancelar Associação | 1. Crie um projeto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Abra a caixa de diálogo Alterar controle do código-fonte.<br />4. desassociar tudo.<br />5. Clique no botão **OK** para fechar a caixa de diálogo. Se essa etapa for concluída com sucesso, continue na próxima etapa.<br />6. reabra a caixa de diálogo **alterar controle do código-fonte** .<br />7. associar a um local não relacionado.<br />8. clique em **Cancelar**. | `Result from Step 5:`<br /><br /> A solução não está mais sob controle do código-fonte<br /><br /> `Result from Step 8:`<br /><br /> A solução ainda não está no controle do código-fonte. |

### <a name="case-5b-unbind"></a>Caso 5b: desassociar
 Desassociar remove informações de controle do código-fonte de projetos e sua solução. Os projetos e a solução afetados são baseados em uma combinação de seleção de usuário e como os itens foram adicionados ao controle do código-fonte.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Desassociar solução que contém um sistema de arquivos ou projeto Web local do IIS e um projeto de cliente|1. criar um sistema de arquivos ou um projeto Web local do IIS.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Adicione um novo projeto de cliente à solução.<br />4. aceitar check-out da solução se solicitado.<br />5. Abra a caixa de diálogo **alterar controle do código-fonte** .<br />6. clique em **desassociar**.<br />7. clique em **OK** para fechar a caixa de diálogo.<br />8. tentativa de fazer check-out da solução, projeto, itens de solução, itens de projeto.|A solução e os projetos não estão sob controle do código-fonte.<br /><br /> Os comandos do menu de controle do código-fonte não são exibidos.|
|Cancelar desassociar|1. Crie um projeto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Abra a caixa de diálogo **alterar controle do código-fonte** .<br />4. clique em **desassociar tudo**.<br />5. clique em **Cancelar**.|A solução está sob controle do código-fonte.|

### <a name="case-5c-rebind"></a>5C de caso: reassociar
 A reassociação é simplesmente uma combinação de desassociar e associar — o processo de reassociar um projeto/solução que estava anteriormente sob controle do código-fonte e estava desassociado.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Reassociar a solução e os projetos sem fechar a caixa de diálogo **alterar controle do código-fonte**|1. Crie um projeto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Abra a caixa de diálogo **alterar controle do código-fonte** .<br />4. clique em **desassociar**.<br />5. Selecione todas as linhas.<br />6. clique em **associar**.<br />7. clique em **OK** para fechar a caixa de diálogo **alterar controle do código-fonte** .<br />8. aceite o check-out se solicitado.|A solução e o projeto estão sob controle do código-fonte.|
|Reassociar o projeto somente sem fechar a caixa de diálogo **alterar controle do código-fonte**|1. Crie um projeto.<br />2. Adicione somente o projeto ao controle do código-fonte usando o controle do código-fonte de >de arquivo->adicionar projetos selecionados ao controle do código-fonte.<br />3. Abra a caixa de diálogo Alterar controle do código-fonte.<br />4. desassociar somente o projeto.<br />5. associar somente o projeto.|A solução permanece sem controle.<br /><br /> O projeto permanece controlado.|
|Reassociar solução somente sem fechar a caixa de diálogo **alterar controle do código-fonte**|1. Crie um projeto.<br />2. Adicione apenas a solução ao controle do código-fonte usando (**arquivo**, **controle do código-fonte**, **adicionar projetos selecionados ao controle do código-fonte**.<br />3. Abra a caixa de diálogo **alterar controle do código-fonte** .<br />4. desassociar somente a solução (não feche a caixa de diálogo **alterar controle do código-fonte** .)<br />5. associar apenas a solução.<br />6. clique em **OK** para fechar a caixa de diálogo.<br />7. Confira os itens da solução e da solução (se houver)|A solução permanece controlada.<br /><br /> O projeto permanece sem controle.|
|Reassociar solução/projeto somente quando estiver no mesmo diretório|1. Crie um projeto.<br />2. Adicione apenas o projeto ao controle do código-fonte usando (**arquivo**, **controle do código-fonte**, **adicione projetos selecionados ao controle do código-fonte**.<br />3. Feche a solução.<br />4. Crie uma nova solução com pelo menos dois projetos.<br />5. Adicione a solução ao controle do código-fonte.<br />6. Adicione o projeto criado na etapa 1 do controle do código-fonte.<br />7. aceite o check-out da solução, se solicitado.<br />8. faça o check-in de toda a solução.<br />9. Abra a caixa de diálogo **alterar controle do código-fonte** .<br />10. Selecione o projeto adicionado (na etapa 6) e clique em **desassociar**.<br />11. clique em **OK** para fechar a caixa de diálogo.<br />12. aceite o check-out, se solicitado.<br />13. abrir novamente a caixa de diálogo **alterar controle do código-fonte** .<br />14. Selecione o projeto adicionado (da etapa 6) e clique em **associar**.<br />15. Selecione o local original.|A solução e os projetos permanecem controlados.|

## <a name="see-also"></a>Confira também
- [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
