---
title: Considerações de segurança específicas para soluções do Office
description: Saiba como os recursos de segurança fornecidos pelo Microsoft .NET Framework e Microsoft Office podem ajudar a proteger suas soluções do Office contra ameaças à segurança.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
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
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 58cd5f7a26be57ce0cb742e153d88ee455b2f85b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826103"
---
# <a name="specific-security-considerations-for-office-solutions"></a>Considerações de segurança específicas para soluções do Office
  Os recursos de segurança fornecidos pelo Microsoft .NET Framework e Microsoft Office podem ajudar a proteger suas soluções do Office contra possíveis ameaças à segurança. Este tópico explica algumas dessas ameaças e fornece recomendações para ajudar a protegê-las. Ele também inclui informações sobre como Microsoft Office configurações de segurança afetam as soluções do Office.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="trusted-code-is-repurposed-in-a-new-malicious-document"></a>O código confiável é realocado em um novo documento mal-intencionado
 Um invasor pode pegar um código confiável destinado a uma finalidade específica, por exemplo, baixar informações pessoais para um aplicativo de emprego e reutilizá-lo em outro documento, como uma planilha. O código não sabe que o documento original não está em execução e pode abrir outras ameaças, como revelar informações pessoais ou executar código com privilégios maiores, quando aberto por um usuário diferente. Como alternativa, o invasor pode modificar os dados na planilha, de modo que, quando enviados para a vítima, ele se comporta inesperadamente. Ao alterar os valores, as fórmulas ou as características de apresentação de uma planilha vinculada ao código, é possível que um usuário mal-intencionado ataque outro usuário enviando um arquivo modificado. Também pode ser possível que os usuários acessem informações que eles não devem ver modificando os valores na planilha.

 Como o local do assembly e o local do documento devem ter evidências suficientes para serem executados, esse ataque não é fácil de montar. Por exemplo, documentos em anexos de email ou em servidores de intranet não confiáveis não têm permissões suficientes para serem executados.

 Para tornar esse ataque possível, o próprio código deve ser escrito de forma que ele toma decisões com base em dados potencialmente não confiáveis. Um exemplo é a criação de uma planilha que tem uma célula oculta que contém o nome de um servidor de banco de dados. O usuário envia a planilha para uma página ASPX, que tenta se conectar a esse servidor usando a autenticação do SQL e uma senha SA embutida em código. Um invasor pode substituir o conteúdo da célula oculta por um nome de computador diferente e obter a senha SA. Para evitar esse problema, nunca codifique as senhas e sempre verifique as IDs do servidor em relação a uma lista interna de servidores que devem ser bons antes de acessar o servidor.

### <a name="recommendations"></a>Recomendações

- Sempre valide a entrada e os dados, sejam eles provenientes do usuário, do documento, de um banco de dado, de um serviço Web ou de qualquer outra fonte.

- Tenha cuidado ao expor tipos específicos de funcionalidade, como obter dados privilegiados em nome do usuário e colocá-los em uma planilha desprotegida.

- Dependendo do tipo de aplicativo, pode fazer sentido verificar se o documento original está em execução antes de executar qualquer código. Por exemplo, verifique se ele está sendo executado de um documento armazenado em um local seguro e conhecido.

- Pode ser uma boa ideia exibir um aviso quando o documento for aberto se seu aplicativo executar qualquer ação privilegiada. Por exemplo, você pode criar uma tela inicial ou uma caixa de diálogo de inicialização informando que o aplicativo acessará informações pessoais e fazer com que o usuário escolha continuar ou cancelar. Se um usuário final receber tal aviso de um documento aparentemente inocente, ele poderá sair do aplicativo antes que qualquer coisa seja comprometida.

## <a name="code-is-blocked-by-the-outlook-object-model-guard"></a>O código está bloqueado pelo Object Model Guard do Outlook
 Microsoft Office pode restringir o uso do código de determinadas propriedades, métodos e objetos no modelo de objeto. Ao restringir o acesso a esses objetos, o Outlook ajuda a impedir que worms de email e vírus usem o modelo de objeto para fins mal-intencionados. Esse recurso de segurança é conhecido como o Object Model Guard do Outlook. Se um suplemento do VSTO tentar usar uma propriedade ou método restrito enquanto o Object Model Guard estiver habilitado, o Outlook exibirá um aviso de segurança que permite ao usuário parar a operação ou permitirá que o usuário conceda acesso à propriedade ou ao método por um período de tempo limitado. Se o usuário parar a operação, os suplementos do VSTO do Outlook criados usando as soluções do Office no Visual Studio lançarão um <xref:System.Runtime.InteropServices.COMException> .

 O Object Model Guard pode afetar os suplementos do VSTO de diferentes maneiras, dependendo se o Outlook é usado com o Microsoft Exchange Server:

- Se o Outlook não for usado com o Exchange, um administrador poderá habilitar ou desabilitar o Object Model Guard para todos os suplementos do VSTO no computador.

- Se o Outlook for usado com o Exchange, um administrador poderá habilitar ou desabilitar o Object Model Guard para todos os suplementos do VSTO no computador, ou o administrador poderá especificar que determinados suplementos do VSTO possam ser executados sem encontrar o Object Model Guard. Os administradores também podem modificar o comportamento do Object Model Guard para determinadas áreas do modelo de objeto. Por exemplo, os administradores podem permitir automaticamente que os suplementos do VSTO enviem email de forma programática, mesmo que o Object Model Guard esteja habilitado.

  A partir do Outlook 2007, o comportamento do Object Model Guard foi alterado para melhorar a experiência do desenvolvedor e do usuário, ajudando a manter o Outlook seguro. Para obter mais informações, consulte [alterações de segurança de código no Outlook 2007](/previous-versions/office/developer/office-2007/bb226709(v=office.12)).

### <a name="minimize-object-model-guard-warnings"></a>Minimizar avisos do Object Model Guard
 Para ajudar a evitar avisos de segurança ao usar propriedades e métodos restritos, certifique-se de que seu suplemento do VSTO obtenha objetos do Outlook do `Application` campo da `ThisAddIn` classe em seu projeto. Para obter mais informações sobre esse campo, consulte [programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md).

 Somente objetos do Outlook obtidos desse objeto podem ser confiáveis pelo Object Model Guard. Por outro lado, os objetos que são obtidos de um novo `Microsoft.Office.Interop.Outlook.Application` objeto não são confiáveis, e as propriedades e os métodos restritos gerarão avisos de segurança se o Object Model Guard estiver habilitado.

 O exemplo de código a seguir exibirá um aviso de segurança se o Object Model Guard estiver habilitado. A `To` propriedade da `Microsoft.Office.Interop.Outlook.MailItem` classe é restrita pelo Object Model Guard. O `Microsoft.Office.Interop.Outlook.MailItem` objeto não é confiável porque o código o obtém de um `Microsoft.Office.Interop.Outlook.Application` que é criado usando o **novo** operador, em vez de obtê-lo do `Application` campo.

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreOutlookSecurity/ThisAddIn.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreOutlookSecurity/ThisAddIn.vb" id="Snippet1":::

 O exemplo de código a seguir demonstra como usar a propriedade Restricted to de um `Microsoft.Office.Interop.Outlook.MailItem` objeto que é confiável pelo Object Model Guard. O código usa o `Application` campo confiável para obter o `Microsoft.Office.Interop.Outlook.MailItem` .

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreOutlookSecurity/ThisAddIn.cs" id="Snippet2":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreOutlookSecurity/ThisAddIn.vb" id="Snippet2":::

> [!NOTE]
> Se o Outlook for usado com o Exchange, a obtenção de todos os objetos do Outlook do `ThisAddIn.Application` não garante que o suplemento do VSTO poderá acessar todo o modelo de objeto do Outlook. Por exemplo, se um administrador do Exchange definir o Outlook para negar automaticamente todas as tentativas de acessar informações de endereço usando o modelo de objeto do Outlook, o Outlook não permitirá que o exemplo de código anterior acesse a propriedade to, mesmo que o exemplo de código use o `ThisAddIn.Application` campo confiável.

### <a name="specify-which-add-ins-to-trust-when-using-exchange"></a>Especificar quais suplementos confiar ao usar o Exchange
 Quando o Outlook é usado com o Exchange, os administradores podem especificar que determinados suplementos do VSTO possam ser executados sem encontrar o Object Model Guard. Os suplementos do VSTO do Outlook criados usando as soluções do Office no Visual Studio não podem ser confiáveis individualmente; Eles só podem ser confiáveis como um grupo.

 O Outlook confia em um suplemento do VSTO com base em um código hash da DLL do ponto de entrada do suplemento do VSTO. Todos os suplementos do VSTO do Outlook que visam [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] usar a mesma DLL de ponto de entrada (*VSTOLoader.dll*). Isso significa que, se um administrador confiar em qualquer suplemento do VSTO que tenha como alvo o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] a ser executado sem encontrar o Object Model Guard, todos os outros suplementos do VSTO destinados ao [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] também serão confiáveis. Para obter mais informações sobre como confiar em suplementos específicos do VSTO para execução sem encontrar o Object Model Guard, consulte [especificar o método que o Outlook usa para gerenciar os recursos de prevenção de vírus](/previous-versions/office/office-2007-resource-kit/cc179194(v=office.12)).

## <a name="permission-changes-do-not-take-effect-immediately"></a>As alterações de permissão não entram em vigor imediatamente
 Se o administrador ajustar as permissões para um documento ou assembly, os usuários deverão encerrar e reiniciar todos os aplicativos do Office para que essas alterações sejam impostas.

 Outros aplicativos que hospedam Microsoft Office aplicativos também podem impedir que as novas permissões sejam impostas. Os usuários devem encerrar todos os aplicativos que usam o Office, hospedado ou autônomo, quando as políticas de segurança são alteradas.

## <a name="trust-center-settings-in-the-microsoft-office-system-do-not-affect-add-ins-or-document-level-customizations"></a>As configurações da central de confiabilidade no sistema Microsoft Office não afetam os suplementos ou personalizações em nível de documento
 Os usuários podem impedir que os suplementos do VSTO sejam carregados definindo uma opção na **central de confiabilidade**. No entanto, os suplementos do VSTO e as personalizações em nível de documento criadas usando as soluções do Office no Visual Studio não são afetadas por essas configurações de confiança.

 Se o usuário impedir que os suplementos do VSTO sejam carregados usando a **central de confiabilidade**, os seguintes tipos de suplementos do VSTO não serão carregados:

- Suplementos do VSTO COM gerenciados e não gerenciados.

- Documentos inteligentes gerenciados e não gerenciados.

- Suplementos do VSTO de automação gerenciados e não gerenciados.

- Componentes de dados em tempo real gerenciados e não gerenciados.

  Os procedimentos a seguir descrevem como os usuários podem usar a **central de confiabilidade** para restringir o carregamento dos suplementos do VSTO na Microsoft [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] e Microsoft Office 2010. Esses procedimentos não afetam os suplementos do VSTO ou as personalizações criadas usando as ferramentas de desenvolvimento do Office no Visual Studio.

#### <a name="to-disable-vsto-add-ins-in-microsoft-office-2010-and-microsoft-office_15_short-applications"></a>Para desabilitar os suplementos do VSTO no Microsoft Office 2010 e nos [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] aplicativos da Microsoft

1. Escolha a guia **arquivo** .

2. Escolha o botão **Opções** de *ApplicationName* .

3. No painel categorias, escolha **central de confiabilidade**.

4. No painel de detalhes, escolha **configurações da central de confiabilidade**.

5. No painel categorias, escolha **suplementos**.

6. No painel de detalhes, selecione **exigir que os suplementos de aplicativo sejam assinados por um fornecedor confiável** ou **desabilite todos os suplementos de aplicativo**.

## <a name="see-also"></a>Consulte também
- [Proteger soluções do Office](../vsto/securing-office-solutions.md)
