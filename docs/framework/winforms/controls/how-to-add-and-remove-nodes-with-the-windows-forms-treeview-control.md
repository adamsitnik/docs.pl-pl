---
title: 'Instrukcje: dodawanie i usuwanie węzłów za pomocą kontrolki TreeView formularzy systemu Windows'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], TreeView control
- TreeView control [Windows Forms], removing nodes
- tree nodes in TreeView control
- TreeView control [Windows Forms], adding nodes
ms.assetid: de1b82db-4905-449a-9f59-af271a6b6673
ms.openlocfilehash: 4cbb5fbdb24790a7ddbce5c38060703c7ba7024a
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/18/2019
ms.locfileid: "59326895"
---
# <a name="how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control"></a>Instrukcje: dodawanie i usuwanie węzłów za pomocą kontrolki TreeView formularzy systemu Windows
Formularze Windows <xref:System.Windows.Forms.TreeView> formant przechowuje węzłów najwyższego poziomu w jego <xref:System.Windows.Forms.TreeView.Nodes%2A> kolekcji. Każdy <xref:System.Windows.Forms.TreeNode> ma również swój własny <xref:System.Windows.Forms.TreeNode.Nodes%2A> kolekcji do przechowywania jego węzłów podrzędnych. Obie te właściwości kolekcji mają wartości typu <xref:System.Windows.Forms.TreeNodeCollection>, udostępniającej elementy członkowskie kolekcji standardowych, które pozwalają na dodawanie, usuwanie i rozmieszczanie węzłów o jeden poziom w hierarchii węzła.  
  
### <a name="to-add-nodes-programmatically"></a>Aby programowo dodać węzły  
  
1. Użyj <xref:System.Windows.Forms.TreeNodeCollection.Add%2A> metoda widok drzewa <xref:System.Windows.Forms.TreeView.Nodes%2A> właściwości.  
  
    ```vb  
    ' Adds new node as a child node of the currently selected node.  
    Dim newNode As TreeNode = New TreeNode("Text for new node")  
    TreeView1.SelectedNode.Nodes.Add(newNode)  
    ```  
  
    ```csharp  
    // Adds new node as a child node of the currently selected node.  
    TreeNode newNode = new TreeNode("Text for new node");  
    treeView1.SelectedNode.Nodes.Add(newNode);  
    ```  
  
    ```cpp  
    // Adds new node as a child node of the currently selected node.  
    TreeNode ^ newNode = new TreeNode("Text for new node");  
    treeView1->SelectedNode->Nodes->Add(newNode);  
    ```  
  
### <a name="to-remove-nodes-programmatically"></a>Aby programowo usunąć węzły  
  
1. Użyj <xref:System.Windows.Forms.TreeNodeCollection.Remove%2A> metoda widok drzewa <xref:System.Windows.Forms.TreeView.Nodes%2A> właściwości do usunięcia jeden węzeł lub <xref:System.Windows.Forms.TreeNodeCollection.Clear%2A> metodę, aby wyczyścić wszystkie węzły.  
  
    ```vb  
    ' Removes currently selected node, or root if nothing is selected.  
    TreeView1.Nodes.Remove(TreeView1.SelectedNode)  
    ' Clears all nodes.  
    TreeView1.Nodes.Clear()  
    ```  
  
    ```csharp  
    // Removes currently selected node, or root if nothing   
    // is selected.  
    treeView1.Nodes.Remove(treeView1.SelectedNode);  
    // Clears all nodes.  
    TreeView1.Nodes.Clear();  
    ```  
  
    ```cpp  
    // Removes currently selected node, or root if nothing  
    // is selected.  
    treeView1->Nodes->Remove(treeView1->SelectedNode);  
    // Clears all nodes.  
    treeView1->Nodes->Clear();  
    ```  
  
## <a name="see-also"></a>Zobacz także

- [TreeView, kontrolka](treeview-control-windows-forms.md)
- [TreeView, kontrolka — omówienie](treeview-control-overview-windows-forms.md)
- [Instrukcje: Ustawienie ikon dla kontrolki TreeView formularzy Windows](how-to-set-icons-for-the-windows-forms-treeview-control.md)
- [Instrukcje: Iterowanie wszystkich węzłów kontrolki TreeView formularzy Windows](how-to-iterate-through-all-nodes-of-a-windows-forms-treeview-control.md)
- [Instrukcje: Określanie, który węzeł TreeView został kliknięty](how-to-determine-which-treeview-node-was-clicked-windows-forms.md)
- [Instrukcje: Dodawanie niestandardowych informacji do TreeView lub ListView — formant (formularze Windows)](add-custom-information-to-a-treeview-or-listview-control-wf.md)
