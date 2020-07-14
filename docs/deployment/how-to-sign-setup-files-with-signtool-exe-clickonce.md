---
title: Como assinar arquivos de instalação com SignTool.exe (ClickOnce) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, signtool.exe
- deploying applications [ClickOnce], re-signing setup.exe
- ClickOnce deployment, signtool.exe
- ClickOnce applications, re-signing setup.exe
- ClickOnce deployment, re-signing setup.exe
ms.assetid: 545a4005-d283-4110-9821-c78a9833c250
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f9e1911b6e86058b7f078f40fa10ca5e0e4e53c0
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382062"
---
# <a name="how-to-sign-setup-files-with-signtoolexe-clickonce"></a>Como assinar arquivos de instalação com SignTool.exe (ClickOnce)
Você pode usar *SignTool.exe* para assinar um programa de instalação (*setup.exe*). Esse processo ajuda a garantir que arquivos violados não sejam instalados nos computadores dos usuários finais.

 Por padrão, o ClickOnce tem manifestos e um programa de instalação assinados. No entanto, se você quiser alterar os parâmetros do programa de instalação mais tarde, assine o programa de instalação mais tarde. Se você alterar os parâmetros depois que o programa de instalação for assinado a assinatura é corrompida.

 O procedimento a seguir gera manifestos assinados e um programa de instalação não assinado. A assinatura do ClickOnce está habilitada no Visual Studio para gerar manifestos assinados. O programa de instalação é deixado sem assinatura para que o cliente possa assinar o executável com seu próprio certificado.

### <a name="to-generate-an-unsigned-setup-program-and-sign-later"></a>Para gerar um programa de instalação não assinado e assinar mais tarde

1. No computador de desenvolvimento, instale o certificado com qual você deseja assinar os manifestos.

2. Selecione o projeto no **Gerenciador de Soluções**.

3. No menu **Projeto**, clique em *ProjectName* **Propriedades**.

4. Na página **Assinatura**, desmarque a opção **Assinar os manifestos do ClickOnce**.

5. Na página **Publicar**, clique em **Pré-requisitos**.

6. Verifique se todos os pré-requisitos estão selecionados e clique em **OK**.

7. Na página **Publicar**, verifique as configurações de publicação e clique em **Publicar Agora**.

     A solução publica o manifesto de aplicativo não assinado, o manifesto de implantação não assinado, os arquivos específicos de versão e o programa de instalação não assinado no local da pasta de publicação.

8. Na página **Publicar**, clique em **Pré-requisitos**.

9. Na caixa de diálogo **Pré-requisitos**, desmarque a opção **Criar programa de instalação para instalar os componentes dos pré-requisitos**.

10. Na página **Publicar**, verifique as configurações de publicação e clique em **Publicar Agora**.

     A solução publica o manifesto de aplicativo assinado, o manifesto de implantação assinado, os arquivos específicos de versão e o local da pasta de publicação. O programa de instalação não assinado não é substituído pelo processo de publicação.

11. No site do cliente, abra um prompt de comando.

12. Mude para o diretório que contém o arquivo *.exe*.

13. Assine o arquivo *.exe* com o seguinte comando:

    ```cmd
    signtool sign /sha1 CertificateHash Setup.exe
    signtool sign /f CertFileName Setup.exe
    ```

     Por exemplo, para assinar o programa de instalação, use um dos seguintes comandos:

    ```cmd
    signtool sign /sha1 CCB... Setup.exe
    signtool sign /f CertFileName Setup.exe
    ```

## <a name="see-also"></a>Veja também
- [Como reassinar manifestos do aplicativo e de implantação](../deployment/how-to-re-sign-application-and-deployment-manifests.md)
