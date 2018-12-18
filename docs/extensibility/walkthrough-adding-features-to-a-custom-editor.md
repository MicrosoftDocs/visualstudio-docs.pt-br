---
title: 'Passo a passo: Adicionando recursos a um Editor personalizado | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - add features
ms.assetid: bfe083b6-3e35-4b9c-ad4f-b30b9ff412a5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 7062f44fe119858e579a53325deca0ea04b46475
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49873013"
---
# <a name="walkthrough-add-features-to-a-custom-editor"></a>Passo a passo: Adicionar recursos a um editor personalizado
Depois de criar um editor personalizado, você pode adicionar mais recursos a ele.  
  
## <a name="to-create-an-editor-for-a-vspackage"></a>Criar um editor para um VSPackage  
  
1.  Crie um editor personalizado usando o modelo de projeto do Visual Studio Package.  
  
     Para obter mais informações, consulte [instruções passo a passo: criar um editor personalizado](../extensibility/walkthrough-creating-a-custom-editor.md).  
  
2.  Decida se deseja que o seu editor para dar suporte a um modo de exibição único ou vários modos de exibição.  
  
     Um editor que oferece suporte a **nova janela** de comando, ou tem o modo de exibição de formulário e exibição de código, requer que os objetos de dados de documento separado e objetos de exibição de documento. Em um editor que dá suporte a apenas uma única exibição, o objeto de dados de documento e o objeto de exibição de documento podem ser implementado no mesmo objeto.  
  
     Para obter um exemplo de vários modos de exibição, consulte [dar suporte a vários modos de exibição de documento](../extensibility/supporting-multiple-document-views.md).  
  
3.  Implementar uma fábrica de editor, configurando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> interface.  
  
     Para obter mais informações, consulte [fábricas](../extensibility/editor-factories.md).  
  
4.  Decida se deseja que seu editor para usar a ativação in-loco ou simplificado de incorporação para gerenciar a janela de objeto de exibição de documento.  
  
     Uma janela do editor de incorporação simplificada hospeda um modo de exibição de documento padrão, enquanto uma janela do editor de ativação in-loco hospeda um controle ActiveX ou outro objeto do Active Directory como seu modo de exibição de documento. Para obter mais informações, consulte [simplificado incorporação](../extensibility/simplified-embedding.md) e [ativação in-loco](../extensibility/in-place-activation.md).  
  
5.  Implementar o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interface para lidar com comandos.  
  
6.  Fornecem persistência de documento e resposta a alterações de arquivo externo:  
  
    1.  Para manter o arquivo, implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> e <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> no objeto de dados de documento do seu editor.  
  
    2.  Para responder a alterações de arquivo externo, implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl> no objeto de dados de documento do seu editor.  
  
        > [!NOTE]
        >  Chame `QueryService` na <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx> para obter um ponteiro para `IVsFileChangeEx`.  
  
7.  Coordene os eventos de edição de documentos com controle do código fonte. Siga estas etapas:  
  
    1.  Obter um ponteiro para `IVsQueryEditQuerySave2` chamando `QueryService` em <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>.  
  
    2.  Quando ocorre o primeiro evento de edição, chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> método.  
  
         Esse método solicitará que o usuário fazer check-out do arquivo se ele ainda não foi verificado. Certifique-se de lidar com uma condição de "arquivo não check-out" para evitar erros.  
  
    3.  Da mesma forma, antes de salvar o arquivo, chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFile%2A> método.  
  
         Este método solicita ao usuário para salvar o arquivo se ele ainda não foi salvo ou se ele for alterado desde o último salvamento.  
  
8.  Habilitar o **propriedades** janela para exibir as propriedades do texto selecionado no editor. Siga estas etapas:  
  
    1.  Chame <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> cada seleção de texto de tempo for alterado, passando na sua implementação de <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>.  
  
    2.  Chame `QueryService` na <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> service para obter um ponteiro para <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>.  
  
9. Permitir que os usuários arrastar e soltar itens entre o editor e o **caixa de ferramentas**, ou entre editores externos (como o Microsoft Word) e o **caixa de ferramentas**. Siga estas etapas:  
  
    1.  Implementar `IDropTarget` em seu editor para alertar o IDE que seu editor é um destino de soltar.  
  
    2.  Implemente a <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser> interface na exibição para que o editor pode habilitar e desabilitar itens na **caixa de ferramentas**.  
  
    3.  Implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.ResetDefaults%2A> e chame `QueryService` nos <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox> service para obter um ponteiro para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> interfaces.  
  
         Essas etapas habilitam o VSPackage adicionar novos itens para o **caixa de ferramentas**.  
  
10. Decida se deseja que os outros recursos opcionais para que o editor.  
  
    -   Se você quiser que o seu editor para dar suporte a localizar e substituir os comandos, implementar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget>.  
  
    -   Se você quiser usar uma janela de ferramentas de estrutura de tópicos do documento em seu editor, implementar `IVsDocOutlineProvider`.  
  
    -   Se você quiser usar uma barra de status em seu editor, implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> e chame `QueryService` para <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> para obter um ponteiro para `IVsStatusBar`.  
  
         Por exemplo, um editor pode exibir a linha / informações de coluna, o modo de seleção (transmitir / caixa) e o modo de inserção (Inserir / /overstrike).  
  
    -   Se você quiser que o seu editor para dar suporte a `Undo` de comando, o método recomendado é usar o modelo do Gerenciador de desfazer OLE. Como alternativa, você pode ter o identificador do editor de `Undo` comando diretamente.  
  
11. Crie registro de informações, incluindo os GUIDs para o VSPackage, os menus, o editor e outros recursos.  
  
     A seguir está um exemplo genérico de código que você colocaria em seu *rgs* script para demonstrar como se registrar corretamente um editor de arquivo.  
  
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
  
12. Implemente suporte a Ajuda contextual.  
  
     Esta etapa permite que você forneça suportam a Ajuda de F1 e a janela Ajuda dinâmica para itens em seu editor. Para obter mais informações, consulte [como: fornecer contexto para editores](../extensibility/how-to-provide-context-for-editors.md).  
  
13. Expor um modelo de objeto de automação do seu editor, Implementando o `IDispatch` interface.  
  
     Para obter mais informações, consulte [contribuindo para o modelo de automação](../extensibility/internals/contributing-to-the-automation-model.md).  
  
## <a name="robust-programming"></a>Programação robusta  
  
- A instância do editor é criada quando o IDE chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> método. Se o editor dá suporte a vários modos de exibição `CreateEditorInstance` cria dados de documento e os objetos de exibição de documento. Se o objeto de dados de documento já está aberto, não-nulos `punkDocDataExisting` valor é passado para `IVsEditorFactory::CreateEditorInstance`. Sua implementação de fábrica de editor deve determinar se um objeto de dados de documento existente é compatível, consultando as interfaces apropriadas nele. Para obter mais informações, consulte [que dão suporte a várias exibições de documento](../extensibility/supporting-multiple-document-views.md).  
  
- Se você usar a abordagem de incorporação simplificada, implemente o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> interface.  
  
- Se você decidir usar a ativação in-loco, implemente as seguintes interfaces:  
  
   <xref:Microsoft.VisualStudio.OLE.Interop.IOleObject>  
  
   <xref:Microsoft.VisualStudio.OLE.Interop.IOleInPlaceActiveObject>  
  
   <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>  
  
  > [!NOTE]
  >  O `IOleInPlaceComponent` interface é usada para evitar a mesclagem de menu do OLE 2.  
  
   Sua `IOleCommandTarget` implementação lida com comandos, como **Recortar**, **cópia**, e **colar**. Ao implementar `IOleCommandTarget`, decida se seu editor requer seu próprio *VSCT* arquivo para definir sua própria estrutura do menu de comando ou se ela pode implementar comandos padrão definidos pelo [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Normalmente, editores de usarem e estendem os menus do IDE e definem suas próprias barras de ferramentas. No entanto, muitas vezes é necessário para um editor definir seus próprios comandos específicos, além de usar o conjunto de comando padrão do IDE. Seu editor deve declarar os comandos padrão, ele usa e, em seguida, definir quaisquer novos comandos, menus de contexto, menus de nível superior e barras de ferramentas em uma *VSCT* arquivo. Se você criar uma ativação in-loco, editor, implementar <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> e definir os menus e barras de ferramentas para o editor em um *VSCT* arquivo em vez de usar a mesclagem de menu do OLE 2.  
  
- Para impedir que o comando de menu acumularem na interface do usuário, você deve usar os comandos existentes no IDE antes de inventar novos comandos. Comandos compartilhados são definidos no *SharedCmdDef.vsct* e *ShellCmdDef.vsct*. Esses arquivos são instalados por padrão no subdiretório VisualStudioIntegration\Common\Inc do seu [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] instalação.  
  
- `ISelectionContainer` pode expressar uma e várias seleções. Cada objeto selecionado é implementado como um `IDispatch` objeto.  
  
- Implementa o IDE `IOleUndoManager` como um serviço acessível a partir de um <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> ou como um objeto que pode ser instanciado por meio de <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A>. A editor implementa o `IOleUndoUnit` interface para cada `Undo` ação.  
  
- Há dois locais um editor personalizado pode expor objetos de automação:  
  
  -   `Document.Object`  
  
  -   `Window.Object`  
  
## <a name="see-also"></a>Consulte também  
 [Contribuir para o modelo de automação](../extensibility/internals/contributing-to-the-automation-model.md)   
 [Como: fornecer contexto para editores](../extensibility/how-to-provide-context-for-editors.md)