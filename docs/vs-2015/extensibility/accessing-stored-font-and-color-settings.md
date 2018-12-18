---
title: Acessando configurações de cor e a fonte armazenada | Microsoft Docs
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
- fonts, accessing stored settings
- font and color control [Visual Studio SDK], persistence
- colors, accessing stored settings
ms.assetid: beba7174-e787-45c2-b6ff-a60f67ad4998
caps.latest.revision: 27
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: ee5ed57639127bd6c30d2e7e1373a56848eca504
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51772814"
---
# <a name="accessing-stored-font-and-color-settings"></a>Acessando configurações de cor e a fonte armazenada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE) armazena configurações modificadas para fontes e cores no registro. Você pode usar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> interface para acessar essas configurações.  
  
## <a name="to-initiate-state-persistence-of-fonts-and-colors"></a>Para iniciar a persistência de estado de fontes e cores  
 Informações de fonte e cor são armazenadas por categoria no seguinte local do registro: [HKCU\SOFTWARE\Microsoft \Visual Studio\\*\<versão do Visual Studio >* \FontAndColors\\  *\<CategoryGUID >*], onde  *\<CategoryGUID >* é a GUID da categoria.  
  
 Portanto, para iniciar a persistência, um VSPackage deve:  
  
-   Obter um <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> interface chamando `QueryService` contra o provedor de serviços globais.  
  
     `QueryService` deve ser chamado usando um argumento de ID de serviço do `SID_SVsFontAndColorStorage` e um argumento de ID de interface do `IID_IVsFontAndColorStorage`.  
  
-   Use o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.OpenCategory%2A> método para abrir uma categoria a ser mantido usando o GUID da categoria e um sinalizador de modo como argumentos.  
  
     O modo especificado pela `fFlags` argumento, é construído a partir de valores no <xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS> enumeração. Esse modo de controles:  
  
    -   As configurações que podem ser acessadas por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> interface.  
  
    -   Todas as configurações ou apenas aqueles que modificam os usuários e que são recuperáveis por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> interface.  
  
    -   A maneira de propagar as alterações às configurações do usuário.  
  
    -   O formato dos valores de cor que são usados.  
  
## <a name="to-use-state-persistence-of-fonts-and-colors"></a>A persistência de estado de uso de fontes e cores  
 Persistência de fontes e cores envolve:  
  
- Sincronizar as configurações de IDE com configurações armazenadas no registro.  
  
- Propagação de informações sobre a modificação do registro.  
  
- Configurando e recuperando as configurações armazenadas no registro.  
  
  Sincronizar a configuração de armazenamento com as configurações do IDE é totalmente transparente. O IDE subjacente gravará automaticamente as configurações atualizadas para **exibir itens** para as entradas do registro de categorias.  
  
  Se vários VSPackages compartilham uma categoria específica, um VSPackage deve exigir que os eventos são gerados quando os métodos do <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> interface são usadas para modificar as configurações do registro armazenado.  
  
  Por padrão, a geração de eventos não está habilitada. Para habilitar a geração de eventos, uma categoria deve ser aberta usando <xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS>. Isso faz com que o IDE chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents> método que implementa um VSPackage.  
  
> [!NOTE]
>  Modificações por meio de **fontes e cores** geram eventos independente da página de propriedades <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>. Você pode usar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> interface para determinar se uma atualização das configurações de fonte e cor armazenada em cache é necessária antes de chamar os métodos do <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> classe.  
  
### <a name="storing-and-retrieving-information"></a>Armazenar e recuperar informações  
 Para obter ou definir informações de que um usuário pode modificar para um item de exibição nomeada em uma categoria de abrir, VSPackages chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.SetItem%2A> métodos.  
  
 Atributos de informações sobre a fonte para uma determinada categoria é obtida usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.SetFont%2A> métodos.  
  
> [!NOTE]
>  O `fFlags` argumento que é passado para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.OpenCategory%2A> método quando essa categoria foi aberta define o comportamento da <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> e o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A> métodos. Por padrão, itemsthat de aboutdisplay de apenas retornar informações esses métodos foram alterados. No entanto, se uma categoria é aberta usando o <xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS> sinalizar, ambos atualizado e itens de exibição inalterado podem ser acessados pelo <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A>.  
  
 Por padrão, só alterado **exibir itens** informações são mantidas no registro. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> interface não pode ser usado para recuperar todas as configurações de fontes e cores.  
  
> [!NOTE]
>  O <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> e o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A> métodos retornam REGDB_E_KEYMISSING, (0x80040152L) quando você os usa para recuperar informações sobre inalterado **itens de exibição**.  
  
 As configurações de todos os **exibir itens** em uma determinada **categoria** pode ser obtida usando os métodos do `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults` interface.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS>   
 [Implementando categorias personalizadas e itens de exibição](../extensibility/implementing-custom-categories-and-display-items.md)

