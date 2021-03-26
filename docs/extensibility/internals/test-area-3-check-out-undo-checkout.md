---
title: 'Área de teste 3: verificar Out-Undo check-out | Microsoft Docs'
description: Esta área de teste de plug-in de controle de origem aborda a edição e a reversão de itens do repositório de versão usando os comandos Check out e Undo check-out.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, checkout
- source control plug-ins, undo checkout
- source control [Visual Studio SDK], checking out
- source control [Visual Studio SDK], undo checkout
ms.assetid: ce00c5a5-d472-4f45-8776-d77a1fbe9d37
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c184aeb1b5a43e54bc00d5694ddee7711a815593
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078624"
---
# <a name="test-area-3-check-outundo-checkout"></a>Área de teste 3: Fazer/desfazer check-out
Esta área de teste de plug-in de controle de origem abrange a edição e a reversão de itens do repositório de versão por meio dos comandos **check-out** e **Undo check-out** .

**Check-out**: marca um item no repositório de versão como checked out, modifica a cópia local para leitura/gravação.

**Desfazer check-out**: marca um item no repositório de versão como check-in, reverte a cópia local para o estado anterior ao check-out (dependendo das opções).

## <a name="command-menu-access"></a>Acesso ao menu de comando

Os seguintes [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] caminhos de menu do ambiente de desenvolvimento integrado são usados nos casos de teste.

##### <a name="check-out"></a>Check-out:

- **Arquivo**, **controle do código-fonte**, **check-out**.

- **Arquivo**, **faça check-out**.

- Menu de atalho, **Confira**.

- Desfazer check-out: **arquivo**, **controle do código-fonte**, **desfazer check-out**.

## <a name="common-expected-behavior"></a>Comportamento comum esperado

- Após a operação de check-out, os arquivos de destino e/ou pastas são marcados como extraídos no repositório de versão.

- O repositório de versão tem como atributo o check-out para o usuário correto.

- A hora e a data do check-out estão corretas (de acordo com as configurações do usuário).

## <a name="test-cases"></a>Casos de teste

Veja a seguir os casos de teste específicos para a área de teste de check-out/desfazer.

### <a name="case-3a-check-out"></a>Caso 3A: check-out

Esta seção se concentra na operação do comando check-out.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Fazer check-out exclusivo (COE) de um projeto de cliente|1. criar um projeto de cliente.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Verifique todo o projeto exclusivamente (**arquivo**, **Confira**).|O check-out ocorre.|
|Fazer check-out exclusivo (COE) de um sistema de arquivos ou projeto Web local do IIS|1. defina a conexão do servidor Web para compartilhamento de arquivos em **ferramentas**, **Opções**, **projetos**, **configurações da Web**.<br />2. Crie um projeto Web.<br />3. Adicione a solução ao controle do código-fonte.<br />4. Confira o projeto inteiro exclusivamente (**arquivo**, **controle do código-fonte**, **check-out**).|O check-out ocorre.|
|Fazer check-out de itens de solução em uma solução (novo método para lidar com outros arquivos)|1. Crie uma solução em branco.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Confira a solução.<br />4. adicionar vários itens de solução.<br />5. faça check-in de todos os itens recém-adicionados.<br />6. Selecione vários itens de solução.<br />7. Confira os itens selecionados (menu de atalho, **check-out**).|O check-out dos arquivos selecionados foi feito.|
|Fazer check-out da versão local (se o plug-in em teste der suporte a esse recurso)|1. usuário 1: criar um projeto de cliente.<br />2. usuário 1: Adicione a solução ao controle do código-fonte.<br />3. usuário 2: Abra a solução do controle do código-fonte para outro local.<br />4. usuário 2: fazer check-out de um arquivo.<br />5. usuário 2: modificar o arquivo.<br />6. usuário 2: fazer check-in do arquivo.<br />7. usuário 1: fazer check-out da versão local do arquivo (marque a opção de **check-out da versão local** avançada na caixa de diálogo **check-out** ).|Foi feito check-out da versão local do arquivo.<br /><br /> As modificações do usuário 2 não são aplicadas ao arquivo 1 do usuário.|

### <a name="case-3b-disconnected-check-out"></a>Caso 3B: check-out desconectado

Operar no modo desconectado permite aos usuários algum nível de suporte contínuo ao controle do código-fonte quando não anexado diretamente a um repositório de versão. Isso é feito armazenando localmente em cache todas as informações relevantes sobre a solução e os projetos inscritos.

As operações de check-out exclusivas só podem ocorrer enquanto estiverem conectadas ao repositório de controle do código-fonte. As operações de check-out compartilhado podem ocorrer a qualquer momento, sejam conectadas ou desconectadas. Portanto, quando desconectado do repositório de versão, somente o comando **check out compartilhado** (cos) é habilitado. Enquanto estiver desconectado, **desfazer o check-out** será desabilitado porque a versão antiga não pode ser recuperada para substituir as alterações feitas pelo usuário.

Quando o usuário se reconecta ao repositório de versão, os Estados de check-out de todas as soluções e projetos inscritos são sincronizados. Isso faz as atualizações necessárias para o armazenamento para os check-outs que o usuário realizou. Depois que a sincronização tiver acontecido, o usuário poderá continuar trabalhando normalmente (conectado).

#### <a name="expected-behavior"></a>Comportamento esperado

- Não é possível usar o comando **check-out exclusivo** enquanto estiver desconectado do repositório de versão.

- Não é possível usar o comando **Undo Checkout** enquanto estiver desconectado do repositório de versão.

- O comando de **check-out compartilhado** funciona.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Enquanto estiver desconectado, confira um arquivo e conecte-se para sincronização|1. desconectar um projeto controlado usando alterar caixa de diálogo controle do código-fonte (**arquivo**, **controle do código-fonte**, **alterar controle do código-** fonte).<br />2. Verifique um arquivo.<br />3. clique em fazer check-out (desconectado) na caixa de diálogo de aviso.<br />4. Edite o arquivo.<br />5. Conecte-se usando a caixa de diálogo Alterar controle do código-fonte.<br />6. obter a versão mais recente do arquivo editado.|Comportamento comum esperado|

### <a name="case-3c-query-editquery-save-qeqs"></a>Caso 3C: Query Edit/consulta Save (QEQS)
 Os itens sob controle do código-fonte são rastreados para edições, alterações e gravações para ajudar os usuários a gerenciar seus arquivos com facilidade. Quando um item controlado que está "checked in" é editado, o QEQS intercepta a tentativa de edição e pergunta ao usuário se deseja fazer check-out do arquivo para editá-lo. Dependendo das **ferramentas**, as configurações de **Opções** , o usuário é forçado a fazer check-out do arquivo para editar ou pode ter permissão para editar uma cópia na memória e fazer check-out posteriormente. Se as **ferramentas** do usuário, a configuração **Opções** não estiver definida para exibir a caixa de diálogo check-out e para apenas fazer check-out, assim que o usuário fizer sua edição, o arquivo fará o check-out automaticamente, sempre que possível.

#### <a name="expected-behavior"></a>Comportamento esperado

- Após a operação de check-out, os arquivos de destino e/ou pastas são marcados como extraídos no repositório de versão.

- O armazenamento de versão Attributes o check-out para o usuário correto.

- A hora e a data de check-out estão corretas (de acordo com as configurações do usuário).

- A cópia local do arquivo ou da pasta de destino é gravável.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Editar arquivo de texto com check-in|1. Crie um novo projeto que contenha um arquivo de texto.<br />2. Adicione a solução ao controle do código-fonte.<br />3. defina **ferramentas**, **Opções**, **controle do código-fonte**, **permitir que os arquivos sejam editados enquanto estiver somente leitura no disco** para desmarcar.<br />4. definir **ferramentas**, **Opções**, **controle do código-fonte**, **solicitar check-out** na caixa de combinação **quando os arquivos marcados são editados** .<br />5. definir **ferramentas**, **Opções**, **controle do código-fonte**, **solicitar check-out** na caixa de combinação **quando os arquivos marcados são salvos** .<br />6. abrir arquivo de texto no editor, tentar digitar um novo texto no arquivo. Se essa etapa for concluída com sucesso, continue na próxima etapa.<br />7. clique em **Cancelar** na caixa **de diálogo fazer check-out para editar** . Se essa etapa for concluída com sucesso, continue na próxima etapa.<br />8. definir **ferramentas**, **Opções**, **controle do código-fonte**, **permitir que os arquivos sejam editados enquanto são somente leitura no disco** para verificação.<br />9. Abra o arquivo de projeto no editor, tente digitar um novo texto no arquivo. Se essa etapa for concluída com sucesso, continue na próxima etapa.<br />10. clique em **Editar** na caixa **de diálogo check-out para editar** . Se essa etapa for concluída com sucesso, continue na próxima etapa.<br />11. Edite o arquivo de texto e tente salvá-lo.|`Result of step 6:`<br /><br /> A caixa de diálogo check-out para editar é exibida.<br /><br /> `Result of step 7:`<br /><br /> O arquivo está inalterado.<br /><br /> `Result of step 9:`<br /><br /> A caixa de diálogo check-out para editar é exibida.<br /><br /> `Result of step 10:`<br /><br /> Você pode editar o arquivo de projeto na memória.<br /><br /> `Result of step 11:`<br /><br /> Ao salvar, a caixa de diálogo check-out na gravação é exibida.|
|Editar um arquivo de solução com check-in|Repita as etapas conforme descrito em teste anterior, mas em vez de modificar um arquivo de texto, modifique a solução alterando as propriedades da solução.|Igual ao teste anterior|
|Editar um arquivo de projeto que está com check-in|Repita as etapas conforme descrito em teste anterior, mas em vez de modificar um arquivo de texto, modifique o projeto alterando as propriedades do projeto.|Mesmo que o teste anterior.|

### <a name="case-3d-silent-check-out"></a>Caso 3D: check-out silencioso
 Essa subárea aborda os cenários de check-out em que a caixa de diálogo **check-out** não aparece por **ferramentas**, **Opções**, **configurações de controle do código-fonte** do usuário.

#### <a name="expected-behavior"></a>Comportamento esperado

- Após a operação de check-out, os arquivos de destino e/ou pastas são marcados como extraídos no repositório de versão.

- O armazenamento de versão Attributes o check-out para o usuário correto.

- A data e a hora da verificação estão corretas (de acordo com as configurações do usuário).

- A cópia local do arquivo ou da pasta de destino é gravável.

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Check-out silencioso de um arquivo|1. defina **ferramentas**, **Opções**, **controle do código-fonte** para fazer **checkout de arquivos automaticamente em Editar**.<br />2. Crie um novo projeto com um arquivo.<br />3. Adicione a solução ao controle do código-fonte.<br />4. Confira o arquivo.|O check-out do arquivo foi realizado silenciosamente (sem interface do usuário).|
|Check-out silencioso de um projeto|1. defina **ferramentas**, **Opções**, **controle do código-fonte** para fazer **checkout de arquivos automaticamente em Editar**.<br />2. Crie um novo projeto.<br />3. Adicione a solução ao controle do código-fonte.<br />4. Confira o projeto.|O check-out do arquivo foi realizado silenciosamente (sem interface do usuário).|

### <a name="case-3e-undo-check-out"></a>O caso 3E: desfazer check-out
 **Undo check out** é usado para cancelar o status de check-out de um arquivo e evitar fazer check-in de alterações feitas no arquivo.

#### <a name="expected-behavior"></a>Comportamento esperado

- O padrão é baseado na configuração de **versão local do check-out** do usuário. Se o usuário tiver optado por fazer check-out da versão local, o padrão para desfazer check-out será sempre reverter para a versão com check-out.

- Após a aceitação do desfazer, os ícones em **Gerenciador de soluções** são atualizados para arquivos afetados e o item é removido da janela **check-ins pendentes** .

|Ação|Etapas de teste|Resultados esperados para verificar|
|------------|----------------|--------------------------------|
|Desfazer o check-out de um único arquivo cujo check-out foi feito exclusivamente|1. criar um projeto de cliente.<br />2. Adicione a solução ao controle do código-fonte.<br />3. fazer check-out de um arquivo exclusivamente.<br />4. modifique o arquivo.<br />5. desfazer check-out (**arquivo**, **controle do código-fonte**, **desfazer check-out**).|Comportamento esperado comum.|
|Desfazer o check-out de um único arquivo com check-out compartilhado|1. criar um projeto de cliente.<br />2. Adicione a solução ao controle do código-fonte.<br />3. Confira um arquivo compartilhado.<br />4. modifique o arquivo.<br />5. desfazer check-out (**arquivo**, **controle do código-fonte**, **desfazer check-out**).|Comportamento esperado comum.|
|Desfazer o check-out de um projeto depois de Adicionar arquivo (s) ao projeto|1. Crie um novo projeto e adicione-o ao controle do código-fonte.<br />2. Confira o projeto.<br />3. Adicione um arquivo ao projeto.<br />4. desfazer o check-out do projeto.|O arquivo adicionado é removido do projeto no Gerenciador de Soluções.<br /><br /> O projeto não está mais com check-out.|
|Desfazer o check-out de um projeto após a exclusão de arquivo (s) do projeto|1. Crie um novo projeto e adicione-o ao controle do código-fonte.<br />2. Confira o projeto.<br />3. exclua um arquivo do projeto.<br />4. desfazer o check-out do projeto.|O arquivo excluído aparece no projeto no Gerenciador de Soluções.<br /><br /> O projeto não está mais com check-out.|

## <a name="see-also"></a>Confira também
- [Guia de teste para plug-ins de controle do código-fonte](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)
