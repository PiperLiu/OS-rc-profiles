## Vscode安装

1. 登录Github，开启自动同步。
2. 修改Setting设置中的Powershell路径。



## Terminal+Powershell7+Starship

1. 安装PowerShell7。
2. 安装Windows Terminal。
3. 安装Powershell插件。

```
# 1. 安装 PSReadline 包，该插件可以让命令行很好用，类似 zsh
Install-Module -Name PSReadLine -AllowPrerelease -Force

# 2. 安装 posh-git 包，让你的 git 更好用
Install-Module posh-git -Scope CurrentUser
```

4. 安装Scoop

```
Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
```

5. Scoop 安装git、starship

```
scoop install git
scoop install starship
```

6. 创建 .config/starship.toml文件，配置starship

```
[time]
disabled = false
format = '⏰[ $time]($style) '
time_format = "%T"
style = "bold #9dc3c1"

[username]
style_user = "#ff7473 bold"
format = "😍 [$user]($style) "
disabled = false
show_always = true

[conda]
format = "[Conda]($style) [$symbol$environment]($style) "
symbol = "🚀 "
style = "bold #ef9e9f"

[python]
format = '[Python]($style) [${symbol}${pyenv_prefix}${version}( \($virtualenv\))]($style) '
symbol = "🥳 "
style = "bold #feee7d"

[directory]
truncation_length = 8
truncation_symbol = "…/"
style = "bold #84b1ed"


# Wait 10 milliseconds for starship to check files under the current directory.
scan_timeout = 10

# Disable the blank line at the start ofthe prompt
add_newline = true
```

7. 配置Powershell7， 在$PROFILE

```
$Env:http_proxy = "http://127.0.0.1:7890"; $Env:https_proxy = "http://127.0.0.1:7890"


#------------------------------- Import Modules BEGIN -------------------------------
# 引入 posh-git
# Import-Module posh-git

# 引入 starship主题
Invoke-Expression (&starship init powershell)

$ENV:STARSHIP_CONFIG = "$HOME\.config\starship.toml"

# PSReadLine
Import-Module PSReadLine
# Enable Prediction History
Set-PSReadLineOption -PredictionSource History
#------------------------------- Import Modules END   -------------------------------





#-------------------------------  Set Hot-keys BEGIN  -------------------------------
# 设置 Tab 键补全
# Set-PSReadlineKeyHandler -Key Tab -Function Complete

# 设置 Ctrl+d 为菜单补全和 Intellisense
Set-PSReadLineKeyHandler -Key "Tab" -Function MenuComplete

# 设置 Ctrl+d 为退出 PowerShell
Set-PSReadlineKeyHandler -Key "Ctrl+q" -Function ViExit

# 设置 Ctrl+z 为撤销
Set-PSReadLineKeyHandler -Key "Ctrl+z" -Function Undo

# 设置向上键为后向搜索历史记录
Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward

# 设置向下键为前向搜索历史纪录
Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward
#-------------------------------  Set Hot-keys END    -------------------------------





#-------------------------------    Functions BEGIN   -------------------------------
# Python 直接执行
$env:PATHEXT += ";.py"

# 更新 pip 的方法
function Update-Packages {
    # update pip
    Write-Host "Step 1: 更新 pip" -ForegroundColor Magenta -BackgroundColor Cyan
    $a = pip list --outdated
    $num_package = $a.Length - 2
    for ($i = 0; $i -lt $num_package; $i++) {
        $tmp = ($a[2 + $i].Split(" "))[0]
        pip install -U $tmp
    }
}
#-------------------------------    Functions END     -------------------------------





#-------------------------------   Set Alias Begin    -------------------------------

# 2. 更新系统 os-update
Set-Alias -Name os-update -Value Update-Packages

# 3. 查看目录 ls & ll
function ListDirectory {
    (Get-ChildItem).Name
    Write-Host("")
}
Set-Alias -Name ls -Value ListDirectory
Set-Alias -Name ll -Value Get-ChildItem
#-------------------------------    Set Alias END     -------------------------------
```

8. 配置windowsterminal

```
"guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
            "hidden": false,
            "name": "PowerShell7",
            "tabTitle": "PowerShell7",
            "icon": "C:\\Users\\hp\\Documents\\powershell.png",
            "source": "Windows.Terminal.PowershellCore",
            "commandline": "C:/Program Files/PowerShell/7/pwsh.exe -nologo",
            "colorScheme": "Snazzy",
            "snapOnInput": true,
            // "cursorColor": "#22c4ff",
            "cursorShape": "filledBox",
            "fontFace": "CaskaydiaCove Nerd Font Mono",
            "fontSize": 14,
            // "background": "#326ebd",
            "historySize": 9001,
            "acrylicOpacity": 0.9,
            // "backgroundImage": "C:\\Users\\hp\\AppData\\Local\\Packages\\windows.immersivecontrolpanel_cw5n1h2txyewy\\RoamingState\\Corporate_Sunrise.png",
            // "backgroundImageStretchMode": "uniformToFill",
            // "backgroundImageOpacity": 1.0,
            "useAcrylic": true,
            "closeOnExit": true,
            "padding": "5, 5, 20, 25",
            "startingDirectory": "%USERPROFILE%"
```



```
            "name": "Snazzy",
            "black": "#000000",
            "red": "#fc4346",
            "green": "#50fb7c",
            "yellow": "#f0fb8c",
            "blue": "#49baff",
            "purple": "#fc4cb4",
            "cyan": "#8be9fe",
            "white": "#ededec",
            "brightBlack": "#555555",
            "brightRed": "#fc4346",
            "brightGreen": "#50fb7c",
            "brightYellow": "#f0fb8c",
            "brightBlue": "#49baff",
            "brightPurple": "#fc4cb4",
            "brightCyan": "#8be9fe",
            "brightWhite": "#ededec",
            "background": "#2C3548",
            "foreground": "#ebece6"
```

