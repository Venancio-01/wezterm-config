# 配置选项说明

## appearance.lua - 外观配置

### 窗口设置
```lua
initial_cols = 180           -- 初始窗口列数
initial_rows = 60            -- 初始窗口行数
window_background_opacity = 0.9  -- 窗口背景透明度 (0.0-1.0)
window_padding = {           -- 窗口内边距
  left = 5,
  right = 5,
  top = 5,
  bottom = 5,
}
```

### 主题和颜色
```lua
color_scheme = "TokyoNight"   -- 颜色主题
```

**可用主题选项：**
- `TokyoNight` - 深色主题
- `TokyoNight Day` - 浅色主题
- `Catppuccin Mocha` - Catppuccin 深色
- `Catppuccin Latte` - Catppuccin 浅色
- `OneDark` - One Dark 主题
- `Solarized Dark` - Solarized 深色
- `Solarized Light` - Solarized 浅色

### 窗口行为
```lua
adjust_window_size_when_changing_font_size = false  -- 改变字体大小时不调整窗口大小
enable_tab_bar = true               -- 启用标签栏
use_fancy_tab_bar = true            -- 使用花式标签栏
tab_bar_at_bottom = false           -- 标签栏位置 (false=顶部, true=底部)
hide_tab_bar_if_only_one_tab = false -- 只有一个标签时隐藏标签栏
```

## fonts.lua - 字体配置

### 基本字体设置
```lua
font = wezterm.font("JetBrainsMono NF")  -- 主字体
font_size = 9                           -- 字体大小
line_height = 1.1                       -- 行高
```

### 字体渲染
```lua
freetype_load_target = "Normal"     -- FreeType 加载目标
freetype_render_target = "Normal"    -- FreeType 渲染目标
```

**渲染选项：**
- `Normal` - 标准渲染
- `Light` - 轻量级渲染
- `Mono` - 等宽渲染
- `HorizontalLcd` - 水平 LCD 渲染

### 字体回退
```lua
font_rules = {
  {
    intensity = "Bold",
    italic = false,
    font = wezterm.font("JetBrainsMono NF", { weight = "Bold" }),
  },
  {
    intensity = "Bold",
    italic = true,
    font = wezterm.font("JetBrainsMono NF", { weight = "Bold", italic = true }),
  },
}
```

## launch.lua - 启动配置

### 默认程序
```lua
default_prog = { "程序路径", "参数" }  -- 默认启动的程序
```

**Windows 示例：**
```lua
-- PowerShell 7
default_prog = { "pwsh" }

-- MSYS2 Fish
default_prog = { "cmd.exe", "/k", "C:\\msys64\\msys2_shell.cmd -defterm -here -no-start -ucrt64 -shell fish" }

-- Git Bash
default_prog = { "C:\\Program Files\\Git\\bin\\bash.exe", "--login" }
```

### 启动菜单
```lua
launch_menu = {
  { label = "显示名称", args = { "程序路径", "参数" } },
}
```

**常用 Shell 配置：**
```lua
launch_menu = {
  -- PowerShell
  { label = "PowerShell v7", args = { "pwsh" } },
  { label = "PowerShell v5", args = { "powershell" } },
  
  -- CMD
  { label = "Command Prompt", args = { "cmd" } },
  
  -- Git Bash
  { label = "Git Bash", args = { "C:\\Program Files\\Git\\bin\\bash.exe", "--login" } },
  
  -- MSYS2
  { label = "MSYS2 Fish", args = { "C:\\msys64\\usr\\bin\\fish.exe" } },
  { label = "MSYS2 Bash", args = { "C:\\msys64\\usr\\bin\\bash.exe", "--login" } },
  
  -- WSL
  { label = "WSL Ubuntu", args = { "wsl", "-d", "Ubuntu" } },
}
```

## bindings.lua - 键位绑定

### 修饰键配置
```lua
mod.SUPER = "ALT"              -- SUPER 键映射
mod.SUPER_REV = "ALT|CTRL"     -- SUPER_REVERSE 键映射
```

### 键位绑定结构
```lua
{
  key = "按键",
  mods = "修饰键",
  action = 动作,
}
```

### 常用动作
```lua
-- 基本动作
act.CopyTo("Clipboard")        -- 复制到剪贴板
act.PasteFrom("Clipboard")      -- 从剪贴板粘贴
act.SpawnTab("DefaultDomain")   -- 新建标签
act.CloseCurrentTab()           -- 关闭标签

-- 窗格操作
act.SplitVertical({ domain = "CurrentPaneDomain" })    -- 垂直分屏
act.SplitHorizontal({ domain = "CurrentPaneDomain" })  -- 水平分屏
act.ActivatePaneDirection("Up")    -- 聚焦上方窗格
act.AdjustPaneSize({ "Up", 1 })     -- 调整窗格大小

-- 窗口操作
act.SpawnWindow()               -- 新建窗口
act.ToggleFullScreen()          -- 全屏切换
act.IncreaseFontSize()          -- 放大字体
act.DecreaseFontSize()          -- 缩小字体
```

### 鼠标绑定
```lua
mouse_bindings = {
  {
    event = { Up = { streak = 1, button = "Left" } },
    mods = "CTRL",
    action = act.OpenLinkAtMouseCursor,
  },
}
```

## platform.lua - 平台检测

### 平台检测函数
```lua
local function platform()
  return {
    is_win = is_found(wezterm.target_triple, "windows"),  -- Windows 系统
    is_linux = is_found(wezterm.target_triple, "linux"),  -- Linux 系统
    is_mac = is_found(wezterm.target_triple, "apple"),    -- macOS 系统
  }
end
```

## 高级配置选项

### 性能设置
```lua
animation_fps = 60              -- 动画帧率
max_fps = 60                    -- 最大帧率
front_end = "WebGpu"            -- 前端渲染器 (WebGpu/OpenGl/DirectX)
```

### 调试设置
```lua
debug_key_events = false        -- 调试按键事件
show_update_window = false     -- 显示更新窗口
check_for_updates = false       -- 检查更新
```

### 行为设置
```lua
audible_bell = "Disabled"       -- 系统提示音
visual_bell = {                 -- 视觉提示
  fade_in_duration_ms = 100,
  fade_out_duration_ms = 100,
  target = "CursorColor",
}
automatically_reload_config = true  -- 自动重载配置
```

### 工作区设置
```lua
enable_scroll_bar = false       -- 启用滚动条
scrollback_lines = 5000        -- 滚动缓冲行数
enable_wayland = false          -- Wayland 支持
```

## 自定义配置建议

### 1. 性能优化
```lua
-- 对于性能较弱的系统
front_end = "OpenGl"
animation_fps = 30
max_fps = 30
```

### 2. 开发环境
```lua
-- 为开发优化的配置
default_prog = { "pwsh" }  -- 使用 PowerShell
launch_menu = {
  { label = "Node.js", args = { "node" } },
  { label = "Python", args = { "python" } },
  { label = "Docker", args = { "docker", "run", "-it", "ubuntu" } },
}
```

### 3. 多平台支持
```lua
-- 跨平台配置示例
if platform.is_win then
  default_prog = { "pwsh" }
elseif platform.is_linux then
  default_prog = { "bash" }
elseif platform.is_mac then
  default_prog = { "zsh" }
end
```

### 4. 主题切换
```lua
-- 根据时间切换主题
local hour = tonumber(os.date("%H"))
if hour >= 6 and hour < 18 then
  config.color_scheme = "TokyoNight Day"
else
  config.color_scheme = "TokyoNight"
end
```

## 配置文件优先级

WezTerm 按以下顺序加载配置文件：
1. `~/.config/wezterm/wezterm.lua`
2. `~/.config/wezterm/config/*.lua` (按字母顺序)
3. 命令行参数指定的配置文件

注意：配置文件修改后需要重启 WezTerm 或按 `Ctrl + Shift + R` 重载配置。