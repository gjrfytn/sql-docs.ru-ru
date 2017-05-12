---
title: "Инструкции DDL, функции, хранимые процедуры и представления для полнотекстового поиска | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98c36715-4195-482e-a4a3-d93ff65b75f1
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d632e025a0a9fe18dbf42d773ff0e943263f4851
ms.lasthandoff: 04/11/2017

---
# <a name="full-text-search-ddl-functions-stored-procedures-and-views"></a>Инструкции полнотекстового поиска DDL, функции, хранимые процедуры и представления
  Содержит список инструкций Transact-SQL и объектов базы данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , поддерживающих полнотекстовый поиск, включая функцию поиска свойств.  
  
 Этот список не содержит устаревшие объекты.  
  
 Список объектов базы данных, которые поддерживают семантический поиск, см. в разделе [Semantic Search DDL, Functions, Stored Procedures, and Views](../../relational-databases/search/semantic-search-ddl-functions-stored-procedures-and-views.md).  
  
##  <a name="ddl"></a> Инструкции языка описания данных (DDL) Transact-SQL  
  
-   [CREATE FULLTEXT CATALOG (Transact-SQL)](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)  
  
-   [CREATE FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
-   [CREATE FULLTEXT STOPLIST (Transact-SQL)](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)  
  
-   [CREATE SEARCH PROPERTY LIST (Transact-SQL)](../../t-sql/statements/create-search-property-list-transact-sql.md)  
  
-   [ALTER FULLTEXT CATALOG (Transact-SQL)](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)  
  
-   [ALTER FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
-   [ALTER FULLTEXT STOPLIST (Transact-SQL)](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)  
  
-   [ALTER SEARCH PROPERTY LIST (Transact-SQL)](../../t-sql/statements/alter-search-property-list-transact-sql.md)  
  
-   [DROP FULLTEXT CATALOG (Transact-SQL)](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)  
  
-   [DROP FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/drop-fulltext-index-transact-sql.md)  
  
-   [DROP FULLTEXT STOPLIST (Transact-SQL)](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)  
  
-   [DROP SEARCH PROPERTY LIST (Transact-SQL)](../../t-sql/statements/drop-search-property-list-transact-sql.md)  
  
##  <a name="func"></a> Системные предикаты и функции  
  
-   [CONTAINS (Transact-SQL)](../../t-sql/queries/contains-transact-sql.md)  
  
-   [CONTAINSTABLE (Transact-SQL)](../../relational-databases/system-functions/containstable-transact-sql.md)  
  
-   [FREETEXT (Transact-SQL)](../../t-sql/queries/freetext-transact-sql.md)  
  
-   [FREETEXTTABLE (Transact-SQL)](../../relational-databases/system-functions/freetexttable-transact-sql.md)  
  
##  <a name="meta"></a> Системные функции метаданных  
  
-   [COLUMNPROPERTY (Transact-SQL)](../../t-sql/functions/columnproperty-transact-sql.md)  
  
-   [FULLTEXTCATALOGPROPERTY (Transact-SQL)](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)  
  
-   [FULLTEXTSERVICEPROPERTY (Transact-SQL)](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)  
  
-   [INDEXPROPERTY (Transact-SQL)](../../t-sql/functions/indexproperty-transact-sql.md)  
  
-   [OBJECTPROPERTY (Transact-SQL)](../../t-sql/functions/objectproperty-transact-sql.md)  
  
-   [OBJECTPROPERTYEX (Transact-SQL)](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
-   [SERVERPROPERTY (Transact-SQL)](../../t-sql/functions/serverproperty-transact-sql.md)  
  
##  <a name="proc"></a> Системные хранимые процедуры  
  
-   [sp_fulltext_keymappings (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)  
  
-   [sp_fulltext_load_thesaurus_file (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)  
  
-   [sp_fulltext_pendingchanges (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql.md)  
  
-   [sp_fulltext_service (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)  
  
-   [sp_help_fulltext_system_components (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)  
  
##  <a name="cat"></a> Системные представления — представления каталога  
  
-   [sys.fulltext_catalogs (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)  
  
-   [sys.fulltext_document_types (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md)  
  
-   [sys.fulltext_index_catalog_usages (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)  
  
-   [sys.fulltext_index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
-   [sys.fulltext_index_fragments (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)  
  
-   [sys.fulltext_indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
-   [sys.fulltext_languages (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)  
  
-   [sys.fulltext_stoplists (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
  
-   [sys.fulltext_stopwords (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
-   [sys.fulltext_system_stopwords (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-system-stopwords-transact-sql.md)  
  
-   [sys.registered_search_properties (Transact-SQL)](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)  
  
-   [sys.registered_search_property_lists (Transact-SQL)](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
##  <a name="dmv"></a> Системные представления — динамические административные представления  
  
-   [sys.dm_fts_active_catalogs (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md)  
  
-   [sys.dm_fts_fdhosts (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql.md)  
  
-   [sys.dm_fts_index_keywords (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
-   [sys.dm_fts_index_keywords_by_document (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
-   [sys.dm_fts_index_keywords_by_property (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
  
-   [sys.dm_fts_index_population (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
-   [sys.dm_fts_memory_buffers (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)  
  
-   [sys.dm_fts_memory_pools (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
  
-   [sys.dm_fts_outstanding_batches (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)  
  
-   [sys.dm_fts_parser (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)  
  
-   [sys.dm_fts_population_ranges (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql.md)  
  
  