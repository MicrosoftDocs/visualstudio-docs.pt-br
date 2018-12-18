---
title: Página de Assinatura, Designer de Projeto
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.AddNewStrongNameKey
- ResolveKeySource.KeyFileForSignAssemblyNotImported
- vb.ProjectPropertiesSigning.ChangePasswordDialog
- ResolveKeySource.KeyFileForManifestNotImported
- vb.ProjectPropertiesSigning
- vb.ProjectPropertiesSigning.PasswordNeededDialog
- vb.ProjectPropertiesSigning.PfxPasswordDialog
helpviewer_keywords:
- Project Designer, Signing page
- Signing page in Project Designer
ms.assetid: dab3ba13-2f92-4827-92bd-1be3c35bc48b
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 859ec81ff3ed2c3b6385de1d093ba512203da9d9
ms.sourcegitcommit: 551f13774e8bb0eb47cbd973745628a956e866aa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49459784"
---
# <a name="signing-page-project-designer"></a>Página de Assinatura, Designer de Projeto
Use a página **Assinatura** do **Designer de Projeto** para assinar os manifestos do aplicativo e de implantação e também para assinar o assembly (assinatura de nome forte).

 Observe que a assinatura dos manifestos do aplicativo e de implantação é um processo diferente da assinatura de um assembly, embora ambas as tarefas sejam realizadas na página **Assinatura**.

 Além disso, o armazenamento de informações do arquivo de chave é diferente da assinatura do manifesto e assinatura do assembly. Para a assinatura do manifesto, as informações de chave são armazenadas no banco de dados de armazenamento criptografado do computador e no repositório de certificados do Windows do usuário atual. Para a assinatura do assembly, as informações de chave são armazenadas somente no banco de dados de armazenamento criptografado do computador.

 Para acessar a página **Assinatura**, selecione um nó do projeto no **Gerenciador de Soluções** e em seguida, no menu **Projeto**, clique em **Propriedades**. Quando o **Designer de Projeto** for exibido, clique na guia **Assinatura**.

## <a name="application-and-deployment-manifest-signing"></a>Assinatura de manifesto do aplicativo e de implantação
 Caixa de seleção **Assinar os manifestos do ClickOnce**

 Marque essa caixa de seleção para assinar os manifestos do aplicativo e de implantação com um par de chaves pública/privada. Para obter mais informações sobre como fazer isso, consulte [Como assinar manifestos do aplicativo e de implantação](../../ide/how-to-sign-application-and-deployment-manifests.md).

 Botão **Selecionar do Repositório**

 Permite selecionar um certificado existente do repositório de certificados pessoais do usuário atual. É possível selecionar um desses certificados para assinar os manifestos do aplicativo e de implantação.

 Ao clicar em **Selecionar do Repositório**, a caixa de diálogo **Selecionar um Certificado** é aberta, que lista os certificados do repositório de certificados pessoais que atualmente são válidos (não expirados) e que têm chaves privadas. A finalidade do certificado selecionado deve incluir a assinatura de código.

 Se você clicar em **exibir propriedades do certificado**, a caixa de diálogo **Detalhes do Certificado** será exibida. Essa caixa de diálogo inclui informações detalhadas sobre o certificado, bem como outras opções. É possível clicar em **Saber mais sobre certificados** para exibir informações adicionais da Ajuda.

 Botão **Selecionar do Arquivo**

 Permite selecionar um certificado de um arquivo de chave existente.

 Ao clicar em **Selecionar do Arquivo**, a caixa de diálogo **Selecionar Arquivo** é aberta, que permite selecionar um arquivo de chave do certificado (.pfx). O arquivo deve ser protegido por senha e não pode já estar localizado no repositório de certificados pessoais.

 Na caixa de diálogo **Inserir senha para abrir o arquivo**, insira uma senha para abrir o arquivo de chave do certificado (.pfx). As informações de senha são armazenadas na lista de contêineres de chaves pessoais e no repositório de certificados pessoais.

 Botão **Criar Certificado de Teste**

 Permite criar um certificado para teste. O certificado de teste é usado para assinar os manifestos do aplicativo e de implantação do ClickOnce.

 Ao clicar em **Criar Certificado de Teste**, a caixa de diálogo **Criar Certificado de Teste** é aberta, na qual é possível digitar uma senha para o arquivo de chave de nome forte para o certificado de teste. O arquivo é nomeado *projectname*_TemporaryKey.pfx. Se você clicar em **OK** sem digitar uma senha, o arquivo .pfx não será criptografado com senha.

 Caixa **URL do servidor de carimbo de data/hora**

 Especifica o endereço de um servidor que gera carimbos de data/hora da assinatura. Ao fornecer um certificado, esse site externo verifica a hora em que o aplicativo foi assinado.

## <a name="assembly-signing"></a>Assinatura de assembly
 Caixa de seleção **Assinar o assembly**

 Marque essa caixa de seleção para assinar o assembly e criar um arquivo de chave de nome forte. Para obter mais informações sobre como assinar um assembly usando o **Designer de Projeto**, consulte [Como assinar um assembly (Visual Studio)](../managing-assembly-and-manifest-signing.md#how-to-sign-an-assembly-in-visual-studio).

 Essa opção usa a ferramenta Al.exe fornecida pelo Software Development Kit do Windows (SDK do Windows) para assinar o assembly. Para obter mais informações sobre o Al.exe, consulte [Como assinar um assembly com um nome forte](/dotnet/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name).

 Lista **Escolher um arquivo de chave de nome forte**

 Permite especificar um arquivo de chave novo ou existente de nome forte que é usado para assinar o assembly. Selecione **\<Procurar...>** para selecionar um arquivo de chave existente.

 Selecione **\<Novo...>** para criar um novo arquivo de chave com o qual assinar o assembly. A caixa de diálogo **Criar Chave de Nome Forte** é exibida, que pode ser usada para especificar um nome de arquivo de chave e proteger o arquivo de chave com uma senha. A senha deve ter, no mínimo, 6 caracteres. Se você especificar uma senha, será criado um arquivo de Troca de Informações Pessoais (.pfx); caso contrário, será criado um arquivo de chave de nome forte (.snk).

 Botão **Alterar Senha**

 Altera a senha do arquivo de chave de Troca de Informações Pessoais (.pfx) usado para assinar o assembly.

 Ao clicar em **Alterar Senha**, a caixa de diálogo **Alterar Senha de Chave** é aberta. Na caixa de diálogo, **Senha antiga** é a senha atual do arquivo de chave. **Nova senha** deve ter, no mínimo, 6 caracteres. As informações de senha são armazenadas no repositório de certificados do Windows do usuário atual.

 Caixa de seleção **Somente sinal de atraso**

 Marque essa caixa de seleção para habilitar a assinatura com atraso.

 Observe que um projeto com assinatura com atraso não será executado e não pode ser depurado. No entanto, é possível usar [Sn.exe (Ferramenta de Nome Forte)](/dotnet/framework/tools/sn-exe-strong-name-tool) com a opção `-Vr` para ignorar a verificação durante o desenvolvimento.

> [!NOTE]
> Ao assinar um assembly, talvez você nem sempre tenha acesso a uma chave privada. Por exemplo, uma organização pode ter um par de chaves bem protegido ao qual os desenvolvedores não têm acesso todos os dias. A chave pública pode estar disponível, mas o acesso à chave privada é restrito a algumas pessoas. Nesse caso, é possível usar a *assinatura com atraso* ou *parcial* para fornecer a chave pública, adiando a adição da chave privada até a entrega do assembly.


## <a name="see-also"></a>Consulte também

- [Referência de Propriedades do Projeto](../../ide/reference/project-properties-reference.md)
- [Gerenciando Assinatura de Assembly e Manifesto](../../ide/managing-assembly-and-manifest-signing.md)
- [Como assinar manifestos de aplicativo e implantação](../../ide/how-to-sign-application-and-deployment-manifests.md)
- [Como Assinar um Assembly (Visual Studio)](../managing-assembly-and-manifest-signing.md#how-to-sign-an-assembly-in-visual-studio)
- [Como assinar um assembly com um nome forte](/dotnet/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name)
- [Assemblies de nomes fortes](/dotnet/framework/app-domains/strong-named-assemblies)