---
title: O VSPackage | Microsoft Docs
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
- registration, VSPackages
- VSPackages, registering
ms.assetid: ecd20da8-b04b-4141-a8f4-a2ef91dd597a
caps.latest.revision: 19
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 30da9208df8c5b9b7c3368ef10fc85e55a994baa
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51782007"
---
# <a name="vspackage-registration"></a>Registro do VSPackage
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Os VSPackages deverá avisar [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] se eles estão instalados e devem ser carregado. Esse processo é realizado gravando informações no registro. Esse é um trabalho típico de um instalador.  
  
> [!NOTE]
>  É uma prática aceita durante o desenvolvimento de VSPackage para usar o auto-registro. No entanto, [!INCLUDE[vsipprvsip](../../includes/vsipprvsip-md.md)] parceiros não é possível entregar seus produtos usando o auto-registro como parte da instalação.  
  
 Entradas do registro em um pacote do Windows Installer geralmente são feitas na tabela de registro. Você também pode registrar as extensões de arquivo na tabela de registro. No entanto, o Windows Installer fornece suporte interno por meio do identificador programático (ProgId), classe, extensão e tabelas do verbo. Para obter mais informações, consulte [tabelas de banco de dados](http://msdn.microsoft.com/library/aa368259\(VS.85\).aspx).  
  
 Certifique-se de que as entradas do registro estão associadas com o componente que é apropriado para sua estratégia de lado a lado escolhida. Por exemplo, entradas do registro para um arquivo compartilhado devem ser associadas com o componente do Windows Installer do arquivo. Da mesma forma, entradas do registro para um arquivo específico da versão devem ser associadas a componente desse arquivo. Caso contrário, instalar ou desinstalar o VSPackage para uma versão do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] poderia interromper o VSPackage em outras versões. Para obter mais informações, consulte [que dão suporte a várias versões do Visual Studio](../../extensibility/supporting-multiple-versions-of-visual-studio.md)  
  
> [!NOTE]
>  A maneira mais fácil de gerenciar o registro é usar os mesmos dados nos mesmos arquivos para o registro do desenvolvedor e o registro durante a instalação. Por exemplo, algumas ferramentas de desenvolvimento do instalador podem consumir o arquivo no formato. reg no momento da compilação. Se os desenvolvedores mantêm arquivos. reg para seu próprio desenvolvimento diário e depuração, esses mesmos arquivos podem ser incluídos no instalador automaticamente. Se você não pode compartilhar automaticamente dados de registro, você deve garantir que a cópia do instalador dos dados de registro é atual.  
  
## <a name="registering-unmanaged-vspackages"></a>Registrar VSPackages gerenciados  
 VSPackages gerenciados (incluindo aquelas geradas pelo modelo de pacote do Visual Studio) usar arquivos. rgs do estilo ATL para armazenar informações de registro. O formato de arquivo. rgs é específico para ATL e geralmente não pode ser consumido como-é uma ferramenta de criação de instalação. Informações de registro para o instalador de VSPackage devem ser mantidas separadamente. Por exemplo, os desenvolvedores podem manter arquivos no formato. reg em sincronia com. rgs alterações de arquivo. Os arquivos. reg podem ser mesclados com RegEdit para trabalhos de desenvolvimento ou consumidos através de um instalador.  
  
## <a name="registering-managed-vspackages"></a>Registrar VSPackages gerenciados  
 A ferramenta de RegPkg lê os atributos de registro de um VSPackage gerenciado e qualquer um pode gravar as informações diretamente para o registro ou arquivos de formato. reg de gravação podem ser consumidos por um instalador.  
  
> [!NOTE]
>  A ferramenta RegPkg não é redistribuível e não pode ser usada para registrar um VSPackage no sistema de um usuário.  
  
## <a name="why-vspackages-should-not-self-register-at-install-time"></a>Por que o VSPackages não deve registrar automaticamente no momento da instalação  
 Os VSPackage instaladores não devem depender de auto-registro. À primeira vista, manter os valores de registro de um VSPackage apenas o VSPackage em si parece ser uma boa ideia. Considerando que os desenvolvedores precisam os valores de registro disponíveis para seu trabalho de rotina e testes, faz sentido para evitar a manter uma cópia separada dos dados do registro no instalador. O instalador pode depender de VSPackage para gravar valores do registro.  
  
 Embora seja ideal, em teoria, o auto-registro tem várias falhas que o tornam inadequados para a instalação de VSPackage:  
  
-   Corretamente que dão suporte a instalação, desinstalação, reversão da instalação e reversão de desinstalação exige que você crie quatro ações personalizadas para cada VSPackage gerenciado que registra automaticamente chamando RegPkg.  
  
-   Sua abordagem para o suporte lado a lado pode exigir que você cria quatro ações personalizadas que invocam RegSvr32 ou RegPkg para todas as versões com suporte do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
-   Uma instalação com módulos automaticamente registrados não pode revertida com segurança porque não há nenhuma maneira de dizer se as chaves automaticamente registradas são usadas por outro recurso ou aplicativo.  
  
-   DLLs automaticamente registrados, às vezes, vincule a auxiliares DLLs que não estão presentes ou são a versão errada. Por outro lado, o Windows Installer pode registrar DLLs usando as tabelas de registro sem dependência no estado atual do sistema.  
  
-   Código de auto-registro pode ser negado acesso a recursos de rede, como bibliotecas de tipos, se um componente for especificado como executado a partir da origem tanto está listado na tabela SelfReg. Isso pode causar a instalação do componente falha durante uma instalação administrativa.  
  
## <a name="see-also"></a>Consulte também  
 [Windows Installer](http://msdn.microsoft.com/library/cc185688\(VS.85\).aspx)   
 [Registro de pacote gerenciado](http://msdn.microsoft.com/en-us/f69e0ea3-6a92-4639-8ca9-4c9c210e58a1)

