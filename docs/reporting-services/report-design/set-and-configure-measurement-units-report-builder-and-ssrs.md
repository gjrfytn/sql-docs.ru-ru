---
title: "Задание и настройка единиц измерения (построитель отчетов и службы SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a15a96c3-7d2c-433e-a440-4ea051e967a9
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Задание и настройка единиц измерения (построитель отчетов и службы SSRS)
  В отчете [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] с разбиением на страницы индикаторы могут иметь два вида единиц измерения: процентные и числовые.   
    
  По умолчанию в качестве единиц измерения у индикаторов настроены процентные показатели. Таким образом, значения индикаторов, назначаемые для каждого значка в наборе индикаторов, определяются процентным диапазоном. Диапазоны в процентах равномерно разделяются по значкам в наборе индикаторов. Каждый значок отображает состояние индикатора. Процентные показатели для каждого значка в наборе индикаторов можно изменять, задавая различные начальные и конечные процентные значения. Индикаторы могут также автоматически определять минимальное и максимальное значения данных.  
  
 В качестве единицы измерения можно выбрать и числовое значение. В этом случае минимальное и максимальное значения не задаются. Вместо этого задаются только начальные и конечные значения для каждого значка, используемого индикатором.  
  
 Такие параметры, как единицы измерения, можно задать с помощью выражений. Дополнительные сведения см. в разделе [Выражения (построитель отчетов и службы SSRS)](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
## Использование числовых единиц измерения  
  
1.  Щелкните правой кнопкой мыши индикатор, который необходимо изменить, и выберите **Свойства индикатора**.  
  
2.  Нажмите кнопку **Значения и состояния** на левой панели.  
  
3.  В списке **Единица измерения состояний** щелкните **Числовая**.  
  
     Также можно нажать кнопку **Выражение** (*fx*), чтобы изменить выражение, которое задает значение параметра.  
  
4.  Для каждого значка в наборе индикаторов обновите значения в текстовых полях **Начало** и **Конец** .  
  
     Также можно нажать кнопку **Выражение** (*fx*), чтобы изменить выражение, которое задает значение параметров **Начало** и **Конец**.  
  
    > [!NOTE]  
    >  Значения в текстовых полях **Начало** и **Конец** должны быть числовыми.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Использование процентных единиц измерения  
  
1.  Щелкните правой кнопкой мыши индикатор, который необходимо изменить, и выберите **Свойства индикатора**.  
  
2.  Нажмите кнопку **Значения и состояния** на левой панели.  
  
3.  В списке **Единица измерения состояний** щелкните **Процентная**.  
  
     Также можно нажать кнопку **Выражение** (*fx*), чтобы изменить выражение, которое задает значение параметра.  
  
4.  Измените параметры **Минимум** и **Максимум** , чтобы вместо автоматического обнаружения минимальных и максимальных значений данных, используемых индикатором, применялись конкретные значения (необязательно). Значение **Минимум** должно быть меньше значения **Максимум**.  
  
    > [!NOTE]  
    >  Если минимальное и максимальное значения заданы явно, то индикатором используется заданный диапазон значений независимо от фактического минимального и максимального значения в данных. Таким образом, значения ниже минимума и выше максимума исключаются из оценки, с помощью которой определяется значок индикатора, отображаемый в отчете.  
  
     Также можно нажать кнопку **Выражение** (*fx*), чтобы изменить выражение, которое задает значения этого параметра.  
  
5.  Для каждого значка в наборе индикаторов обновите значения в текстовых полях **Начало** и **Конец** .  
  
     Также можно нажать кнопку **Выражение** (*fx*), чтобы изменить выражение, которое задает значение параметров **Начало** и **Конец**.  
  
    > [!NOTE]  
    >  Значения в текстовых полях **Начало** и **Конец** должны быть числовыми.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## См. также  
 [Индикаторы (построитель отчетов и службы SSRS)](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  