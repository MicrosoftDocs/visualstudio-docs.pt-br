---
title: Expor listas de símbolos fornecidos ao Gerenciador de objetos | Microsoft Docs
description: Saiba como implementar a interface IVsSimpleObjectList2 para expor listas de símbolos ao Gerenciador de objetos no Visual Studio e atualizar as ferramentas de navegação de símbolos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- IVsSimpleLibrary2 interface, lists of symbols
- IVsLibrary2 interface, lists of symbols
- symbols, call browser
- lists, symbols for the object manager
- symbols, exposing lists to the object manager
ms.assetid: 19757068-bdaa-4e7e-85d6-f8ce5026a859
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fceb8b2d4a79243117e03aab57ce239b13c3d750
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898169"
---
# <a name="how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager"></a>Como: expor listas de símbolos fornecidos pela biblioteca para o Gerenciador de objetos
As ferramentas de navegação de símbolos, **modo de exibição de classe**, **pesquisador de objetos**, **pesquisador de chamadas** e **Localizar resultados de símbolos**, passar solicitações para novos dados para o Gerenciador de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] objetos. O Gerenciador de objetos localiza as bibliotecas apropriadas e solicita novas listas de símbolos. As bibliotecas respondem fornecendo os dados solicitados ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de objetos por meio da <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> interface. O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de objetos chama os métodos na <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> interface para obter os dados e usa-os para preencher ou atualizar as exibições das ferramentas de navegação de símbolos.

 Uma biblioteca pode receber solicitações de dados quando a ferramenta é chamada, o nó é expandido ou a exibição é atualizada. Quando uma ferramenta de navegação de símbolos é invocada pela primeira vez, o Gerenciador de objetos solicita a biblioteca para fornecer a lista de nível superior. Quando o usuário expande um nó de lista, a biblioteca fornece uma lista de filhos sob esse nó. Cada consulta do Gerenciador de objetos contém um índice do item de interesse. Para exibir uma nova lista, o Gerenciador de objetos deve determinar quantos itens estão na lista, o tipo dos itens, seus nomes, acessibilidade e outras propriedades.

> [!NOTE]
> Os exemplos de código gerenciado a seguir demonstram como fornecer listas de símbolos por meio da implementação da <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> interface. O Gerenciador de objetos chama os métodos nesta interface e usa os dados obtidos para popular ou atualizar as ferramentas de navegação de símbolos.
>
> Para a implementação do provedor de símbolo de código nativo, use a <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectList2> interface.

## <a name="to-provide-lists-of-symbols-to-the-object-manager"></a>Para fornecer listas de símbolos para o Gerenciador de objetos

1. Obtenha o número de itens na lista de símbolos implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetItemCount%2A> método. O exemplo a seguir demonstra como o Gerenciador de objetos obtém as informações sobre o número de itens na lista.

    ```vb
    Protected m_Methods As System.Collections.Generic.SortedList(Of String, Method) = New System.Collections.Generic.SortedList(Of String, Method)()

    Public Function GetItemCount(ByRef pCount As UInteger) As Integer
        pCount = CUInt(m_Methods.Count)
        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function
    ```

    ```csharp
    protected System.Collections.Generic.SortedList<string, Method> m_Methods = new System.Collections.Generic.SortedList<string, Method>();

    public int GetItemCount(out uint pCount)
    {
        pCount = (uint)m_Methods.Count;
        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    ```

2. Obtenha informações sobre as categorias e os atributos de um determinado item de lista implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetCategoryField2%2A> método. As categorias de item são especificadas na <xref:Microsoft.VisualStudio.Shell.Interop.LIB_CATEGORY> enumeração. O exemplo a seguir demonstra como o Gerenciador de objetos obtém atributos de itens para uma determinada categoria.

    ```vb
    Public Function GetCategoryField2(ByVal index As UInteger, ByVal Category As Integer, ByRef pfCatField As UInteger) As Integer
        pfCatField = 0

        Select Case CType(Category, LIB_CATEGORY)
            Case LIB_CATEGORY.LC_MEMBERTYPE
                pfCatField = CUInt(_LIBCAT_MEMBERTYPE.LCMT_METHOD)

            Case LIB_CATEGORY.LC_MEMBERACCESS
                Dim method As Method = m_Methods.Values(CInt(Fix(index)))

                If method.IsPublic Then
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PUBLIC)
                ElseIf method.IsPrivate Then
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PRIVATE)
                ElseIf method.IsFamily Then
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PROTECTED)
                ElseIf method.IsFamilyOrAssembly Then
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PROTECTED) Or CUInt(_LIBCAT_MEMBERACCESS.LCMA_PACKAGE)
                Else
                    ' Show everything else as internal.
                    pfCatField = CUInt(_LIBCAT_MEMBERACCESS.LCMA_PACKAGE)
                End If

            Case LIB_CATEGORY.LC_VISIBILITY
                pfCatField = CUInt(_LIBCAT_VISIBILITY.LCV_VISIBLE)

            Case LIB_CATEGORY.LC_LISTTYPE
                pfCatField = CUInt(_LIB_LISTTYPE.LLT_MEMBERS)

            Case Else
                Return Microsoft.VisualStudio.VSConstants.S_FALSE
        End Select
        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int GetCategoryField2(uint index, int Category, out uint pfCatField)
    {
        pfCatField = 0;

        switch ((LIB_CATEGORY)Category)
        {
            case LIB_CATEGORY.LC_MEMBERTYPE:
                pfCatField = (uint)_LIBCAT_MEMBERTYPE.LCMT_METHOD;
                break;

            case LIB_CATEGORY.LC_MEMBERACCESS:
                {
                    Method method = m_Methods.Values[(int)index];

                    if (method.IsPublic)
                    {
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PUBLIC;
                    }
                    else if (method.IsPrivate)
                    {
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PRIVATE;
                    }
                    else if (method.IsFamily)
                    {
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PROTECTED;
                    }
                    else if (method.IsFamilyOrAssembly)
                    {
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PROTECTED |
                                     (uint)_LIBCAT_MEMBERACCESS.LCMA_PACKAGE;
                    }
                    else
                    {
                        // Show everything else as internal.
                        pfCatField = (uint)_LIBCAT_MEMBERACCESS.LCMA_PACKAGE;
                    }
                }
                break;

            case LIB_CATEGORY.LC_VISIBILITY:
                pfCatField = (uint)_LIBCAT_VISIBILITY.LCV_VISIBLE;
                break;

            case LIB_CATEGORY.LC_LISTTYPE:
                pfCatField = (uint)_LIB_LISTTYPE.LLT_MEMBERS;
                break;

            default:
                return Microsoft.VisualStudio.VSConstants.S_FALSE;
        }
        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    ```

3. Obtenha a representação de texto de um determinado item de lista implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetTextWithOwnership%2A> método. O exemplo a seguir demonstra como obter um nome completo de um determinado item.

    ```vb
    Public Function GetTextWithOwnership(<System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.OLE.Interop.ULONG")> ByVal index As UInteger, <System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.Shell.Interop.VSTREETEXTOPTIONS")> ByVal tto As Microsoft.VisualStudio.Shell.Interop.VSTREETEXTOPTIONS, <System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.OLE.Interop.WCHAR")> ByRef ppszText As String) As Integer
        ppszText = m_Methods.Values(CInt(Fix(index))).FullName
        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function
    ```

    ```csharp
    public int GetTextWithOwnership([System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.OLE.Interop.ULONG")] uint index, [System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.Shell.Interop.VSTREETEXTOPTIONS")] Microsoft.VisualStudio.Shell.Interop.VSTREETEXTOPTIONS tto, [System.Runtime.InteropServices.ComAliasNameAttribute("Microsoft.VisualStudio.OLE.Interop.WCHAR")] out string ppszText)
    {
        ppszText = m_Methods.Values[(int)index].FullName;
        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    ```

4. Obtenha as informações de ícone de um determinado item de lista implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetDisplayData%2A> método. O ícone representa o tipo (classe, método e assim por diante) e acessibilidade (privado, público e assim por diante) de um item de lista. O exemplo a seguir demonstra como obter as informações de ícone com base em um determinado atributo de item.

    ```vb
    Public Overridable Function GetDisplayData(ByVal index As UInteger, ByVal pData As Microsoft.VisualStudio.Shell.Interop.VSTREEDISPLAYDATA()) As Integer
        If pData Is Nothing Then
            Return Microsoft.VisualStudio.VSConstants.E_INVALIDARG
        End If

        Dim method As Method = m_Methods.Values(CInt(Fix(index)))

        Dim iImage As Integer = 12 * 6 ' See env\inc\OMGlyphs.h.

        Const OM_GLYPH_ACC_PUBLIC As Integer = 0
        Const OM_GLYPH_ACC_INTERNAL As Integer = 1
        Const OM_GLYPH_ACC_PROTECTED As Integer = 3
        Const OM_GLYPH_ACC_PRIVATE As Integer = 4

        If method.IsPublic Then
            iImage += OM_GLYPH_ACC_PUBLIC
        ElseIf method.IsPrivate Then
            iImage += OM_GLYPH_ACC_PRIVATE
        ElseIf method.IsFamily Then
            iImage += OM_GLYPH_ACC_PROTECTED
        ElseIf method.IsFamilyOrAssembly Then
            iImage += OM_GLYPH_ACC_PROTECTED
        Else
            iImage += OM_GLYPH_ACC_INTERNAL
        End If

        pData(0).Image = CUShort(iImage)
        pData(0).SelectedImage = CUShort(iImage)

        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function
    ```

    ```csharp
    public virtual int GetDisplayData(uint index, Microsoft.VisualStudio.Shell.Interop.VSTREEDISPLAYDATA[] pData)
    {
        if (pData == null)
        {
            return Microsoft.VisualStudio.VSConstants.E_INVALIDARG;
        }

        Method method = m_Methods.Values[(int)index];

        int iImage = 12 * 6;    // See env\inc\OMGlyphs.h.

        const int OM_GLYPH_ACC_PUBLIC = 0;
        const int OM_GLYPH_ACC_INTERNAL = 1;
        const int OM_GLYPH_ACC_PROTECTED = 3;
        const int OM_GLYPH_ACC_PRIVATE = 4;

        if (method.IsPublic)
        {
            iImage += OM_GLYPH_ACC_PUBLIC;
        }
        else if (method.IsPrivate)
        {
            iImage += OM_GLYPH_ACC_PRIVATE;
        }
        else if (method.IsFamily)
        {
            iImage += OM_GLYPH_ACC_PROTECTED;
        }
        else if (method.IsFamilyOrAssembly)
        {
            iImage += OM_GLYPH_ACC_PROTECTED;
        }
        else
        {
            iImage += OM_GLYPH_ACC_INTERNAL;
        }

        pData[0].Image = (ushort)iImage;
        pData[0].SelectedImage = (ushort)iImage;

        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    ```

5. Obtenha as informações sobre se um determinado item de lista é expansível implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetExpandable3%2A> método. O exemplo a seguir demonstra como obter as informações sobre se um determinado item pode ser expandido.

    ```vb
    Public Function GetExpandable(ByVal index As UInteger, ByRef pfExpandable As Integer) As Integer
        pfExpandable = Microsoft.VisualStudio.VSIP.Samples.CallBrowser.Constants.TRUE
        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function

    Public Function GetExpandable3(ByVal index As UInteger, ByVal ListTypeExcluded As UInteger, ByRef pfExpandable As Integer) As Integer
        Return GetExpandable(index, pfExpandable)
    End Function
    ```

    ```csharp
    public int GetExpandable(uint index, out int pfExpandable)
    {
        pfExpandable = Microsoft.VisualStudio.VSIP.Samples.CallBrowser.Constants.TRUE;
        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    public int GetExpandable3(uint index, uint ListTypeExcluded, out int pfExpandable)
    {
        return GetExpandable(index, out pfExpandable);
    }

    ```

6. Obtenha uma lista de símbolos filho de um determinado item de lista implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetList2%2A> método. O exemplo a seguir demonstra como obter uma lista de símbolos filho de um determinado item para grafos de **chamada** ou de **chamadores** .

    ```vb
    ' Call graph list.
    Public Class CallsList
        Inherits ResultsList
        Implements Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2
        Public Sub New(ByVal library As Library)
            MyBase.New(library)
        End Sub

        Public Function GetList2(ByVal index As UInteger, ByVal ListType As UInteger, ByVal flags As UInteger, ByVal pobSrch As Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2(), ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer
            Return MyBase.GetCallsList(index, ppList)
        End Function
    End Class

    ' Callers graph list.
    Public Class CallersList
        Inherits ResultsList
        Implements Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2
        Public Sub New(ByVal library As Library)
            MyBase.New(library)
        End Sub

        Public Function GetList2(ByVal index As UInteger, ByVal ListType As UInteger, ByVal flags As UInteger, ByVal pobSrch As Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2(), ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer
            Return MyBase.GetCallersList(index, ppList)
        End Function
    End Class

    ' Call graph list.
    Public Function GetCallsList(ByVal index As UInteger, ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer
        ppList = Nothing
        Dim callsList As ResultsList = New CallsList(m_Library)

        Dim method As Method = m_Methods.Values(CInt(Fix(index)))
        Dim strMethod As String = method.m_strPrototype

        Dim Calls As System.Collections.Generic.List(Of CallInstance) = m_Library.CallGraph.GetCallGraph(method)

        For i As Integer = 0 To Calls.Count - 1
            Dim caller As Method = Calls(i).m_Target
            callsList.AddMethod(caller)
        Next i

        ppList = CType(callsList, Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2)
        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function

    ' Callers graph list.
    Public Function GetCallersList(ByVal index As UInteger, ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer
        ppList = Nothing
        Dim callersList As ResultsList = New CallersList(m_Library)

        Dim method As Method = m_Methods.Values(CInt(Fix(index)))
        Dim strMethod As String = method.m_strPrototype

        Dim Callers As System.Collections.Generic.List(Of CallInstance) = m_Library.CallGraph.GetCallersGraph(method)

        For i As Integer = 0 To Callers.Count - 1
            Dim caller As Method = Callers(i).m_Source
            callersList.AddMethod(caller)
        Next i

        ppList = CType(callersList, Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2)
        Return Microsoft.VisualStudio.VSConstants.S_OK
    End Function

    ' Get a child list of symbols for a given list item.
    Public Function GetList2(ByVal index As UInteger, ByVal ListType As UInteger, ByVal flags As UInteger, ByVal pobSrch As Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2(), ByRef ppList As Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2) As Integer
        ppList = Nothing

        Dim method As Method = m_Methods.Values(CInt(Fix(index)))
        Dim strMethod As String = method.m_strPrototype

        ' Determine if the list belongs to Call or Callers graphs.
        If CUInt(m_nFlags And CUInt(Microsoft.VisualStudio.Shell.Interop._VSOBSEARCHOPTIONS2.VSOBSO_CALLSFROM)) > 0 Then
            ' Build the list for the Call graph.
            Return MyBase.GetCallsList(index, ppList)
        ElseIf CUInt(m_nFlags And CUInt(Microsoft.VisualStudio.Shell.Interop._VSOBSEARCHOPTIONS2.VSOBSO_CALLSTO)) > 0 Then
            ' Build the list for the Callers graph.
            Return MyBase.GetCallersList(index, ppList)
        End If

        Return Microsoft.VisualStudio.VSConstants.E_FAIL
    End Function
    ```

    ```csharp
    // Call graph list.
    public class CallsList :
        ResultsList,
        Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2
    {
        public CallsList(Library library) :
            base(library)
        {
        }

        public int GetList2(uint index, uint ListType, uint flags, Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2[] pobSrch, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)
        {
            return base.GetCallsList(index, out ppList);
        }
    }

    // Callers graph list.
    public class CallersList :
        ResultsList,
        Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2
    {
        public CallersList(Library library) :
            base(library)
        {
        }

        public int GetList2(uint index, uint ListType, uint flags, Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2[] pobSrch, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)
        {
            return base.GetCallersList(index, out ppList);
        }
    }

    // Call graph list.
    public int GetCallsList(uint index, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)
    {
        ppList = null;
        ResultsList callsList = new CallsList(m_Library);

        Method method = m_Methods.Values[(int)index];
        string strMethod = method.m_strPrototype;

        System.Collections.Generic.List<CallInstance> Calls = m_Library.CallGraph.GetCallGraph(method);

        for (int i = 0; i < Calls.Count; i++)
        {
            Method caller = Calls[i].m_Target;
            callsList.AddMethod(caller);
        }

        ppList = (Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2)(callsList);
        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    // Callers graph list.
    public int GetCallersList(uint index, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)
    {
        ppList = null;
        ResultsList callersList = new CallersList(m_Library);

        Method method = m_Methods.Values[(int)index];
        string strMethod = method.m_strPrototype;

        System.Collections.Generic.List<CallInstance> Callers = m_Library.CallGraph.GetCallersGraph(method);

        for (int i = 0; i < Callers.Count; i++)
        {
            Method caller = Callers[i].m_Source;
            callersList.AddMethod(caller);
        }

        ppList = (Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2)(callersList);
        return Microsoft.VisualStudio.VSConstants.S_OK;
    }

    // Get a child list of symbols for a given list item.
    public int GetList2(uint index, uint ListType, uint flags, Microsoft.VisualStudio.Shell.Interop.VSOBSEARCHCRITERIA2[] pobSrch, out Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2 ppList)
    {
        ppList = null;

        Method method = m_Methods.Values[(int)index];
        string strMethod = method.m_strPrototype;

        // Determine if the list belongs to Call or Callers graphs.
        if ((uint)(m_nFlags & (uint)Microsoft.VisualStudio.Shell.Interop._VSOBSEARCHOPTIONS2.VSOBSO_CALLSFROM) > 0)
        {
            // Build the list for the Call graph.
            return base.GetCallsList(index, out ppList);
        }
        else if ((uint)(m_nFlags & (uint)Microsoft.VisualStudio.Shell.Interop._VSOBSEARCHOPTIONS2.VSOBSO_CALLSTO) > 0)
        {
            // Build the list for the Callers graph.
            return base.GetCallersList(index, out ppList);
        }

        return Microsoft.VisualStudio.VSConstants.E_FAIL;
    }

    ```

## <a name="see-also"></a>Confira também
- [Símbolo de suporte – ferramentas de navegação](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [Como registrar uma biblioteca com o Gerenciador de objetos](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [Como identificar símbolos em uma biblioteca](../../extensibility/internals/how-to-identify-symbols-in-a-library.md)
- [Extensibilidade do serviço de linguagem herdada](../../extensibility/internals/legacy-language-service-extensibility.md)
