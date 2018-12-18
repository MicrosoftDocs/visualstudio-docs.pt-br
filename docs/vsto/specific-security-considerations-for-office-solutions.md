---
title: Considerações sobre segurança específicas para soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- troubleshooting Office development in Visual Studio, security
- trusted code [Office development in Visual Studio]
- blocked code [Office development in Visual Studio]
- Outlook [Office development in Visual Studio], object model guard
- malicious code [Office development in Visual Studio]
- Outlook object model guard [Office development in Visual Studio]
- security [Office development in Visual Studio], troubleshooting
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: dcb2e0a3c381b1dd07c7724c3a64c53307856014
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49951386"
---
# <a name="specific-security-considerations-for-office-solutions"></a>Considerações sobre segurança específicas para soluções do Office
  Os recursos de segurança fornecidos pelo Microsoft .NET Framework e do Microsoft Office podem ajudar a proteger suas soluções do Office em relação a possíveis ameaças à segurança. Este tópico explica algumas dessas ameaças e fornece recomendações para ajudar a proteger contra elas. Ele também inclui informações sobre como as configurações de segurança do Microsoft Office afetam soluções do Office.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
## <a name="trusted-code-is-repurposed-in-a-new-malicious-document"></a>Código confiável é redefinido em um novo documento mal-intencionado  
 Um invasor pode executar código confiável destina-se para uma finalidade específica, por exemplo, download de informações pessoais para um aplicativo de emprego, e reutilizá-lo em outro documento, como uma planilha. O código não sabe que o documento original não está em execução e outras ameaças, como revelar informações pessoais ou executar o código com privilégios de aumento, quando aberto por um usuário diferente pode abrir. Como alternativa, o invasor pode modificar os dados na planilha, de modo que, quando enviado para a vítima, ele se comporta inesperadamente. Alterando os valores, fórmulas ou características de apresentação de uma planilha vinculada ao código, é possível que um usuário mal-intencionado atacar a outro usuário por meio do envio de um arquivo modificado. Também é possível que os usuários para acessar as informações que não deveriam ver modificando os valores na planilha.  
  
 Como o local do assembly e o local do documento devem ter as evidências suficientes para executar, não é fácil montar esse ataque. Por exemplo, documentos em anexos de email ou em servidores de intranet não confiáveis não tem permissões suficientes para executar.  
  
 Para possibilitar a esse ataque, o código em si deve ser escrito de forma que ele toma decisões com base nos dados potencialmente não confiáveis. Um exemplo é criar uma planilha que tenha uma célula ocultada que contém o nome de um servidor de banco de dados. O usuário envia a planilha para uma página ASPX, que tenta se conectar ao servidor usando a autenticação do SQL e uma senha de SA embutido em código. Um invasor pode substituir o conteúdo da célula oculto com um nome de computador diferente e obter a senha SA. Para evitar esse problema, as senhas nunca embutido em código e, sempre verifique as IDs do servidor em relação a uma lista interna de servidores que são conhecidos em boas condições antes de acessar o servidor.  
  
### <a name="recommendations"></a>Recomendações  
  
-   Sempre valide entrada de dados e, se ela é proveniente do usuário, o documento, um banco de dados, um serviço web ou qualquer outra fonte.  
  
-   Tenha cuidado ao expor determinados tipos de funcionalidades, como obter dados privilegiados em nome do usuário e colocá-lo em uma planilha desprotegida.  
  
-   Dependendo do tipo de aplicativo, ele pode fazer sentido para verificar se o documento original está em execução antes de executar qualquer código. Por exemplo, verificar se ele está em execução de um documento armazenado em um local seguro, conhecido.  
  
-   Ele pode ser uma boa ideia para exibir um aviso quando o documento é aberto, se o aplicativo executa as ações privilegiadas. Por exemplo, você pode criar uma tela inicial ou uma caixa de diálogo de inicialização dizendo que o aplicativo acessar informações pessoais e peça que o usuário optar por continuar ou em Cancelar. Se um usuário final obtém um aviso desse tipo de um documento aparentemente inocente, ele ou ela poderá encerrar o aplicativo antes de qualquer coisa está comprometida.  
  
## <a name="code-is-blocked-by-the-outlook-object-model-guard"></a>Código está bloqueado pelo object model guard do Outlook  
 Microsoft Office pode impedir que o código usando determinadas propriedades, métodos e objetos no modelo de objeto. Restringindo o acesso a esses objetos, o Outlook ajuda a evitar que vírus e worms de email usando o modelo de objeto para fins mal-intencionados. Esse recurso de segurança é conhecido como o object model guard do Outlook. Se um suplemento do VSTO tenta usar um método ou propriedade restrita enquanto o object model guard estiver habilitado, o Outlook exibe um aviso de segurança que permite que o usuário interromper a operação ou permite que o usuário conceder acesso à propriedade ou método por um período limitado de t IME. Se o usuário para a operação, Add-ins do VSTO do Outlook criados usando as soluções do Office no Visual Studio gerará um <xref:System.Runtime.InteropServices.COMException>.  
  
 O object model guard pode afetar o VSTO Add-ins de maneiras diferentes, dependendo do Outlook é usado com o Microsoft Exchange Server:  
  
- Se o Outlook não for usado com o Exchange, um administrador pode habilitar ou desabilitar o object model guard para todos os suplementos do VSTO no computador.  
  
- Se o Outlook é usado com o Exchange, um administrador pode habilitar ou desabilitar o object model guard para todos os suplementos do VSTO no computador ou o administrador pode especificar que certos VSTO Add-ins pode ser executada sem encontrar o object model guard. Os administradores também podem modificar o comportamento do object model guard para determinadas áreas do modelo de objeto. Por exemplo, os administradores podem automaticamente permitir que VSTO Add-ins enviar email programaticamente, mesmo se o object model guard estiver habilitado.  
  
  A partir do Outlook 2007, o comportamento do object model guard foi alterado para melhorar a experiência do usuário e do desenvolvedor, ajudando a manter o Outlook seguro. Para obter mais informações, consulte [alterações de segurança do Outlook 2007 de código](http://go.microsoft.com/fwlink/?LinkId=73429).  
  
### <a name="minimize-object-model-guard-warnings"></a>Minimizar os avisos de proteção de modelo de objeto  
 Para evitar avisos de segurança quando você usa métodos e propriedades restritas, certifique-se de que seu suplemento do VSTO obtém objetos do Outlook do `Application` campo do `ThisAddIn` classe em seu projeto. Para obter mais informações sobre esse campo, consulte [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md).  
  
 Somente objetos do Outlook obtidos a partir esse objeto podem ser confiável pelo object model guard. Em contraste, os objetos que são obtidos de um novo `Microsoft.Office.Interop.Outlook.Application` objeto não são confiáveis e as propriedades restritas e os métodos gerará avisos de segurança se o object model guard estiver habilitado.  
  
 O exemplo de código a seguir exibe um aviso de segurança se o object model guard estiver habilitado. O `To` propriedade do `Microsoft.Office.Interop.Outlook.MailItem` classe é restrito pelo object model guard. O `Microsoft.Office.Interop.Outlook.MailItem` objeto não é confiável porque o código obtém-o de um `Microsoft.Office.Interop.Outlook.Application` que é criado usando o **novos** operador, em vez de obtenção do `Application` campo.  
  
 [!code-csharp[Trin_VstcoreOutlookSecurity#1](../vsto/codesnippet/CSharp/Trin_VstcoreOutlookSecurity/ThisAddIn.cs#1)]
 [!code-vb[Trin_VstcoreOutlookSecurity#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreOutlookSecurity/ThisAddIn.vb#1)]  
  
 O exemplo de código a seguir demonstra como usar o restrito à propriedade de um `Microsoft.Office.Interop.Outlook.MailItem` objeto que é confiável pelo object model guard. O código usa o confiável `Application` campo para obter o `Microsoft.Office.Interop.Outlook.MailItem`.  
  
 [!code-csharp[Trin_VstcoreOutlookSecurity#2](../vsto/codesnippet/CSharp/Trin_VstcoreOutlookSecurity/ThisAddIn.cs#2)]
 [!code-vb[Trin_VstcoreOutlookSecurity#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreOutlookSecurity/ThisAddIn.vb#2)]  
  
> [!NOTE]  
>  Se o Outlook é usado com o Exchange, em seguida, obtendo todos os objetos do Outlook de `ThisAddIn.Application` não garante que o suplemento do VSTO poderão acessar todo o modelo de objeto do Outlook. Por exemplo, se um administrador do Exchange define automaticamente o Outlook negar todas as tentativas de acessar informações de endereço usando o modelo de objeto do Outlook, em seguida, o Outlook não permitirá que o exemplo de código anterior acessar a propriedade To, mesmo que use o exemplo de código o confiável `ThisAddIn.Application` campo.  
  
### <a name="specify-which-add-ins-to-trust-when-using-exchange"></a>Especifique quais suplementos confiar ao usar o Exchange  
 Quando o Outlook é usado com o Exchange, os administradores podem especificar que certos VSTO Add-ins pode ser executada sem encontrar o object model guard. Outlook VSTO Add-ins criados por meio de soluções do Office no Visual Studio não pode ser confiáveis individualmente; eles só podem ser confiáveis como um grupo.  
  
 Outlook confia em um suplemento VSTO com base em um código hash da DLL de ponto de entrada do suplemento do VSTO. Todos os Outlook suplementos do VSTO que se destinam a [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] usar a mesma DLL de ponto de entrada (*vstoloader. dll*). Isso significa que, se um administrador confia qualquer suplemento VSTO que tem como alvo o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] para ser executada sem encontrar o object model guard e, em seguida, todos os outros suplementos do VSTO que se destinam a [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] também são confiáveis. Para obter mais informações sobre como confiar em específicos suplementos do VSTO para ser executada sem encontrar o object model guard, consulte [especificar o método que usa o Outlook para gerenciar recursos de prevenção de vírus](http://go.microsoft.com/fwlink/?LinkId=128773).  
  
## <a name="permission-changes-do-not-take-effect-immediately"></a>As alterações de permissão não entram em vigor imediatamente  
 Se o administrador ajusta as permissões para um documento ou um assembly, os usuários deverão encerrar e, em seguida, reinicie todos os aplicativos do Office para essas alterações devem ser aplicadas.  
  
 Outros aplicativos que hospedam aplicativos do Microsoft Office também podem impedir que as novas permissões do que está sendo imposta. Os usuários devem encerrar todos os aplicativos que usam o Office, hospedado ou autônomo, quando as políticas de segurança são alteradas.  
  
## <a name="trust-center-settings-in-the-microsoft-office-system-do-not-affect-add-ins-or-document-level-customizations"></a>Configurações da Central de confiabilidade do Microsoft Office System não afetam os suplementos ou personalizações no nível do documento  
 Os usuários podem impedir que VSTO Add-ins carregamento, definindo uma opção na **Central de confiabilidade**. No entanto, VSTO Add-ins e personalizações no nível do documento criadas usando as soluções do Office no Visual Studio não são afetadas por essas configurações de confiança.  
  
 Se o usuário impede que suplementos do VSTO carregamento usando o **Central de confiabilidade**, os seguintes tipos de suplementos do VSTO não serão carregado:  
  
- Gerenciado e COM suplementos do VSTO.  
  
- Documentos inteligentes de gerenciados e não gerenciados.  
  
- Gerenciado e automação VSTO Add-ins.  
  
- Componentes gerenciados e dados em tempo real.  
  
  Os procedimentos a seguir descrevem como os usuários podem usar o **Central de confiabilidade** para restringir o VSTO Add-ins de carregamento no Microsoft [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] e o Microsoft Office 2010. Esses procedimentos não afetam o VSTO Add-ins ou personalizações criadas usando ferramentas de desenvolvimento do Office no Visual Studio.  
  
#### <a name="to-disable-vsto-add-ins-in-microsoft-office-2010-and-microsoft-includeoffice15shortvstoincludesoffice-15-short-mdmd-applications"></a>Para desabilitar o VSTO Add-ins no Microsoft Office 2010 e Microsoft [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] aplicativos  
  
1.  Escolha o **arquivo** guia.  
  
2.  Escolha o *ApplicationName* **opções** botão.  
  
3.  No painel de categorias, escolha **Central de confiabilidade**.  
  
4.  No painel de detalhes, escolha **configurações da Central de confiabilidade**.  
  
5.  No painel de categorias, escolha **Add-ins**.  
  
6.  No painel de detalhes, selecione **Add-ins do aplicativo exigir a ser assinado por um fornecedor confiável** ou **desabilitar todos os suplementos do aplicativo**.  
  
## <a name="see-also"></a>Consulte também  
 [Proteger as soluções do Office](../vsto/securing-office-solutions.md)  
  
  