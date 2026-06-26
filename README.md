# 项目介绍

本项目是 SPlayer 播放器第三方控制类插件，通过 LyricsIsland 协议推送歌词，显示到 ClassIsland 主界面。支持自定义端口、背景歌词过滤、对唱分行、翻译展示、下一行预览等个性化配置。

# 功能特性

1. 切歌同步推送歌曲名、歌手信息
2. 实时逐行同步播放歌词，主/副双行展示
3. 背景歌词处理逻辑
   - 可绑定归属主歌词行展示
   - 可选开关跳过背景歌词，仅显示主唱
4. 对唱歌词分行处理
   - 重叠时间对唱自动放入副行，主行保留主唱文本
5. 副行内容优先级
   - 背景歌词 / 重叠对唱 > 歌词翻译 > 下一行歌词预览
6. 可自定义本地服务端口
7. 静默捕获网络异常，不会弹窗报错干扰播放

# 依赖

1. [SPlayer-Next](https://github.com/SPlayer-Dev/SPlayer-Next) 音乐播放器
2. [ClassIsland](https://github.com/ClassIsland/ClassIsland) 班级大屏课表软件
3. ClassIsland 插件 [ExtraIsland](https://github.com/LiPolymer/ExtraIsland)，默认监听端口：50063

# 使用教程

## 安装插件

1. 打开 SPlayer-Next，打开 '设置' → '插件管理' → '在线导入'
2. 输入以下链接并导入

```

https://github.com/WindDrift/SPlayerLRC-In-ClassIsland/raw/refs/heads/main/SPlayerLRC-In-ClassIsland.js

```

## ClassIsland 配置

1. 打开 ClassIsland，确保 ExtraIsland 插件已安装且正常运行
2. 在 '应用设置' → '主界面' 中添加来自 ExtraIsland 插件的组件 '实时活动' 或 '动态歌词'
3. '实时活动' 组件需要开启 '启用歌词'

# 插件设置项说明

| 设置项 | 类型 | 默认值 | 说明 |
|---|---|---|---|
| 端口 | 数字 | 50063 | ClassIsland 歌词组件本地监听端口，范围 1024~65535 |
| 显示翻译 | 开关 | 开启 | 歌词自带翻译时，无特殊副行则副行展示翻译文本 |
| 无翻译时显示下一行 | 开关 | 开启 | 无翻译、无背景/对唱歌词时，副行展示下一行歌词 |
| 跳过背景歌词 | 开关 | 关闭 | 开启后背景歌词不会出现在副行，仅保留所属主歌词 |
| 重叠对唱显示在副行 | 开关 | 开启 | 与主唱时间重叠的对唱歌词自动放入副行区分显示 |

# 数据推送逻辑

## 接口地址

```

POST http://127.0.0.1:端口/component/lyrics/lyrics/

```

## 请求体 JSON 结构

```

{
"lyric": "主行歌词文本",
"extra": "副行歌词文本（翻译/对唱/背景/下一行）"
}

```
