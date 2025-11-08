# NotificationLib

一个可自定义的 Roblox 通知库，支持彩虹渐变、声音、头像、图标，以及可选的确认/取消按钮用于脚本执行。

## 安装

在 LocalScript 中加载库：

```lua
local NotificationLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/CNHM/miscellaneous/main/Notifying"))()
```

## API

- `NotificationLib.Show(params)`: 显示通知。参数包括 `title`、`subtitle`、`duration`、`position` ("right" 或 "left")、`userId`、`icon`、`soundId`、`usebuttons` (布尔值)、`useavatar` (布尔值)、`onConfirm` (函数)。
- `NotificationLib.PlaySound(soundId)`: 独立播放声音。
- `NotificationLib.DetectUI()`: 获取 UI 状态（活跃数量、屏幕高度、总高度）。

## 示例

### 示例 1: 基本通知（不使用按钮或头像）

```lua
local NotificationLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/CNHM/miscellaneous/main/Notifying"))()

NotificationLib.Show({
    title = "系统通知",
    subtitle = "这是一个测试通知，将在5秒后自动消失。",
    duration = 5,
    position = "right",
    icon = "rbxassetid://1234567890",  -- 可选图标
    soundId = "rbxassetid://18595195017",  -- 可选声音
    usebuttons = false,
    useavatar = false
})
```

### 示例 2: 带玩家头像的通知（不使用按钮）

```lua
local NotificationLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/CNHM/miscellaneous/main/Notifying"))()

local targetUserId = game.Players.LocalPlayer.UserId  -- 使用当前玩家ID
NotificationLib.Show({
    title = "玩家消息",
    subtitle = "来自玩家的问候：你好！",
    duration = 7,
    position = "right",
    userId = targetUserId,  -- 指定用户ID以显示头像
    usebuttons = false,
    useavatar = true  -- 启用头像
})
```

### 示例 3: 带确认/取消按钮的通知（左下角：取消，右下角：确认）

```lua
local NotificationLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/CNHM/miscellaneous/main/Notifying"))()

NotificationLib.Show({
    title = "脚本执行确认",
    subtitle = "是否执行以下脚本？（例如：打印消息并创建GUI）",
    onConfirm = function()
        -- 这里执行玩家写的特定代码（本地执行），当前为空
        -- 示例：print("用户确认执行脚本！")
    end,
    duration = 10,  -- 按钮模式下，duration仅用于显示，但不会自动消失，除非点击按钮
    position = "right",
    usebuttons = true,  -- 启用按钮
    useavatar = false  -- 不使用头像
})
```

### 示例 4: 带按钮和头像

```lua
local NotificationLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/CNHM/miscellaneous/main/Notifying"))()

NotificationLib.Show({
    title = "带头像的确认",
    subtitle = "确认执行带头像的通知？",
    onConfirm = function()
        -- 这里执行玩家写的特定代码（本地执行），当前为空
        -- 示例：print("确认执行！")
    end,
    duration = 8,
    position = "left",
    userId = 1,  -- 示例用户ID
    usebuttons = true,
    useavatar = true
})
```

### 示例 5: 仅播放声音

```lua
local NotificationLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/CNHM/miscellaneous/main/Notifying"))()

NotificationLib.PlaySound("rbxassetid://131961136")
```

### 示例 6: 检测 UI 状态（调试用）

```lua
local NotificationLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/CNHM/miscellaneous/main/Notifying"))()

local uiInfo = NotificationLib.DetectUI()
print("活跃通知数量:", uiInfo.activeCount)
print("屏幕高度:", uiInfo.screenHeight)
print("总高度占用:", uiInfo.totalHeight)
