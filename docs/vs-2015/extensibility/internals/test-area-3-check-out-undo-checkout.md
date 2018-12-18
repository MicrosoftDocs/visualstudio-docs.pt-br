---
title: 'Área de teste 3: Check-out / desfazer check-out | Microsoft Docs'
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
- source control plug-ins, checkout
- source control plug-ins, undo checkout
- source control [Visual Studio SDK], checking out
- source control [Visual Studio SDK], undo checkout
ms.assetid: ce00c5a5-d472-4f45-8776-d77a1fbe9d37
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: adc6a84dbdc4fb182dd589c54527f02a1aa90d99
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51723001"
---
# <a name="test-area-3-check-outundo-checkout"></a>Área de teste 3: Fazer Check-Out / desfazer check-out
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Essa área de plug-in de teste de controle de origem aborda itens de edição e reversão do repositório de versão por meio de **Check-Out** e **desfazer check-out** comandos.  
  
 **Fazer Check-Out**: as marcas de um item no repositório de versão como check-out, modifica a cópia local como leitura/gravação.  
  
 **Desfazer check-out**: marca um item no repositório de versão, como check-in, reverte a cópia local para o estado antes do check-out (dependendo das opções).  
  
## <a name="command-menu-access"></a>Acesso ao Menu de comando  
 O seguinte [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] caminhos de menu de ambiente de desenvolvimento integrado são usados nos casos de teste.  
  
##### <a name="check-out"></a>Fazer Check-out:  
  
-   **Arquivo**, **controle de origem**, **Fazer Check-Out**.  
  
-   **Arquivo**, **Fazer Check-Out**.  
  
-   Menu de atalho **Check-Out**.  
  
-   Desfazer check-out: **arquivo**, **controle de fonte**, **desfazer check-out**.  
  
## <a name="common-expected-behavior"></a>Comportamento esperado comuns  
  
-   Após o check-out de operação, o arquivo de destino (s) e/ou pastas são marcadas como check-out no repositório de versão.  
  
-   O check-out de atributos no repositório de versão para o usuário correto.  
  
-   A data e hora do check-out estão corretos (de acordo com as configurações do usuário).  
  
## <a name="test-cases"></a>Casos de teste  
 Estes são os casos de teste específicos para a área de teste de check-out/desfazer check-out.  
  
### <a name="case-3a-check-out"></a>Caso 3a: Fazer Check-Out  
 Esta seção concentra-se a operação de comando de check-out.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Check-Out exclusivo (COE) um projeto de cliente|1.  Crie um projeto de cliente.<br />2.  Adicione a solução ao controle de origem.<br />3.  Check-out de todo o projeto exclusivamente (**arquivo**, **Check-Out**).|Ocorre o check-out.|  
|Fazer o Check-Out exclusivo COE (), um sistema de arquivos ou um projeto de Web do IIS local|1.  Definir a Conexão de servidor Web para compartilhamento de arquivos **ferramentas**, **opções**, **projetos**, **configurações Web**.<br />2.  Crie um projeto Web.<br />3.  Adicione a solução ao controle de origem.<br />4.  Check-out de todo o projeto exclusivamente (**arquivo**, **controle do código-fonte**, **Check-Out**).|Ocorre o check-out.|  
|Fazer check-out de itens de solução em uma solução (novo método para lidar com outros arquivos)|1.  Crie uma solução em branco.<br />2.  Adicione a solução ao controle de origem.<br />3.  Verificar a solução.<br />4.  Adicione vários itens de solução.<br />5.  Fazer check-in de todos os itens adicionados recentemente.<br />6.  Selecione vários itens de solução.<br />7.  Fazer check-out dos itens selecionados (Menu de atalho **Check-Out**).|Arquivos selecionados são check-out.|  
|Check-Out Local Version (se o plug-in em teste dá suporte a esse recurso)|1.  O usuário 1: Crie um projeto do cliente.<br />2.  O usuário 1: Adicione a solução ao controle de origem.<br />3.  O usuário 2: Abra a solução de controle de origem para outro local.<br />4.  Usuário 2: Fazer Check-out de um arquivo.<br />5.  O usuário 2: Modificar o arquivo.<br />6.  O usuário 2: Verifique o arquivo.<br />7.  Usuário 1: Fazer Check-out de uma versão local do arquivo (Verifique a **Check-Out da versão Local** opção no avançada **Check-Out** caixa de diálogo).|A versão local do arquivo foi extraído.<br /><br /> Modificações pelo usuário 2 não são aplicadas ao arquivo do usuário 1.|  
  
### <a name="case-3b-disconnected-check-out"></a>Caso 3b: desconectado Check-out  
 Operando no modo desconectado permite que os usuários algum nível de suporte de controle de origem contínuo quando não anexado diretamente a um repositório de versão. Isso é feito localmente em cache todas as informações relevantes sobre a solução inscrita e projetos.  
  
 Check-out de operações exclusivo pode ocorrer apenas enquanto estiver conectado ao armazenamento de controle de origem. Compartilhado check-out de operações pode ocorrer a qualquer momento, se conectado ou desconectado. Portanto, quando desconectado do armazenamento de versão, somente o **Check-Out compartilhado** (COS) comando está habilitado. Enquanto estiver desconectado, **desfazer check-out** está desabilitado porque a versão antiga não pode ser recuperada para substituir as alterações feitas pelo usuário.  
  
 Quando o usuário reconecta-se para a versão de armazenar, os estados de check-out de todas as soluções inscritos e projetos estão sincronizados. Isso faz as atualizações necessárias para o repositório para os check-outs que o usuário executou. Depois que a sincronização tenha ocorrido, o usuário é capaz de continuar funcionando normalmente (conectado).  
  
#### <a name="expected-behavior"></a>Comportamento esperado  
  
-   Não é possível usar **Check-Out exclusivamente** enquanto estiver desconectado do repositório de versão de comando.  
  
-   Não é possível usar **desfazer check-out** enquanto estiver desconectado do repositório de versão de comando.  
  
-   **Compartilhado Check-Out** comando funciona.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Enquanto estiver desconectado, fazer check-out de um arquivo, em seguida, conectar-se para a sincronização|1.  Desconectar um projeto controlado usando a caixa de diálogo Alterar controle do código-fonte (**arquivo**, **controle do código-fonte**, **Alterar origem Contro**l).<br />2.  Confira um arquivo.<br />3.  Clique em Fazer Check-Out (desconectado) na caixa de diálogo de aviso.<br />4.  Edite o arquivo.<br />5.  Conecte-se usando a caixa de diálogo Alterar controle do código-fonte.<br />6.  Obter a versão mais recente do arquivo editado.|Comportamento esperado comuns|  
  
### <a name="case-3c-query-editquery-save-qeqs"></a>Caso 3c: Editar consulta/salvar (QEQS)  
 Itens sob controle de origem são controladas para as edições, alterações, e salva para ajudar os usuários facilmente gerenciar seus arquivos. Quando um item controlado que é "check-in" for editado, QEQS intercepta a edição de tentativa e pede ao usuário se ele deseja fazer check-out do arquivo para editá-lo. Dependendo da **ferramentas**, **opções** configurações, o usuário é forçada a verificar k-out do arquivo para editar ou com podem ter permissão para editar uma cópia na memória e conferir mais tarde. Se o usuário **ferramentas**, **opções** configuração não está definida para exibir o check-out de caixa de diálogo e apenas fizer check-out e, em seguida, quando o usuário faz sua edição, o arquivo automaticamente faz check-out, sempre que possível.  
  
#### <a name="expected-behavior"></a>Comportamento esperado  
  
-   Após o check-out de operação, o arquivo de destino (s) e/ou pastas são marcadas como check-out no repositório de versão.  
  
-   O check-out de atributos no repositório de versão para o usuário correto.  
  
-   A hora e data do check-out estão corretos (de acordo com as configurações do usuário).  
  
-   A cópia local do arquivo de destino ou da pasta é gravável.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Editar o arquivo de texto que o check-in|1.  Crie um novo projeto que contém um arquivo de texto.<br />2.  Adicione a solução ao controle de origem.<br />3.  Definir **ferramentas**, **opções**, **controle do código-fonte**, **permitir que os arquivos a ser editada enquanto somente leitura no disco** para desmarcada.<br />4.  Definir **ferramentas**, **opções**, **controle de origem**, **Prompt para check-out** no **quando o check-in arquivos são editados** caixa de combinação.<br />5.  Definir **ferramentas**, **opções**, **controle de origem**, **Prompt para check-out** no **quando o check-in arquivos são salvos** caixa de combinação.<br />6.  Abra o arquivo de texto no editor, tente digitar um novo texto no arquivo. Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />7.  Clique em **cancele** na **Check-out para edição** caixa de diálogo. Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />8.  Definir **ferramentas**, **opções**, **controle de origem**, **permitir que os arquivos a ser editada enquanto somente leitura no disco** como marcada.<br />9. Abra o arquivo de projeto no editor, tente digitar um novo texto no arquivo. Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />10. Clique em **edite** na **Check-out para edição** caixa de diálogo. Se essa etapa for bem-sucedida, continue para a próxima etapa.<br />11. Edite o arquivo de texto e tentar salvá-lo.|`Result of step 6:`<br /><br /> Fazer check-out de caixa de diálogo de edição é exibida.<br /><br /> `Result of step 7:`<br /><br /> O arquivo permanece inalterado.<br /><br /> `Result of step 9:`<br /><br /> Fazer check-out de caixa de diálogo de edição é exibida.<br /><br /> `Result of step 10:`<br /><br /> Você pode editar o arquivo de projeto na memória.<br /><br /> `Result of step 11:`<br /><br /> Em Salvar, o Check-out na caixa de diálogo de salvamento é exibido.|  
|Editar um arquivo de solução que o check-in|Repita as etapas conforme descrito no anterior de teste, mas em vez de modificar um arquivo de texto, modificar a solução, alterando as propriedades da solução.|Mesmo que o teste anterior|  
|Editar um arquivo de projeto que o check-in|Repita as etapas conforme descrito no anterior de teste, mas em vez de modificar um arquivo de texto, modifique o projeto, alterando as propriedades do projeto.|Mesmo que o teste anterior.|  
  
### <a name="case-3d-silent-check-out"></a>Caso 3d: Silencioso Check-Out  
 Essa verificação de bastidores subárea cenários em que o **Check-Out** caixa de diálogo não aparecer por do usuário **ferramentas**, **opções**, **as configurações de controle do código-fonte** .  
  
#### <a name="expected-behavior"></a>Comportamento esperado  
  
-   Após o check-out de operação, o arquivo de destino (s) e/ou pastas são marcadas como check-out no repositório de versão.  
  
-   O check-out de atributos no repositório de versão para o usuário correto.  
  
-   A hora e data do check-out está correto (de acordo com as configurações do usuário).  
  
-   A cópia local do arquivo de destino ou da pasta é gravável.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Silenciosa check-out de um arquivo|1.  Definir **ferramentas**, **opções**, **controle de origem** para **arquivos de check-out automaticamente em Editar**.<br />2.  Crie um novo projeto com um arquivo.<br />3.  Adicione a solução ao controle de origem.<br />4.  Check-out do arquivo.|Arquivo de check-out silenciosamente (sem interface do usuário).|  
|Silenciosa check-out de um projeto|1.  Definir **ferramentas**, **opções**, **controle de origem** para **arquivos de check-out automaticamente em Editar**.<br />2.  Crie um novo projeto.<br />3.  Adicione a solução ao controle de origem.<br />4.  Check-out do projeto.|Arquivo de check-out silenciosamente (sem interface do usuário).|  
  
### <a name="case-3e-undo-check-out"></a>Caso 3e: Desfazer Check-Out  
 **Desfazer Check-Out** é usado para cancelar um arquivo com check-out de status e evitar a verificar as alterações feitas no arquivo.  
  
#### <a name="expected-behavior"></a>Comportamento esperado  
  
-   O padrão baseia-se se o usuário **Check-out da versão Local** configuração. Se o usuário tiver escolhido fazer check-out da versão local, em seguida, o padrão para desfazer check-out é sempre reverter para a versão com check-out.  
  
-   Mediante a aceitação de desfazer, os ícones no **Gerenciador de soluções** são atualizados para afetado arquivos e o item é removido do **check-ins pendentes** janela.  
  
|Ação|Etapas de teste|Resultados esperados para verificar|  
|------------|----------------|--------------------------------|  
|Desfazer check-out de um único arquivo que o check-out exclusivo|1.  Crie um projeto de cliente.<br />2.  Adicione a solução ao controle de origem.<br />3.  Check-out de um arquivo exclusivamente.<br />4.  Modifique o arquivo.<br />5.  Desfazer check-out (**arquivo**, **controle de fonte**, **desfazer check-out**).|Comportamento esperado comuns.|  
|Desfazer check-out de um único arquivo check-out compartilhado|1.  Crie um projeto de cliente.<br />2.  Adicione a solução ao controle de origem.<br />3.  Fazer check-out de um arquivo compartilhado.<br />4.  Modifique o arquivo.<br />5.  Desfazer check-out (**arquivo**, **controle de fonte**, **desfazer check-out**).|Comportamento esperado comuns.|  
|Desfazer check-out de um projeto depois de adicionar arquivos ao projeto|1.  Criar um novo projeto e adicioná-lo ao controle do código-fonte.<br />2.  Check-out do projeto.<br />3.  Adicione um arquivo ao projeto.<br />4.  Desfazer check-out do projeto.|Arquivo adicionado é removido do projeto no Gerenciador de soluções.<br /><br /> Projeto não foi verificado.|  
|Desfazer check-out de um projeto após a exclusão de arquivo (s) do projeto|1.  Criar um novo projeto e adicioná-lo ao controle do código-fonte.<br />2.  Check-out do projeto.<br />3.  Exclua um arquivo de projeto.<br />4.  Desfazer check-out do projeto.|Arquivo excluído aparece sob o projeto no Gerenciador de soluções.<br /><br /> Projeto não foi verificado.|  
  
## <a name="see-also"></a>Consulte também  
 [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)

