---
title: Implementação de categorias personalizadas e itens de exibição | Microsoft Docs
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
- font and color control [Visual Studio SDK], categories
- custom categories
ms.assetid: 99311a93-d642-4344-bbf9-ff6e7fa5bf7f
caps.latest.revision: 26
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 394f8f99539ab49c1201fa61ce612aee22ff2064
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51769128"
---
# <a name="implementing-custom-categories-and-display-items"></a>Implementação de categorias personalizadas e itens de exibição
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um VSPackage pode fornecer controle de fontes e cores do texto para o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE) por meio de categorias personalizadas e itens de exibição.  
  
 Categorias personalizadas e itens de exibição são sobre o **fontes e cores** página de propriedades. Para abrir o **fontes e cores** página de propriedades na **ferramentas** menu, clique em **opções**. Expandir **ambiente** e, em seguida, clique em **fontes e cores**.  
  
 Ao usar esse mecanismo, VSPackages deve implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider> interface e respectivas interfaces associadas.  
  
 Em princípio, esse mecanismo pode ser usado para modificar todas as existentes **exibir itens** e o **categorias** que eles contêm. No entanto, ele não deve ser usado para modificar a **texto EditorCategory** ou seus **exibir itens**. Para obter mais informações, consulte [visão geral de cor e de fonte](../extensibility/font-and-color-overview.md).  
  
 Para implementar personalizado **categorias** ou **exibir itens**, um VSPackage deve:  
  
- Crie ou identifique categorias no registro.  
  
   Implementação do IDE do **fontes e cores** página de propriedades usa essas informações para consultar corretamente para o serviço que dão suporte a uma determinada categoria.  
  
- Criar ou identificar grupos (opcionais) no registro.  
  
   Ele pode ser útil definir um grupo, que representa a união de duas ou mais categorias. Se um grupo estiver definido, o IDE automaticamente mescla subcategorias e distribui itens de exibição dentro do grupo.  
  
- Implementar o suporte do IDE.  
  
- Manipule as alterações de fonte e cor.  
  
  Para obter informações, consulte [acessar fonte armazenados e as configurações de cor](../extensibility/accessing-stored-font-and-color-settings.md).  
  
## <a name="to-create-or-identify-categories"></a>Para criar ou identificar categorias  
  
- Construir um tipo especial de entrada de registro de categoria em [HKLM\Software\Microsoft. \Visual Studio\\*\<versão do Visual Studio >* \FontAndColors\\`<Category>`]  
  
   *\<Categoria >* é o nome não localizado da categoria.  
  
- Preencha o registro com dois valores:  
  
  |Nome|Tipo|Dados|Descrição|  
  |----------|----------|----------|-----------------|  
  |Categoria|REG_SZ|GUID|Um GUID criado para identificar a categoria.|  
  |Pacote|REG_SZ|GUID|O GUID do serviço VSPackage que dá suporte a categoria.|  
  
  O serviço especificado no registro deve fornecer uma implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> para a categoria correspondente.  
  
## <a name="to-create-or-identify-groups"></a>Para criar ou identificar grupos  
  
- Construir um tipo especial de entrada de registro de categoria em [HKLM\Software\Microsoft. \Visual Studio\\*\<versão do Visual Studio >* \FontAndColors\\  *\<grupo >*]  
  
   *\<grupo >* é o nome não localizado do grupo.  
  
- Preencha o registro com dois valores:  
  
  |Nome|Tipo|Dados|Descrição|  
  |----------|----------|----------|-----------------|  
  |Categoria|REG_SZ|GUID|Um GUID criado para identificar o grupo.|  
  |Pacote|REG_SZ|GUID|O GUID do serviço que dá suporte a categoria.|  
  
  O serviço especificado no registro deve fornecer uma implementação de `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup` para o grupo correspondente.  
  
## <a name="to-implement-ide-support"></a>Para implementar o suporte IDE  
  
- Implemente <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider.GetObject%2A>, que retorna um uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> interface ou uma `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup` interface para o IDE para cada **categoria** ou grupo GUID fornecida.  
  
- Para cada **categoria** com suporte, um VSPackage implementa uma instância separada do <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> interface.  
  
- Os métodos implementados por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> deve fornecer o IDE com:  
  
  -   Lista de **exibir itens** no **categoria.**  
  
  -   Nomes localizáveis **exibir itens**.  
  
  -   Exibir informações para cada membro da **categoria**.  
  
  > [!NOTE]
  >  Cada **categoria** deve conter pelo menos um **item de exibição**.  
  
- O IDE usa o `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup` interface para definir uma união de várias categorias.  
  
   Sua implementação fornece o IDE com:  
  
  -   Uma lista da **categorias** que compõem um grupo específico.  
  
  -   Acesso às instâncias do <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> que dão suporte a cada **categoria** dentro do grupo.  
  
  -   Nomes de grupo localizável.  
  
- Atualizando o IDE:  
  
   O IDE armazena informações sobre **fontes e cores** configurações. Portanto, após qualquer modificação do IDE **fontes e cores** configuração, é aconselhável para certificar-se de que o cache é atualizado.  
  
  Atualizar o cache é feito por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> de interface e pode ser realizados itens selecionados globalmente ou apenas no.  
  
## <a name="to-handle-font-and-color-changes"></a>Para lidar com a fonte e cor muda  
 Para suportar adequadamente a colorização do texto que exibe um VSPackage, o serviço de colorização VSPackage de suporte deve responder às alterações iniciadas pelo usuário feitas por meio de **fontes e cores** página de propriedades. Um VSPackage é feito:  
  
-   A manipulação de eventos gerados pelo IDE, Implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents> interface.  
  
     O IDE chama o método apropriado seguindo as modificações de usuário do **fontes e cores** página. Por exemplo, ele chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents.OnFontChanged%2A> método se uma nova fonte é selecionada.  
  
     -ou-  
  
-   Sondando o IDE para que as alterações.  
  
     Isso pode ser feito por meio do sistema implementado <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> interface. Embora principalmente para oferecer suporte a persistência, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> método pode ser usado para obter informações de fonte e cor para **exibir itens**. Para obter mais informações, consulte [acessar fonte armazenados e as configurações de cor](../extensibility/accessing-stored-font-and-color-settings.md).  
  
    > [!NOTE]
    >  Para garantir que os resultados obtidos por meio de sondagem estão corretos, talvez seja útil usar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> interface para determinar se uma liberação do cache e atualização são necessários antes de chamar os métodos de recuperação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> interface.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>   
 [Obtendo informações de cores para colorização de texto e fonte](../extensibility/getting-font-and-color-information-for-text-colorization.md)   
 [Acessando configurações de cor e a fonte armazenada](../extensibility/accessing-stored-font-and-color-settings.md)   
 [Como: acessar o esquema de cores e fontes internas](../extensibility/how-to-access-the-built-in-fonts-and-color-scheme.md)   
 [Visão geral de cor e de fonte](../extensibility/font-and-color-overview.md)

