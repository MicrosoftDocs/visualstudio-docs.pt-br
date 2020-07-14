---
title: Como usar assistentes com modelos do projeto
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- project templates [Visual Studio], wizards
- Visual Studio templates, wizards
- wizards [Visual Studio], project templates
- templates [Visual Studio], wizards
- IWizard interface
ms.assetid: 47ee26cf-67b7-4ff1-8a9d-ab11a725405c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e9d36ae9b3a4a4fbbb3c54cc3f3320e9878b6745
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905522"
---
# <a name="how-to-use-wizards-with-project-templates"></a>Como: usar assistentes com modelos de projeto

O Visual Studio fornece a <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface que, quando implementada, permite que você execute código personalizado quando um usuário cria um projeto a partir de um modelo.

A personalização do modelo de projeto pode ser usada para exibir a interface do usuário personalizada que coleta a entrada do cliente para personalizar o modelo, adicionar arquivos adicionais ao modelo ou qualquer outra ação permitida em um projeto.

Os <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> métodos de interface são chamados em vários momentos enquanto o projeto está sendo criado, iniciando assim que um usuário clica em **OK** na caixa de diálogo **novo projeto** . Cada método da interface é nomeado para descrever o ponto em que é chamado. Por exemplo, o Visual Studio chama <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> imediatamente quando começa a criar o projeto, tornando-o um bom local para escrever código personalizado para coletar a entrada do usuário.

## <a name="create-a-project-template-project-with-a-vsix-project"></a>Criar um projeto de modelo de projeto com um projeto VSIX

Você começa a criar um modelo personalizado com o projeto de modelo de projeto, que faz parte do SDK do Visual Studio. Neste procedimento, usaremos um projeto de modelo de projeto C#, mas também há um projeto de modelo de projeto Visual Basic. Em seguida, você adiciona um projeto VSIX à solução que contém o projeto de modelo de projeto.

1. Crie um projeto de modelo de projeto C# (no Visual Studio, selecione **arquivo**  >  **novo**  >  **projeto** e pesquise "modelo de projeto"). Nomeie-o como **MyProjectTemplate**.

   > [!NOTE]
   > Você pode ser solicitado a instalar o SDK do Visual Studio. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

2. Adicione um novo projeto VSIX na mesma solução que o projeto de modelo de projeto (no **Gerenciador de soluções**, selecione o nó da solução, clique com o botão direito do mouse e selecione **Adicionar**  >  **novo projeto** e pesquise por "VSIX"). Nomeie-o como **MyProjectWizard.**

3. Defina o projeto VSIX como o projeto de inicialização. Em **Gerenciador de soluções**, selecione o nó do projeto VSIX, clique com o botão direito do mouse e selecione **definir como projeto de inicialização**.

4. Adicione o projeto de modelo como um ativo do projeto VSIX. No **Gerenciador de soluções**, no nó do projeto VSIX, localize o arquivo *Source. Extension. vsixmanifest* . Clique duas vezes nele para abri-lo no editor de manifesto.

5. No editor de manifesto, selecione a guia **ativos** no lado esquerdo da janela.

6. Na guia **ativos** , selecione **novo**. Na janela **Adicionar novo ativo** , para o campo tipo, selecione **Microsoft. VisualStudio. ProjectTemplate**. No campo **origem** , selecione **um projeto na solução atual**. No campo **projeto** , selecione **MyProjectTemplate**. Em seguida, clique em **OK**.

7. Compile a solução e inicie a depuração. Uma segunda instância do Visual Studio é exibida. (Isso pode levar alguns minutos).

8. Na segunda instância do Visual Studio, tente criar um novo projeto com o novo modelo (**arquivo**  >  **novo**  >  **projeto**, pesquise "MyProject"). O novo projeto deve aparecer com uma classe chamada **Class1**. Agora você criou um modelo de projeto personalizado! Pare a depuração agora.

## <a name="create-a-custom-template-wizard"></a>Criar um assistente de modelo personalizado

Este procedimento mostra como criar um assistente personalizado que abre um formulário do Windows antes de o projeto ser criado. O formulário permite que os usuários adicionem um valor de parâmetro personalizado que é adicionado ao código-fonte durante a criação do projeto.

1. Configure o projeto VSIX para permitir que ele crie um assembly.

2. Em **Gerenciador de soluções**, selecione o nó do projeto VSIX. Abaixo **Gerenciador de soluções**, você deverá ver a janela **Propriedades** . Se você não fizer isso, selecione **Exibir**  >  **Propriedades janela**ou pressione **F4**. Na janela **Propriedades** , selecione os seguintes campos para `true` :

   - **Incluir assembly no contêiner VSIX**

   - **Incluir símbolos de depuração no contêiner VSIX**

   - **Incluir símbolos de depuração na implantação do VSIX local**

3. Adicione o assembly como um ativo ao projeto VSIX. Abra o arquivo *Source. Extension. vsixmanifest* e selecione a guia **ativos** . Na janela **Adicionar novo ativo** , para **tipo** , selecione **Microsoft. VisualStudio. assembly**, para **origem** , selecione **um projeto na solução atual**e, para **projeto** , selecione **MyProjectWizard**.

4. Adicione as seguintes referências ao projeto VSIX. (No **Gerenciador de soluções**, no nó do projeto VSIX, selecione **referências**, clique com o botão direito do mouse e selecione **Adicionar referência**.) Na caixa de diálogo **Adicionar referência** , na guia **estrutura** , localize o assembly **System. Windows Forms** e selecione-o. Além disso, encontre e selecione os assemblies **sistema** e **sistema. Drawing** . Agora, selecione a guia **extensões** . Localize o assembly **EnvDTE** e selecione-o. Além disso, encontre o assembly **Microsoft. VisualStudio. TemplateWizardInterface** e selecione-o. Clique em **OK**.

5. Adicione uma classe para a implementação do assistente ao projeto VSIX. (Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto VSIX e selecione **Adicionar**, **novo item**e **classe**.) Nomeie a classe **WizardImplementation**.

6. Substitua o código no arquivo *WizardImplementationClass.cs* pelo código a seguir:

   ```csharp
   using System;
   using System.Collections.Generic;
   using Microsoft.VisualStudio.TemplateWizard;
   using System.Windows.Forms;
   using EnvDTE;

   namespace MyProjectWizard
   {
       public class WizardImplementation:IWizard
       {
           private UserInputForm inputForm;
           private string customMessage;

           // This method is called before opening any item that
           // has the OpenInEditor attribute.
           public void BeforeOpeningFile(ProjectItem projectItem)
           {
           }

           public void ProjectFinishedGenerating(Project project)
           {
           }

           // This method is only called for item templates,
           // not for project templates.
           public void ProjectItemFinishedGenerating(ProjectItem
               projectItem)
           {
           }

           // This method is called after the project is created.
           public void RunFinished()
           {
           }

           public void RunStarted(object automationObject,
               Dictionary<string, string> replacementsDictionary,
               WizardRunKind runKind, object[] customParams)
           {
               try
               {
                   // Display a form to the user. The form collects
                   // input for the custom message.
                   inputForm = new UserInputForm();
                   inputForm.ShowDialog();

                   customMessage = UserInputForm.CustomMessage;

                   // Add custom parameters.
                   replacementsDictionary.Add("$custommessage$",
                       customMessage);
               }
               catch (Exception ex)
               {
                   MessageBox.Show(ex.ToString());
               }
           }

           // This method is only called for item templates,
           // not for project templates.
           public bool ShouldAddProjectItem(string filePath)
           {
               return true;
           }
       }
   }
   ```

    O **UserInputForm** referenciado neste código será implementado posteriormente.

    A `WizardImplementation` classe contém implementações de método para cada membro de <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> . Neste exemplo, somente o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> método executa uma tarefa. Todos os outros métodos não fazem nada ou retornam `true` .

    O <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> método aceita quatro parâmetros:

   - Um <xref:System.Object> parâmetro que pode ser convertido no objeto raiz <xref:EnvDTE._DTE> , para permitir que você personalize o projeto.

   - Um <xref:System.Collections.Generic.Dictionary%602> parâmetro que contém uma coleção de todos os parâmetros predefinidos no modelo. Para obter mais informações sobre parâmetros de modelo, consulte [parâmetros de modelo](../ide/template-parameters.md).

   - Um <xref:Microsoft.VisualStudio.TemplateWizard.WizardRunKind> parâmetro que contém informações sobre o tipo de modelo que está sendo usado.

   - Uma <xref:System.Object> matriz que contém um conjunto de parâmetros passados para o assistente pelo Visual Studio.

     Este exemplo adiciona um valor de parâmetro do formulário de entrada do usuário para o <xref:System.Collections.Generic.Dictionary%602> parâmetro. Cada instância do `$custommessage$` parâmetro no projeto será substituída pelo texto inserido pelo usuário.

7. Agora, crie o **UserInputForm**. No arquivo *WizardImplementation.cs* , adicione o código a seguir após o final da `WizardImplementation` classe.

   ```csharp
   public partial class UserInputForm : Form
       {
           private static string customMessage;
           private TextBox textBox1;
           private Button button1;

           public UserInputForm()
           {
               this.Size = new System.Drawing.Size(155, 265);

               button1 = new Button();
               button1.Location = new System.Drawing.Point(90, 25);
               button1.Size = new System.Drawing.Size(50, 25);
               button1.Click += button1_Click;
               this.Controls.Add(button1);

               textBox1 = new TextBox();
               textBox1.Location = new System.Drawing.Point(10, 25);
               textBox1.Size = new System.Drawing.Size(70, 20);
               this.Controls.Add(textBox1);
           }
           public static string CustomMessage
           {
               get
               {
                   return customMessage;
               }
               set
               {
                   customMessage = value;
               }
           }
           private void button1_Click(object sender, EventArgs e)
           {
               customMessage = textBox1.Text;
               this.Close();
           }
       }
   ```

    O formulário entrada do usuário fornece um formulário simples para inserir um parâmetro personalizado. O formulário contém uma caixa de texto chamada `textBox1` e um botão chamado `button1` . Quando o botão é clicado, o texto da caixa de texto é armazenado no `customMessage` parâmetro.

## <a name="connect-the-wizard-to-the-custom-template"></a>Conectar o assistente ao modelo personalizado

Para que o modelo de projeto personalizado use seu assistente personalizado, você precisa assinar o assembly do assistente e adicionar algumas linhas ao seu modelo de projeto personalizado para que ele saiba onde encontrar a implementação do assistente quando um novo projeto é criado.

1. Assinar o assembly. No **Gerenciador de soluções**, selecione o projeto VSIX, clique com o botão direito do mouse e selecione **Propriedades do projeto**.

2. Na janela **Propriedades do projeto** , selecione a **guia assinatura** . na guia **assinatura** , marque **assinar o assembly**. No campo **escolher um arquivo de chave de nome forte** , selecione **\<New>** . Na janela **criar chave de nome forte** , no campo **nome do arquivo de chave** , digite **Key. SNK**. Desmarque o campo **proteger meu arquivo de chave com uma senha** .

3. Na **Gerenciador de soluções**, selecione o projeto VSIX e localize a janela **Propriedades** .

4. Defina o campo **copiar saída da compilação para diretório de saída** como **verdadeiro**. Isso permite que o assembly seja copiado no diretório de saída quando a solução é recriada. Ele ainda está contido no `.vsix` arquivo. Você precisa ver o assembly para descobrir sua chave de assinatura.

5. Recriar a solução.

6. Agora você pode encontrar o arquivo Key. SNK no diretório do projeto MyProjectWizard (* \<your disk location> \MyProjectTemplate\MyProjectWizard\key.SNK*). Copie o arquivo *Key. SNK* .

7. Vá para o diretório de saída e localize o assembly (* \<your disk location> \ MyProjectTemplate/MyProjectWizard\bin\Debug\MyProjectWizard.dll*). Cole o arquivo *Key. SNK* aqui. (Isso não é absolutamente necessário, mas vai facilitar as etapas a seguir).

8. Abra uma janela de comando e altere para o diretório no qual o assembly foi criado.

9. Localize a ferramenta de assinatura de *sn.exe* . Por exemplo, em um sistema operacional Windows de 10 64 bits, um caminho típico seria o seguinte:

     *C:\Arquivos de programas (x86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.6.1 Tools*

     Se você não encontrar a ferramenta, tente executar **onde/r. sn.exe** na janela de comando. Anote o caminho.

10. Extraia a chave pública do arquivo *Key. SNK* . Na janela de comando, digite

     **\<location of sn.exe>\sn.exe-p key. SNK outfile. Key.**

     Não se esqueça de colocar o caminho de *sn.exe* entre aspas se houver espaços nos nomes de diretório!

11. Obtenha o token de chave pública do outfile:

     **\<location of sn.exe>\sn.exe-t outfile. Key.**

     Novamente, não se esqueça das aspas. Você deverá ver uma linha na saída como esta

     **O token de chave pública é\<token>**

     Anote esse valor.

12. Adicione a referência ao assistente personalizado para o arquivo *. vstemplate* do modelo de projeto. Na **Gerenciador de soluções**, localize o arquivo chamado *MyProjectTemplate. vstemplate*e abra-o. Após o final da \<TemplateContent> seção, adicione a seguinte seção:

    ```xml
    <WizardExtension>
        <Assembly>MyProjectWizard, Version=1.0.0.0, Culture=Neutral, PublicKeyToken=token</Assembly>
        <FullClassName>MyProjectWizard.WizardImplementation</FullClassName>
    </WizardExtension>
    ```

     Em que **MyProjectWizard** é o nome do assembly e **token** é o token que você copiou na etapa anterior.

13. Salve todos os arquivos no projeto e recompile.

## <a name="add-the-custom-parameter-to-the-template"></a>Adicionar o parâmetro personalizado ao modelo

Neste exemplo, o projeto usado como o modelo exibe a mensagem especificada no formulário entrada do usuário do assistente personalizado.

1. Na **Gerenciador de soluções**, vá para o projeto **MyProjectTemplate** e abra *Class1.cs*.

2. No `Main` método do aplicativo, adicione a seguinte linha de código.

   ```csharp
   Console.WriteLine("$custommessage$");
   ```

    O parâmetro `$custommessage$` é substituído pelo texto inserido no formulário de entrada do usuário quando um projeto é criado a partir do modelo.

Este é o arquivo de código completo antes de ser exportado para um modelo.

```csharp
using System;
using System.Collections.Generic;
$if$ ($targetframeworkversion$ >= 3.5)using System.Linq;
$endif$using System.Text;

namespace $safeprojectname$
{
    public class Class1
    {
          static void Main(string[] args)
          {
               Console.WriteLine("$custommessage$");
          }
    }
}
```

## <a name="use-the-custom-wizard"></a>Usar o assistente personalizado

Agora você pode criar um projeto do seu modelo e usar o assistente personalizado.

1. Recompile a solução e inicie a depuração. Uma segunda instância do Visual Studio deve ser exibida.

2. Crie um novo projeto MyProjectTemplate. (**Arquivo**  >  **Novo**  >  **Projeto**).

3. Na caixa de diálogo **novo projeto** , pesquise "MyProject" para localizar o modelo, digite um nome e clique em **OK**.

     O formulário de entrada do usuário do assistente é aberto.

4. Digite um valor para o parâmetro personalizado e clique no botão.

     O formulário de entrada do usuário do assistente é fechado e um projeto é criado a partir do modelo.

5. Em **Gerenciador de soluções**, clique com o botão direito do mouse no arquivo de código-fonte e clique em **Exibir código**.

     Observe que foi `$custommessage$` substituído pelo texto inserido no formulário de entrada do usuário do assistente.

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.TemplateWizard.IWizard>
- [Personalizar modelos](../ide/customizing-project-and-item-templates.md)
- [Elemento WizardExtension (modelos do Visual Studio)](../extensibility/wizardextension-element-visual-studio-templates.md)
- [Pacotes NuGet em modelos do Visual Studio](/nuget/visual-studio-extensibility/visual-studio-templates)
