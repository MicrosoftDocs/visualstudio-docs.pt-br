---
title: Obtendo informações de cores para colorização de texto e fonte | Microsoft Docs
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
- text, coloring
- font and color control [Visual Studio SDK], coloring
ms.assetid: d1f985bd-743e-40b7-9458-d9af53647c91
caps.latest.revision: 23
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 41fc6ac7ba20bc552ebdfde2cab69dd28867ee7f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741280"
---
# <a name="getting-font-and-color-information-for-text-colorization"></a>Obtendo informações de cores para colorização de texto e fonte
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O processo que processa ou exibe texto coloridos serão em elementos de (UI) interface do usuário depende do tipo de projeto, sua tecnologia e desenvolvedor preferências. O **fontes e cores** página de propriedades armazena as configurações.  
  
 A maioria das implementações que exibem texto coloridos serão precisa o `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults` e associados a interfaces para as configurações de exibição de apresentação, recuperar e armazenar texto.  
  
> [!NOTE]
>  Ao personalizar o editor principal (que oferece suporte a **EditorCategory texto**), é altamente recomendável que você use a tecnologia de cores no serviço de linguagem. Para obter mais informações, consulte [visão geral de cor e de fonte](../extensibility/font-and-color-overview.md).  
  
## <a name="getting-default-font-and-color-information"></a>Obtendo informações de cor e a fonte padrão  
 Todos os as **fontes e cores** configurações de qualquer janela de exibição de texto devem ser especificadas na **itens de exibição** de um **categoria**. Para obter mais informações, consulte [fontes e cores, ambiente, caixa de diálogo Opções](../ide/reference/fonts-and-colors-environment-options-dialog-box.md).  
  
 Para colorir, um VSPackage deverá obter o atual **fontes e cores** configurações. Um VSPackage pode fazer isso das seguintes maneiras, dependendo das suas necessidades:  
  
- Use o mecanismo de persistência de fontes e cores para recuperar o estado atual ou armazenado. Para obter mais informações, consulte [acessar fonte armazenados e as configurações de cor](../extensibility/accessing-stored-font-and-color-settings.md).  
  
- Use o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider> interface de um serviço que fornece dados de fontes e cores para obter uma instância de <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>, se o VSPackage não é também o provedor de fonte e cor.  
  
- Implementar a interface <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents>.  
  
  Para garantir que os resultados obtidos por meio de sondagem são atualizadas, talvez seja útil usar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> interface para determinar se uma atualização é necessária antes de chamar os métodos de recuperação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> interface.  
  
  Depois que você obteve informações de fonte e cor, analisar o texto a ser exibido para identificar a necessidade de colorização de elementos e, em seguida, exibir o texto na janela usando as cores e fontes apropriadas.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>   
 [Usando fontes e texto](http://msdn.microsoft.com/library/d43640f3-da94-4df2-a29d-a9d021a1c069)   
 [Trabalhando com cor](http://msdn.microsoft.com/library/d34ff96f-241d-494f-abdd-13811ada8cd3)   
 [GDI (interface gráfica de dispositivo)](http://msdn.microsoft.com/en-us/7e1d4540-bb2e-4257-8eee-eee376acba83)

