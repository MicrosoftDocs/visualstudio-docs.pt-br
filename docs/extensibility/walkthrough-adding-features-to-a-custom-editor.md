---
title: 'Walkthrough: adicionando recursos a um editor personalizado | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], custom - add features
ms.assetid: bfe083b6-3e35-4b9c-ad4f-b30b9ff412a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d7605307d24aa320d2f892dc332f9ff78e14114e
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905948"
---
# <a name="walkthrough-add-features-to-a-custom-editor"></a>Walkthrough: adicionar recursos a um editor personalizado
Depois de criar um editor personalizado, você pode adicionar mais recursos a ele.

## <a name="to-create-an-editor-for-a-vspackage"></a>Para criar um editor para um VSPackage

1. Crie um editor personalizado usando o modelo de projeto de pacote do Visual Studio.

     Para obter mais informações, consulte [Walkthrough: criar um editor personalizado](../extensibility/walkthrough-creating-a-custom-editor.md).

2. Decida se deseja que seu editor dê suporte a uma única exibição ou a várias exibições.

     Um editor que dá suporte ao comando **nova janela** , ou tem exibição de formulário e exibição de código, requer objetos de dados de documento e objetos de exibição de documento separados. Em um editor que dá suporte apenas a uma única exibição, o objeto de dados do documento e o objeto de exibição de documento podem ser implementados no mesmo objeto.

     Para obter um exemplo de várias exibições, consulte [suporte para vários modos de exibição de documentos](../extensibility/supporting-multiple-document-views.md).

3. Implemente uma fábrica de editor Configurando a <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> interface.

     Para obter mais informações, consulte [fábricas de editor](/visualstudio/extensibility/editor-factories?view=vs-2015).

4. Decida se deseja que seu editor use ativação in-loco ou incorporação simplificada para gerenciar a janela de objeto de exibição de documento.

     Uma janela de editor de incorporação simplificada hospeda uma exibição de documento padrão, enquanto uma janela do editor de ativação in-loco hospeda um controle ActiveX ou outro objeto ativo como sua exibição de documento. Para obter mais informações, consulte [inserção simplificada](../extensibility/simplified-embedding.md) e [ativação in-loco](/visualstudio/misc/in-place-activation?view=vs-2015).

5. Implemente a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface para manipular comandos.

6. Fornecer persistência de documentos e resposta a alterações de arquivos externos:

    1. Para manter o arquivo, implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> e <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> no objeto de dados de documento do editor.

    2. Para responder a alterações de arquivo externo, implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl> no objeto de dados de documento do editor.

        > [!NOTE]
        > Ligue `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx> para para obter um ponteiro para `IVsFileChangeEx` .

7. Coordenar eventos de edição de documento com controle do código-fonte. Siga estas etapas:

    1. Obtenha um ponteiro `IVsQueryEditQuerySave2` chamando `QueryService` on <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> .

    2. Quando o primeiro evento de edição ocorrer, chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> método.

         Esse método solicita que o usuário Verifique o arquivo se ele ainda não tiver feito check-out. Certifique-se de lidar com a condição "arquivo não verificado" para erros de AVERT.

    3. Da mesma forma, antes de salvar o arquivo, chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A> método.

         Esse método solicita que o usuário salve o arquivo se ele não tiver sido salvo ou se for alterado desde o último salvamento.

8. Habilite a janela **Propriedades** para exibir as propriedades do texto selecionado no editor. Siga estas etapas:

    1. Chame <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> cada vez que as alterações de seleção de texto, passando a sua implementação do <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> .

    2. Ligue `QueryService` <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> para o serviço para obter um ponteiro <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> .

9. Permita que os usuários arrastem e soltem itens entre o editor e a **caixa de ferramentas**, ou entre editores externos (como o Microsoft Word) e a **caixa de ferramentas**. Siga estas etapas:

    1. Implemente `IDropTarget` em seu editor para alertar o IDE de que seu editor é um destino de soltura.

    2. Implemente a <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser> interface na exibição para que o editor possa habilitar e Desabilitar itens na **caixa de ferramentas**.

    3. Implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.ResetDefaults%2A> e chame `QueryService` on <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox> Service para obter um ponteiro para <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> as <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> interfaces e.

         Essas etapas permitem que seu VSPackage Adicione novos itens à **caixa de ferramentas**.

10. Decida se deseja outros recursos opcionais para o seu editor.

    - Se você quiser que o editor ofereça suporte a comandos de localização e substituição, implemente <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget> .

    - Se você quiser usar uma janela de ferramenta de estrutura de tópicos de documento em seu editor, implemente `IVsDocOutlineProvider` .

    - Se você quiser usar uma barra de status em seu editor, implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> e chame `QueryService` para <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> para obter um ponteiro para `IVsStatusBar` .

         Por exemplo, um editor pode exibir informações de linha/coluna, modo de seleção (fluxo/caixa) e modo de inserção (inserir/sobreposição).

    - Se você quiser que o editor dê suporte ao `Undo` comando, o método recomendado é usar o modelo do Gerenciador de desfazer OLE. Como alternativa, você pode fazer com que o editor manipule o `Undo` comando diretamente.

11. Crie informações de registro, incluindo os GUIDs para o VSPackage, os menus, o editor e outros recursos.

     Veja a seguir um exemplo genérico de código que você colocaria no script do arquivo *. rgs* para demonstrar como registrar adequadamente um editor.

    ```csharp
    NoRemove Editors
    {
          ForceRemove {...guidEditor...} = s 'RTF Editor'
          {
             val Package = s '{...guidVsPackage...}'
             ForceRemove Extensions
             {
                val rtf = d 50
             }
          }
    }
    NoRemove Menus
    {
          val {...guidVsPackage...} = s ',203,11'
    }
    ```

12. Implemente o suporte à ajuda contextual.

     Esta etapa permite que você forneça ajuda F1 e suporte à janela de ajuda dinâmica para itens em seu editor. Para obter mais informações, consulte [como: fornecer contexto para editores](/visualstudio/extensibility/how-to-provide-context-for-editors?view=vs-2015).

13. Expor um modelo de objeto de automação do seu editor implementando a `IDispatch` interface.

     Para obter mais informações, consulte [contribuindo para o modelo de automação](../extensibility/internals/contributing-to-the-automation-model.md).

## <a name="robust-programming"></a>Programação robusta

- A instância do editor é criada quando o IDE chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> método. Se o editor oferecer suporte a várias exibições, o `CreateEditorInstance` criará os dados do documento e os objetos de exibição de documento. Se o objeto de dados do documento já estiver aberto, um valor não nulo `punkDocDataExisting` será passado para `IVsEditorFactory::CreateEditorInstance` . Sua implementação de fábrica do editor deve determinar se um objeto de dados de documento existente é compatível consultando as interfaces apropriadas nele. Para obter mais informações, consulte [dando suporte a exibições de vários documentos](../extensibility/supporting-multiple-document-views.md).

- Se você usar a abordagem de incorporação simplificada, implemente a <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> interface.

- Se você decidir usar a ativação in-loco, implemente as seguintes interfaces:

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleObject>

   <xref:Microsoft.VisualStudio.OLE.Interop.IOleInPlaceActiveObject>

   <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>

  > [!NOTE]
  > A `IOleInPlaceComponent` interface é usada para evitar a mesclagem de menus OLE 2.

   Sua `IOleCommandTarget` implementação manipula comandos como **recortar**, **copiar**e **colar**. Ao implementar `IOleCommandTarget` , decida se o seu editor exige seu próprio arquivo *. vsct* para definir sua própria estrutura de menu de comando ou se ele pode implementar comandos padrão definidos pelo [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . Normalmente, os editores usam e estendem os menus do IDE e definem suas próprias barras de ferramentas. No entanto, muitas vezes é necessário que um editor defina seus próprios comandos específicos além de usar o conjunto de comandos padrão do IDE. O editor deve declarar os comandos padrão que ele usa e, em seguida, definir novos comandos, menus de contexto, menus de nível superior e barras de ferramentas em um arquivo *. vsct* . Se você criar um editor de ativação in-loco, implemente <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> e defina os menus e as barras de ferramentas para o editor em um arquivo *. vsct* em vez de usar a mesclagem de menu OLE 2.

- Para evitar a distorcida de comando de menu na interface do usuário, você deve usar os comandos existentes no IDE antes de inventar novos comandos. Os comandos compartilhados são definidos em *SharedCmdDef. vsct* e *ShellCmdDef. vsct*. Esses arquivos são instalados por padrão no subdiretório VisualStudioIntegration\Common\Inc da [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] instalação do.

- `ISelectionContainer`pode expressar seleções únicas e múltiplas. Cada objeto selecionado é implementado como um `IDispatch` objeto.

- O IDE implementa `IOleUndoManager` como um serviço acessível de um <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> ou como um objeto que pode ser instanciado por meio do <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> . O editor implementa a `IOleUndoUnit` interface para cada `Undo` ação.

- Há dois lugares em que um editor personalizado pode expor objetos de automação:

  - `Document.Object`

  - `Window.Object`

## <a name="see-also"></a>Confira também

- [Contribuir para o modelo de automação](../extensibility/internals/contributing-to-the-automation-model.md)
