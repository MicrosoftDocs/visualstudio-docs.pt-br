---
title: Melhorar o desempenho de um suplemento do VSTO
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 918ff0ac0a0b7f4e16c779516c015d7b74cec415
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672646"
---
# <a name="improve-the-performance-of-a-vsto-add-in"></a>Melhorar o desempenho de um suplemento do VSTO
  Você pode dar aos usuários uma experiência melhor ao otimizar o VSTO Add-ins que você cria para o Office, aplicativos para que eles são rapidamente iniciados, desligar, abrir itens e executar outras tarefas. Se o suplemento do VSTO para Outlook, você também pode reduzir a chance de que seu suplemento do VSTO será desabilitado devido a um desempenho ruim. Você pode aumentar o desempenho do seu suplemento do VSTO, implementando as estratégias a seguir:  
  
- [Carregar o VSTO Add-ins sob demanda](#Load).  
  
- [Publicar soluções do Office usando o Windows Installer](#Publish).  
  
- [Ignorar a reflexão de faixa de opções](#Bypass).  
  
- [Executar operações caras em um thread de execução separado](#Perform).  
  
  Para obter mais informações sobre como otimizar um suplemento do VSTO do Outlook, consulte [critérios de desempenho para manter os suplementos do VSTO habilitados](http://go.microsoft.com/fwlink/?LinkID=266503).  
  
##  <a name="Load"></a> Carregar o VSTO Add-ins sob demanda  
 Você pode configurar um suplemento do VSTO para carregar somente nas seguintes circunstâncias:  
  
- Na primeira vez que o usuário inicia o aplicativo depois que o suplemento do VSTO é instalado.  
  
- Na primeira vez que o usuário interage com o suplemento do VSTO depois de iniciar o aplicativo a qualquer momento.  
  
  Por exemplo, o suplemento do VSTO pode preencher uma planilha com os dados quando o usuário escolhe um botão personalizado que é rotulado **obter dados de meu**. O aplicativo deve carregar o suplemento do VSTO, pelo menos uma vez para que o **obter dados de meu** botão poderá aparecer na faixa de opções. No entanto, o suplemento do VSTO não carrega novamente quando o usuário inicia o aplicativo na próxima vez. O suplemento do VSTO carrega apenas quando o usuário escolhe o **obter dados de meu** botão.  
  
### <a name="to-configure-a-clickonce-solution-to-load-vsto-add-ins-on-demand"></a>Para configurar uma solução de ClickOnce para carregar o VSTO Add-ins sob demanda  
  
1.  Na **Gerenciador de soluções**, escolha o nó do projeto.  
  
2.  Na barra de menus, escolha **Exibir** > **Páginas de Propriedade**.  
  
3.  Sobre o **Publish** guia, escolha o **opções** botão.  
  
4.  No **opções de publicação** caixa de diálogo, escolha o **configurações do Office** item de lista, escolha o **carga sob demanda** opção e, em seguida, escolha o **Okey**botão.  
  
### <a name="to-configure-a-windows-installer-solution-to-load-vsto-add-ins-on-demand"></a>Para configurar uma solução do Windows Installer para carregar o VSTO Add-ins sob demanda  
  
1.  No registro, defina as `LoadBehavior` entrada do **_raiz_\Software\Microsoft\Office\\_ApplicationName_\Addins\\  _ID do suplemento_** chave **0x10**.  
  
     Para obter mais informações, consulte [entradas do registro para suplementos VSTO](../vsto/registry-entries-for-vsto-add-ins.md).  
  
### <a name="to-configure-a-solution-to-load-vsto-add-ins-on-demand-while-you-debug-the-solution"></a>Para configurar uma solução para carregar o VSTO Add-ins sob demanda ao depurar a solução  
  
1.  Criar um script que define o `LoadBehavior` entrada do **_raiz_\Software\Microsoft\Office\\_ApplicationName_\Addins\\  _ID do suplemento_** chave **0x10**.  
  
     O código a seguir mostra um exemplo desse script.  
  
    ```cmd/sh
    [HKEY_CURRENT_USER\Software\Microsoft\Office\Excel\Addins\MyAddIn]  
    "Description"="MyAddIn"  
    "FriendlyName"="MyAddIn"  
    "LoadBehavior"=dword:00000010  
    "Manifest"="c:\\Temp\\MyAddIn\\bin\\Debug\\MyAddIn.vsto|vstolocal"  
  
    ```  
  
2.  Crie um evento de pós-compilação que atualiza o registro usando o script.  
  
     O código a seguir mostra um exemplo de uma cadeia de caracteres de comando que você pode adicionar a um evento de pós-compilação.  
  
    ```cmd/sh
    regedit /s "$(SolutionDir)$(SolutionName).reg"  
  
    ```  
  
     Para obter informações sobre como criar um evento de pós-compilação em um C# projeto, consulte [como: especificar eventos de build &#40;C&#35;&#41;](/visualstudio/ide/how-to-specify-build-events-csharp).  
  
     Para obter informações sobre como criar um evento de pós-compilação em um projeto do Visual Basic, consulte [como: especificar eventos de build &#40;Visual Basic&#41;](/visualstudio/ide/how-to-specify-build-events-visual-basic).  
  
##  <a name="Publish"></a> Publicar soluções do Office usando o Windows Installer  
 Se você publicar sua solução usando o Windows Installer, o Visual Studio 2010 Tools for Office runtime ignora as etapas a seguir, quando o suplemento do VSTO é carregado.  
  
- Validação do esquema de manifesto.  
  
- Verificando atualizações automaticamente.  
  
- Validação de assinaturas digitais de manifestos de implantação.  
  
  > [!NOTE]  
  >  Essa abordagem não é necessária se você implantar seu suplemento do VSTO em um local seguro nos computadores dos usuários.  
  
  Para obter mais informações, consulte [implantar uma solução do Office usando o Windows Installer](../vsto/deploying-an-office-solution-by-using-windows-installer.md).  
  
##  <a name="Bypass"></a> Ignorar a reflexão de faixa de opções  
 Se você criar uma solução usando [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)], certifique-se de que seus usuários tenham instalado a versão mais recente do Visual Studio 2010 Tools para Office runtime quando você implanta a solução. Versões mais antigas do que em tempo de execução são refletidas em assemblies de solução para localizar as personalizações da faixa de opções. Esse processo pode fazer com que o suplemento do VSTO seja carregada mais lentamente.  
  
 Como alternativa, você pode impedir que qualquer versão do Visual Studio 2010 Tools para Office runtime usando a reflexão para identificar as personalizações da faixa de opções. Para seguir essa estratégia, substituir o `CreateRibbonExtensibility` método e retorno explicitamente objetos da faixa de opções. Se o suplemento do VSTO não contiver quaisquer personalizações da faixa de opções, retorno `null` dentro do método.  
  
 O exemplo a seguir retorna um objeto de faixa de opções com base no valor de um campo.  
  
 [!code-vb[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/VisualBasic/trin_ribbon_choose_ribbon_4/ThisWorkbook.vb#1)]
 [!code-csharp[Trin_Ribbon_Choose_Ribbon#1](../vsto/codesnippet/CSharp/trin_ribbon_choose_ribbon_4/ThisWorkbook.cs#1)]  
  
##  <a name="Perform"></a> Executar operações caras em um thread de execução separado  
 Considere a execução de tarefas demoradas (por exemplo, tarefas de longa execução, as conexões de banco de dados ou outros tipos de chamadas de rede) em um thread separado. Para obter mais informações, consulte [suporte a Threading no Office](../vsto/threading-support-in-office.md).  
  
> [!NOTE]  
>  Todo o código que chama o modelo de objeto do Office deve executar no thread principal.  
  
## <a name="see-also"></a>Consulte também  
 [Suplementos do VSTO do carregamento por demanda](https://blogs.msdn.microsoft.com/andreww/2008/07/14/demand-loading-vsto-add-ins/)   
 [Carregamento de atraso do CLR em suplementos do Office](https://blogs.msdn.microsoft.com/andreww/2008/04/19/delay-loading-the-clr-in-office-add-ins/)   
 [Criar suplementos para Office do VSTO usando o Visual Studio](create-vsto-add-ins-for-office-by-using-visual-studio.md)   
