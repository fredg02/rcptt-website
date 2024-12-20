---
title: Define EMF model for ShowViews command
slug: define-emf-model
sidebar: userguide
menu:
  sidebar:
      parent: ecl
layout: doc
---

## Create Ecore Model
- Create **model** folder in the root directory of your plugin
- Right click on model folder and select **New > Other... > Eclipse Modeling Framework > Ecore Model > Next**
- Choose a name for your model. In our case it will be **view.ecore**
- Press {{< uielement >}}Finish{{< / uielement >}}


Created model will be opened in the editor and we need to specify package details using Properties View as shown below:

![](screenshot-new-command-guide-2.png)

### Add ShowViews command class

We need to create new EClass for our ECL command.
- Create new EClass and change its name to **ShowViews** in the Properties View
- Right click your editor and select {{< uielement >}}Load Resource...{{< / uielement >}} menu item
- In the opened dialog press {{< uielement >}}Browse Workspace...{{< / uielement >}} button
- Select **org.eclipse.rcptt.ecl.core/model/ecl.ecore** package:

![](screenshot-new-command-guide-3.png)
- Add **Command** from the ECL package as a super type to your ShowViews class.

### Add View class

Now we need one more EClass to represent Eclipse View details.
- Create EClass called **View**
- Add three string attributes to this class: **id**, **label** and **description**

![](../screenshot-new-command-guide-4.png)

### Generate java sources

We need to create generation model to build java sources for our model.
- Right click on the **view.ecore** file in the **Package Explorer** and select **New > Other... > Eclipse Modeling Framework > EMF Generator Model > Next**
- Default **view.genmodel** name for generator model is OK for us, so just press {{< uielement >}}Next{{< / uielement >}}
- Select Ecore model item and press {{< uielement >}}Next{{< / uielement >}}
- Click {{< uielement >}}Load{{< / uielement >}} button and press {{< uielement >}}Next{{< / uielement >}} again
- Select view.ecore as a root package and add ECL and EMF packages as references. Press {{< uielement >}}Finish{{< / uielement >}}

![](screenshot-new-command-guide-5.png)
- In the opened editor select View package and change base package attribute to **org.eclipse.rcptt.ecl.example**:

![](screenshot-new-command-guide-6.png)

- Right click View package and select {{< uielement >}}Generate Model Core{{< / uielement >}}. All necessary java sources will be generated.

>Please note, that you should set the same runtime version for **view.genmodel** as you have for **ecl.genmodel** in **org.eclipse.rcptt.ecl.core**.