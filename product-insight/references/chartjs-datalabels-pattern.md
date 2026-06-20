# Chart.js + chartjs-plugin-datalabels 静态数据标签模式

用于行业趋势报告中**数据值始终可见**（不靠鼠标悬停）的图表渲染。

## CDN 依赖

```html
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.7/dist/chart.umd.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels@2.2.0/dist/chartjs-plugin-datalabels.min.js"></script>
```

## 注册插件（全局生效）

```html
<script>
Chart.register(ChartDataLabels);
</script>
```

## 柱状图 + 静态数据标签（白色文字，柱顶显示）

```javascript
new Chart(ctx, {
  type: 'bar',
  data: { labels: [...], datasets: [{ data: [...] }] },
  options: {
    plugins: {
      legend: { display: false },
      datalabels: {
        color: '#fff',
        font: { weight: 'bold', size: 9 },
        anchor: 'end',
        align: 'end',
        offset: 0,
        formatter: function(v) { return v.toLocaleString(); }
      }
    }
  }
});
```

## 折线图 + 静态数据标签（彩色文字，线端显示）

```javascript
new Chart(ctx, {
  type: 'line',
  data: { labels: [...], datasets: [{ data: [...] }] },
  options: {
    plugins: {
      datalabels: {
        color: '#764ba2',
        font: { weight: 'bold', size: 10 },
        anchor: 'end',
        align: 'end',
        offset: 3,
        formatter: function(v) { return v.toLocaleString(); }
      }
    }
  }
});
```

## 双折线图（移动AI + Edge AI 对比）

每个 dataset 可以走全局 `datalabels` 配置，无需逐 dataset 配置。数据量大时可在 `formatter` 中根据数值调整字号。

## Agent数量柱状图（百万→亿单位转换）

```javascript
datalabels: {
  formatter: function(v) {
    if (v >= 100) return (v/100).toFixed(1) + '亿';
    return v + '百万';
  }
}
```

Y轴 ticks 同理：

```javascript
ticks: {
  callback: function(value) {
    if (value >= 100) return (value/100).toFixed(0) + '亿';
    return value + '百万';
  }
}
```

## 来源 Badge（HTML，Chart.js 之外）

```html
<div class="source-badge badge-gartner">📊 Gartner / Fortune Business Insights</div>
```

CSS 配色：
```css
.badge-gartner  { background: #e8f0fe; color: #1a73e8; }
.badge-idc      { background: #fce8e6; color: #d93025; }
.badge-grandview{ background: #e6f4ea; color: #137333; }
.badge-mordor   { background: #fef7e0; color: #ea8600; }
.badge-fortune  { background: #e8d5f5; color: #7b1fa2; }
```

## 常见陷阱

### 陷阱1：百万→亿的单位转换错误（⚠️ 最常踩的坑）

**问题**：图表数据以**百万（millions）** 为单位存储（如 2216 代表 2216 百万），但显示时需要转为「亿」。

**错误写法**：
```javascript
// ❌ 除以 1000 — 导致 2216 → "2.2亿"
(v / 1000).toFixed(1) + '亿'
```

**正确写法**：
```javascript
// ✅ 除以 100 — 1亿 = 100百万，2216 → "22.16亿"
(v / 100).toFixed(1) + '亿'
```

**真实案例**：某长期报告 IDC 数据显示「2030年22亿Agent」正确，但图表标签因除以1000显示为「2.2亿」，用户发现数据不一致后追查定位到该换算错误。**必须同时检查 datalabels.formatter 和 ticks.callback 两处代码**，确保统一使用 `/100`。

### 陷阱2：datalabels 与 legend 冲突

如果 `plugins.legend` 省略不写，datalabels 仍然会显示。两者独立配置。

### 陷阱3：数字格式

`toLocaleString()` 在 Chrome 中输出千分位逗号（如 `2,416`），在大数字（≥1000）时建议保留。

### 陷阱4：CDN 版本锁定

务必使用精确版本号（`@4.4.7` / `@2.2.0`），不要用 `latest` 避免破坏性更新。
