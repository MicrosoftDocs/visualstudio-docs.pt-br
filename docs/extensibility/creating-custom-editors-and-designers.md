---
title: Criando editores e designers personalizados | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- designers [Visual Studio SDK]
- editors [Visual Studio SDK], custom
ms.assetid: b6a5e8b2-0ae1-4fc3-812d-09d40051b435
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0ddfe2b61c8ef08d77fbb7c841b3bb69c167af2f
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903737"
---
# <a name="create-custom-editors-and-designers"></a>Criar editores e designers personalizados

O IDE (ambiente de desenvolvimento integrado) do Visual Studio pode hospedar diferentes tipos de editor:

- O editor principal do Visual Studio

- Editores personalizados

- Editores externos

- Designers

As informações a seguir ajudam a escolher o tipo de editor de que você precisa.

## <a name="types-of-editor"></a>Tipos de editor

Para obter informações sobre o editor de núcleo do Visual Studio, consulte [estender os serviços de editor e linguagem](../extensibility/extending-the-editor-and-language-services.md).

### <a name="custom-editors"></a>Editores personalizados
 Um editor personalizado é aquele projetado para funcionar em circunstâncias especializadas. Por exemplo, você pode criar um editor cuja função é ler e gravar dados em um repositório específico, como um Microsoft Exchange Server. Escolha um editor personalizado se desejar um editor que funcione somente com o tipo de projeto ou se desejar um editor que tenha apenas alguns comandos específicos. No entanto, observe que os usuários não poderão usar um editor personalizado para editar projetos padrão [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

 Um editor personalizado pode usar uma fábrica de editor e adicionar informações sobre o editor ao registro. No entanto, o tipo de projeto associado ao editor personalizado pode instanciar o editor personalizado de outras maneiras.

 Um editor personalizado pode usar a ativação in-loco ou a incorporação simplificada para implementar uma exibição.

### <a name="external-editors"></a>Editores externos
 Editores externos são editores que não estão integrados ao Visual Studio, como o Microsoft Word, o bloco de notas ou o Microsoft FrontPage. Você pode chamar tal editor se, por exemplo, estiver passando um texto para ele de seu VSPackage. Os editores externos se registram e podem ser usados fora do Visual Studio. Quando você chama um editor externo e ele pode ser inserido em uma janela de host, ele aparece em uma janela no IDE. Caso contrário, o IDE cria uma janela separada para ele.

 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> método define a prioridade do documento usando a <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> enumeração. Se o `DP_External` valor for especificado, o arquivo poderá ser aberto por um editor externo.

## <a name="editor-design-decisions"></a>Decisões de design do editor
 As seguintes perguntas de design ajudarão você a escolher o tipo de editor mais adequado para seu aplicativo:

- Seu aplicativo salvará seus dados em arquivos ou não? Se ele salvar seus dados em arquivos, eles estarão em um formato personalizado ou padrão?

   Se você usar um formato de arquivo padrão, outros tipos de projeto além do seu projeto poderão abrir e ler/gravar dados neles. No entanto, se você usar um formato de arquivo personalizado, somente o tipo de projeto poderá abrir e ler/gravar dados neles.

   Se o seu projeto usa arquivos, você deve personalizar o editor padrão. Se o seu projeto não usar arquivos, mas, em vez disso, usar itens em um banco de dados ou em outro repositório, você deverá criar um editor personalizado.

- Seu editor precisa hospedar controles ActiveX?

   Se o editor hospedar controles ActiveX, implemente um editor de ativação in-loco, conforme descrito na [ativação](/visualstudio/misc/in-place-activation?view=vs-2015)in-loco. Se não hospedar controles ActiveX, use um editor de incorporação simplificado ou personalize o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor padrão.

- Seu editor dará suporte a várias exibições? Você deve dar suporte a várias exibições se quiser que as exibições do seu editor fiquem visíveis ao mesmo tempo que o editor padrão.

   Se o editor precisar oferecer suporte a várias exibições, os dados do documento e os objetos de exibição de documento do editor deverão ser objetos separados. Para obter mais informações, consulte [suporte para vários modos de exibição de documento](../extensibility/supporting-multiple-document-views.md).

   Se o seu editor oferecer suporte a várias exibições, você planeja usar a [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] implementação do buffer de texto do editor principal ( <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> objeto) para o objeto de dados do documento? Ou seja, você deseja dar suporte à exibição do editor lado a lado com o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor principal? A capacidade de fazer isso é a base do designer de formulários.

- Se você precisar hospedar um editor externo, o editor poderá ser incorporado dentro [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ?

   Se puder ser inserido, você deverá criar uma janela de host para o editor externo e, em seguida, chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> método e definir o <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> valor de enumeração como `DP_External` . Se o editor não puder ser inserido, o IDE criará automaticamente uma janela separada para ele.

## <a name="in-this-section"></a>Nesta seção

[Walkthrough: criar um editor personalizado](../extensibility/walkthrough-creating-a-custom-editor.md)\
Explica como criar um editor personalizado.

[Walkthrough: adicionar recursos a um editor personalizado](../extensibility/walkthrough-adding-features-to-a-custom-editor.md)\
Explica como adicionar recursos a um editor personalizado.

[Configuração de metadados e inicialização do designer](../extensibility/designer-initialization-and-metadata-configuration.md)\
Explica como inicializar um designer.

[Fornecer suporte de desfazer para designers](../extensibility/supplying-undo-support-to-designers.md)\
Explica como fornecer suporte de desfazer para designers.

[Cores de sintaxe em editores personalizados](../extensibility/syntax-coloring-in-custom-editors.md)\
Explica a diferença entre as cores de sintaxe no editor principal e em editores personalizados.

[Dados de documento e exibição de documento em editores personalizados](../extensibility/document-data-and-document-view-in-custom-editors.md)\
Explica como implementar dados de documentos e exibições de documentos em editores personalizados.

## <a name="related-sections"></a>Seções relacionadas

[Interfaces herdadas no editor](/visualstudio/extensibility/legacy-interfaces-in-the-editor?view=vs-2015)\
Explica como acessar o editor principal por meio da API herdada.

[Desenvolver um serviço de linguagem herdado](../extensibility/internals/developing-a-legacy-language-service.md)\
Explica como implementar um serviço de linguagem.

[Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)\
Explica como criar elementos de interface do usuário que correspondem ao restante do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>
