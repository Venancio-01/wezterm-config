# WezTerm 配置使用文档

## 概述

这是一个高度定制化的 WezTerm 终端配置，专为 Windows 系统优化，支持多种 shell 和丰富的快捷键操作。

## 配置文件结构

```
.config/wezterm/
├── config/
│   ├── appearance.lua    # 外观和窗口设置
│   ├── bindings.lua      # 键位绑定配置
│   ├── fonts.lua         # 字体配置
│   └── launch.lua        # 启动配置
├── utils/
│   └── platform.lua      # 平台检测工具
└── docs/                 # 使用文档（本文件夹）
```

## 主要特性

### 🎨 外观配置
- **窗口大小**: 180x60 字符
- **透明度**: 90% 背景透明
- **主题**: TokyoNight 风格
- **字体**: JetBrainsMono Nerd Font, 9pt

### 🚀 启动配置
- **默认 Shell**: MSYS2 Fish
- **备用 Shell**: PowerShell 7, Git Bash, MSYS2 Bash
- **启动命令**: 通过 MSYS2 Shell 启动 Fish

### ⌨️ 快捷键系统
- **模块化设计**: 分类清晰的功能快捷键
- **无冲突**: 避免与系统快捷键冲突
- **高效操作**: 支持分屏、导航、调整等操作

## 安装和使用

### 前置条件

1. **安装 WezTerm**
   ```bash
   # 从官网下载安装包
   # https://wezterm.org/
   ```

2. **安装字体**
   - [JetBrainsMono Nerd Font](https://github.com/ryanoasis/nerd-fonts)
   - 字体版本: v3.2.1

3. **安装 MSYS2**
   - 确保 MSYS2 已安装并配置了 Fish shell
   - 路径: `C:\msys64\`

### 配置步骤

1. **克隆配置**
   ```bash
   git clone https://github.com/Venancio-01/wezterm-config.git
   ```

2. **复制配置文件**
   ```bash
   # 将配置文件复制到 WezTerm 配置目录
   cp -r wezterm-config/* ~/.config/wezterm/
   ```

3. **重启 WezTerm**
   - 完全关闭并重新启动 WezTerm

### 配置文件详解

#### appearance.lua
```lua
return {
  initial_cols = 180,           -- 初始列数
  initial_rows = 60,            -- 初始行数
  window_background_opacity = 0.9,  -- 背景透明度
  color_scheme = "TokyoNight",  -- 颜色主题
}
```

#### fonts.lua
```lua
return {
  font = wezterm.font("JetBrainsMono NF"),
  font_size = 9,
  freetype_load_target = "Normal",
  freetype_render_target = "Normal",
}
```

#### launch.lua
```lua
if platform.is_win then
  options.default_prog = { "cmd.exe ", "/k", "C:\\msys64\\msys2_shell.cmd -defterm -here -no-start -ucrt64 -shell fish" }
  options.launch_menu = {
    { label = "PowerShell v7", args = { "pwsh" } },
    { label = "GitBash", args = { "C:\\soft\\Git\\bin\\bash.exe" } },
    { label = "MSYS2 Fish", args = { "C:\\msys64\\usr\\bin\\fish.exe" } },
  }
end
```

## 常见问题

### Fish Shell 启动问题
如果遇到 Fish Shell 启动错误，请检查：
1. MSYS2 是否正确安装
2. Fish shell 是否已安装: `pacman -S fish`
3. 系统工具是否完整: `pacman -S coreutils`

### 字体显示问题
如果图标显示异常：
1. 确认安装了正确版本的 Nerd Font
2. 检查 WezTerm 字体设置
3. 重启 WezTerm

### 快捷键冲突
如果快捷键不工作：
1. 检查是否有其他程序占用相同快捷键
2. 确认按键组合设置正确
3. 查看 WezTerm 调试信息 (F12)

## 自定义配置

### 修改窗口大小
编辑 `config/appearance.lua`:
```lua
initial_cols = 200,  -- 修改列数
initial_rows = 80,  -- 修改行数
```

### 添加新的 Shell
编辑 `config/launch.lua`:
```lua
{
  label = "新 Shell",
  args = { "路径到/shell.exe" },
},
```

### 自定义快捷键
编辑 `config/bindings.lua` 添加新的键位绑定。

## 贡献

欢迎提交 Issue 和 Pull Request 来改进这个配置！

## 许可证

MIT License