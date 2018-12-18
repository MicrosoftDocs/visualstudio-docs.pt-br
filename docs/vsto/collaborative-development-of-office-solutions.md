---
title: Colaboração de desenvolvimento de soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], collaborative development
- Office development in Visual Studio, collaboration
- source control [Office development in Visual Studio]
- collaborative development [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9bf85dd1ba39df35e337f1b6b80099e3d5bcd774
ms.sourcegitcommit: 209c2c068ff0975994ed892b62aa9b834a7f6077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34267770"
---
# <a name="collaborative-development-of-office-solutions"></a>Colaboração de desenvolvimento de soluções do Office
  Vários desenvolvedores podem trabalhar em um projeto do Office, da mesma forma que eles colaboram em outros projetos do Visual Studio. O Visual Studio corretamente localiza a instalação do Microsoft Office em cada computador, mesmo se o Office é instalado em locais diferentes. No entanto, há algumas considerações importantes a serem consideradas.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
## <a name="debug-properties-are-not-shared"></a>Depurar propriedades não são compartilhadas  
 Depurar propriedades não são compartilhadas entre vários usuários sob controle de origem. Projetos Visual Basic e Visual c# armazenam propriedades de depuração em um arquivo específico do usuário (*ProjectName*. vbproj.user ou *ProjectName*. csproj.user), e esse arquivo não está sob controle de origem. Se a depuração de mais de uma pessoa, cada pessoa deve inserir propriedades de depuração manualmente.  
  
 Se o projeto está hospedado em um compartilhamento de rede em vez de no controle do código-fonte, algumas etapas adicionais devem ser executadas para habilitar os desenvolvedores de colaboração para abrir a solução e o assembly de teste.  
  
## <a name="source-control-requires-checking-out-all-files"></a>Controle de origem requer o check-out de todos os arquivos  
 Se você usar o controle de origem para seus projetos, você deve verificar todos os arquivos em um arquivo de código em **Solution Explorer** (como o *ThisDocument*, *ThisWorkbook*, ou *ThisAddIn* arquivos de código) sempre que você alterar o arquivo de código, até mesmo os arquivos que são ocultos por padrão. Se você verificar somente o arquivo de código de nível superior, as alterações podem ser perdidas.  
  
 Depois de fazer suas alterações, verifique todos os arquivos novamente. Para obter mais informações sobre arquivos de código oculto em projetos, consulte [projetos do Office no ambiente do Visual Studio](../vsto/office-projects-in-the-visual-studio-environment.md).  
  
## <a name="security-for-informal-collaboration-on-a-network"></a>Segurança para colaboração informal em uma rede  
 Todas as soluções de nível de documento que estão em um local de rede (como \\ \\ *Servername*\\*Sharename*), o local totalmente qualificado deve ser adicionado ao a lista de pasta confiável no aplicativo do Microsoft Office que você está trabalhando. Selecione a opção para incluir as subpastas da pasta principal, ou especificamente adicione debug e criar pastas à lista de pastas confiáveis. Para obter mais informações sobre como fazer isso, consulte [conceder confiança a documentos](../vsto/granting-trust-to-documents.md).  
  
 Os certificados temporários que são gerados automaticamente em tempo de compilação não estão protegidos por senhas. Os certificados contêm o nome de logon do desenvolvedor e outras informações pessoais. Se você implantar as personalizações que foram assinadas por certificados temporários, outros usuários poderá acessar essas informações.  
  
## <a name="see-also"></a>Consulte também  
 [Proteger as soluções do Office](../vsto/securing-office-solutions.md)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)   
 [Criar soluções do Office](../vsto/building-office-solutions.md)  
  
  