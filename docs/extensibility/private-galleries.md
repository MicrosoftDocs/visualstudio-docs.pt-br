---
title: Galerias privadas | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSIX galleries, private
- private galleries, VSIX
ms.assetid: b6b3dee7-91c5-4556-9f69-0d56b675e83b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e91b3ecec969ab6a717598d8dfb77e674890216a
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39638577"
---
# <a name="private-galleries"></a>Galerias privadas
Você pode compartilhar os controles, modelos e ferramentas que você desenvolve postando-as para um *Galeria privada* na intranet de sua organização, da seguinte maneira:  
  
-   Crie um Atom (RSS) para um local central (repositório) adequadamente configurado na sua intranet. Para obter mais informações, consulte [como: criar um feed Atom para uma galeria privada](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md).  
  
-   Distribuir uma *pkgdef* arquivo que descreve a Galeria privada. Recomendamos essa configuração para os administradores que desejam se conectar a uma galeria privada em vários computadores ao mesmo tempo.  
  
## <a name="add-a-private-gallery-to-extensions-and-updates-in-visual-studio"></a>Adicionar uma galeria privada para extensões e atualizações no Visual Studio  
 Quando uma galeria privada está disponível, você pode adicioná-lo para **extensões e atualizações** no Visual Studio.  
  
 ![Caixa de diálogo de adicionar Gerenciador de extensões](../extensibility/media/em_adddialog.png "EM_AddDialog")  
  
### <a name="to-add-a-private-gallery-to-extensions-and-updates"></a>Para adicionar uma galeria privada para extensões e atualizações  
  
1.  Na barra de menus, escolha **Ferramentas** > **Opções**.  
  
2.  No **ambiente** nó, selecione **extensões e atualizações**.  
  
3.  Escolha o botão **Adicionar**.  
  
4.  No **nome** , insira um nome para a Galeria privada, por exemplo, `My Gallery`.  
  
5.  No **URL** , insira a URL do feed Atom ou site do SharePoint que está hospedando a Galeria privada.  
  
    1.  Se o host é um feed Atom que se conecta à Galeria privada, a URL seria semelhante a este: http://www.mywebsite/mygallery/atom.xml.  Essa URL pode se referir a um arquivo ou um caminho de rede.  
  
    2.  Se o host for um site do SharePoint, a URL seria semelhante a este: http://mysharepoint/sites/mygallery/forms/AllItems.aspx.  
  
### <a name="manage-private-galleries"></a>Gerenciar galerias privadas  
 Um administrador pode disponibilizar uma galeria privada em vários computadores ao mesmo tempo, modificando o registro do sistema em cada computador. Para fazer isso, crie uma *pkgdef* arquivo que descreve as novas chaves de registro e seus valores.  O formato desse arquivo é da seguinte maneira.  
  
```  
[$RootKey$\ExtensionManager\Repositories\{UniqueGUID}]  
@={URI}  (REG_SZ)  
Disabled=0 | 1 (DWORD)  
Priority=0 (highest priority) ... MaxInt (lowest priority) (DWORD) (uint)  
Protocol=Atom|Sharepoint (REG_SZ)  
DisplayName={DisplayName} (REG_SZ)  
DisplayNameResourceID={ID} (REG_SZ)  
DisplayNamePackageGuid={GUID} (REG_SZ)  
  
```  
  
 Para obter mais informações, consulte [como: gerenciar uma galeria privada usando configurações de registro](../extensibility/how-to-manage-a-private-gallery-by-using-registry-settings.md).  
  
## <a name="install-extensions-from-a-private-gallery"></a>Instalar as extensões de uma galeria privada  
 Você pode procurar e instalar extensões do Visual Studio de uma galeria privada em **extensões e atualizações**. As etapas a seguir usam uma galeria privada chamada `My Gallery`.  
  
 ![Gerenciador de extensões instalando Galeria privada](../extensibility/media/em_.png "EM_")  
  
### <a name="to-search-for-and-install-extensions-from-a-private-gallery"></a>Para procurar e instalar as extensões de uma galeria privada  
  
1.  Na barra de menus, escolha **ferramentas** > **extensões e atualizações**.  
  
2.  No painel esquerdo, selecione **extensões Online**e, em seguida, selecione **minha galeria**.  
  
3.  No painel direito, selecione uma extensão e, em seguida, escolha o **baixar** botão.  
  
## <a name="update-extensions-from-a-private-gallery"></a>Atualizar extensões de uma galeria privada  
 Conforme novas versões de extensões do Visual Studio são lançadas na Galeria privada, você pode atualizar as extensões que você instalou. As etapas a seguir usam uma galeria privada chamada `My Repository`.  
  
 ![Atualização de galeria privada do Gerenciador de extensão](../extensibility/media/em_update.png "EM_Update")  
  
### <a name="to-update-an-installed-extension-from-a-private-gallery"></a>Para atualizar uma extensão instalada de uma galeria privada  
  
1.  Na barra de menus, escolha **ferramentas** > **extensões e atualizações**.  
  
2.  No painel esquerdo, selecione **atualizações**e, em seguida, selecione **meu repositório**.  
  
3.  No painel direito, selecione uma extensão e, em seguida, escolha o **atualização** botão.  
  
## <a name="see-also"></a>Consulte também  
 [Localizar e usar extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md)   
 [Enviar extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md)