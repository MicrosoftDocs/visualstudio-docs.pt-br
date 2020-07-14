---
title: Implantação de uma DSL por MSI e VSIX
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6d4de8d7560cb43115a30e29516e0e88b4d02d21
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542610"
---
# <a name="msi-and-vsix-deployment-of-a-dsl"></a>Implantação de uma DSL por MSI e VSIX
Você pode instalar uma linguagem específica de domínio em seu próprio computador ou em outros computadores. O Visual Studio já deve estar instalado no computador de destino.

## <a name="choosing-between-vsix-and-msi-deployment"></a><a name="which"></a>Escolhendo entre a implantação do VSIX e do MSI
 Há dois métodos de implantação de uma linguagem específica de domínio:

|Método|Benefícios|
|-|-|
|VSX (extensão do Visual Studio)|Muito fácil de implantar: Copie e execute o arquivo **. vsix** do projeto DslPackage.<br /><br /> Para obter mais informações [, consulte Instalando e desinstalando uma DSL usando o VSX](#Installing).|
|MSI (arquivo do instalador)|– Permite que o usuário abra o Visual Studio clicando duas vezes em um arquivo DSL.<br />-Associa um ícone ao tipo de arquivo DSL no computador de destino.<br />-Associa um XSD (esquema XML) ao tipo de arquivo DSL. Isso evita avisos quando o arquivo é carregado no Visual Studio.<br /><br /> Você deve adicionar um projeto de instalação à sua solução para criar um MSI.<br /><br /> Para obter mais informações, consulte [implantando uma DSL usando um arquivo MSI](#msi).|

## <a name="install-and-uninstall-a-dsl-by-using-the-vsx"></a><a name="Installing"></a>Instalar e desinstalar uma DSL usando o VSX

Quando o DSL é instalado por esse método, o usuário pode abrir um arquivo DSL no Visual Studio, mas o arquivo não pode ser aberto no Windows Explorer.

### <a name="to-install-a-dsl-by-using-the-vsx"></a>Para instalar uma DSL usando o VSX

1. Localize o arquivo **. vsix** criado por seu projeto de pacote DSL:

   1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **DslPackage** e clique em **abrir pasta no explorador de arquivos**.

   2. Localize o arquivo **bin \\ \* \\ **_seuprojeto_**. DslPackage. vsix**

2. Copie o arquivo **. vsix** para o computador de destino no qual você deseja instalar a DSL. Este pode ser seu próprio computador ou outro.

   - O computador de destino deve ter uma das edições do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] que dá suporte a DSLs em tempo de execução. Para obter mais informações, consulte [supported Visual Studio Editions for visualization & Modeling SDK](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md).

   - O computador de destino deve ter uma das edições do Visual Studio especificadas em **DslPackage\source.Extensions.manifest**.

3. No computador de destino, clique duas vezes no arquivo **. vsix** .

    O **instalador de extensão do Visual Studio** é aberto e instala a extensão.

4. Iniciar ou reiniciar [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] .

5. Para testar a DSL, use o Visual Studio para criar um novo arquivo com a extensão que você definiu para a sua DSL.

### <a name="to-uninstall-a-dsl-that-was-installed-by-using-vsx"></a>Para desinstalar uma DSL que foi instalada usando o VSX

1. No menu **Ferramentas**, escolha **Extensões e Atualizações**.

2. Expanda **extensões instaladas**.

3. Selecione a extensão na qual a DSL está definida e clique em **desinstalar**.

   Raramente, uma extensão defeituosa não carrega e cria um relatório na janela de erro, mas não aparece no Gerenciador de extensões. Nesse caso, você pode remover a extensão excluindo o arquivo de:

   *LocalAppData* **\Microsoft\VisualStudio\10.0\Extensions**

## <a name="deploying-a-dsl-in-an-msi"></a><a name="msi"></a>Implantando uma DSL em um MSI
 Ao definir um arquivo MSI (Windows Installer) para sua DSL, você pode permitir que os usuários abram arquivos DSL no Windows Explorer. Você também pode associar um ícone e uma breve descrição à sua extensão de nome de arquivo. Além disso, o MSI pode instalar um XSD que pode ser usado para validar arquivos DSL. Se desejar, você pode adicionar outros componentes ao MSI que serão instalados ao mesmo tempo.

 Para obter mais informações sobre arquivos MSI e outras opções de implantação, consulte [Implantando aplicativos, serviços e componentes](../deployment/deploying-applications-services-and-components.md).

 Para criar um MSI, você adiciona um projeto de instalação à sua solução do Visual Studio. O método mais fácil de criar um projeto de instalação é usar o modelo CreateMsiSetupProject.tt, que pode ser baixado do [site do VMSDK](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db).

### <a name="to-deploy-a-dsl-in-an-msi"></a>Para implantar uma DSL em um MSI

1. Defina `InstalledByMsi` no manifesto de extensão. Isso impede que o VSX seja instalado e desinstalado, exceto pelo MSI. Isso será importante se você incluir outros componentes no MSI.

   1. Abrir DslPackage\source.extension.tt

   2. Insira a seguinte linha antes de `<SupportedProducts>` :

       ```xml
       <InstalledByMsi>true</InstalledByMsi>
       ```

2. Crie ou edite um ícone que representará sua DSL no Windows Explorer. Por exemplo, edite **DslPackage\Resources\File.ico**

3. Verifique se os seguintes atributos de sua DSL estão corretos:

   - No Gerenciador de DSL, clique no nó raiz e, em janela Propriedades, examine:

       - Descrição

       - Versão

   - Clique no nó do **Editor** e, na janela Propriedades, clique em **ícone**. Defina o valor para fazer referência a um arquivo de ícone em **DslPackage\Resources**, como **File. ico**

   - No menu **Compilar** , abra **Configuration Manager**e selecione a configuração que você deseja compilar, como **liberar** ou **depurar**.

4. Acesse o [SDK de visualização e modelagem Home Page](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)e, na guia **Downloads** , baixe **CreateMsiSetupProject.tt**.

5. Adicione **CreateMsiSetupProject.tt** ao seu projeto DSL.

    O Visual Studio criará um arquivo chamado **CreateMsiSetupProject. vdproj**.

6. No Windows Explorer, copie DSL \\ *. vdproj para uma nova pasta chamada setup.

    (Se desejar, agora você pode excluir CreateMsiSetupProject.tt de seu projeto DSL.)

7. Em **Gerenciador de soluções**, adicione **Setup \\ \* . vdproj** como um projeto existente.

8. No menu **projeto** , clique em **dependências do projeto**.

    Na caixa de diálogo **dependências do projeto** , selecione o projeto de instalação.

    Selecione a caixa ao lado de **DslPackage**.

9. Recriar a solução.

10. No Windows Explorer, localize o arquivo MSI compilado em seu projeto de instalação.

     Copie o arquivo MSI em um computador no qual você deseja instalar o DSL. Clique duas vezes no arquivo MSI. O instalador é executado.

11. No computador de destino, crie um novo arquivo que tenha a extensão de arquivo de sua DSL. Verifique se:

    - No modo de exibição de lista do Windows Explorer, o arquivo aparece com o ícone e a descrição que você definiu.

    - Quando você clica duas vezes no arquivo, o Visual Studio é iniciado e abre o arquivo DSL em seu editor DSL.

    Se preferir, você pode criar o projeto de instalação manualmente, em vez de usar o modelo de texto. Para obter uma explicação que inclui esse procedimento, consulte o capítulo 5 do [laboratório de visualização e do SDK de modelagem](https://code.msdn.microsoft.com/DSLToolsLab/Release/ProjectReleases.aspx?ReleaseId=4207).

### <a name="to-uninstall-a-dsl-that-was-installed-from-an-msi"></a>Para desinstalar uma DSL que foi instalada a partir de um MSI

1. No Windows, abra o painel de controle **programas e recursos** .

2. Desinstale a DSL.

3. Reinicie o Visual Studio.
