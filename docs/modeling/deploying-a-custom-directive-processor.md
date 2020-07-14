---
title: Implantando um processador de diretiva personalizada
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- text templates, custom directive processors
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4762ad21f117bebe22ecfce1c846f15d154b1bf5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536013"
---
# <a name="deploying-a-custom-directive-processor"></a>Implantando um processador de diretiva personalizada

Para usar um processador de diretiva personalizado no Visual Studio em qualquer computador, você deve registrá-lo por um dos métodos descritos neste tópico.

Os métodos alternativos são:

- [Extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md). Isso fornece uma maneira de instalar e desinstalar o processador de diretriz em seu próprio computador e em outros computadores. Normalmente, você pode empacotar outros recursos na mesma VSIX.

- [VSPackage](../extensibility/internals/vspackages.md). Se você estiver for definir um VSPackage que contém outros recursos além do processador de diretriz, há um método conveniente para registrar o processador de diretriz.

- Definir uma chave do Registro. Nesse método, você adiciona uma entrada de Registro para o processador de diretriz.

Você precisará usar um desses métodos somente se quiser transformar seu modelo de texto no Visual Studio ou MSBuild. Se você usar um host personalizado em seu próprio aplicativo, seu host personalizado será responsável por localizar os processadores de diretrizes para cada diretiva.

## <a name="deploying-a-directive-processor-in-a-vsix"></a>Implantando um processador de diretriz em uma VSIX

Você pode adicionar um processador de diretriz personalizado a uma [extensão do Visual Studio (VSIX)](../extensibility/starting-to-develop-visual-studio-extensions.md).

 Você precisará certificar-se de que os dois seguintes itens estejam contidos no arquivo .vsix:

- O assembly (.dll) que contém a classe do processador de diretriz personalizado.

- Um arquivo .pkgdef que registra o processador de diretriz. O nome raiz do arquivo deve ser igual ao do assembly. Por exemplo, seus arquivos podem ser nomeados como CDP.dll e CDP.pkgdef.

Para inspecionar ou alterar o conteúdo de um arquivo .vsix, altere a extensão do seu nome de arquivo para .zip e abra-o. Depois de editar o conteúdo, altere o nome do arquivo de volta para .vsix.

Há várias maneiras de criar um arquivo .vsix. O procedimento a seguir descreve um método.

#### <a name="to-develop-a-custom-directive-processor-in-a-vsix-project"></a>Para desenvolver um processador de diretriz personalizado em um projeto VSIX

1. Crie um novo projeto de **projeto VSIX** .

2. Em **Source. Extension. vsixmanifest**, defina o tipo de conteúdo e as edições com suporte.

    1. No editor de manifesto do VSIX, na guia **ativos** , escolha **novo** e defina as propriedades do novo item:

         **Tipo**  =  de conteúdo **VSPackage**

         **Projeto de origem** = \<*the current project*>

    2. Clique em **edições selecionadas** e verifique os tipos de instalação nos quais você deseja que o processador de diretiva seja utilizável.

3. Adicione um arquivo .pkgdef e defina suas propriedades para ser incluídas no VSIX.

    1. Crie um arquivo de texto e nomeie-o \<*assemblyName*> . pkgdef.

         \<*assemblyName*>é geralmente o mesmo que o nome do projeto.

    2. Selecione-o no Gerenciador de Soluções e defina suas propriedades da seguinte maneira:

         **Ação**  =  de Build **Conteúdo** do

         **Copiar para diretório**  =  de saída **Copiar sempre**

         **Incluir no VSIX**  =  **Verdadeiro**

    3. Defina o nome da VSIX e verifique se a ID é exclusiva.

4. Adicione o seguinte texto ao arquivo .pkgdef.

    ```
    [$RootKey$\TextTemplating]
    [$RootKey$\TextTemplating\DirectiveProcessors]
    [$RootKey$\TextTemplating\DirectiveProcessors\ CustomDirectiveProcessorName]
    @="Custom Directive Processor description"
    "Class"="NamespaceName.ClassName"
    "CodeBase"="$PackageFolder$\AssemblyName.dll"
    ```

     Substitua os seguintes nomes pelos seus próprios nomes: `CustomDirectiveProcessorName`, `NamespaceName`, `ClassName`, `AssemblyName`.

5. Adicione as seguintes referências ao projeto:

    - **Microsoft. VisualStudio. TextTemplating. \* . 0**

    - **Microsoft. VisualStudio. TextTemplating. interfaces. \* . 0**

    - **Microsoft. VisualStudio. TextTemplating. VSHost. \* . 0**

6. Adicione sua classe de processador de diretriz personalizado ao projeto.

     Essa é uma classe pública que deve implementar <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> ou <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>.

#### <a name="to-install-the-custom-directive-processor"></a>Para instalar o Processador de Diretriz Personalizado

1. No Windows Explorer, abra o diretório de compilação (geralmente bin\Debug ou bin\Release).

2. Se você desejar instalar o processador de diretriz em outro computador, copie o arquivo .vsix para o outro computador.

3. Clique duas vezes no arquivo .vsix. O instalador de extensão do Visual Studio é exibido.

4. Reinicie o Visual Studio. Agora você poderá executar os modelos de texto que contêm diretivas que se referem ao processador de diretriz personalizado. Cada diretiva tem este formato:

     `<#@ CustomDirective Processor="CustomDirectiveProcessorName" parameter1="value1" ... #>`

#### <a name="to-uninstall-or-temporarily-disable-the-custom-directive-processor"></a>Para desinstalar ou desabilitar temporariamente o processador de diretriz personalizado

1. No menu **ferramentas** do Visual Studio, clique em **Gerenciador de extensões**.

2. Selecione o VSIX que contém o processador de diretiva e, em seguida, clique em **desinstalar** ou **desabilitar**.

### <a name="troubleshooting-a-directive-processor-in-a-vsix"></a>Solução de problemas de um processador de diretriz em uma VSIX
 Se o processador de diretriz não funcionar, as sugestões a seguir podem ajudar:

- O nome do processador que você especifica na diretiva personalizada deve corresponder ao `CustomDirectiveProcessorName` que você especificou no arquivo .pkgdef.

- O método `IsDirectiveSupported` deve retornar `true` quando o nome de seu `CustomDirective` é aprovado.

- Se você não conseguir ver a extensão no Gerenciador de extensões, mas o sistema não permitirá que você a instale, exclua a extensão de **%LocalAppData%\Microsoft\VisualStudio \\ \* 0 \ extensões \\ **.

- Abra o arquivo .vsix e inspecione seu conteúdo. Para abri-lo, altere a extensão do nome do arquivo para .zip. Verifique se contém os arquivos .dll, .pkgdef e extension.vsixmanifest. O arquivo extension.vsixmanifest deve conter a lista apropriada no nó SupportedProducts e deve conter também um nó VsPackage, sob o nó Conteúdo:

     `<Content>`

     `<VsPackage>CustomDirectiveProcessor.dll</VsPackage>`

     `</Content>`

## <a name="deploying-a-directive-processor-in-a-vspackage"></a>Implantando um processador de diretriz em um VSPackage
 Se o processador de diretriz fizer parte de um VSPackage que será instalado no GAC, é possível fazer com que o sistema gere o arquivo .pkgdef para você.

 Coloque o seguinte atributo na classe do pacote:

```csharp
[ProvideDirectiveProcessor(typeof(DirectiveProcessorClass), "DirectiveProcessorName", "Directive processor description.")]
```

> [!NOTE]
> Esse atributo é colocado na classe de pacote, e não na classe de processador de diretriz.

 O arquivo .pkgdef será gerado quando você compilar o projeto. Quando você instala o VSPackage, o arquivo .pkgdef registra o processador de diretriz.

 Verifique se o arquivo .pkgdef aparece na pasta de compilação, que é geralmente bin\Debug ou bin\Release. Se não for exibido, abra o arquivo .csproj em um editor de texto e remova o seguinte nó: `<GeneratePkgDefFile>false</GeneratePkgDefFile>`.

 Para obter mais informações, consulte [VSPackages](../extensibility/internals/vspackages.md).

## <a name="setting-a-registry-key"></a>Configuração de uma chave do Registro
 Esse método de instalação de um processador de diretriz personalizado é o menos preferido. Não fornece uma maneira conveniente de habilitar e desabilitar o processador de diretriz, e não fornece um método de distribuição do processador de diretriz para outros usuários.

> [!CAUTION]
> A edição incorreta do Registro pode danificar seriamente o sistema. Antes de alterar o Registro, faça o backup de todos os dados importantes no computador.

#### <a name="to-register-a-directive-processor-by-setting-a-registry-key"></a>Para registrar um processador de diretriz definindo uma chave do Registro

1. Execute `regedit`.

2. Em regedit, navegue até

    **HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\VisualStudio \\ \* . 0 \ TextTemplating\DirectiveProcessors**

    Se você quiser instalar o processador de diretiva na versão experimental do Visual Studio, insira "exp" após "11,0".

3. Adicione uma chave do Registro que tenha o mesmo nome da classe do processador de diretriz.

   - Na árvore do registro, clique com o botão direito do mouse no nó **DirectiveProcessors** , aponte para **novo**e clique em **chave**.

4. No novo nó, adicione valores de cadeia de caracteres para Class e CodeBase ou Assembly, de acordo com as tabelas a seguir.

   1. Clique com o botão direito do mouse no nó que você criou, aponte para **novo**e clique em **valor da cadeia de caracteres**.

   2. Edite o nome do valor.

   3. Clique duas vezes no nome e edite os dados.

   Se o processador de diretriz personalizado não estiver no GAC, as subchaves do Registro deverão se parecer como na tabela a seguir:

|Nome|Type|Dados|
|-|-|-|
|(Padrão)|REG_SZ|(valor não definido)|
|Classe|REG_SZ|**\<Namespace Name>.\<Class Name>**|
|CodeBase|REG_SZ|**\<Your Path>\\<o nome do assembly\>**|

 Se o assembly estiver no GAC, as subchaves do Registro deverão se parecer como na tabela a seguir:

|Nome|Type|Dados|
|-|-|-|
|(Padrão)|REG_SZ|(valor não definido)|
|Classe|REG_SZ|\<**Your Fully Qualified Class Name**>|
|Assembly|REG_SZ|\<**Your Assembly Name in the GAC**>|

## <a name="see-also"></a>Confira também

- [Criando processadores de diretiva de modelo de texto T4 personalizados](../modeling/creating-custom-t4-text-template-directive-processors.md)
