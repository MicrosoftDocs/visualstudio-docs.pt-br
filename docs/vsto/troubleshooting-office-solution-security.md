---
title: Solucionar problemas de segurança de solução do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], troubleshooting
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 002759a1a5fd8a16ee3e7842df7439d6e6b9755f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49862925"
---
# <a name="troubleshoot-office-solution-security"></a>Solucionar problemas de segurança de solução do Office
  Este tópico contém dicas para resolver problemas comuns que você pode encontrar ao trabalhar com Protegendo soluções do Office.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
## <a name="trusted-solutions-cannot-be-installed-from-restricted-sites"></a>Soluções confiáveis não podem ser instaladas de sites restritos  
 Os usuários não é possível instalar uma solução de um local da web se o site estiver listado na zona de sites restritos do Internet Explorer. Isso é verdadeiro mesmo se a solução é assinada com um certificado confiável.  
  
 A URL do manifesto de implantação pode ser categorizada em um dos cinco zonas:  
  
- Meu computador  
  
- Internet  
  
- Intranet local  
  
- Sites confiáveis  
  
- Sites restritos  
  
  Se o local do manifesto de implantação tiver sido atribuído à zona de sites restritos [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] não instala a solução. Se o local for conhecido e pode ser confiável, o usuário pode remover o local da zona de sites restritos e instalar a solução. Para obter informações sobre como gerenciar as zonas, consulte [Configurar editores confiáveis do ClickOnce](http://go.microsoft.com/fwlink/?LinkId=94774).  
  
## <a name="solutions-cannot-be-installed-from-network-file-shares-or-web-locations-when-internet-explorer-enhanced-security-configuration-or-internet-explorer-7-is-installed"></a>Soluções não podem ser instaladas de compartilhamentos de arquivos de rede ou locais da web quando a configuração de segurança reforçada do Internet Explorer ou Internet Explorer 7 é instalado  
 Internet Explorer Enhanced Security Configuration (IEESC) no Windows Server 2003 e superior e o Internet Explorer 7 e superior, restringe consideravelmente a capacidade dos usuários para navegar pela Internet. Quando os usuários tentarem instalar soluções do Office a partir de um local da web ou de compartilhamento do arquivo de rede, eles podem receber a seguinte mensagem de erro: "a funcionalidade personalizada neste aplicativo não funcionará porque o certificado usado para assinar o manifesto de implantação *SolutionName* não é confiável. Entre em contato com seu administrador para obter mais assistência."  
  
 Com IEESC e o Internet Explorer 7 e posterior, se a URL do manifesto de implantação está categorizada na zona da Internet, o manifesto deve ter um certificado de um fornecedor confiável ou a solução não pode ser instalada. Sem IEESC, o comportamento padrão é solicitar ao usuário final para tomar uma decisão de confiança.  
  
 Para gerenciar o efeito de IEESC e Internet Explorer 7 e superior, identificar sites e universal de nomenclatura de caminhos UNC (convenção) que você confia e adicioná-los para uma das zonas de segurança confiável (intranet Local ou sites confiáveis). Para obter informações sobre como gerenciar as zonas, consulte [editores confiáveis do ClickOnce configurar](http://go.microsoft.com/fwlink/?LinkId=94774).  
  
## <a name="see-also"></a>Consulte também  
 [Proteger as soluções do Office](../vsto/securing-office-solutions.md)  
  
  