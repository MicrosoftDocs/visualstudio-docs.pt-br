---
title: Atualizando projetos personalizados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- upgrading project systems
- projects [Visual Studio SDK], upgrading
- project system upgrades [Visual Studio]
ms.assetid: 262ada44-7689-44d8-bacb-9c6d33834d4e
caps.latest.revision: 11
manager: douge
ms.openlocfilehash: 12b99770a7ab884e077ad6ba051a35d6e5316a49
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49844666"
---
# <a name="upgrading-custom-projects"></a>Atualizando projetos personalizados
Se você alterar as informações mantidas no arquivo de projeto entre diferentes versões do Visual Studio do seu produto, em seguida, você precisa dar suporte à atualização de seu arquivo de projeto do ambiente antigo para a nova versão. Para dar suporte à atualização que permite que você participe de **Assistente de conversão do Visual Studio**, implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> interface. Essa interface contém o único mecanismo disponível para a atualização da cópia. A atualização do projeto ocorre como parte da solução é aberta. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> interface é implementada pela fábrica de projeto ou pelo menos deve ser obtido da fábrica de projeto.  
  
 O antigo mecanismo que usa o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> interface ainda tem suporte, mas conceitualmente atualiza o sistema de projeto como parte do projeto aberto. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> interface, portanto, é chamado pelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ambiente mesmo se o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> interface é chamado ou implementada. Essa abordagem permite que você use <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> para implementar a cópia e somente as partes da atualização de projeto e delegue o resto do trabalho a ser feito no local (possivelmente no novo local), o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> interface.  
  
 Para uma implementação de exemplo <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>, consulte [exemplos de VSSDK](../misc/vssdk-samples.md).  
  
 Os seguintes cenários ocorrem com atualizações de projeto:  
  
-   Se o arquivo for de um formato mais recente que o projeto pode suportar, em seguida, ele deve retornar um erro informando isso. Isso pressupõe que a versão mais antiga do produto — por exemplo, Visual Studio .NET 2003 — inclui código para verificar a versão.  
  
-   Se o <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> sinalizador for especificado no <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> método, a atualização vai ser implementado como uma atualização in loco antes da abertura do projeto.  
  
-   Se o <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> sinalizador for especificado no <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> método, a atualização é implementado como uma atualização de cópia.  
  
-   Se o <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS> sinalizador for especificado no <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> chama, em seguida, o usuário foi solicitado pelo ambiente ao atualizar o arquivo de projeto como uma atualização in-loco, depois que o projeto é aberto. Por exemplo, o ambiente solicita ao usuário atualizar quando o usuário abre uma versão mais antiga da solução.  
  
-   Se o <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS> sinalizador não for especificado no <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> chama, em seguida, você deve solicitar que o usuário para atualizar o arquivo de projeto.  
  
     A seguir está uma mensagem de prompt de atualização de exemplo:  
  
     "O projeto '%1' foi criado com uma versão mais antiga do Visual Studio. Se você abri-lo com esta versão do Visual Studio, você não poderá abri-lo com as versões mais antigas do Visual Studio. Você deseja continuar e abrir este projeto?"  
  
### <a name="to-implement-ivsprojectupgradeviafactory"></a>Para implementar IVsProjectUpgradeViaFactory  
  
1.  Implementar o método do <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> interface, especificamente o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> método em sua implementação de fábrica de projeto, ou fazer com que as implementações seja chamado de sua implementação de fábrica do projeto.  
  
2.  Se você quiser fazer uma atualização no local como parte da solução abrindo, forneça o sinalizador <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> como o `VSPUVF_FLAGS` parâmetro em seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> implementação.  
  
3.  Se você quiser fazer uma atualização no local como parte da solução abrindo, forneça o sinalizador <xref:Microsoft.VisualStudio.Shell.Interop.__VSPPROJECTUPGRADEVIAFACTORYFLAGS> como o `VSPUVF_FLAGS` parâmetro em seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory.UpgradeProject%2A> implementação.  
  
4.  Para ambos os as etapas 2 e 3, o arquivo real atualizar etapas, usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>, podem ser implementados conforme descrito no "Implementando `IVsProjectUpgade`" seção abaixo, ou você pode delegar a atualização do arquivo real <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>.  
  
5.  Use os métodos da <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> relacionados mensagens para o usuário usando o Assistente de migração do Visual Studio a após a atualização.  
  
6.  <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileUpgrade> interface é usada para implementar qualquer tipo de atualização de arquivo que precisa ocorrer como parte da atualização do projeto. Essa interface não é chamada de <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>, mas é fornecido como um mecanismo para atualizar os arquivos que fazem parte do sistema de projeto, mas o sistema de projeto principal pode não ser diretamente compatível. Por exemplo, essa situação poderá ocorrer se o compilador relacionadas a arquivos e as propriedades não são manipuladas pela mesma equipe de desenvolvimento que cuida do resto do sistema de projeto.  
  
## <a name="ivsprojectupgrade-implementation"></a>Implementação de IVsProjectUpgrade  
 Se seu sistema de projeto implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> somente, ele não pode participar de **Assistente de conversão do Visual Studio**. No entanto, mesmo se você implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> interface, você ainda pode delegar a atualização do arquivo <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> implementação.  
  
#### <a name="to-implement-ivsprojectupgrade"></a>Para implementar IVsProjectUpgrade  
  
1. Quando um usuário tenta abrir um projeto, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> método é chamado pelo ambiente depois que o projeto é aberto e a ação antes de qualquer outro usuário possa ser executada no projeto. Se o usuário já tinha sido avisado para atualizar a solução, em seguida, a <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS> sinalizador é passado a `grfUpgradeFlags` parâmetro. Se o usuário abrir um projeto diretamente, tal como usando o **Adicionar projeto existente** comando, em seguida, a <xref:Microsoft.VisualStudio.Shell.Interop.__VSUPGRADEPROJFLAGS> sinalizador não for passado, e o projeto precisa solicitar ao usuário para atualizar.  
  
2. Em resposta ao <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> chamada, o projeto deve avaliar se o arquivo de projeto é atualizado. Se o projeto não precisa atualizar o tipo de projeto para uma nova versão e, em seguida, pode simplesmente retornar o <xref:Microsoft.VisualStudio.VSConstants.S_OK> sinalizador.  
  
3. Se o projeto precisa atualizar o tipo de projeto para uma nova versão, ele deve determinar se o arquivo de projeto pode ser modificado por meio da chamada a <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> método e passar um valor de <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags> para o `rgfQueryEdit` parâmetro. O projeto, em seguida, precisa fazer o seguinte:  
  
   -   Se o `VSQueryEditResult` valor retornado na `pfEditCanceled` parâmetro é <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult>, em seguida, a atualização pode continuar porque o arquivo de projeto pode ser gravado.  
  
   -   Se o `VSQueryEditResult` valor retornado na `pfEditCanceled` parâmetro é <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> e o `VSQueryEditResult` valor tem o <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags> bit definido, em seguida, <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> deve retornar a falha, porque os usuários devem resolver as permissões execute em si. O projeto deve, em seguida, faça o seguinte:  
  
        Relatar o erro para o usuário ao chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>. e retornar os <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes> código de erro para <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade>.  
  
   -   Se o `VSQueryEditResult` valor é <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> e o `VSQueryEditResultFlags` tem valor de <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags> bit definido, em seguida, o arquivo de projeto deve fazer check-out chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags>, <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags>,...).  
  
4. Se o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> chamada no arquivo de projeto faz com que o arquivo de check-out e a versão mais recente a ser recuperado, em seguida, o projeto seja descarregado e recarregado. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> método é chamado novamente depois de criar outra instância do projeto. Na segunda chamada, o arquivo de projeto pode ser gravado em disco; é recomendável que o projeto de salvar uma cópia do arquivo de projeto no formato anterior com um. Extensão antiga, faça suas alterações de atualização necessárias e salve o arquivo de projeto no novo formato. Novamente, se qualquer parte do processo de atualização falhar, o método deve indicar falha, retornando <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes>. Isso faz com que o projeto a ser descarregado no Gerenciador de soluções.  
  
    É importante compreender o processo de conclusão que ocorre no ambiente para o caso em que a chamada para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> método (especificando um valor de ReportOnly) retorna o <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> e o <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags> sinalizadores.  
  
5. O usuário tenta abrir o arquivo de projeto.  
  
6. O ambiente chama seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> implementação.  
  
7. Se <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> retorna `true`, em seguida, chama o ambiente seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CanCreateProject%2A> implementação.  
  
8. O ambiente chama seu <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A> implementação para abrir o arquivo e inicializar o objeto de projeto, por exemplo, Projeto1.  
  
9. O ambiente chama seu `IVsProjectUpgrade::UpgradeProject` implementação para determinar se o arquivo de projeto precisa ser atualizado.  
  
10. Você chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> e passar um valor de <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags> para o `rgfQueryEdit` parâmetro.  
  
11. Retorna o ambiente <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> para `VSQueryEditResult` e o <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResultFlags> bit é definido em `VSQueryEditResultFlags`.  
  
12. Sua <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade> implementação chama `IVsQueryEditQuerySave::QueryEditFiles` (<xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags>, <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags>).  
  
    Essa chamada pode causar uma nova cópia do arquivo de projeto para fazer check-out e recuperar a versão mais recente, bem como a necessidade de recarregar o arquivo de projeto. Neste ponto, uma das duas coisas acontecem:  
  
- Se você manipular seu próprio recarregar o projeto, em seguida, o ambiente chama seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.ReloadItem%2A> implementação (VSITEMID_ROOT). Quando você receber essa chamada, recarregue a primeira instância do seu projeto (Projeto1) e continuar atualizando seu arquivo de projeto. O ambiente sabe que você trate seu próprio recarregar o projeto se você retornar `true` para <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>).  
  
- Se você não tratar seu próprios recarregar o projeto, então você retornar `false` para <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>). Nesse caso, antes de <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>([QEF_ForceEdit_NoPrompting](assetId:///T:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags?qualifyHint=False&autoUpgrade=True), [QEF_DisallowInMemoryEdits](assetId:///T:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags?qualifyHint=False&autoUpgrade=True),) é retornado, o ambiente cria outra nova, a instância do seu projeto, por exemplo, Projeto2, como a seguir:  
  
  1.  As chamadas de ambiente <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.Close%2A> em seu primeiro objeto de projeto, Projeto1, colocando esse objeto no estado inativo.  
  
  2.  O ambiente chama seu `IVsProjectFactory::CreateProject` implementação para criar uma segunda instância do seu projeto, Projeto2.  
  
  3.  O ambiente chama seu `IPersistFileFormat::Load` implementação para abrir o arquivo e inicializar o segundo objeto de projeto Projeto2.  
  
  4.  As chamadas de ambiente `IVsProjectUpgrade::UpgradeProject` pela segunda vez determinar se o objeto de projeto deve ser atualizado. No entanto, essa chamada é feita em um novo em segundo lugar, a instância do projeto, Projeto2. Esse é o projeto que é aberto na solução.  
  
      > [!NOTE]
      >  Na instância do seu primeiro projeto, Projeto1, é colocado no estado inativo, em seguida, você deve retornar <xref:Microsoft.VisualStudio.VSConstants.S_OK> da primeira chamada para seu <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgrade.UpgradeProject%2A> implementação. Ver [projeto básico](http://msdn.microsoft.com/en-us/385fd2a3-d9f1-4808-87c2-a3f05a91fc36) para a implementação de `IVsProjectUpgrade::UpgradeProject`.  
  
  5.  Você chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> e passar um valor de <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditFlags> para o `rgfQueryEdit` parâmetro.  
  
  6.  Retorna o ambiente <xref:Microsoft.VisualStudio.Shell.Interop.tagVSQueryEditResult> e a atualização pode continuar porque o arquivo de projeto pode ser gravado.  
  
  Se você não conseguir atualizar, retorne <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes> de `IVsProjectUpgrade::UpgradeProject`. Se nenhuma atualização é necessária ou se você optar por não atualizar, trate o `IVsProjectUpgrade::UpgradeProject` chamar como inoperante. Se você retornar <xref:Microsoft.VisualStudio.Shell.Interop.VSErrorCodes>, um nó de espaço reservado é adicionado à solução para seu projeto.  
  
## <a name="see-also"></a>Consulte também  
 [Assistente de conversão do Visual Studio](http://msdn.microsoft.com/en-us/4acfd30e-c192-4184-a86f-2da5e4c3d83c)   
 [Atualizando itens de projeto](../misc/upgrading-project-items.md)   
 [Projetos](../extensibility/internals/projects.md)