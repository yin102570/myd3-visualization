# 斑鸠观测数据综合可视化分析平台

一个基于D3.js的交互式斑鸠观测数据可视化分析系统，展示2015-2025年间的斑鸠分布、数量趋势及栖息地分析。通过多维度数据可视化，帮助研究者和鸟类爱好者理解斑鸠的生态分布特征。

## 项目特点

- **多维度数据可视化**：整合时间趋势、空间分布和栖息地类型三大核心维度
- **交互式体验**：所有图表支持悬停详情、缩放和平移等交互操作
- **视觉设计优雅**：采用渐变色系、卡片式布局和微动画提升用户体验
- **响应式布局**：适配不同屏幕尺寸，保持良好的显示效果
- **模块化架构**：代码结构清晰，便于维护和功能扩展

## 可视化组件

1. **时间趋势分析**
   - 年度数量变化折线图，展示10年间的观测数量趋势
   - 月度热力图，直观呈现各年月度观测数量分布
   - 关键统计指标卡片，快速掌握核心数据

2. **空间分布分析**
   - 交互式中国地图，展示各省份斑鸠分布密度
   - 支持地图缩放、平移和重置操作
   - 省份悬停显示详细观测数据

3. **栖息地类型分析**
   - 栖息地类型柱状图，展示不同环境中的斑鸠数量
   - 栖息地占比饼图，直观呈现各类环境的分布比例
   - 支持图表元素交互，显示详细数据

## 技术栈

- **前端框架**：原生JavaScript (ES6+)
- **可视化库**：D3.js v7 用于所有图表绘制
- **地图数据**：GeoJSON格式地理数据
- **样式处理**：CSS3 (包含动画、渐变和响应式设计)
- **数据处理**：使用D3.js的数据处理和聚合功能

## 核心功能实现

### 数据可视化管道

```javascript
// 数据处理流程示例
function init() {
  // 1. 生成/加载数据
  ALL_DATA = generateMockData();
  
  // 2. 数据聚合与处理
  const yearGroups = d3.group(ALL_DATA, d => d.year);
  const provinceGroups = d3.group(ALL_DATA, d => d.stateProvince);
  
  // 3. 绘制可视化图表
  drawTimeCharts();
  drawMapChart(generateSimpleChinaGeoJSON());
  drawHabitatCharts();
}
```

### 交互式地图实现

```javascript
// 地图投影与交互示例
const projection = d3.geoMercator()
  .center([108, 34])
  .scale(mapWidth * 0.8)
  .translate([mapWidth / 2, mapHeight / 2]);

// 缩放行为
zoomBehavior = d3.zoom()
  .scaleExtent([0.5, 5])
  .on('zoom', (event) => {
    mapG.attr('transform', event.transform);
  });

mapSvg.call(zoomBehavior);
```

### 响应式 tooltip 实现

```javascript
function showTooltip(event, content) {
  TOOLTIP
    .classed('show', true)
    .html(content.replace(/\n/g, '<br>'))
    .style('left', (event.pageX + 15) + 'px')
    .style('top', (event.pageY - 10) + 'px');
}
```

## 安装与使用

1. 克隆本仓库
   ```bash
   git clone https://github.com/yourusername/woodpigeon-visualization.git
   ```

2. 进入项目目录
   ```bash
   cd woodpigeon-visualization
   ```

3. 启动本地服务器（推荐使用VS Code Live Server或类似工具）

4. 在浏览器中打开 `add.html` 文件

## 数据说明

项目使用模拟数据展示2015-2025年间的斑鸠观测记录，包含以下字段：
- 观测年份与月份
- 个体数量
- 地理位置（经纬度）
- 所在省份
- 具体地点描述
- 栖息地类型

实际应用中，可替换为真实观测数据，数据格式保持一致即可。

## 未来扩展方向

- 增加数据筛选功能，支持按时间、地区和栖息地类型筛选
- 集成真实的鸟类观测数据集
- 添加更多统计分析指标和图表类型
- 实现数据导出功能
- 增加多语言支持
