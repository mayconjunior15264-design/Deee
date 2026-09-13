-- Maycon HUB - Loader com 4 scripts
-- Cole este script no executor do Roblox

local CoreGui = game:GetService("CoreGui")
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

-- Evita duplicar
if CoreGui:FindFirstChild("MayconHUB") then
    CoreGui.MayconHUB:Destroy()
end

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "MayconHUB"
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Parent = CoreGui

-- ===== JANELA PRINCIPAL =====
local Main = Instance.new("Frame")
Main.Name = "Main"
Main.Size = UDim2.new(0, 260, 0, 300)
Main.Position = UDim2.new(0.5, -130, 0.5, -150)
Main.BackgroundColor3 = Color3.fromRGB(20, 20, 20) -- preto fosco
Main.BorderSizePixel = 0
Main.Active = true
Main.Draggable = true
Main.Parent = ScreenGui

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 14)
MainCorner.Parent = Main

local MainStroke = Instance.new("UIStroke")
MainStroke.Color = Color3.fromRGB(139, 0, 0) -- vermelho escuro
MainStroke.Thickness = 2
MainStroke.Parent = Main

-- ===== TÍTULO =====
local Title = Instance.new("TextLabel")
Title.Name = "Title"
Title.Size = UDim2.new(1, 0, 0, 45)
Title.Position = UDim2.new(0, 0, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "Maycon HUB"
Title.TextColor3 = Color3.fromRGB(255, 0, 0) -- vermelho vivo
Title.TextScaled = true
Title.Font = Enum.Font.GothamBold
Title.Parent = Main

local TitlePadding = Instance.new("UIPadding")
TitlePadding.PaddingTop = UDim.new(0, 6)
TitlePadding.Parent = Title

-- ===== CONTAINER DOS BOTÕES =====
local ButtonHolder = Instance.new("Frame")
ButtonHolder.Name = "ButtonHolder"
ButtonHolder.Size = UDim2.new(1, -20, 1, -60)
ButtonHolder.Position = UDim2.new(0, 10, 0, 55)
ButtonHolder.BackgroundTransparency = 1
ButtonHolder.Parent = Main

local UIList = Instance.new("UIListLayout")
UIList.Padding = UDim.new(0, 8)
UIList.SortOrder = Enum.SortOrder.LayoutOrder
UIList.HorizontalAlignment = Enum.HorizontalAlignment.Center
UIList.Parent = ButtonHolder

-- ===== FUNÇÃO CRIAR BOTÃO =====
local function criarBotao(texto, ordem, callback)
    local btn = Instance.new("TextButton")
    btn.Name = texto:gsub("%s", "")
    btn.Size = UDim2.new(1, 0, 0, 42)
    btn.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    btn.BorderSizePixel = 0
    btn.Text = texto
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Font = Enum.Font.GothamSemibold
    btn.TextScaled = true
    btn.LayoutOrder = ordem
    btn.AutoButtonColor = false
    btn.Parent = ButtonHolder

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 10)
    corner.Parent = btn

    local stroke = Instance.new("UIStroke")
    stroke.Color = Color3.fromRGB(139, 0, 0) -- vermelho escuro
    stroke.Thickness = 2
    stroke.Parent = btn

    local pad = Instance.new("UIPadding")
    pad.PaddingLeft = UDim.new(0, 6)
    pad.PaddingRight = UDim.new(0, 6)
    pad.Parent = btn

    -- Efeitos hover
    btn.MouseEnter:Connect(function()
        TweenService:Create(btn, TweenInfo.new(0.15), {
            BackgroundColor3 = Color3.fromRGB(45, 0, 0)
        }):Play()
    end)
    btn.MouseLeave:Connect(function()
        TweenService:Create(btn, TweenInfo.new(0.15), {
            BackgroundColor3 = Color3.fromRGB(20, 20, 20)
        }):Play()
    end)

    btn.MouseButton1Click:Connect(function()
        -- Feedback visual
        TweenService:Create(btn, TweenInfo.new(0.08), {
            BackgroundColor3 = Color3.fromRGB(80, 0, 0)
        }):Play()
        task.wait(0.1)
        TweenService:Create(btn, TweenInfo.new(0.15), {
            BackgroundColor3 = Color3.fromRGB(20, 20, 20)
        }):Play()

        -- Executa o loadstring
        local ok, err = pcall(callback)
        if not ok then
            warn("[Maycon HUB] Erro ao executar " .. texto .. ": " .. tostring(err))
        end
    end)

    return btn
end

-- ===== BOTÕES =====
criarBotao("MIRANDA HUB", 1, function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/miirandahub/loader/refs/heads/main/stealaeggs"))()
end)

criarBotao("CLOVER", 2, function()
    loadstring(game:HttpGet("https://cloverhub.app/clover.lua"))()
end)

criarBotao("LENNON", 3, function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/lennonxscripts/lennonhubv2/refs/heads/main/stealaneggv2"))()
end)

criarBotao("SERVIDOR PRIVADO", 4, function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/desyble/serverprivate/refs/heads/main/loader.luau"))()
end)

-- ===== BOTÃO FECHAR (X) =====
local CloseBtn = Instance.new("TextButton")
CloseBtn.Name = "Close"
CloseBtn.Size = UDim2.new(0, 26, 0, 26)
CloseBtn.Position = UDim2.new(1, -32, 0, 8)
CloseBtn.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
CloseBtn.BorderSizePixel = 0
CloseBtn.Text = "X"
CloseBtn.TextColor3 = Color3.fromRGB(255, 0, 0)
CloseBtn.Font = Enum.Font.GothamBold
CloseBtn.TextScaled = true
CloseBtn.Parent = Main

local CloseCorner = Instance.new("UICorner")
CloseCorner.CornerRadius = UDim.new(0, 8)
CloseCorner.Parent = CloseBtn

local CloseStroke = Instance.new("UIStroke")
CloseStroke.Color = Color3.fromRGB(139, 0, 0)
CloseStroke.Thickness = 2
CloseStroke.Parent = CloseBtn

CloseBtn.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- ===== BOTÃO MINIMIZAR =====
local MinBtn = Instance.new("TextButton")
MinBtn.Name = "Minimize"
MinBtn.Size = UDim2.new(0, 26, 0, 26)
MinBtn.Position = UDim2.new(1, -62, 0, 8)
MinBtn.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MinBtn.BorderSizePixel = 0
MinBtn.Text = "-"
MinBtn.TextColor3 = Color3.fromRGB(255, 0, 0)
MinBtn.Font = Enum.Font.GothamBold
MinBtn.TextScaled = true
MinBtn.Parent = Main

local MinCorner = Instance.new("UICorner")
MinCorner.CornerRadius = UDim.new(0, 8)
MinCorner.Parent = MinBtn

local MinStroke = Instance.new("UIStroke")
MinStroke.Color = Color3.fromRGB(139, 0, 0)
MinStroke.Thickness = 2
MinStroke.Parent = MinBtn

local minimizado = false
MinBtn.MouseButton1Click:Connect(function()
    minimizado = not minimizado
    if minimizado then
        TweenService:Create(Main, TweenInfo.new(0.25, Enum.EasingStyle.Quad), {
            Size = UDim2.new(0, 260, 0, 45)
        }):Play()
        ButtonHolder.Visible = false
    else
        TweenService:Create(Main, TweenInfo.new(0.25, Enum.EasingStyle.Quad), {
            Size = UDim2.new(0, 260, 0, 300)
        }):Play()
        task.wait(0.15)
        ButtonHolder.Visible = true
    end
end)

print("[Maycon HUB] Carregado com sucesso!")

