# Chaos_excel

当前顶层工作簿按业务合并为6本，原25本单页工作簿连同Unity元数据保留在 `_archive_single_sheet/`，不再对归档目录执行导表。

| 工作簿 | 页签 |
| --- | --- |
| 村庄养成.xlsx | Building、Effect、FamilyTree、FamilyTreeEffect、Item、Retainer、VillageScene、VillageText |
| 局内地图.xlsx | ChunkSlot、ChunkSocket、MapBiome、MapChunk、MapGeneration、MapLoading、MapPreset、PresetLayer、RunBehavior、RunInteraction、Drop |
| 进程与通用.xlsx | Era、Depth、LoadingTable、TestTable |
| 局外事务.xlsx | Event、EventOption、OfficeTaskConfig、OfficeTaskOptionConfig、OfficeEraGateConfig |
| WorldMap_世界观地图表.xlsx | 世界观绘图工具源表，保留原工具工作方式 |
| WorldFaction_势力范围配置表.xlsx | 势力绘图工具源表，保留原工具工作方式 |

各页B1填写实际类名或旧基名（Building会补为BuildingConfig，OfficeTaskConfig不重复加后缀），B2填写IsConfig或IsData。第3行备注、第4行字段、第5行端标记、第6行类型、第7行起为数据。空页和说明页可跳过，启用页的非法数据会定位报错。

沿用Unity原ExcelTool菜单导表；每页独立输出，JSON规范为“完整工作簿基名_完整类名.json”，例如 `局外事务_OfficeTaskConfig.json`。生成C#类名保持BuildingConfig等既有类型。运行时按ConfigTableIndex.json索引加载类型，不手写旧物理JSON路径。索引现有31项，含30页导出与1张派生势力名称表；该名称表仍由原绘图工具生成。

局外任务字段、资源码、倒计时与时代门槛口径见[系统30](../../Chaos_Story/Story/02_系统策划/30_办事单位四类任务与配置管线.md)。OfficeEraGateConfig.Era是当前时代（1约束1→2），样例门槛及尚未接战斗的遭袭样例默认关闭。配置中的任务为首轮可替换示例，不代表真实历史法令。

导出先验证整批，再发布JSON、C#和索引；中途写入失败回滚。旧28张JSON数据已逐表核对不变，旧资产重命名保留GUID。不要再次导入归档旧表来制造同类型重复，也不要手改生成JSON/C#。
