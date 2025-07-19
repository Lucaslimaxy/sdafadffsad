-- Ralsei Hub Chaos Mobile (Botões bonitos para cada função)
-- By Lucaslimaxy

local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui")
gui.Name = "RalseiHubMobile"
gui.Parent = player:WaitForChild("PlayerGui")

-- Funções do Hub
local btns = {
    {name = "Fly", func = function()
        loadstring(game:HttpGet("https://pastebin.com/raw/6s7Y1K4V"))()
    end},
    {name = "Infinite Jump", func = function()
        if not _G.Ralsei_InfJump then
            _G.Ralsei_InfJump = true
            game:GetService("UserInputService").JumpRequest:Connect(function()
                local char = player.Character
                if _G.Ralsei_InfJump and char and char:FindFirstChildOfClass("Humanoid") then
                    char:FindFirstChildOfClass("Humanoid"):ChangeState("Jumping")
                end
            end)
        end
    end},
    {name = "Speed x80", func = function()
        local char = player.Character
        if char and char:FindFirstChildOfClass("Humanoid") then
            char:FindFirstChildOfClass("Humanoid").WalkSpeed = 80
        end
    end},
    {name = "Jump Power x120", func = function()
        local char = player.Character
        if char and char:FindFirstChildOfClass("Humanoid") then
            char:FindFirstChildOfClass("Humanoid").JumpPower = 120
        end
    end},
    {name = "TP para Cofre", func = function()
        local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
        if hrp then hrp.CFrame = CFrame.new(-455.8, 24.5, -320.4) end
    end},
    {name = "TP para Escola", func = function()
        local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
        if hrp then hrp.CFrame = CFrame.new(-228.5, 24.5, -349.0) end
    end},
    {name = "TP para Loja", func = function()
        local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
        if hrp then hrp.CFrame = CFrame.new(-265.3, 25.1, -487.4) end
    end},
    {name = "Explodir Cofres", func = function()
        for _,obj in pairs(game:GetService("Workspace"):GetChildren()) do
            if obj.Name:lower():find("safe") or obj.Name:lower():find("cofre") then
                obj:BreakJoints()
            end
        end
    end},
    {name = "Remover Portas", func = function()
        for _,obj in pairs(game:GetService("Workspace"):GetChildren()) do
            if obj.Name:lower():find("door") or obj.Name:lower():find("porta") then
                obj:Destroy()
            end
        end
    end},
    {name = "TP Todos para Você", func = function()
        local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
        if hrp then
            for _,plr in pairs(game.Players:GetPlayers()) do
                if plr ~= player and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
                    plr.Character.HumanoidRootPart.CFrame = hrp.CFrame + Vector3.new(0,5,0)
                end
            end
        end
    end},
}

-- Visual bonito (cor, fonte, layout vertical)
local btnColor = Color3.fromRGB(120, 220, 170)
local txtColor = Color3.fromRGB(30,30,30)
local btnFont = Enum.Font.FredokaOne

local frame = Instance.new("Frame", gui)
frame.AnchorPoint = Vector2.new(0.5,0)
frame.Position = UDim2.new(0.5,0,0.05,0)
frame.Size = UDim2.new(0,270,0,50 + #btns*45)
frame.BackgroundColor3 = Color3.fromRGB(255,255,255)
frame.BackgroundTransparency = 0.18
frame.BorderSizePixel = 2
frame.BorderColor3 = btnColor
frame.Name = "RalseiMenu"
frame.Active = true
frame.Draggable = true

local title = Instance.new("TextLabel", frame)
title.Text = "✨ Ralsei Hub ✨"
title.Font = Enum.Font.FredokaOne
title.TextColor3 = btnColor
title.Size = UDim2.new(1,0,0,40)
title.BackgroundTransparency = 1
title.TextScaled = true

for i,btninfo in ipairs(btns) do
    local btn = Instance.new("TextButton", frame)
    btn.Text = btninfo.name
    btn.Font = btnFont
    btn.TextColor3 = txtColor
    btn.BackgroundColor3 = btnColor
    btn.Size = UDim2.new(0.92,0,0,35)
    btn.Position = UDim2.new(0.04,0,0,(i-1)*40+45)
    btn.TextScaled = true
    btn.BorderSizePixel = 0
    btn.AutoButtonColor = true
    btn.MouseButton1Click:Connect(function()
        btninfo.func()
        game.StarterGui:SetCore("SendNotification", {
            Title = "Ralsei Hub",
            Text = btninfo.name.." ativado!",
            Duration = 3
        })
    end)
end

-- Mensagem inicial fofa
game.StarterGui:SetCore("SendNotification", {
    Title = "Ralsei Hub Mobile",
    Text = "Hub carregado!\nClique nos botões para ativar funções.",
    Duration = 7
})
