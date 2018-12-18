---
title: 'Como: usar assistentes com modelos de projeto | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- project templates [Visual Studio], wizards
- Visual Studio templates, wizards
- wizards [Visual Studio], project templates
- templates [Visual Studio], wizards
- IWizard interface
ms.assetid: 47ee26cf-67b7-4ff1-8a9d-ab11a725405c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 76bcd13fcee2f8b0bda775cc3ae241d7a363658e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49928426"
---
# <a name="how-to-use-wizards-with-project-templates"></a>Como: usar assistentes com modelos de projeto
O Visual Studio fornece o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> da interface que, quando implementada, permite que você execute o código personalizado quando um usuário cria um projeto de um modelo.  
  
 Personalização do modelo de projeto pode ser usada para exibir a interface do usuário personalizada que coleta a entrada do usuário para personalizar o modelo, adicione arquivos adicionais para o modelo, ou qualquer outra ação permitida em um projeto.  
  
 O <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> métodos de interface são chamados em vários momentos enquanto o projeto está sendo criado, iniciando assim que um usuário clica **Okey** sobre o **novo projeto** caixa de diálogo. Cada método da interface é denominado para descrever o ponto no qual ele é chamado. Por exemplo, o Visual Studio chama <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> imediatamente no início da criação do projeto, tornando-um bom local para escrever código personalizado para coletar entrada do usuário.  
  
## <a name="create-a-project-template-project-with-a-vsix-project"></a>Criar um projeto de modelo de projeto com um projeto VSIX  
 Começar a criar um modelo personalizado com o modelo de projeto project., que faz parte do SDK do Visual Studio. Neste procedimento, usaremos um projeto de modelo de projeto c#, mas também há um projeto de modelo de projeto do Visual Basic. Em seguida, você adicionar um projeto VSIX para a solução que contém o projeto de modelo de projeto.  
  
1. Criar um projeto de modelo de projeto c# (no Visual Studio, **arquivo** > **New** > **projeto** > **Visual c#**   >  **Extensibilidade** > **o modelo de projeto c#**). Denomine **MyProjectTemplate**.  
  
   > [!NOTE]
   >  Você pode ser solicitado a instalar o SDK do Visual Studio. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
2. Adicionar um novo projeto VSIX (**arquivo** > **New** > <strong>projeto > * * Visual C#</strong>   >  <strong>extensibilidade > * * Projeto VSIX</strong>) na mesma solução que o projeto de modelo de projeto (na **Gerenciador de soluções**, selecione o nó da solução, clique com botão direito e selecione **Add**  >  **Novo projeto**). Nomeie- **MyProjectWizard.**  
  
3. Defina o projeto VSIX como o projeto de inicialização. No **Gerenciador de soluções**, selecione o nó do projeto VSIX, clique com botão direito e selecione **definir como projeto de inicialização**.  
  
4. Adicione o projeto de modelo como um ativo do projeto VSIX. No **Gerenciador de soluções**, sob o nó de projeto do VSIX, localizar o *vsixmanifest* arquivo. Clique duas vezes nele para abri-lo no editor de manifesto.  
  
5. No editor de manifesto, selecione a **ativos** guia no lado esquerdo da janela.  
  
6. No **ativos** guia, selecione **New**. No **adicionar novo ativo** janela, para o campo de tipo, selecione **Microsoft.VisualStudio.ProjectTemplate**. No **fonte** campo, selecione **um projeto na solução atual**. No **Project** campo, selecione **MyProjectTemplate**. Clique em **OK**.  
  
7. Compile a solução e inicie a depuração. Uma segunda instância do Visual Studio é exibida. (Isso pode levar alguns minutos.)  
  
8. Na segunda instância do Visual Studio, tente criar um novo projeto com o novo modelo. (**Arquivo** > **nova** > **projeto > Visual c#** > **MyProject modelo**). O novo projeto deve aparecer com uma classe chamada **Class1**. Agora você criou um modelo de projeto personalizado! Pare a depuração agora.  
  
## <a name="create-a-custom-template-wizard"></a>Criar um Assistente de modelo personalizado  
 Este tópico mostra como criar um assistente personalizado que abre um formulário do Windows antes do projeto é criado. O formulário permite que os usuários adicionem um valor de parâmetro personalizado que é adicionado ao código-fonte durante a criação do projeto.  
  
1. Configure o projeto do VSIX para permitir que ele crie um assembly.  
  
2. No **Gerenciador de soluções**, selecione o nó do projeto VSIX. Abaixo do Gerenciador de soluções, você deverá ver a **propriedades** janela. Se você não fizer isso, selecione **modo de exibição** > **janela de propriedades**, ou pressione **F4**. No **propriedades** janela, selecione os seguintes campos para `true`:  
  
   -   **IncludeAssemblyInVSIXContainer**  
  
   -   **IncludeDebugSymbolsInVSIXContainer**  
  
   -   **IncludeDebugSymbolsInLocalVSIXDeployment**  
  
3. Adicione o assembly como um ativo para o projeto do VSIX. Abra o *vsixmanifest* do arquivo e selecione o **ativos** guia. No **adicionar novo ativo** janela, para **tipo** selecionar **Microsoft.VisualStudio.Assembly**, para **origem** selecione **um projeto na solução atual**e para **Project** selecionar **MyProjectWizard**.  
  
4. Adicione as seguintes referências ao projeto de VSIX. (Na **Gerenciador de soluções**, selecione do nó do projeto sob o VSIX **referências**, mouse e selecione **Add Reference**.) No **adicionar referência** caixa de diálogo, no **Framework** guia, localize o **System. Windows Forms** assembly e selecioná-lo. Agora, selecione a **extensões** find na guia o **EnvDTE** assembly e selecioná-lo. Encontre também a **Microsoft.VisualStudio.TemplateWizardInterface** assembly e selecioná-lo. Clique em **OK**.  
  
5. Adicione uma classe para a implementação do Assistente para o projeto do VSIX. (Na **Gerenciador de soluções**, clique com botão direito no nó do projeto VSIX e selecione **Add**, em seguida, **Novo Item**, em seguida, **classe**.) Nomeie a classe **WizardImplementation**.  
  
6. Substitua o código na *WizardImplementationClass.cs* arquivo pelo código a seguir:  
  
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
  
    O **UserInputForm** referenciado neste código será implementado mais tarde.  
  
    O `WizardImplementation` classe contém implementações de método para cada membro do <xref:Microsoft.VisualStudio.TemplateWizard.IWizard>. Neste exemplo, somente o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> método executa uma tarefa. Todos os outros métodos não fazem nada ou retornam `true`.  
  
    O <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> método aceita quatro parâmetros:  
  
   - Uma <xref:System.Object> parâmetro que pode ser convertido para a raiz <xref:EnvDTE._DTE> objeto, para que você possa personalizar o projeto.  
  
   - Um <xref:System.Collections.Generic.Dictionary%602> parâmetro que contém uma coleção de todos os parâmetros pré-definidos no modelo. Para obter mais informações sobre parâmetros de modelo, consulte [parâmetros de modelo](../ide/template-parameters.md).  
  
   - Um <xref:Microsoft.VisualStudio.TemplateWizard.WizardRunKind> parâmetro que contém informações sobre o tipo de modelo está sendo usado.  
  
   - Um <xref:System.Object> matriz que contém um conjunto de parâmetros passados para o assistente pelo Visual Studio.  
  
     Este exemplo adiciona um valor de parâmetro de formulário de entrada do usuário para o <xref:System.Collections.Generic.Dictionary%602> parâmetro. Todas as instâncias da `$custommessage$` parâmetro no projeto será substituído pelo texto inserido pelo usuário. Você deve adicionar os seguintes assemblies ao seu projeto: **System** e **System. Drawing**.
  
7. Agora, crie o **UserInputForm**. No *WizardImplementation.cs* do arquivo, adicione o seguinte código após o final do `WizardImplementation` classe.  
  
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
  
    Formulário de entrada do usuário fornece um formulário simples para inserir um parâmetro personalizado. O formulário contém uma caixa de texto denominada `textBox1` e um botão chamado `button1`. Quando o botão é clicado, o texto da caixa de texto é armazenado no `customMessage` parâmetro.  
  
## <a name="connect-the-wizard-to-the-custom-template"></a>O Assistente de conexão para o modelo personalizado  
 Para o modelo de projeto personalizado usar o assistente personalizado, você precisa assinar o assembly de assistente e adicionar algumas linhas ao seu modelo de projeto personalizados para permitir que ele saiba onde encontrar a implementação do assistente quando um novo projeto é criado.  
  
1. Assine o assembly. No **Gerenciador de soluções**, selecione o projeto VSIX, clique com botão direito e selecione **propriedades do projeto**.  
  
2. No **propriedades do projeto** janela, selecione a **Signing** na guia no **Signing** guia, seleção **assinar o assembly**. No **escolher um arquivo de chave de nome forte** campo, selecione  **\<New >**. No **criar chave de nome forte** janela, no **nome do arquivo de chave** , digite **snk**. Desmarque a **proteger o arquivo de chave com uma senha** campo.  
  
3. No **Gerenciador de soluções**, selecione o projeto do VSIX e localizar o **propriedades** janela.  
  
4. Defina a **diretório de saída para saída de compilação de cópia** campo **true**. Isso permite que o assembly a ser copiado para o diretório de saída quando a solução é reconstruída. Ainda está contida no `.vsix` arquivo. Você precisa ver o assembly para descobrir a chave de assinatura.  
  
5. Recompile a solução.  
  
6. Agora você pode encontrar o arquivo snk no diretório do projeto MyProjectWizard (*\<seu local de disco > \MyProjectTemplate\MyProjectWizard\key.snk*). Cópia de *snk* arquivo.  
  
7. Vá para o diretório de saída e localize o assembly (*\<seu local de disco > \MyProjectTemplate/MyProjectWizard\bin\Debug\MyProjectWizard.dll*). Cole a *snk* arquivo aqui. (Isso não é absolutamente necessário, mas facilitará as etapas a seguir).  
  
8. Abra uma janela de comando e altere o diretório no qual o assembly foi criado.  
  
9. Localizar o *sn.exe* ferramenta de assinatura. Por exemplo, em um sistema de operacional de 64 bits do Windows 10, um caminho típico seria o seguinte:  
  
     *C:\Program arquivos (x86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.6.1 ferramentas*  
  
     Se você não encontrar a ferramenta, tente executar **onde /R.  Sn.exe** na janela de comando. Anote o caminho.  
  
10. Extrair a chave pública a partir de *snk* arquivo. Na janela de comando, digite  
  
     **\<local do sn.exe > \sn.exe -p snk outfile.key.**  
  
     Não se esqueça de colocar o caminho de *sn.exe* com as aspas se houver espaços em nomes de diretório!  
  
11. Obter token de chave pública do outfile:  
  
     **\<local do sn.exe > \sn.exe -t outfile.key.**  
  
     Novamente, não se esqueça as aspas. Você deve ver uma linha na saída como esta  
  
     **Token de chave pública é <token>**  
  
     Anote esse valor.  
  
12. Adicionar a referência para o assistente personalizado para o *. vstemplate* arquivo do modelo de projeto. No **Gerenciador de soluções**, localize o arquivo chamado *MyProjectTemplate.vstemplate*e abri-lo. Após o final do \<TemplateContent > seção, adicione a seção a seguir:  
  
    ```xml  
    <WizardExtension>  
        <Assembly>MyProjectWizard, Version=1.0.0.0, Culture=Neutral, PublicKeyToken=token</Assembly>  
        <FullClassName>MyProjectWizard.WizardImplementation</FullClassName>  
    </WizardExtension>  
    ```  
  
     Em que **MyProjectWizard** é o nome do assembly, e **token** é o token que você copiou na etapa anterior.  
  
13. Salve todos os arquivos no projeto e recompile.  
  
## <a name="add-the-custom-parameter-to-the-template"></a>Adicionar o parâmetro personalizado para o modelo  
 Neste exemplo, o projeto usado como modelo exibe a mensagem especificada no formulário de entrada do usuário do assistente personalizado.  
  
1. No **Gerenciador de soluções**, vá para o **MyProjectTemplate** do projeto e abra *Class1.cs*.  
  
2. No `Main` método do aplicativo, adicione a seguinte linha de código.  
  
   ```csharp  
   Console.WriteLine("$custommessage$");  
   ```  
  
    O parâmetro `$custommessage$` é substituído pelo texto inserido no formulário de entrada do usuário quando um projeto é criado a partir do modelo.  
  
   Aqui está o arquivo de código completo antes que ele foi exportado para um modelo.  
  
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
  
1.  Recompile a solução e iniciar a depuração. Uma segunda instância do Visual Studio deve ser exibida.  
  
2.  Crie um novo projeto de MyProjectTemplate. (**Arquivo** > **nova** > **projeto** > **Visual C#**  >  **MyProjectTemplate**)  
  
3.  No **novo projeto** caixa de diálogo, localize seu modelo, digite um nome e clique em **Okey**.  
  
     Abre o formulário de entrada de usuário do assistente.  
  
4.  Digite um valor para o parâmetro personalizado e clique no botão.  
  
     O formulário de entrada de usuário de Assistente fecha e um projeto é criado a partir do modelo.  
  
5.  Na **Gerenciador de soluções**, o arquivo de código de origem com o botão direito e clique em **Exibir código**.  
  
     Observe que `$custommessage$` foi substituído pelo texto inserido no formulário de entrada do usuário do assistente.  
  
## <a name="see-also"></a>Consulte também  

<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>   
[Personalizar modelos](../ide/customizing-project-and-item-templates.md)  
[Elemento WizardExtension (modelos do Visual Studio)](../extensibility/wizardextension-element-visual-studio-templates.md)  
[Pacotes do NuGet em modelos do Visual Studio](/nuget/visual-studio-extensibility/visual-studio-templates)
