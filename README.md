--═══════════════════════════════════════════════
--  DZ7 Hub | Meme Sea (motor Redz Hub) — Tema VERMELHO
--  Renomeia + ícone próprio + abre/fecha + sem Discord
--═══════════════════════════════════════════════
if not game:IsLoaded() then game.Loaded:Wait() end

local CoreGui = game:GetService("CoreGui")
local Players = game:GetService("Players")
local LP = Players.LocalPlayer

local NOME = "DZ7 Hub"
local SUA_IMAGEM = "rbxassetid://119601999103521"  -- seu decal

local ICONS_REZ = { "15298567397", "17382040552" }

-- Paleta vermelha
local VM_ESCURO = Color3.fromRGB(60, 10, 10)
local VM_MEDIO  = Color3.fromRGB(100, 20, 20)
local VM_CLARO  = Color3.fromRGB(180, 30, 30)
local TEXTO     = Color3.fromRGB(255, 225, 225)

task.spawn(function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/tlredz/Scripts/refs/heads/main/main.luau"))({
        JoinTeam = "Pirates",
        Translator = true
    })
end)

local function alvos()
    local t = {CoreGui}
    local pg = LP:FindFirstChild("PlayerGui")
    if pg then table.insert(t, pg) end
    return t
end

local function renomearTextos()
    pcall(function()
        for _, root in ipairs(alvos()) do
            for _, obj in ipairs(root:GetDescendants()) do
                if obj:IsA("TextLabel") or obj:IsA("TextBox") or obj:IsA("TextButton") then
                    local t = obj.Text
                    if t and t:lower():find("redz") then
                        obj.Text = t:gsub("[Rr][Ee][Dd][Zz]%s*[Hh][Uu][Bb]", NOME)
                                      :gsub("[Rr][Ee][Dd][Zz]", NOME)
                    end
                end
            end
        end
    end)
end

local function ehIconeRedz(asset)
    if not asset then return false end
    for _, id in ipairs(ICONS_REZ) do
        if asset:find(id, 1, true) then return true end
    end
    return false
end

local function trocarIcones()
    pcall(function()
        for _, root in ipairs(alvos()) do
            for _, obj in ipairs(root:GetDescendants()) do
                if obj:IsA("ImageLabel") or obj:IsA("ImageButton") then
                    if ehIconeRedz(obj.Image) then
                        obj.Image = SUA_IMAGEM
                    end
                end
            end
        end
    end)
end

local function removerDiscord()
    pcall(function()
        for _, root in ipairs(alvos()) do
            for _, obj in ipairs(root:GetDescendants()) do
                local nome = obj.Name:lower()
                local texto = nil
                if obj:IsA("TextLabel") or obj:IsA("TextButton") or obj:IsA("TextBox") then
                    texto = obj.Text or ""
                end

                local ehDiscord =
                    nome:find("discord") or
                    (texto and (texto:lower():find("discord") or texto:find("discord.gg"))) or
                    nome:find("invite") or
                    (obj:IsA("TextButton") and texto and texto:lower():find("copy"))

                if ehDiscord and obj.Parent then
                    obj:Destroy()
                end

                if obj:IsA("ImageLabel") or obj:IsA("ImageButton") then
                    local img = obj.Image or ""
                    if img:find("17382040552") then
                        obj:Destroy()
                    end
                end
            end
        end
    end)
end

local function pintarVermelho()
    pcall(function()
        for _, root in ipairs(alvos()) do
            for _, obj in ipairs(root:GetDescendants()) do
                if obj:IsA("Frame") or obj:IsA("ImageButton") or obj:IsA("ImageLabel")
                    or obj:IsA("TextBox") or obj:IsA("TextButton")
                    or obj:IsA("ScrollingFrame") then

                    if obj.BackgroundTransparency <= 0.95 then
                        local r, g, b = obj.BackgroundColor3.R, obj.BackgroundColor3.G, obj.BackgroundColor3.B
                        if r < 0.25 and g < 0.25 and b < 0.25 then
                            obj.BackgroundColor3 = VM_ESCURO
                        else
                            obj.BackgroundColor3 = VM_MEDIO
                        end
                    end
                end

                if obj:IsA("UIStroke") then
                    obj.Color = VM_CLARO
                end

                if obj:IsA("TextLabel") or obj:IsA("TextButton") or obj:IsA("TextBox") then
                    obj.TextColor3 = TEXTO
                end
            end
        end
    end)
end

--═══════════ BOTÃO ABRIR/FECHAR com sua foto ═══════════
local function criarBotaoAbrirFechar()
    pcall(function()
        if CoreGui:FindFirstChild("DZ_Toggle") or LP.PlayerGui:FindFirstChild("DZ_Toggle") then return end
        local gui = Instance.new("ScreenGui")
        gui.Name = "DZ_Toggle"
        gui.ResetOnSpawn = false
        pcall(function() gui.Parent = CoreGui end)
        if not gui.Parent then gui.Parent = LP:WaitForChild("PlayerGui") end

        local btn = Instance.new("ImageButton")
        btn.Name = "BtnAbrirFechar"
        btn.Size = UDim2.fromOffset(44, 44)
        btn.Position = UDim2.new(0, 10, 0.5, -22)
        btn.BackgroundColor3 = VM_ESCURO
        btn.Image = SUA_IMAGEM
        btn.Parent = gui
        Instance.new("UICorner", btn).CornerRadius = UDim.new(1, 0)

        local stroke = Instance.new("UIStroke", btn)
        stroke.Color = VM_CLARO
        stroke.Thickness = 2

        -- Arrastar o botão
        local UserInputService = game:GetService("UserInputService")
        local arrastando = false
        btn.InputBegan:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseButton1
                or input.UserInputType == Enum.UserInputType.Touch then
                arrastando = true
            end
        end)
        UserInputService.InputChanged:Connect(function(input)
            if arrastando and (input.UserInputType == Enum.UserInputType.MouseMovement
                or input.UserInputType == Enum.UserInputType.Touch) then
                local pos = UserInputService:GetMouseLocation()
                btn.Position = UDim2.new(0, pos.X - 22, 0, pos.Y - 22)
            end
        end)
        UserInputService.InputEnded:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseButton1
                or input.UserInputType == Enum.UserInputType.Touch then
                arrastando = false
            end
        end)

        -- Localiza a janela principal do hub
        local function acharJanela()
            local melhor, melhorArea = nil, 0
            for _, sg in ipairs({CoreGui, LP.PlayerGui}) do
                for _, obj in ipairs(sg:GetDescendants()) do
                    if obj:IsA("Frame") and obj.Visible
                        and obj.AbsoluteSize.X > 300 and obj.AbsoluteSize.Y > 200 then
                        local area = obj.AbsoluteSize.X * obj.AbsoluteSize.Y
                        if area > melhorArea then
                            melhor, melhorArea = obj, area
                        end
                    end
                end
            end
            return melhor
        end

        local escondido = false
        local cliqueMoveu = false
        btn.InputBegan:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseMovement then cliqueMoveu = false end
        end)
        btn.MouseButton1Click:Connect(function()
            if cliqueMoveu then return end
            local janela = acharJanela()
            if janela then
                escondido = not escondido
                janela.Visible = not escondido
            end
        end)
    end)
end

task.spawn(function()
    task.wait(1)
    criarBotaoAbrirFechar()  -- cria o botão com sua foto uma única vez
    while task.wait(0.2) do
        renomearTextos()
        trocarIcones()
        removerDiscord()
        pintarVermelho()
    end
end)

print("[DZ7 Hub] Carregado — tema vermelho, ícone próprio e botão abrir/fechar") 
