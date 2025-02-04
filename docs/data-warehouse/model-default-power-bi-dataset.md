---
title: Data modeling in the default Power BI dataset
description: Learn how to model your data in the default Power BI dataset in Microsoft Fabric.
author: salilkanade
ms.author: salilkanade
ms.reviewer: wiassaf
ms.date: 05/23/2023
ms.topic: conceptual
ms.custom: build-2023
ms.search.form: Model view # This article's title should not change. If so, contact engineering.
---
# Data modeling in the default Power BI dataset in Microsoft Fabric

**Applies to:** [!INCLUDE[fabric-se-and-dw](includes/applies-to-version/fabric-se-and-dw.md)]

The default Power BI dataset inherits all relationships between entities defined in the model view and infers them as Power BI dataset relationships, when objects are enabled for BI (Power BI Reports). Inheriting the warehouse's business logic allows a warehouse developer or BI analyst to decrease the time to value towards building a useful semantic model and metrics layer for analytical business intelligence (BI) reports in Power BI, Excel, or external tools like Tableau that read the XMLA format.

While all constraints are translated to relationships, currently in Power BI, only one relationship can be active at a time, whereas multiple primary and foreign key constraints can be defined for warehouse entities and are shown visually in the diagram lines. The active Power BI relationship is represented with a solid line and the rest is represented with a dotted line. We recommend choosing the primary relationship as active for BI reporting purposes.

[!INCLUDE [preview-note](../includes/preview-note.md)]

## Data modeling properties

The following table provides a description of the properties available when using the model view diagram and creating relationships:

| **Column name** | **Description** |
|---|---|
| **FromObjectName** | Table/View name "From" which relationship is defined. |
| **ToObjectName** | Table/View name "To" which a relationship is defined. |
| **TypeOfRelationship** | Relationship cardinality, the possible values are: None, OneToOne, OneToMany, ManyToOne, and ManyToMany. |
| **SecurityFilteringBehavior** | Indicates how relationships influence filtering of data when evaluating row-level security expressions and is a Power BI specific semantic. The possible values are: OneDirection, BothDirections, and None. |
| **IsActive** | A Power BI specific semantic, and a boolean value that indicates whether the relationship is marked as Active or Inactive. This defines the default relationship behavior within the semantic model |
| **RelyOnReferentialIntegrity** | A boolean value that indicates whether the relationship can rely on referential integrity or not. |
| **CrossFilteringBehavior** | Indicates how relationships influence filtering of data and is Power BI specific. The possible values are: 1 - OneDirection, 2 - BothDirections, and 3 - Automatic. |

## Add or remove objects to the default Power BI dataset

In Power BI, a dataset is always required before any reports can be built, so the default Power BI dataset enables quick reporting capabilities on top of the warehouse. Within the warehouse, a user can add warehouse objects - tables or views to their default Power BI dataset. They can also add other semantic modeling properties, such as hierarchies and descriptions. These properties are then used to create the Power BI dataset's tables. Users can also remove objects from the default Power BI dataset.

To add objects such as tables or views to the default Power BI dataset, you have options:

1. Automatically add objects to the dataset, which happens by default with no user intervention needed.

1. Manually add objects to the dataset.

The auto detect experience determines any tables or views and opportunistically adds them.

The manually detect option in the ribbon allows fine grained control of which object(s), such as tables and/or views, should be added to the default Power BI dataset:

- Select all
- Filter for tables or views
- Select specific objects

To remove objects, a user can use the manually select button in the ribbon and:

- Un-select all
- Filter for tables or views
- Un-select specific objects

> [!TIP]
> We recommend reviewing the objects enabled for BI and ensuring they have the correct logical relationships to ensure a smooth downstream reporting experience.

## Create a measure

A [measure](/power-bi/transform-model/desktop-measures) is a collection of standardized metrics. Similar to Power BI Desktop, the DAX editing experience in warehouse presents a rich editor complete with autocomplete for formulas (IntelliSense). The DAX editor enables you to easily develop measures right in warehouse, making it a more effective single source for business logic, semantics, and business critical calculations. 

1. To create a measure, select the **New Measure** button in the ribbon, as shown in the following image.

    :::image type="content" source="media\model-default-power-bi-dataset\table-explorer-ribbon.png" alt-text="Screenshot showing the table explorer and where the new measure button appears on the ribbon." lightbox="media\model-default-power-bi-dataset\table-explorer-ribbon.png":::

1. Enter the measure into the formula bar and specify the table and the column to which it applies. The formula bar lets you enter your measure. For detailed information on measures, see [Tutorial: Create your own measures in Power BI Desktop](/power-bi/transform-model/desktop-tutorial-create-measures).

1. You can expand the table to find the measure in the table.

## Hide elements from downstream reporting

You can hide elements of your warehouse from downstream reporting by right-clicking on the column or table you want to hide from the object explorer. 

Select **Hide** in **Report view** from the menu that appears to hide the item from downstream reporting.

:::image type="content" source="media\model-default-power-bi-dataset\hide-report-view-menu.png" alt-text="Screenshot showing where to find the hide option in the context menu." lightbox="media\model-default-power-bi-dataset\hide-report-view-menu.png":::

You can also hide the entire table and individual columns by using the **Model view** canvas options, as shown in the following image.

:::image type="content" source="media\model-default-power-bi-dataset\model-view-canvas.png" alt-text="Screenshot showing the model view canvas options." lightbox="media\model-default-power-bi-dataset\model-view-canvas.png":::

## Next steps

- [Define relationships in data models](model-default-power-bi-dataset.md)
- [Create reports in the Power BI service](reports-power-bi-service.md)
