---
title: Atualizando projetos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- upgrading VSPackages
- upgrading applications, strategies
- VSPackages, upgrade support
ms.assetid: e01cb44a-8105-4cf4-8223-dfae65f8597a
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ea5c29819d0035e45f97122fd108ea1f51d60806
ms.sourcegitcommit: 0bf2aff6abe485e3fe940f5344a62a885ad7f44e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2018
ms.locfileid: "37057522"
---
# <a name="upgrading-projects"></a>Atualizando projetos

As alterações no modelo de projeto de uma versão do Visual Studio para o próximo podem exigir que as soluções e projetos sejam atualizados para que eles podem executar a versão mais recente. O [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] fornece interfaces que podem ser usados para implementar o suporte à atualização em seus próprios projetos.

## <a name="upgrade-strategies"></a>Estratégias de atualização

Para dar suporte a uma atualização, sua implementação do sistema de projeto deve definir e implementar uma estratégia de atualização. Para determinar sua estratégia, você pode optar por dar suporte a backup lado a lado (SxS), o backup de cópia ou ambos.

-   Backup de SxS significa que um projeto copia somente os arquivos que precisam de atualização in loco, adicionando um sufixo de nome adequado do arquivo, por exemplo, ". old".

-   Backup de cópia significa que um projeto copia todos os itens de projeto para um local de backup fornecido pelo usuário. Os arquivos relevantes no local original do projeto, em seguida, são atualizados.

## <a name="how-upgrade-works"></a>Como a atualização funciona

Quando uma solução criada em uma versão anterior do Visual Studio é aberta em uma versão mais recente, o IDE verifica o arquivo de solução para determinar se ele precisa ser atualizado. Se a atualização for necessária, o **Assistente de atualização** é iniciado automaticamente para explicar ao usuário o processo de atualização.

Quando as necessidades de uma solução de atualização, ele consulta cada fábrica de projeto para sua estratégia de atualização. A estratégia determina se a fábrica de projeto dá suporte à cópia backup ou SxS. As informações são enviadas para o **Assistente de atualização**, que coleta as informações necessárias para o backup e apresenta as opções aplicáveis ao usuário.

### <a name="multi-project-solutions"></a>Soluções multiprojeto

Se uma solução contiver vários projetos e as estratégias de atualização forem diferentes, como quando um projeto de C++ que só oferece suporte a backup de SxS e um projeto Web que só há suporte para backup de cópia, as fábricas de projeto devem negociar a estratégia de atualização.

A solução consulta cada fábrica de projeto para <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>. Em seguida, ele chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject_CheckOnly%2A> para ver se os arquivos de projeto global precisam atualizar e determinar as estratégias de atualização com suporte. O **Assistente de atualização** , em seguida, é invocado.

Depois que o usuário conclui o assistente, <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> é chamado em cada fábrica de projeto para executar a atualização real. Para facilitar o backup, os métodos de IVsProjectUpgradeViaFactory fornecem o <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> serviço para registrar em log os detalhes do processo de atualização. Esse serviço não pode ser armazenado em cache.

Depois de atualizar todos os arquivos globais relevantes, cada fábrica de projeto pode optar por criar uma instância de um projeto. A implementação do projeto deve dar suporte à <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> método é chamado para atualizar todos os itens de projeto relevantes.

> [!NOTE]
> O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> método não fornece o serviço SVsUpgradeLogger. Esse serviço pode ser obtido chamando <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>.

## <a name="best-practices"></a>Práticas recomendadas

Use o <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> serviço para verificar se você editar um arquivo antes de editá-lo e pode salvá-lo antes de salvá-lo. Isso ajudará o backup e implementações de atualização lidar com arquivos de projeto sob controle do código-fonte, arquivos com permissões insuficientes e assim por diante.

Use o <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> durante todas as fases de backup de serviço e de atualização para fornecer informações sobre o êxito ou falha do processo de atualização.

Para obter mais informações sobre como fazer backup e atualização de projetos, consulte os comentários para IVsProjectUpgrade em vsshell2.idl.

## <a name="upgrading-custom-projects"></a> Atualizando projetos personalizados

Se você alterar as informações mantidas no arquivo de projeto entre diferentes versões do Visual Studio do seu produto, em seguida, você precisa dar suporte à atualização de seu arquivo de projeto do ambiente antigo para a nova versão. Para dar suporte à atualização que permite que você participe de **Assistente de conversão do Visual Studio**, implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> interface. Essa interface contém o único mecanismo disponível para a atualização da cópia. A atualização do projeto ocorre como parte da solução é aberta. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> interface é implementada pela fábrica de projeto ou pelo menos deve ser obtido da fábrica de projeto.

O antigo mecanismo que usa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> interface ainda tem suporte, mas conceitualmente atualiza o sistema de projeto como parte do projeto aberto. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> interface, portanto, é chamado do Visual Studio ambiente mesmo se o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> interface é chamado ou implementada. Essa abordagem permite que você use <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> para implementar a cópia e somente as partes da atualização de projeto e delegue o resto do trabalho a ser feito no local (possivelmente no novo local), o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> interface.

Para uma implementação de exemplo <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>, consulte [exemplos de VSSDK](http://aka.ms/vs2015sdksamples).

Os seguintes cenários ocorrem com atualizações de projeto:

-   Se o arquivo for de um formato mais recente que o projeto pode suportar, em seguida, ele deve retornar um erro informando isso. Isso pressupõe que a versão mais antiga do seu produto inclui código para verificar a versão.

-   Se o <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_SXSBACKUP> sinalizador for especificado no <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> método, a atualização vai ser implementado como uma atualização in loco antes da abertura do projeto.

-   Se o <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_COPYBACKUP> sinalizador for especificado no <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> método, a atualização é implementado como uma atualização de cópia.

-   Se o <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE> sinalizador for especificado no <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> chama, em seguida, o usuário foi solicitado pelo ambiente ao atualizar o arquivo de projeto como uma atualização in-loco, depois que o projeto é aberto. Por exemplo, o ambiente solicita ao usuário atualizar quando o usuário abre uma versão mais antiga da solução.

-   Se o <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE> sinalizador não for especificado no <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> chama, em seguida, você deve solicitar que o usuário para atualizar o arquivo de projeto.

     A seguir está uma mensagem de prompt de atualização de exemplo:

     "O projeto '%1' foi criado com uma versão mais antiga do Visual Studio. Se você abri-lo com esta versão do Visual Studio, você não poderá abri-lo com as versões mais antigas do Visual Studio. Você deseja continuar e abrir este projeto?"

### <a name="to-implement-ivsprojectupgradeviafactory"></a>Para implementar IVsProjectUpgradeViaFactory

1.  Implementar o método do <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> interface, especificamente o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> método em sua implementação de fábrica de projeto, ou fazer com que as implementações seja chamado de sua implementação de fábrica do projeto.

2.  Se você quiser fazer uma atualização no local como parte da solução abrindo, forneça o sinalizador <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_SXSBACKUP> como o `VSPUVF_FLAGS` parâmetro em seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> implementação.

3.  Se você quiser fazer uma atualização no local como parte da solução abrindo, forneça o sinalizador <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_COPYBACKUP> como o `VSPUVF_FLAGS` parâmetro em seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> implementação.

4.  Para ambos os as etapas 2 e 3, o arquivo real atualizar etapas, usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>, podem ser implementados conforme descrito no "Implementando `IVsProjectUpgade`" seção abaixo, ou você pode delegar a atualização do arquivo real <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>.

5.  Use os métodos da <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> relacionados mensagens para o usuário usando o Assistente de migração do Visual Studio a após a atualização.

6.  <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileUpgrade> interface é usada para implementar qualquer tipo de atualização de arquivo que precisa ocorrer como parte da atualização do projeto. Essa interface não é chamada de <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>, mas é fornecido como um mecanismo para atualizar os arquivos que fazem parte do sistema de projeto, mas o sistema de projeto principal pode não ser diretamente compatível. Por exemplo, essa situação poderá ocorrer se o compilador relacionadas a arquivos e as propriedades não são manipuladas pela mesma equipe de desenvolvimento que cuida do resto do sistema de projeto.

### <a name="ivsprojectupgrade-implementation"></a>Implementação de IVsProjectUpgrade

Se seu sistema de projeto implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> somente, ele não pode participar de **Assistente de conversão do Visual Studio**. No entanto, mesmo se você implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> interface, você ainda pode delegar a atualização do arquivo <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> implementação.

#### <a name="to-implement-ivsprojectupgrade"></a>Para implementar IVsProjectUpgrade

1.  Quando um usuário tenta abrir um projeto, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> método é chamado pelo ambiente depois que o projeto é aberto e a ação antes de qualquer outro usuário possa ser executada no projeto. Se o usuário já tinha sido avisado para atualizar a solução, em seguida, a <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE> sinalizador é passado a `grfUpgradeFlags` parâmetro. Se o usuário abrir um projeto diretamente, tal como usando o **Adicionar projeto existente** comando, em seguida, a <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS.UPF_SILENTMIGRATE> sinalizador não for passado, e o projeto precisa solicitar ao usuário para atualizar.

2.  Em resposta ao <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> chamada, o projeto deve avaliar se o arquivo de projeto é atualizado. Se o projeto não precisa atualizar o tipo de projeto para uma nova versão e, em seguida, pode simplesmente retornar o <xref:Microsoft.VisualStudio.VSConstants.S_OK> sinalizador.

3.  Se o projeto precisa atualizar o tipo de projeto para uma nova versão, ele deve determinar se o arquivo de projeto pode ser modificado por meio da chamada a <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> método e passar um valor de <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags> para o `rgfQueryEdit` parâmetro. O projeto, em seguida, precisa fazer o seguinte:

    -   Se o `VSQueryEditResult` valor retornado na `pfEditCanceled` parâmetro é <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditOK>, em seguida, a atualização pode continuar porque o arquivo de projeto pode ser gravado.

    -   Se o `VSQueryEditResult` valor retornado na `pfEditCanceled` parâmetro é <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditNotOK> e o `VSQueryEditResult` valor tem o <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags.QER_ReadOnlyNotUnderScc> bit definido, em seguida, <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> deve retornar a falha, porque os usuários devem resolver as permissões execute em si. O projeto deve, em seguida, faça o seguinte:

         Relatar o erro para o usuário chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> e retornar o <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes.VS_E_PROJECTMIGRATIONFAILED> código de erro para <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>.

    -   Se o `VSQueryEditResult` valor é <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditNotOK> e o `VSQueryEditResultFlags` tem valor de <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags.QER_ReadOnlyUnderScc> bit definido, em seguida, o arquivo de projeto deve fazer check-out chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_ForceEdit_NoPrompting>, <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_DisallowInMemoryEdits>,...).

4.  Se o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> chamada no arquivo de projeto faz com que o arquivo de check-out e a versão mais recente a ser recuperado, em seguida, o projeto seja descarregado e recarregado. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> método é chamado novamente depois de criar outra instância do projeto. Na segunda chamada, o arquivo de projeto pode ser gravado em disco; é recomendável que o projeto de salvar uma cópia do arquivo de projeto no formato anterior com um. Extensão antiga, faça suas alterações de atualização necessárias e salve o arquivo de projeto no novo formato. Novamente, se qualquer parte do processo de atualização falhar, o método deve indicar falha, retornando <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes.VS_E_PROJECTMIGRATIONFAILED>. Isso faz com que o projeto a ser descarregado no Gerenciador de soluções.

     É importante compreender o processo de conclusão que ocorre no ambiente para o caso em que a chamada para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> método (especificando um valor de ReportOnly) retorna o <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditNotOK> e o <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags.QER_ReadOnlyUnderScc> sinalizadores.

5.  O usuário tenta abrir o arquivo de projeto.

6.  O ambiente chama seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> implementação.

7.  Se <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> retorna `true`, em seguida, chama o ambiente seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> implementação.

8.  O ambiente chama seu <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A> implementação para abrir o arquivo e inicializar o objeto de projeto, por exemplo, Projeto1.

9. O ambiente chama seu `IVsProjectUpgrade::UpgradeProject` implementação para determinar se o arquivo de projeto precisa ser atualizado.

10. Você chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> e passar um valor de <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_ReportOnly> para o `rgfQueryEdit` parâmetro.

11. Retorna o ambiente <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditNotOK> para `VSQueryEditResult` e o <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags.QER_ReadOnlyUnderScc> bit é definido em `VSQueryEditResultFlags`.

12. Sua <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> implementação chama `IVsQueryEditQuerySave::QueryEditFiles` (<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_ForceEdit_NoPrompting>, <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_DisallowInMemoryEdits>).

Essa chamada pode causar uma nova cópia do arquivo de projeto para fazer check-out e recuperar a versão mais recente, bem como a necessidade de recarregar o arquivo de projeto. Neste ponto, uma das duas coisas acontecem:

-   Se você manipular seu próprio recarregar o projeto, em seguida, o ambiente chama seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> implementação (VSITEMID_ROOT). Quando você receber essa chamada, recarregue a primeira instância do seu projeto (Projeto1) e continuar atualizando seu arquivo de projeto. O ambiente sabe que você trate seu próprio recarregar o projeto se você retornar `true` para <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_HandlesOwnReload>).

-   Se você não tratar seu próprios recarregar o projeto, então você retornar `false` para <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_HandlesOwnReload>). Nesse caso, antes de <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>(QEF_ForceEdit_NoPrompting, QEF_DisallowInMemoryEdits) é retornado, o ambiente cria outra nova instância do seu projeto, por exemplo, Projeto2, da seguinte maneira:

    1.  As chamadas de ambiente <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.Close%2A> em seu primeiro objeto de projeto, Projeto1, colocando esse objeto no estado inativo.

    2.  O ambiente chama seu `IVsProjectFactory::CreateProject` implementação para criar uma segunda instância do seu projeto, Projeto2.

    3.  O ambiente chama seu `IPersistFileFormat::Load` implementação para abrir o arquivo e inicializar o segundo objeto de projeto Projeto2.

    4.  As chamadas de ambiente `IVsProjectUpgrade::UpgradeProject` pela segunda vez determinar se o objeto de projeto deve ser atualizado. No entanto, essa chamada é feita em um novo em segundo lugar, a instância do projeto, Projeto2. Esse é o projeto que é aberto na solução.

        > [!NOTE]
        > Na instância do seu primeiro projeto, Projeto1, é colocado no estado inativo, em seguida, você deve retornar <xref:Microsoft.VisualStudio.VSConstants.S_OK> da primeira chamada para seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> implementação.

    5.  Você chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> e passar um valor de <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags.QEF_ReportOnly> para o `rgfQueryEdit` parâmetro.

    6.  Retorna o ambiente <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult.QER_EditOK> e a atualização pode continuar porque o arquivo de projeto pode ser gravado.

Se você não conseguir atualizar, retorne <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes.VS_E_PROJECTMIGRATIONFAILED> de `IVsProjectUpgrade::UpgradeProject`. Se nenhuma atualização é necessária ou se você optar por não atualizar, trate o `IVsProjectUpgrade::UpgradeProject` chamar como inoperante. Se você retornar <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes.VS_E_PROJECTMIGRATIONFAILED>, um nó de espaço reservado é adicionado à solução para seu projeto.

## <a name="upgrading-project-items"></a>Atualizando itens de projeto

Se você adicionar ou gerenciar itens de sistemas de projeto, você não implemente, você talvez precise participar do processo de atualização do projeto. Crystal Reports é um exemplo de um item que pode ser adicionado ao sistema de projeto.

Normalmente, os implementadores de item de projeto desejam aproveitar um projeto já totalmente instanciado e atualizado porque eles precisam saber o que o projeto são referências e o que outras propriedades do projeto existem para tomar uma decisão de atualização.

### <a name="to-get-the-project-upgrade-notification"></a>Para obter a notificação de atualização de projeto

1.  Defina o <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80.SolutionOrProjectUpgrading> sinalizador (definida em vsshell80.idl) em sua implementação de item de projeto. Isso faz com que o item de projeto VSPackage a carga automaticamente quando o shell do Visual Studio determina que um sistema de projeto está no processo de atualização.

2.  Aconselhamos a <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> por meio da interface de <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution2.AdviseSolutionEvents%2A> método.

3.  O <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> interface é disparado após a implementação do sistema de projeto tiver concluído suas operações de atualização e o novo projeto atualizado. Dependendo do cenário, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEventsProjectUpgrade> interface é disparado após o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenSolution%2A>, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>, ou o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterLoadProject%2A> métodos.

### <a name="to-upgrade-the-project-item-files"></a>Para atualizar os arquivos de item de projeto

1.  Você deve gerenciar cuidadosamente o processo de backup do arquivo em sua implementação de item de projeto. Isso se aplica especificamente para um backup de lado a lado, em que o `fUpgradeFlag` parâmetro do <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> método está definido como <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS.PUVFF_SXSBACKUP>, onde os arquivos que tinham sido feitos são posicionados ao longo de arquivos lado que são designados como ". old". Arquivos de backup mais antigos do que a hora do sistema quando o projeto foi atualizado podem ser designados como obsoletos. Além disso, eles poderão ser substituídos, a menos que você siga etapas específicas para evitar isso.

2.  No momento em seu item de projeto recebe uma notificação de atualização de projeto, o **Assistente de conversão do Visual Studio** ainda é exibido. Portanto, você deve usar os métodos do <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> interface para fornecer mensagens de atualização para o Assistente de interface do usuário.

## <a name="see-also"></a>Consulte também

- [Projetos](../../extensibility/internals/projects.md)