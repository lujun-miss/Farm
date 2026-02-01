# 商品定价页面UI优化产品需求文档

## 1. 文档信息

| 项目 | 内容 |
|------|------|
| 文档名称 | 商品定价页面UI优化PRD |
| 版本号 | 1.0 |
| 作者 | [产品需求分析师] |
| 创建日期 | [当前日期] |
| 最后更新日期 | [当前日期] |
| 审批状态 | 草稿 |

## 2. 执行摘要

本PRD旨在优化商品定价页面的搜索筛选区域UI，解决当前布局不合理导致的用户体验问题。主要优化内容包括调整输入框和选择框大小、改进布局结构、减小元素间隙，确保在100%浏览器缩放比例下无需水平滚动即可查看完整查询条件和操作按钮。优化后将提升页面的视觉效果、操作效率和用户满意度，与商品管理页面的查询条件保持一致的设计规范。
## 3. 背景与目标

### 3.1 背景
当前商品定价页面的搜索筛选区域存在以下问题：
- 输入框和选择框尺寸过大，占据过多页面空间
- 元素之间间隙过大，导致布局松散
- 布局结构不合理，在100%浏览器缩放比例下需要水平滚动才能看到完整查询条件和操作按钮
- 与商品管理页面的查询条件区域大小不一致，缺乏设计统一性

### 3.2 目标
- 优化搜索筛选区域布局，提高空间利用率
- 确保在100%浏览器缩放比例下无需水平滚动即可查看完整内容
- 统一与商品管理页面的查询条件区域设计规范
- 提升页面视觉效果和用户操作效率

## 4. 用户故事

| ID | 用户故事 | 验收标准 |
|----|----------|----------|
| US-001 | 作为UI设计师，我希望搜索筛选区域的输入框和选择框尺寸更合理，以便提高页面空间利用率 | 所有输入框和选择框宽度统一为w-40，与商品管理页面保持一致 |
| US-002 | 作为UI设计师，我希望搜索筛选区域的元素间隙更小，以便使布局更紧凑 | 元素之间的gap值从4调整为2，整体布局更紧凑 |
| US-003 | 作为UI设计师，我希望搜索筛选区域在中等屏幕上能一排放置2-3个查询条件，以便优化空间布局 | 在md屏幕尺寸下采用grid布局，每行显示2个查询条件 |
| US-004 | 作为系统用户，我希望在100%浏览器缩放比例下无需水平滚动即可看到完整查询条件和操作按钮，以便提高操作效率 | 在1920x1080分辨率下，100%缩放时查询条件区域完整显示，无水平滚动条 |
| US-005 | 作为系统用户，我希望商品定价页面的查询条件区域与商品管理页面保持一致的设计规范，以便获得统一的用户体验 | 两个页面的查询条件区域在尺寸、布局和样式上保持一致 |
## 5. 功能需求

| ID | 功能需求 | 详细说明 |
|----|----------|----------|
| FR-001 | 搜索筛选区域布局优化 | 将搜索筛选区域修改为grid布局，在小屏幕上单列显示，中等屏幕及以上每行显示2个查询条件 |
| FR-002 | 控件尺寸调整 | 所有输入框和选择框宽度统一设置为w-40，与商品管理页面保持一致 |
| FR-003 | 元素间隙调整 | 将查询条件之间的gap值从4调整为2，减小元素之间的间距 |
| FR-004 | 水平滚动控制 | 添加max-w-full overflow-x-hidden属性，确保在任何屏幕尺寸下都不会出现水平滚动条 |
| FR-005 | 操作按钮布局 | 将查询和重置按钮放置在搜索筛选区域的右下角，确保始终可见且易于操作 |
| FR-006 | 保持功能完整性 | 优化后所有查询功能（商品名称搜索、状态筛选、分类筛选、供应商筛选）保持不变 |

## 6. 非功能需求

| ID | 非功能需求 | 详细说明 |
|----|------------|----------|
| NFR-001 | 视觉设计一致性 | 搜索筛选区域的设计风格与商品管理页面的查询条件区域保持一致，包括颜色、字体、边框样式等 |
| NFR-002 | 响应式设计 | 在不同屏幕尺寸下（sm、md、lg）都能提供良好的用户体验，布局自动调整 |
| NFR-003 | 性能影响 | UI优化不应影响页面加载性能和交互响应速度 |
| NFR-004 | 浏览器兼容性 | 优化后的布局在主流浏览器（Chrome、Firefox、Safari、Edge）中表现一致 |
| NFR-005 | 可维护性 | 代码结构清晰，易于维护和后续扩展 |
## 7. 设计规范

### 7.1 布局设计

| 元素 | 布局配置 |
|------|----------|
| 搜索筛选区域容器 | 采用grid布局，grid-cols-1 md:grid-cols-2 gap-2，添加max-w-full overflow-x-hidden防止水平滚动 |
| 查询条件组 | 每个查询条件包含一个label和一个input/select，采用flex items-center space-x-2布局 |
| 操作按钮组 | 采用flex justify-end space-x-3布局，放置在搜索筛选区域的右下角 |

### 7.2 控件设计

| 控件类型 | 设计规格 |
|----------|----------|
| 输入框 | 宽度：w-40<br>内边距：px-3 py-2<br>边框：border rounded<br>聚焦状态：focus:outline-none focus:ring-2 focus:ring-blue-500 |
| 选择框 | 宽度：w-40<br>内边距：px-3 py-2<br>边框：border rounded<br>聚焦状态：focus:outline-none focus:ring-2 focus:ring-blue-500 |
| 标签 | 文字大小：text-sm<br>文字权重：font-medium<br>文字颜色：text-gray-700<br>不换行：whitespace-nowrap |
| 按钮 | 内边距：px-4 py-2<br>边框：border border-gray-300 rounded<br>悬停状态：hover:bg-gray-50<br>图标：使用Font Awesome图标，与文字间距mr-2 |

### 7.3 间距与对齐

| 元素 | 间距配置 |
|------|----------|
| 容器内边距 | p-4 |
| 查询条件之间的间隙 | gap-2 |
| 标签与输入框之间的间隙 | space-x-2 |
| 操作按钮之间的间隙 | space-x-3 |
| 容器外边距 | mb-6 |

### 7.4 响应式设计

| 屏幕尺寸 | 布局调整 |
|----------|----------|
| sm (640px) | 单列显示，每个查询条件独占一行 |
| md (768px) | 双列显示，每行显示2个查询条件 |
| lg (1024px+) | 双列显示，每行显示2个查询条件，保持与md相同的布局结构 |
## 8. 实现细节

### 8.1 文件路径
修改文件：`D:\工具\Trae\Farm\Vendor\product-pricing.html`

### 8.2 HTML结构优化

将原有的搜索筛选区域替换为以下优化后的代码：

```html
<!-- 搜索筛选区域 - 优化版（避免水平滚动） -->
<div class="border rounded-lg p-4 mb-6 max-w-full overflow-x-hidden">
    <div class="grid grid-cols-1 md:grid-cols-2 gap-2 mb-4">
        <!-- 商品名称 -->
        <div class="flex items-center space-x-2">
            <label for="product-name" class="text-sm font-medium text-gray-700 whitespace-nowrap">商品名称:</label>
            <input 
                type="text" 
                id="product-name" 
                placeholder="请输入" 
                class="w-40 px-3 py-2 border rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
            >
        </div>
        <!-- 商品状态 -->
        <div class="flex items-center space-x-2">
            <label for="product-status" class="text-sm font-medium text-gray-700 whitespace-nowrap">商品状态:</label>
            <select 
                id="product-status" 
                class="w-40 px-3 py-2 border rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
                onchange="handleStatusChange(this.value)"
            >
                <option value="">全部</option>
                <option value="0">禁用</option>
                <option value="1">启用</option>
            </select>
        </div>
        <!-- 商品分类 -->
        <div class="flex items-center space-x-2">
            <label for="product-category" class="text-sm font-medium text-gray-700 whitespace-nowrap">商品分类:</label>
            <select 
                id="product-category" 
                class="w-40 px-3 py-2 border rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
            >
                <option value="">全部</option>
                <option value="fruit">水果</option>
                <option value="vegetable">蔬菜</option>
                <option value="grain">粮食</option>
                <!-- 更多分类选项 -->
            </select>
        </div>
        <!-- 供应商 -->
        <div class="flex items-center space-x-2">
            <label for="supplier" class="text-sm font-medium text-gray-700 whitespace-nowrap">供应商:</label>
            <select 
                id="supplier" 
                class="w-40 px-3 py-2 border rounded focus:outline-none focus:ring-2 focus:ring-blue-500"
            >
                <option value="">全部</option>
                <option value="supplier1">供应商1</option>
                <option value="supplier2">供应商2</option>
                <!-- 更多供应商选项 -->
            </select>
        </div>
    </div>
    <!-- 操作按钮 -->
    <div class="flex justify-end space-x-3">
        <button onclick="searchProducts()" class="px-4 py-2 border border-gray-300 rounded hover:bg-gray-50">
            <i class="fas fa-search mr-2"></i>查询
        </button>
        <button onclick="resetFilters()" class="px-4 py-2 border border-gray-300 rounded hover:bg-gray-50">
            <i class="fas fa-undo mr-2"></i>重置
        </button>
    </div>
</div>
```

### 8.3 JavaScript函数

保留原有JavaScript函数，无需修改：
- `handleStatusChange(status)`: 处理商品状态变化
- `searchProducts()`: 执行商品搜索
- `resetFilters()`: 重置所有筛选条件

## 9. 测试需求

| ID | 测试项 | 测试方法 | 预期结果 |
|----|--------|----------|----------|
| T-001 | 控件尺寸验证 | 检查所有输入框和选择框的宽度是否为w-40 | 所有输入框和选择框宽度统一为w-40 |
| T-002 | 布局结构验证 | 检查搜索筛选区域是否采用grid布局，md屏幕尺寸下每行显示2个查询条件 | 在md屏幕尺寸下，每行显示2个查询条件 |
| T-003 | 间隙验证 | 检查查询条件之间的gap值是否为2 | 查询条件之间的gap值为2，布局紧凑 |
| T-004 | 水平滚动验证 | 在1920x1080分辨率下，100%缩放比例查看页面 | 无需水平滚动即可看到完整查询条件和操作按钮 |
| T-005 | 响应式设计验证 | 在不同屏幕尺寸（sm、md、lg）下查看布局 | 在sm屏幕下单列显示，md及以上屏幕双列显示 |
| T-006 | 功能完整性验证 | 测试商品名称搜索、状态筛选、分类筛选、供应商筛选等功能 | 所有筛选功能正常工作，与优化前保持一致 |
| T-007 | 浏览器兼容性验证 | 在Chrome、Firefox、Safari、Edge浏览器中查看页面 | 在所有主流浏览器中显示效果一致 |
## 10. 风险与缓解措施

| 风险 ID | 风险描述 | 风险等级 | 缓解措施 |
|---------|----------|----------|----------|
| R-001 | 优化后的布局在某些特殊分辨率下仍可能出现显示问题 | 低 | 充分测试不同分辨率和浏览器，确保在主流设备上都能正常显示 |
| R-002 | 输入框宽度减小后可能影响用户输入体验 | 低 | 保持输入框宽度与商品管理页面一致，并进行用户测试验证 |
| R-003 | 布局变更可能影响原有JavaScript功能 | 中 | 保留原有JavaScript函数，仅修改HTML结构和CSS样式，确保功能完整性 |
| R-004 | 与现有设计系统不兼容 | 低 | 参考商品管理页面的设计规范，确保设计一致性 |

## 11. 验收标准

| 验收项 | 验收条件 |
|--------|----------|
| 控件尺寸 | 所有输入框和选择框宽度统一为w-40，与商品管理页面保持一致 |
| 布局结构 | 在md屏幕尺寸下采用grid布局，每行显示2个查询条件 |
| 元素间隙 | 查询条件之间的gap值为2，布局紧凑 |
| 水平滚动 | 在1920x1080分辨率下，100%缩放时无需水平滚动即可看到完整查询条件和操作按钮 |
| 响应式设计 | 在sm屏幕下单列显示，md及以上屏幕双列显示 |
| 功能完整性 | 所有筛选功能（商品名称搜索、状态筛选、分类筛选、供应商筛选）正常工作 |
| 视觉一致性 | 与商品管理页面的查询条件区域设计风格保持一致 |
| 浏览器兼容性 | 在Chrome、Firefox、Safari、Edge浏览器中显示效果一致 |
## 12. 变更历史

| 版本号 | 变更内容 | 变更人 | 变更日期 | 审批人 |
|--------|----------|--------|----------|--------|
| 1.0 | 创建商品定价页面UI优化PRD文档 | [产品需求分析师] | [当前日期] | 草稿 |