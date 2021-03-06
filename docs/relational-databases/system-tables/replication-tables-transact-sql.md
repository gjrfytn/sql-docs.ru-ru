---
title: Таблицы репликации (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system tables [SQL Server], replication
- replication [SQL Server], system tables
ms.assetid: 5696ee73-5d7c-4f26-b7ee-6831c9c3edf7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e18c78f55b48061597abb0daa07ca9862cef5738
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207713"
---
# <a name="replication-tables-transact-sql"></a>Таблицы репликации (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Топология репликации поддерживается с помощью системных таблиц репликации. При конфигурации пользовательской базы данных в качестве издателя или подписчика в ходе репликации в базу данных добавляются системные таблицы. При удалении пользовательской базы данных из топологии репликации эти таблицы удаляются. Общие правила в отношении использования системных таблиц см. в разделе [системные таблицы &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md).  
  
## <a name="replication-tables"></a>Таблицы репликации  
 Ниже приведен список системных таблиц, используемых при репликации и сгруппированных по базам данных.  
  
### <a name="replication-tables-in-the-master-database"></a>Таблицы репликации в базе данных master  
  
|||  
|-|-|  
|[MSreplication_options &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msreplication-options-transact-sql.md)||  
  
### <a name="replication-tables-in-the-msdb-database"></a>Таблицы репликации в базе данных msdb  
  
|||  
|-|-|  
|[MSagentparameterlist](../../relational-databases/system-tables/msagentparameterlist-transact-sql.md)|[MSdbms_map](../../relational-databases/system-tables/msdbms-map-transact-sql.md)|  
|[MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md)|[MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md)|  
|[MSdbms_datatype](../../relational-databases/system-tables/msdbms-datatype-transact-sql.md)|[sysreplicationalerts](../../relational-databases/system-tables/sysreplicationalerts-transact-sql.md)|  
|[MSdbms_datatype_mapping](../../relational-databases/system-tables/msdbms-datatype-mapping-transact-sql.md)||  
  
### <a name="replication-tables-in-the-distribution-database"></a>Таблицы репликации в базе данных распространителя  
  
|||  
|-|-|  
|[MSagent_parameters](../../relational-databases/system-tables/msagent-parameters-transact-sql.md)|[MSpublicationthresholds](../../relational-databases/system-tables/mspublicationthresholds-transact-sql.md)|  
|[MSagent_profiles](../../relational-databases/system-tables/msagent-profiles-transact-sql.md)|[MSpublisher_databases](../../relational-databases/system-tables/mspublisher-databases-transact-sql.md)|  
|[MSarticles](../../relational-databases/system-tables/msarticles-transact-sql.md)|[MSreplication_objects](../../relational-databases/system-tables/msreplication-objects-transact-sql.md)|  
|[MScached_peer_lsns](../../relational-databases/system-tables/mscached-peer-lsns-transact-sql.md)|[MSreplication_subscriptions](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)|  
|[MSdistpublishers](../../relational-databases/system-tables/msdistpublishers-transact-sql.md)|[MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md)|  
|[MSdistribution_agents](../../relational-databases/system-tables/msdistribution-agents-transact-sql.md)|[MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md)|  
|[MSdistribution_history](../../relational-databases/system-tables/msdistribution-history-transact-sql.md)|[MSrepl_originators](../../relational-databases/system-tables/msrepl-originators-transact-sql.md)|  
|[MSdistributiondbs](../../relational-databases/system-tables/msdistributiondbs-transact-sql.md)|[MSrepl_transactions](../../relational-databases/system-tables/msrepl-transactions-transact-sql.md)|  
|[MSdistributor](../../relational-databases/system-tables/msdistributor-transact-sql.md)|[MSrepl_version](../../relational-databases/system-tables/msrepl-version-transact-sql.md)|  
|[MSlogreader_agents](../../relational-databases/system-tables/mslogreader-agents-transact-sql.md)|[MSsnapshot_agents](../../relational-databases/system-tables/mssnapshot-agents-transact-sql.md)|  
|[MSlogreader_history](../../relational-databases/system-tables/mslogreader-history-transact-sql.md)|[MSsnapshot_history](../../relational-databases/system-tables/mssnapshot-history-transact-sql.md)|  
|[MSmerge_agents](../../relational-databases/system-tables/msmerge-agents-transact-sql.md)|[MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md)|  
|[MSmerge_history](../../relational-databases/system-tables/msmerge-history-transact-sql.md)|[MSsubscriber_schedule](../../relational-databases/system-tables/mssubscriber-schedule-transact-sql.md)|  
|[MSmerge_sessions](../../relational-databases/system-tables/msmerge-sessions-transact-sql.md)|[MSsubscriptions](../../relational-databases/system-tables/mssubscriptions-transact-sql.md)|  
|[MSmerge_subscriptions](../../relational-databases/system-tables/msmerge-subscriptions-transact-sql.md)|[MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)|  
|[MSpublication_access](../../relational-databases/system-tables/mspublication-access-transact-sql.md)|[MStracer_history](../../relational-databases/system-tables/mstracer-history-transact-sql.md)|  
|[MSpublications](../../relational-databases/system-tables/mspublications-transact-sql.md)|[MStracer_tokens](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md)|  
  
 Эти таблицы в базе данных распространителя используются для репликации данных, отличными от [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] издателя. Дополнительные сведения см. в разделе [издателей, не SQL Server](../../relational-databases/replication/non-sql/non-sql-server-publishers.md).  
  
|||  
|-|-|  
|[IHarticles](../../relational-databases/system-tables/iharticles-transact-sql.md)|[IHpublishercolumnindexes](../../relational-databases/system-tables/ihpublishercolumnindexes-transact-sql.md)|  
|[IHcolumns](../../relational-databases/system-tables/ihcolumns-transact-sql.md)|[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)|  
|[IHconstrainttypes](../../relational-databases/system-tables/ihconstrainttypes-transact-sql.md)|[IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md)|  
|[IHindextypes](../../relational-databases/system-tables/ihindextypes-transact-sql.md)|[IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md)|  
|[IHindextypes](../../relational-databases/system-tables/ihindextypes-transact-sql.md)|[IHpublishers](../../relational-databases/system-tables/ihpublishers-transact-sql.md)|  
|[IHpublications](../../relational-databases/system-tables/ihpublications-transact-sql.md)|[IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md)|  
|[IHpublishercolumnconstraints](../../relational-databases/system-tables/ihpublishercolumnconstraints-transact-sql.md)|[IHsubscriptions](../../relational-databases/system-tables/ihsubscriptions-transact-sql.md)|  
  
### <a name="replication-tables-in-the-publication-database"></a>Таблицы репликации в базе данных публикации  
  
|||  
|-|-|  
|[conflict_\<схема > _\<таблицы >](../../relational-databases/system-tables/conflict-schema-table-transact-sql.md)|[MSpeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md)|  
|[MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md)|[MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md)|  
|[MSdynamicsnapshotviews](../../relational-databases/system-tables/msdynamicsnapshotviews-transact-sql.md)|[MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md)|  
|[MSmerge_altsyncpartners](../../relational-databases/system-tables/msmerge-altsyncpartners-transact-sql.md)|[MSpeer_request](../../relational-databases/system-tables/mspeer-request-transact-sql.md)|  
|[MSmerge_conflicts_info](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)|[MSpeer_response](../../relational-databases/system-tables/mspeer-response-transact-sql.md)|  
|[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)|[MSpub_identity_range](../../relational-databases/system-tables/mspub-identity-range-transact-sql.md)|  
|[MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md)|[sysarticlecolumns](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)|  
|[MSmerge_dynamic_snapshots](../../relational-databases/system-tables/msmerge-dynamic-snapshots-transact-sql.md)|[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)|  
|[MSmerge_errorlineage](../../relational-databases/system-tables/msmerge-errorlineage-transact-sql.md)|[sysarticleupdates](../../relational-databases/system-tables/sysarticleupdates-transact-sql.md)|  
|[MSmerge_generation_partition_mappings](../../relational-databases/system-tables/msmerge-generation-partition-mappings-transact-sql.md)|[sysmergearticlecolumns](../../relational-databases/system-tables/sysmergearticlecolumns-transact-sql.md)|  
|[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)|[sysmergearticles](../../relational-databases/system-tables/sysmergearticles-transact-sql.md)|  
|[MSmerge_identity_range](../../relational-databases/system-tables/msmerge-identity-range-transact-sql.md)|[sysmergepartitioninfo](../../relational-databases/system-tables/sysmergepartitioninfo-transact-sql.md)|  
|[MSmerge_metadataaction_request](../../relational-databases/system-tables/msmerge-metadataaction-request-transact-sql.md)|[sysmergepublications](../../relational-databases/system-tables/sysmergepublications-transact-sql.md)|  
|[MSmerge_partition_groups](../../relational-databases/system-tables/msmerge-partition-groups-transact-sql.md)|[sysmergeschemaarticles](../../relational-databases/system-tables/sysmergeschemaarticles-transact-sql.md)|  
|[MSmerge_past_partition_mappings](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)|[sysmergeschemachange](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)|  
|[MSmerge_replinfo](../../relational-databases/system-tables/msmerge-replinfo-transact-sql.md)|[sysmergesubscriptions](../../relational-databases/system-tables/sysmergesubscriptions-transact-sql.md)|  
|[MSmerge_settingshistory](../../relational-databases/system-tables/msmerge-settingshistory-transact-sql.md)|[sysmergesubsetfilters](../../relational-databases/system-tables/sysmergesubsetfilters-transact-sql.md)|  
|[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)|[syspublications](../../relational-databases/system-tables/syspublications-transact-sql.md)|  
|[MSpeer_conflictdetectionconfigrequest](../../relational-databases/system-tables/mspeer-conflictdetectionconfigrequest-transact-sql.md)|[sysschemaarticles](../../relational-databases/system-tables/sysschemaarticles-transact-sql.md)|  
|[MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md)|[syssubscriptions](../../relational-databases/system-tables/syssubscriptions-transact-sql.md)|  
|[MSpeer_lsns](../../relational-databases/system-tables/mspeer-lsns-transact-sql.md)|["systranschemas"](../../relational-databases/system-views/systranschemas-transact-sql.md)|  
  
### <a name="replication-tables-in-the-subscription-database"></a>Таблицы репликации в базе данных подписки  
  
|||  
|-|-|  
|[MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md)|[MSmerge_settingshistory](../../relational-databases/system-tables/msmerge-settingshistory-transact-sql.md)|  
|[MSdynamicsnapshotviews](../../relational-databases/system-tables/msdynamicsnapshotviews-transact-sql.md)|[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)|  
|[MSmerge_altsyncpartners](../../relational-databases/system-tables/msmerge-altsyncpartners-transact-sql.md)|[MSpeer_lsns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mspeer-lsns-transact-sql.md)|  
|[MSmerge_conflicts_info](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)|[MSrepl_queuedtraninfo](../../relational-databases/system-tables/msrepl-queuedtraninfo-transact-sql.md)|  
|[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)|[MSsnapshotdeliveryprogress](../../relational-databases/system-tables/mssnapshotdeliveryprogress-transact-sql.md)|  
|[MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md)|[MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)|  
|[MSmerge_dynamic_snapshots](../../relational-databases/system-tables/msmerge-dynamic-snapshots-transact-sql.md)|[sysmergearticlecolumns](../../relational-databases/system-tables/sysmergearticlecolumns-transact-sql.md)|  
|[MSmerge_errorlineage](../../relational-databases/system-tables/msmerge-errorlineage-transact-sql.md)|[sysmergearticles](../../relational-databases/system-tables/sysmergearticles-transact-sql.md)|  
|[MSmerge_generation_partition_mappings](../../relational-databases/system-tables/msmerge-generation-partition-mappings-transact-sql.md)|[sysmergepartitioninfo](../../relational-databases/system-tables/sysmergepartitioninfo-transact-sql.md)|  
|[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)|[sysmergepublications](../../relational-databases/system-tables/sysmergepublications-transact-sql.md)|  
|[MSmerge_identity_range](../../relational-databases/system-tables/msmerge-identity-range-transact-sql.md)|[sysmergeschemaarticles](../../relational-databases/system-tables/sysmergeschemaarticles-transact-sql.md)|  
|[MSmerge_metadataaction_request](../../relational-databases/system-tables/msmerge-metadataaction-request-transact-sql.md)|[sysmergeschemachange](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)|  
|[MSmerge_partition_groups](../../relational-databases/system-tables/msmerge-partition-groups-transact-sql.md)|[sysmergesubscriptions](../../relational-databases/system-tables/sysmergesubscriptions-transact-sql.md)|  
|[MSmerge_past_partition_mappings](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)|[sysmergesubsetfilters](../../relational-databases/system-tables/sysmergesubsetfilters-transact-sql.md)|  
|[MSmerge_replinfo](../../relational-databases/system-tables/msmerge-replinfo-transact-sql.md)|["systranschemas"](../../relational-databases/system-views/systranschemas-transact-sql.md)|  
  
## <a name="see-also"></a>См. также  
 [Настройка публикации и распространения](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Disable Publishing and Distribution](../../relational-databases/replication/disable-publishing-and-distribution.md)  (Отключение публикации и распространения)  
 [Представления репликации (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
