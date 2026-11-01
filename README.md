# Chaos_excel 配置表

正式配置按小模块归纳，同一模块的基础表、关联表和文案放在同一本工作簿的多个简短中文页签中。所有正式xlsx放在本目录根层，编辑器专用 `_worldmap_tool/` 单独保留。

## 命名规则（2026-11-01最终确认）

- Excel：`英文表名_中文说明.xlsx`。第一个下划线前为英文表名，后面中文只供策划识别。
- B1：该页的英文基础名，例如Test、Building、OfficeTask；不填写表名前缀或自动模式后缀。
- JSON：`英文表名_B1基础名.json`。
- Config脚本：`英文表名_B1基础名Config.cs`；类名与脚本名一致。
- Data模式：`英文表名_B1基础名.record`、`英文表名_B1基础名Data.cs`。
- 例：`TestTable_测试表.xlsx`，B1=`Test`，输出 `TestTable_Test.json`、`TestTable_TestConfig.cs`，声明 `public class TestTable_TestConfig`。

导出文件名与类名只允许ASCII英文标识符，中文页签名仅作显示，不参与生成。不同英文表名前缀可使用相同B1；同英文前缀、相同B1即使中文说明不同也会冲突并整批拒绝。模式只由B2或导出请求决定，不根据B1末尾文字猜测。

## 当前工作簿

| 工作簿 | 页签及B1基础名（按位置顺序） |
| --- | --- |
| BuildingTable_建筑表.xlsx | 1 建筑（Building） |
| EffectTable_效果表.xlsx | 1 通用效果（Effect） |
| MetaSkillTreeTable_局外技能树表.xlsx | 1 节点（FamilyTree）、2 效果映射（FamilyTreeEffect）、3 板块（FamilyTreeBoard）、4 文案（FamilyTreeText） |
| VillageTable_村庄表.xlsx | 1 场景（VillageScene）、2 文案（VillageText） |
| ItemTable_物品表.xlsx | 1 物品（Item）、2 掉落（Drop） |
| RetainerTable_门客表.xlsx | 1 门客（Retainer） |
| RunMapTable_地图生成表.xlsx | 1 地图预设（MapPreset）、2 预设分层（PresetLayer）、3 生成参数（MapGeneration）、4 地形主题（MapBiome）、5 结构区块（MapChunk）、6 区块接口（ChunkSocket）、7 放置插槽（ChunkSlot） |
| RunContentTable_局内内容表.xlsx | 1 交互物（RunInteraction）、2 角色行为（RunBehavior） |
| LoadingTable_读条表.xlsx | 1 轮播设置（Loading）、2 地图读条（MapLoading） |
| ProgressTable_时代进度表.xlsx | 1 时代（Era）、2 深度（Depth） |
| OfficeTaskTable_办事任务表.xlsx | 1 任务（OfficeTask）、2 选项（OfficeTaskOption）、3 时代门槛（OfficeEraGate） |
| EventTable_剧情事件表.xlsx | 1 事件（Event）、2 选项（EventOption） |
| TestTable_测试表.xlsx | 1 测试（Test） |
| WorldMapTable_世界观地图表.xlsx | 1 地点（WorldMap）、2 疆域（WorldFaction） |

共14本、32页；33张运行时配置包括额外派生的势力名称表。该派生数据输出 `WorldMapTable_WorldFactionLabel.json`，Config类为WorldMapTable_WorldFactionLabelConfig，仍由世界观工具的历史名录生成，不手写或改名编辑器作者JSON。

## 导表与读取

B2仍填写IsConfig/IsData；第3行备注、第4行英文属性、第5行端标记、第6行类型、第7行起数据。沿用Unity的ExcelTool菜单。中文注释保留，字段与配置数值不随本次命名迁移变动。

程序通过ConfigTableIndex按完整Config类名解析JSON路径，例如TestTable_TestConfig映射到Data/Json/Runtime/TestTable_Test；同步/异步一致。不得直接用类名拼JSON路径。输出先整批校验再发布，有变化才写文件，失败回滚并清理本批暂存。

编辑器默认使用ExcelWorksheetAccess.GetByIndex，索引从1开始；GetByName保留为精确名称扩展接口。世界观工具共用一本WorldMapTable，固定1地点、2疆域，单独导出一页会保留另一页及额外页。

本次名称迁移与验收见[ConfigEnglish](../../QA/ConfigEnglish/README.md)；上次小模块归纳的历史证据见[ConfigModules](../../QA/ConfigModules/README.md)。不要运行旧批次迁移工具来恢复已退役布局，不手改生成JSON或Config脚本。
