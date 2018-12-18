---
title: Como assinar manifestos de aplicativo e de implantação
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- manifests [Visual Studio]
- code signing [Visual Studio], Authenticode
- deployment manifests [Visual Studio]
- signing manifests [Visual Studio]
- application manifests [Visual Studio]
- ClickOnce deployment [Visual Studio], signing assemblies
- key files [Visual Studio]
- assemblies [Visual Studio], signing
ms.assetid: 64173505-8bfb-41cf-a0de-b9075173f3a2
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 903bc0df9b24cd6f944e9e92c6dc5283cd1d25ea
ms.sourcegitcommit: 495bba1d8029646653f99ad20df2f80faad8d58b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39381941"
---
# <a name="how-to-sign-application-and-deployment-manifests"></a>Como assinar manifestos de aplicativo e de implantação

Se você desejar publicar um aplicativo usando a implantação do ClickOnce, os manifestos do aplicativo e de implantação deverão ser assinados com um par de chaves pública/privada e assinados usando a tecnologia Authenticode. É possível assinar os manifestos usando um certificado do repositório de certificados do Windows ou um arquivo de chave.

 Para obter mais informações sobre a implantação do ClickOnce, consulte [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md).

 A assinatura dos manifestos do ClickOnce é opcional para aplicativos baseados em *.exe*. Para obter mais informações, consulte a seção “Gerar manifestos não assinados” deste documento.

 Para obter informações sobre como criar arquivos de chave, consulte [Como criar um par de chaves pública-privada](/dotnet/framework/app-domains/how-to-create-a-public-private-key-pair).

> [!NOTE]
> O [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] é compatível apenas com arquivos de chave de Troca de Informações Pessoais (PFX) que têm a extensão *.pfx*. No entanto, é possível selecionar outros tipos de certificados do repositório de certificados do Windows do usuário atual, clicando em **Selecionar do Repositório** na página **Assinatura** das propriedades do projeto.

## <a name="to-sign-application-and-deployment-manifests-using-a-certificate"></a>Para assinar os manifestos do aplicativo e de implantação usando um certificado

1.  Acesse a janela Propriedades do projeto (clique com o botão direito do mouse no nó do projeto no **Gerenciador de Soluções** e selecione **Propriedades**, digite **propriedades do projeto** na janela **Início Rápido** ou pressione **Alt**+**Enter** no **Gerenciador de Soluções**). Na guia **Assinatura**, selecione a caixa de seleção **Assinar os manifestos do ClickOnce**.

2.  Clique no botão **Selecionar do Repositório**.

     A caixa de diálogo **Selecionar um Certificado** é exibida e mostra o conteúdo do repositório de certificados do Windows.

    > [!TIP]
    > Se você clicar em **Clique aqui para exibir as propriedades do certificado**, a caixa de diálogo **Detalhes do Certificado** será exibida. Essa caixa de diálogo inclui informações detalhadas sobre o certificado, bem como outras opções. É possível clicar em **Certificados** para exibir informações adicionais de ajuda.

3.  Selecione o certificado que você deseja usar para assinar os manifestos.

4.  Além disso, é possível especificar o endereço de um servidor de carimbo de data/hora na caixa de texto **URL do servidor de carimbo de data/hora**. Esse é um servidor que fornece um carimbo de data/hora que especifica quando o manifesto foi assinado.

## <a name="to-sign-application-and-deployment-manifests-using-an-existing-key-file"></a>Para assinar os manifestos do aplicativo e de implantação usando um arquivo de chave existente

1.  Na página **Assinatura**, selecione a caixa de seleção **Assinar os manifestos do ClickOnce**.

2.  Clique no botão **Selecionar do Arquivo**.

     A caixa de diálogo **Selecionar Arquivo** é exibida.

3.  Na caixa de diálogo **Selecionar Arquivo**, procure o local do arquivo de chave (*.pfx*) que você deseja usar e clique no botão **Abrir**.

    > [!NOTE]
    > Essa opção é compatível apenas com os arquivos que têm a extensão *.pfx*. Se você tiver um arquivo de chave ou um certificado em outro formato, armazene-o no repositório de certificados do Windows e selecione o certificado que é descrito no procedimento anterior. A finalidade do certificado selecionado deve incluir a assinatura de código.

     A caixa de diálogo **Inserir senha para abrir o arquivo** é exibida. (Se o arquivo *.pfx* já estiver armazenado no repositório de certificados do Windows ou não for protegido por senha, você não precisará inserir uma senha.)

4.  Insira a senha para acessar o arquivo de chave e pressione **Enter**.

## <a name="to-sign-application-and-deployment-manifests-using-a-test-certificate"></a>Para assinar os manifestos do aplicativo e de implantação usando um certificado de teste

1.  Na página **Assinatura**, selecione a caixa de seleção **Assinar os manifestos do ClickOnce**.

2.  Para criar um novo certificado para teste, clique no botão **Criar Certificado de Teste**.

3.  Na caixa de diálogo **Criar Certificado de Teste**, insira uma senha para ajudar a proteger o certificado de teste.

## <a name="generate-unsigned-manifests"></a>Gerar manifestos não assinados

A assinatura dos manifestos do ClickOnce é opcional para aplicativos baseados em *.exe*. Os procedimentos a seguir mostram como gerar manifestos não assinados do ClickOnce.

> [!IMPORTANT]
> Manifestos não assinados podem simplificar o desenvolvimento e o teste do aplicativo. No entanto, os manifestos não assinados introduzem riscos de segurança significativos em um ambiente de produção. Apenas considere o uso de manifestos não assinados se o aplicativo ClickOnce for executado em computadores em uma intranet que está completamente isolada da Internet ou de outras fontes de código mal-intencionado.

 Por padrão, o ClickOnce gera manifestos assinados automaticamente, a menos que um ou mais arquivos sejam excluídos especificamente do hash gerado. Em outras palavras, a publicação do aplicativo resultará em manifestos assinados se todos os arquivos forem incluídos no hash, mesmo quando a caixa de seleção **Assinar os manifestos do ClickOnce** estiver desmarcada.

### <a name="to-generate-unsigned-manifests-and-include-all-files-in-the-generated-hash"></a>Para gerar manifestos não assinados e incluir todos os arquivos no hash gerado

1.  Para gerar manifestos não assinados que incluem todos os arquivos no hash, primeiro é necessário publicar o aplicativo junto com manifestos assinados. Portanto, primeiro assine os manifestos do ClickOnce seguindo um dos procedimentos anteriores e, em seguida, publique o aplicativo.

2.  Na página **Assinatura**, limpe a caixa de seleção **Assinar os manifestos do ClickOnce**.

3.  Redefina a versão de publicação para que apenas uma versão do aplicativo esteja disponível. Por padrão, o Visual Studio incrementa automaticamente o número de revisão da versão de publicação sempre que um aplicativo é publicado. Para obter mais informações, consulte [Como definir a versão de publicação do ClickOnce](../deployment/how-to-set-the-clickonce-publish-version.md).

4.  Publique o aplicativo.

### <a name="to-generate-unsigned-manifests-and-exclude-one-or-more-files-from-the-generated-hash"></a>Para gerar manifestos não assinados e excluir um ou mais arquivos do hash gerado

1.  Na página **Assinatura**, limpe a caixa de seleção **Assinar os manifestos do ClickOnce**.

2.  Abra a caixa de diálogo **Arquivos do Aplicativo** e defina o **Hash** como **Excluir** para os arquivos que você deseja excluir do hash gerado.

    > [!NOTE]
    > A exclusão de um arquivo do hash configura o ClickOnce para desabilitar a assinatura automática dos manifestos; portanto, você não precisa primeiro publicar com manifestos assinados, conforme mostrado no procedimento anterior.

3.  Publique o aplicativo.

## <a name="see-also"></a>Consulte também

- [Assemblies de nome forte](/dotnet/framework/app-domains/strong-named-assemblies)
- [Como criar um par de chaves pública/privada](/dotnet/framework/app-domains/how-to-create-a-public-private-key-pair)
- [Página de assinatura, Designer de Projeto](../ide/reference/signing-page-project-designer.md)
- [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md)