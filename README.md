<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Script Roblox</title>
    <style>
        body {
            background: #0e0e0e;
            color: #ffffff;
            font-family: Arial, sans-serif;
            padding: 20px;
        }
        h1, h2 {
            color: #00ffcc;
        }
        pre {
            background: #1b1b1b;
            padding: 15px;
            border-radius: 8px;
            overflow-x: auto;
            border-left: 4px solid #00ffcc;
            font-size: 14px;
        }
    </style>
</head>
<body>

<h1>Script Roblox</h1>

<h2>LocalScript - Admin Panel V1</h2>
<pre>
local player = game.Players.LocalPlayer
local remote = game.ReplicatedStorage:WaitForChild("AdminCommand")

local KEY = "Adminkick123"

local gui = script.Parent
local frame = Instance.new("Frame", gui)
frame.Size = UDim2.fromScale(0.45, 0.35)
frame.Position = UDim2.fromScale(0.275, 0.3)
frame.BackgroundColor3 = Color3.fromRGB(20,20,20)
frame.Visible = false
frame.Active = true
frame.Draggable = true

local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1,0,0,40)
title.Text = "Admin Panel V1"
title.TextScaled = true
title.TextColor3 = Color3.new(1,1,1)
title.BackgroundTransparency = 1

local cmd = Instance.new("TextBox", frame)
cmd.Size = UDim2.new(0.9,0,0,40)
cmd.Position = UDim2.new(0.05,0,0,70)
cmd.PlaceholderText = "kick Nome"
cmd.TextScaled = true
cmd.BackgroundColor3 = Color3.fromRGB(40,40,40)
cmd.TextColor3 = Color3.new(1,1,1)

local exec = Instance.new("TextButton", frame)
exec.Size = UDim2.new(0.9,0,0,40)
exec.Position = UDim2.new(0.05,0,0,120)
exec.Text = "Executar"
exec.TextScaled = true
exec.BackgroundColor3 = Color3.fromRGB(60,60,60)
exec.TextColor3 = Color3.new(1,1,1)

local keyBox = Instance.new("TextBox", gui)
keyBox.Size = UDim2.fromScale(0.4, 0.1)
keyBox.Position = UDim2.fromScale(0.3, 0.4)
keyBox.PlaceholderText = "Digite a Key"
keyBox.TextScaled = true
keyBox.BackgroundColor3 = Color3.fromRGB(25,25,25)
keyBox.TextColor3 = Color3.new(1,1,1)

keyBox.FocusLost:Connect(function(enter)
    if enter and keyBox.Text == KEY then
        keyBox.Visible = false
        frame.Visible = true
    end
end)

exec.MouseButton1Click:Connect(function()
    if cmd.Text ~= "" then
        remote:FireServer(cmd.Text)
        cmd.Text = ""
    end
end)
</pre>

<h2>Script do Servidor - Kick</h2>
<pre>
local remote = game.ReplicatedStorage:WaitForChild("AdminCommand")

remote.OnServerEvent:Connect(function(player, text)
    local args = string.split(text, " ")

    if args[1] == "kick" and args[2] then
        for _,plr in pairs(game.Players:GetPlayers()) do
            if string.lower(plr.Name) == string.lower(args[2]) then
                plr:Kick("Você foi kickado por um Admin.")
            end
        end
    end
end)
</pre>

</body>
</html>
