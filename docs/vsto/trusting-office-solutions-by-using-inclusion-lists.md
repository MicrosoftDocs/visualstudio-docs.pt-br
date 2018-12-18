---
title: Confiar em soluções do Office usando listas de inclusão
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio]
- inclusion lists [Office development in Visual Studio], about inclusion lists
- security [Office development in Visual Studio], inclusion lists
- inclusion lists [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9e2fea115b941af4b119b59dade16114cab3383d
ms.sourcegitcommit: c57ae28181ffe14a30731736661bf59c3eff1211
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38783695"
---
# <a name="trust-office-solutions-by-using-inclusion-lists"></a>Confiar em soluções do Office usando listas de inclusão
  Listas de inclusão habilitar usuários para conceder confiança a soluções do Office que são assinados com um certificado que identifica o Editor. Listas de inclusão são específicas do usuário, e eles podem ser usados para personalizações no nível de documento e suplementos do VSTO.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
 Quando um usuário inicia uma solução do Office que não tenha sido concedida a relação de confiança para que o usuário, a solução do Microsoft Office solicitará que ele ou ela para uma decisão de segurança com um [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] prompt confiável. Se o usuário decide confiar a solução, as execuções de personalização e o usuário não é solicitado na próxima vez.  
  
## <a name="inclusion-list-and-windows-installer"></a>Lista de inclusão e do Windows Installer  
 Instalação de soluções do Office para o *arquivos de programas* directory usando o Windows Installer requer direitos de administrador. Para soluções do Office na *arquivos de programas* diretório, o Visual Studio Tools for Office runtime não verifica a lista de inclusão porque as soluções do Office já foi concedidas permissão FullTrust.  
  
## <a name="clickonce-trust-prompt"></a>Solicitação de confiança do ClickOnce  
 Usando o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] implementação para soluções do Office, os administradores pode configurar o nível de confiança de prompt para permitir a solicitar, desabilitar solicitando que ou exigem um certificado confiável. Essa configuração é feita usando uma chave do registro que controla o acesso à lista de inclusão.  
  
 Se Avisar estiver desabilitada, apenas as soluções que têm um certificado confiável e conhecido podem ser instaladas. Se o nível de solicitação é definido como Authenticode necessária, a solução deve ser assinada com um certificado de uma autoridade conhecido, mas ele não requer um certificado que se encadeie a uma autoridade raiz confiável (um certificado confiável). Se o prompt é permitido, a solução poderia ser assinada com um certificado com uma identidade desconhecido. Nesse cenário, a decisão de confiança é adiada para o usuário final e um certificado temporário seria suficiente para instalar uma solução.  
  
 Para obter mais informações, consulte [como: configurar a segurança da lista de inclusões](../vsto/how-to-configure-inclusion-list-security.md) e a tabela 2, intitulada solicitando que nível de registro chave valor iniciar efeitos, na [editores confiáveis do ClickOnce configurar](http://go.microsoft.com/fwlink/?LinkId=94774).  
  
## <a name="structure-of-the-inclusion-list"></a>Estrutura da lista de inclusão  
 Uma entrada da lista de inclusão válido tem duas partes: um caminho para o manifesto de implantação e a chave pública usada para assinar a solução. Depois que uma solução é adicionada à lista de inclusão, ele é considerado confiável. Quando a solução do Office é executado, o aplicativo do Office compara a chave pública na lista de inclusão com a chave de assinatura no manifesto de implantação para verificar se a solução que está sendo executado é o mesmo que a versão original de confiável.  
  
## <a name="see-also"></a>Consulte também  
 [Conceder confiança a soluções do Office](../vsto/granting-trust-to-office-solutions.md)   
 [Proteger as soluções do Office](../vsto/securing-office-solutions.md)  
  
  