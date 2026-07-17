-- ============================================
-- KINGERX HUB v6.0 - ULTIMATE COMPLETE
-- Developer: Julainorei
-- Colaborador: xicoooo73
-- Studio: KingerX
-- Copyright (c) 2026
-- ============================================

-- ============================================================
-- KEY SYSTEM
-- ============================================================
local key = "kingerxstudio"
local userKey = ""

-- Cria GUI de key
local keyGui = Instance.new("ScreenGui")
keyGui.Name = "KingerXKeyGui"
keyGui.Parent = game:GetService("CoreGui")

local keyFrame = Instance.new("Frame")
keyFrame.Size = UDim2.new(0, 400, 0, 250)
keyFrame.Position = UDim2.new(0.5, -200, 0.5, -125)
keyFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 30)
keyFrame.BorderSizePixel = 0
keyFrame.BackgroundTransparency = 0.15
keyFrame.Active = true
keyFrame.Draggable = true
keyFrame.Parent = keyGui

local uiCorner = Instance.new("UICorner")
uiCorner.CornerRadius = UDim.new(0, 12)
uiCorner.Parent = keyFrame

local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, 0, 0, 45)
titleLabel.Position = UDim2.new(0, 0, 0, 10)
titleLabel.BackgroundTransparency = 1
titleLabel.Text = "KingerX Hub"
titleLabel.TextColor3 = Color3.fromRGB(255, 50, 50)
titleLabel.TextScaled = true
titleLabel.Font = Enum.Font.GothamBold
titleLabel.Parent = keyFrame

local subLabel = Instance.new("TextLabel")
subLabel.Size = UDim2.new(1, 0, 0, 25)
subLabel.Position = UDim2.new(0, 0, 0, 55)
subLabel.BackgroundTransparency = 1
subLabel.Text = "Digite a chave para acessar"
subLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
subLabel.TextScaled = false
subLabel.TextSize = 14
subLabel.Font = Enum.Font.Gotham
subLabel.Parent = keyFrame

local keyBox = Instance.new("TextBox")
keyBox.Size = UDim2.new(0.8, 0, 0, 40)
keyBox.Position = UDim2.new(0.1, 0, 0, 90)
keyBox.BackgroundColor3 = Color3.fromRGB(40, 40, 50)
keyBox.BackgroundTransparency = 0.3
keyBox.PlaceholderText = "Insira a chave..."
keyBox.Text = ""
keyBox.TextColor3 = Color3.fromRGB(255, 255, 255)
keyBox.TextScaled = false
keyBox.TextSize = 16
keyBox.Font = Enum.Font.Gotham
keyBox.ClearTextOnFocus = false
local boxCorner = Instance.new("UICorner")
boxCorner.CornerRadius = UDim.new(0, 8)
boxCorner.Parent = keyBox
keyBox.Parent = keyFrame

local statusLabel = Instance.new("TextLabel")
statusLabel.Size = UDim2.new(0.8, 0, 0, 20)
statusLabel.Position = UDim2.new(0.1, 0, 0, 135)
statusLabel.BackgroundTransparency = 1
statusLabel.Text = ""
statusLabel.TextColor3 = Color3.fromRGB(255, 100, 100)
statusLabel.TextScaled = false
statusLabel.TextSize = 13
statusLabel.Font = Enum.Font.Gotham
statusLabel.Parent = keyFrame

local submitBtn = Instance.new("TextButton")
submitBtn.Size = UDim2.new(0.5, 0, 0, 40)
submitBtn.Position = UDim2.new(0.25, 0, 0, 165)
submitBtn.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
submitBtn.Text = "ENTRAR"
submitBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
submitBtn.TextScaled = false
submitBtn.TextSize = 18
submitBtn.Font = Enum.Font.GothamBold
local btnCorner = Instance.new("UICorner")
btnCorner.CornerRadius = UDim.new(0, 8)
btnCorner.Parent = submitBtn
submitBtn.Parent = keyFrame

local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.new(0, 25, 0, 25)
closeBtn.Position = UDim2.new(1, -30, 0, 5)
closeBtn.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
closeBtn.BackgroundTransparency = 0.5
closeBtn.Text = "X"
closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
closeBtn.TextScaled = true
closeBtn.Font = Enum.Font.GothamBold
local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(0, 6)
closeCorner.Parent = closeBtn
closeBtn.Parent = keyFrame

-- Bloqueia o jogo até a key ser inserida
local player = game.Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()
local hum = char:WaitForChild("Humanoid")
hum.WalkSpeed = 0
hum.JumpPower = 0

local keyVerified = false

submitBtn.MouseButton1Click:Connect(function()
    if keyBox.Text == key then
        keyVerified = true
        keyGui:Destroy()
        hum.WalkSpeed = 16
        hum.JumpPower = 50
        -- Inicia o hub
        startHub()
    else
        statusLabel.Text = "Chave inválida! Tente novamente."
        keyBox.Text = ""
    end
end)

closeBtn.MouseButton1Click:Connect(function()
    hum.WalkSpeed = 16
    hum.JumpPower = 50
    keyGui:Destroy()
    player:Kick("Chave necessária para usar o KingerX Hub!")
end)

keyBox.FocusLost:Connect(function(enter)
    if enter then
        if keyBox.Text == key then
            keyVerified = true
            keyGui:Destroy()
            hum.WalkSpeed = 16
            hum.JumpPower = 50
            startHub()
        else
            statusLabel.Text = "Chave inválida! Tente novamente."
            keyBox.Text = ""
        end
    end
end)

-- ============================================================
-- FUNÇÃO PRINCIPAL DO HUB (chamada após key verificada)
-- ============================================================
function startHub()

local player = game.Players.LocalPlayer
local roleName = "[ KingerX User ]"

-- Donos
local owners = {
    ["Breno010L"] = true,
    ["RUANRODRIGO121121"] = true,
    ["Gabriel263633j"] = true,
    ["Julainorei"] = true,
    ["xicoooo73"] = true
}
local leader = "Julainorei"

if owners[player.Name] then roleName = "[ KingerX Owner ]" end
if player.Name == leader then roleName = "[ KingerX Leader ]" end

-- ============================================================
-- FUNCAO CORRIGIDA: NOME, BIO E CORES
-- ============================================================
local function setRoleplayVisuals()
    local char = player.Character
    if not char then return end
    
    pcall(function()
        local re = ReplicatedStorage:FindFirstChild("RE")
        if not re then return end
        
        local nameEvent = re:FindFirstChild("1RPNam1eTex1t")
        local colorEvent = re:FindFirstChild("1RPNam1eColo1r")
        
        if nameEvent then
            nameEvent:FireServer("RolePlayBio", "julainorei criador dessa obra prima")
            nameEvent:FireServer("RolePlayName", "(KingerX o rei dos hub)")
        end
        
        if colorEvent then
            colorEvent:FireServer("PickingRPBioColor", Color3.new(1,1,1))
            colorEvent:FireServer("PickingRPNameColor", Color3.new(1,0,0))
        end
    end)
    
    pcall(function()
        for _, obj in ipairs(char:GetDescendants()) do
            if obj:IsA("StringValue") then
                local n = obj.Name:lower()
                if n:find("rpname") or n:find("nick") or n:find("display") then
                    obj.Value = "(KingerX o rei dos hub)"
                end
                if n:find("rpbio") or n:find("bio") or n:find("desc") then
                    obj.Value = "julainorei criador dessa obra prima"
                end
            end
            if obj:IsA("Color3Value") then
                local n = obj.Name:lower()
                if n:find("rpnamecolor") or n:find("namecolor") then
                    obj.Value = Color3.new(1,0,0)
                end
                if n:find("rpbiocolor") or n:find("biocolor") then
                    obj.Value = Color3.new(1,1,1)
                end
            end
        end
    end)
end

setRoleplayVisuals()

-- ============================================================
-- BIBLIOTECA ORIGINAL
-- ============================================================
local redzlib = loadstring(game:HttpGet("https://api.rubis.app/v2/scrap/HcbTJDQEatJPsFJL/raw"))()

local Window = redzlib:MakeWindow({
    Title = "KingerX Hub",
    SubTitle = "v6.0 - Ultimate Complete",
    SaveFolder = "KingerXHub"
})

workspace.FallenPartsDestroyHeight = -math.huge

-- Servicos
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TeleportService = game:GetService("TeleportService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local TweenService = game:GetService("TweenService")
local VirtualUser = game:GetService("VirtualUser")
local Lighting = game:GetService("Lighting")
local Debris = game:GetService("Debris")
local HttpService = game:GetService("HttpService")
local MarketService = game:GetService("MarketplaceService")
local Mouse = player:GetMouse()

-- Anti-AFK
player.Idled:Connect(function()
    VirtualUser:Button2Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
    task.wait(1)
    VirtualUser:Button2Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
end)

-- Variaveis
local KX = {
    AntiSit = false, AntiSitHum = nil, AntiSitChair = nil,
    WalkspeedEnabled = false, WSVal = 16,
    JumpPowerEnabled = false, JPVal = 50,
    HipHeight = 0,
    NoClip = false,
    FlyEnabled = false, FlySpeed = 50, FlyConn = nil, BG = nil, BV = nil,
    ClickTP = false,
    InfYields = false,
    AutoRP = false,
    AutoHeal = false,
    NoFall = false,
    AntiDrown = false,
    WalkWater = false, WalkWaterConn = nil,
    ESP = false, ESPObjs = {},
    FovEnabled = false, FovVal = 70,
    ZoomEnabled = false, ZoomVal = 100000,
    Fullbright = false,
    VehSpeed = false, VehSpeedVal = 100,
    LoopTP = false,
    FarmActive = false, FarmConn = nil,
    MusicLoop = false, MusicLoopConn = nil,
    Tempo = 0, TempoRunning = true,
    RGB = false, RGBConn = nil,
    UIHidden = false,
    
    -- NOVAS VARIAVEIS
    AntiFlingVehicles = false, AntiFlingBalls = false,
    AntiFlingPortas = false, hiddenDoors = {},
    AntiFlingBloco = false, playerDoorData = {},
    antiSitActive = false,
    englishFlingActive = false, brazilianFlingActive = false,
    flingCouchActive = false, flingCouchFastActive = false,
    autoFlingActive = false, touchedFlingActive = false,
    shieldBall = nil, shieldLoop = nil,
    loopTPfling = false, glitchFlingCouchActiveAll = false,
    FlingConnection = nil, BringConnection = nil,
    KillConnection = nil, RGBConnection = nil, OrbitConnection = nil,
    PropsRGBEnabled = false,
    loopAtivo = false, loopTodosAtivo = false,
    rgbHouse = false, rgbHouseConnection = nil,
    houseTextRgb = false, houseTextConnection = nil,
    hackedHouseText = false, hackedConnection = nil,
    loopGarage = false,
    vehicleRgbConnection = nil,
    fireEnabled = false, fireLoop = nil,
    selectedEffect = nil, selectedFire = "Verde",
    selectedColor = "White", selectedSmokeColor = "White",
}

local function getRoot(p)
    local c = p.Character
    return c and c:FindFirstChild("HumanoidRootPart")
end
local function getHum(p)
    local c = p.Character
    return c and c:FindFirstChildOfClass("Humanoid")
end
local function tpTo(cf)
    local r = getRoot(player)
    if r then r.CFrame = cf end
end

-- ============================================================
-- FUNCAO DE MUSICA (NÃO MEXIDA)
-- ============================================================
local function tocarMusica(id)
    local rs = ReplicatedStorage
    local re = rs:WaitForChild("RE")
    
    pcall(function()
        re:WaitForChild("PlayerToolEvent"):FireServer("ToolMusicText", id)
    end)
    pcall(function()
        re:WaitForChild("1Player1sHous1e"):FireServer("PickHouseMusicText", id)
    end)
    pcall(function()
        re:WaitForChild("1Player1sCa1r"):FireServer("PickingCarMusicText", id)
    end)
    pcall(function()
        re:WaitForChild("1NoMoto1rVehicle1s"):FireServer("PickingScooterMusicText", id)
    end)
end

local function tocarMusicaParaTodos(id)
    local rs = ReplicatedStorage
    local re = rs:WaitForChild("RE")
    
    for _, plr in ipairs(Players:GetPlayers()) do
        pcall(function()
            re:WaitForChild("PlayerToolEvent"):FireServer("ToolMusicText", id)
        end)
        pcall(function()
            re:WaitForChild("1Player1sHous1e"):FireServer("PickHouseMusicText", id)
        end)
        pcall(function()
            re:WaitForChild("1Player1sCa1r"):FireServer("PickingCarMusicText", id)
        end)
        pcall(function()
            re:WaitForChild("1NoMoto1rVehicle1s"):FireServer("PickingScooterMusicText", id)
        end)
    end
end

local function serverHop()
    local ok, res = pcall(function()
        return HttpService:JSONDecode(game:HttpGet("https://games.roblox.com/v1/games/"..game.PlaceId.."/servers/Public?limit=100"))
    end)
    if ok and res and res.data then
        for _, s in ipairs(res.data) do
            if s.playing < s.maxPlayers and s.id ~= game.JobId then
                TeleportService:TeleportToPlaceInstance(game.PlaceId, s.id, player)
                return
            end
        end
    end
    TeleportService:Teleport(game.PlaceId, player)
end

-- Anti-Sit
local function setupAntiSit()
    local hum = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
    if hum then
        pcall(function() hum:SetStateEnabled(Enum.HumanoidStateType.Seated, false) end)
        pcall(function() hum:SetStateEnabled(Enum.HumanoidStateType.Seat, false) end)
        if KX.AntiSitHum then KX.AntiSitHum:Disconnect() end
        KX.AntiSitHum = hum:GetPropertyChangedSignal("Sit"):Connect(function()
            if hum.Sit then hum.Sit = false; if hum.SeatPart then pcall(function() hum.SeatPart:Sit(nil) end) end end
        end)
        for _, v in ipairs(workspace:GetDescendants()) do
            if (v:IsA("Seat") or v:IsA("VehicleSeat")) and v:IsA("BasePart") then v.CanTouch = false; v.Disabled = true end
        end
        if KX.AntiSitChair then KX.AntiSitChair:Disconnect() end
        KX.AntiSitChair = RunService.Heartbeat:Connect(function()
            if hum and hum.SeatPart then hum.Sit = false; pcall(function() hum.SeatPart:Sit(nil) end) end
        end)
    end
end

local function disableAntiSit()
    if KX.AntiSitHum then KX.AntiSitHum:Disconnect(); KX.AntiSitHum = nil end
    if KX.AntiSitChair then KX.AntiSitChair:Disconnect(); KX.AntiSitChair = nil end
    local hum = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
    if hum then
        pcall(function() hum:SetStateEnabled(Enum.HumanoidStateType.Seated, true) end)
        pcall(function() hum:SetStateEnabled(Enum.HumanoidStateType.Seat, true) end)
    end
    for _, v in ipairs(workspace:GetDescendants()) do
        if (v:IsA("Seat") or v:IsA("VehicleSeat")) and v:IsA("BasePart") then v.CanTouch = true; v.Disabled = false end
    end
end

player.CharacterAdded:Connect(function()
    task.wait(1)
    setRoleplayVisuals()
    if KX.AntiSit then setupAntiSit() end
end)

local function notify(text, dur)
    pcall(function() redzlib:Notify({Title="KingerX Hub", Text=text or "", Duration=dur or 3}) end)
end

-- ============================================================
-- FUNCAO RGB
-- ============================================================
local function rgbLoop()
    local hue = 0
    KX.RGBConn = RunService.RenderStepped:Connect(function()
        if not KX.RGB then
            if KX.RGBConn then KX.RGBConn:Disconnect(); KX.RGBConn = nil end
            return
        end
        hue = (hue + 0.005) % 1
        local color = Color3.fromHSV(hue, 1, 1)
        
        pcall(function()
            ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPNameColor", color)
            ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPBioColor", color)
        end)
        
        pcall(function()
            if Window and Window.Toggle and Window.Toggle:FindFirstChild("Button") then
                local btn = Window.Toggle.Button
                if btn then
                    btn.BackgroundColor3 = color
                    local circle = btn:FindFirstChild("UICorner") or btn:FindFirstChildWhichIsA("ImageLabel")
                    if circle then circle.BackgroundColor3 = color end
                end
            end
        end)
        
        pcall(function()
            if Window and Window.Main and Window.Main:FindFirstChild("Title") then
                Window.Main.Title.TextColor3 = color
            end
        end)
    end)
end

-- ============================================================
-- CRIACAO DAS ABAS
-- ============================================================
local InfoTab = Window:MakeTab({"Info", "info"})
local PlayerTab = Window:MakeTab({"Player", "player"})
local TeleportTab = Window:MakeTab({"Teleport", "teleport"})
local VisualTab = Window:MakeTab({"Visual", "visual"})
local VehicleTab = Window:MakeTab({"Veículos", "car"})
local WorldTab = Window:MakeTab({"Mundo", "world"})
local MusicTab = Window:MakeTab({"Música", "music"})
local TrollTab = Window:MakeTab({"Troll", "troll"})
local FarmTab = Window:MakeTab({"Farm", "farm"})
local SettingsTab = Window:MakeTab({"Config", "settings"})
local RGBTab = Window:MakeTab({"RGB", "colors"})

-- NOVAS ABAS
local ShadersTab = Window:MakeTab({"Shaders", "server"})
local GamepassTab = Window:MakeTab({"Gamepass", "star"})
local AnimationsTab = Window:MakeTab({"Animações", "Play"})
local AvatarTab = Window:MakeTab({"Avatar", "Users"})
local HouseTab = Window:MakeTab({"Casa", "home"})
local PropsTab = Window:MakeTab({"Props", "box"})
local FunTab = Window:MakeTab({"Fun", "usb"})
local NameBioTab = Window:MakeTab({"Nome & Bio", "Paper"})
local ItensTab = Window:MakeTab({"Itens", "rbxassetid://127904742940104"})
local ScriptsTab = Window:MakeTab({"Scripts", "codesandbox"})
local ProtectionTab = Window:MakeTab({"Proteção", "rbxassetid://11322093465"})

-- ============================================================
-- INFO TAB
-- ============================================================
InfoTab:AddSection({"KingerX Hub"})
InfoTab:AddParagraph({"Developer:", "Julainorei"})
InfoTab:AddParagraph({"Colaborador:", "xicoooo73"})
InfoTab:AddParagraph({"Team:", "KingerX Studio"})
InfoTab:AddParagraph({"Versao:", "v6.0 - Ultimate Complete"})
InfoTab:AddParagraph({"Status:", "Carregado com sucesso!"})
InfoTab:AddParagraph({"Key:", "kingerxstudio"})

InfoTab:AddSection({"Tempo de Uso"})
local playTimeParagraph = InfoTab:AddParagraph({Title = "00:00:00", Text = "Tempo de Uso:"})
local seconds = 0
task.spawn(function()
    while true do
        task.wait(1)
        seconds = seconds + 1
        local h = math.floor(seconds / 3600)
        local m = math.floor((seconds % 3600) / 60)
        local s = seconds % 60
        playTimeParagraph:SetTitle(string.format("%02d:%02d:%02d", h, m, s))
    end
end)

InfoTab:AddSection({"Tempo no Servidor"})
local serverTimeParagraph = InfoTab:AddParagraph({Title = "00:00:00", Text = "Seu Tempo:"})
task.spawn(function()
    while true do
        task.wait(0.5)
        local secs = math.floor(workspace.DistributedGameTime)
        local h = math.floor(secs / 3600)
        local m = math.floor((secs % 3600) / 60)
        local s = secs % 60
        serverTimeParagraph:SetTitle(string.format("%02d:%02d:%02d", h, m, s))
    end
end)

InfoTab:AddSection({"Ações"})
InfoTab:AddButton({Name = "Rejoin", Callback = function() TeleportService:TeleportToPlaceInstance(game.PlaceId, game.JobId, player) end})
InfoTab:AddButton({Name = "Server Hop", Callback = serverHop})
InfoTab:AddButton({Name = "Destruir UI", Callback = function()
    KX.TempoRunning = false
    if KX.FarmConn then KX.FarmConn:Disconnect() end
    if KX.FlyConn then KX.FlyConn:Disconnect() end
    if KX.FlyEnabled then toggleFly(false) end
    if KX.AntiSitHum then KX.AntiSitHum:Disconnect() end
    if KX.AntiSitChair then KX.AntiSitChair:Disconnect() end
    if KX.WalkWaterConn then KX.WalkWaterConn:Disconnect() end
    if KX.MusicLoopConn then task.cancel(KX.MusicLoopConn) end
    if KX.RGBConn then KX.RGBConn:Disconnect() end
    if KX.FlingConnection then KX.FlingConnection:Disconnect() end
    if KX.BringConnection then KX.BringConnection:Disconnect() end
    if KX.KillConnection then KX.KillConnection:Disconnect() end
    if KX.RGBConnection then KX.RGBConnection:Disconnect() end
    if KX.OrbitConnection then KX.OrbitConnection:Disconnect() end
    if KX.vehicleRgbConnection then KX.vehicleRgbConnection:Disconnect() end
    if KX.rgbHouseConnection then KX.rgbHouseConnection:Disconnect() end
    if KX.houseTextConnection then KX.houseTextConnection:Disconnect() end
    if KX.hackedConnection then KX.hackedConnection:Disconnect() end
    if KX.shieldLoop then KX.shieldLoop:Disconnect() end
    if KX.shieldBall then KX.shieldBall:Destroy() end
    clearESP(); disableAntiSit(); task.wait(1); Window:Destroy()
end})

-- ============================================================
-- PLAYER TAB (ORIGINAL + MELHORIAS)
-- ============================================================
PlayerTab:AddSection({"Controles"})

PlayerTab:AddButton({"Anti-Sit", function()
    KX.AntiSit = not KX.AntiSit
    if KX.AntiSit then setupAntiSit(); notify("Anti-Sit ativado!") else disableAntiSit(); notify("Anti-Sit desativado!") end
end})

PlayerTab:AddButton({"Anti-Sit (Fixo)", function()
    local hum = player.Character and player.Character:FindFirstChildOfClass("Humanoid")
    if hum then
        pcall(function() hum:SetStateEnabled(Enum.HumanoidStateType.Seated, false) end)
        pcall(function() hum:SetStateEnabled(Enum.HumanoidStateType.Seat, false) end)
        hum.Sit = false
        if hum.SeatPart then pcall(function() hum.SeatPart:Sit(nil) end) end
        notify("Anti-Sit fixo aplicado!")
    end
end})

PlayerTab:AddToggle({"Walkspeed", false, function(v)
    KX.WalkspeedEnabled = v
    local hum = getHum(player)
    if hum then hum.WalkSpeed = v and KX.WSVal or 16 end
end})

PlayerTab:AddSlider({"Velocidade", 0, 250, 16, function(v)
    KX.WSVal = v
    if KX.WalkspeedEnabled then local hum = getHum(player); if hum then hum.WalkSpeed = v end end
end})

PlayerTab:AddToggle({"JumpPower", false, function(v)
    KX.JumpPowerEnabled = v
    local hum = getHum(player)
    if hum then hum.JumpPower = v and KX.JPVal or 50 end
end})

PlayerTab:AddSlider({"Pulo", 0, 350, 50, function(v)
    KX.JPVal = v
    if KX.JumpPowerEnabled then local hum = getHum(player); if hum then hum.JumpPower = v end end
end})

PlayerTab:AddSlider({"HipHeight", 0, 10, 0, function(v)
    KX.HipHeight = v
    local hum = getHum(player)
    if hum then hum.HipHeight = v end
end})

PlayerTab:AddToggle({"NoClip", false, function(v)
    KX.NoClip = v
    local hum = getHum(player)
    if hum then hum.PlatformStand = v end
end})

-- Fly
local function toggleFly(state)
    local hum = getHum(player)
    local root = getRoot(player)
    if not hum or not root then return end
    if state then
        hum.PlatformStand = true
        KX.BG = Instance.new("BodyGyro"); KX.BG.MaxTorque = Vector3.new(9e9,9e9,9e9); KX.BG.P = 9e9; KX.BG.Parent = root
        KX.BV = Instance.new("BodyVelocity"); KX.BV.MaxForce = Vector3.new(9e9,9e9,9e9); KX.BV.Velocity = Vector3.new(0,0,0); KX.BV.Parent = root
        KX.FlyConn = RunService.RenderStepped:Connect(function()
            local cam = workspace.CurrentCamera
            if not root or not hum then return end
            local moveDir = Vector3.new(
                (UserInputService:IsKeyDown(Enum.KeyCode.D) and 1 or 0) - (UserInputService:IsKeyDown(Enum.KeyCode.A) and 1 or 0),
                (UserInputService:IsKeyDown(Enum.KeyCode.Space) and 1 or 0) - (UserInputService:IsKeyDown(Enum.KeyCode.LeftShift) and 1 or 0),
                (UserInputService:IsKeyDown(Enum.KeyCode.S) and 1 or 0) - (UserInputService:IsKeyDown(Enum.KeyCode.W) and 1 or 0)
            )
            local cf = cam.CFrame
            local vel = (cf.RightVector * moveDir.X + cf.UpVector * moveDir.Y + cf.LookVector * -moveDir.Z) * KX.FlySpeed
            KX.BV.Velocity = vel
            KX.BG.CFrame = cf
        end)
    else
        hum.PlatformStand = false
        if KX.BG then KX.BG:Destroy(); KX.BG = nil end
        if KX.BV then KX.BV:Destroy(); KX.BV = nil end
        if KX.FlyConn then KX.FlyConn:Disconnect(); KX.FlyConn = nil end
    end
end

PlayerTab:AddToggle({"Fly (WASD/Space/Shift)", false, function(v)
    KX.FlyEnabled = v; toggleFly(v)
end})

PlayerTab:AddSlider({"Fly Speed", 1, 300, 50, function(v) KX.FlySpeed = v end})

-- Click TP
PlayerTab:AddToggle({"Click TP", false, function(v)
    KX.ClickTP = v
end})

UserInputService.InputBegan:Connect(function(inp, gpe)
    if gpe then return end
    if inp.UserInputType == Enum.UserInputType.MouseButton1 and KX.ClickTP then
        local hit = Mouse.Hit
        if hit then tpTo(hit + Vector3.new(0,3,0)) end
    end
end)

PlayerTab:AddToggle({"Inf Yields", false, function(v)
    KX.InfYields = v
end})

local yieldLoopRunning = false
PlayerTab:AddButton({"Loop Yields (Loot)", function()
    if yieldLoopRunning then return end
    yieldLoopRunning = true
    task.spawn(function()
        while yieldLoopRunning do
            pcall(function()
                for _, v in ipairs(workspace:GetDescendants()) do
                    if v:IsA("Part") and (v.Name:lower():find("yield") or v.Name:lower():find("loot") or v.Name:lower():find("coin")) then
                        if KX.InfYields then firetouchinterest(player.Character and player.Character:FindFirstChild("HumanoidRootPart"), v, 0) end
                    end
                end
            end)
            task.wait(0.5)
        end
    end)
    notify("Loop Yields ativo!")
end})

PlayerTab:AddButton({"Parar Loop Yields", function()
    yieldLoopRunning = false; notify("Loop Yields parado!")
end})

PlayerTab:AddSection({"Auto"})
PlayerTab:AddToggle({"Auto RP", false, function(v)
    KX.AutoRP = v
    if v then
        task.spawn(function()
            while KX.AutoRP do
                setRoleplayVisuals()
                task.wait(15)
            end
        end)
    end
end})

PlayerTab:AddToggle({"Auto Heal", false, function(v)
    KX.AutoHeal = v
    if v then
        task.spawn(function()
            while KX.AutoHeal do
                local hum = getHum(player)
                if hum and hum.Health > 0 and hum.Health < 100 then
                    pcall(function() ReplicatedStorage.RE["1Play1erHea1lth"]:FireServer() end)
                end
                task.wait(2)
            end
        end)
    end
end})

PlayerTab:AddToggle({"No Fall Damage", false, function(v)
    KX.NoFall = v
end})

local function onCharAdded()
    task.wait(0.5)
    local hum = getHum(player)
    if hum and KX.NoFall then
        hum.FallDamage = false
        hum:GetPropertyChangedSignal("FallDamage"):Connect(function()
            if KX.NoFall and hum then hum.FallDamage = false end
        end)
    end
end
player.CharacterAdded:Connect(onCharAdded)
if player.Character then onCharAdded() end

PlayerTab:AddToggle({"Anti Drown", false, function(v)
    KX.AntiDrown = v
end})

RunService.Heartbeat:Connect(function()
    local hum = getHum(player)
    if not hum then return end
    if KX.WalkspeedEnabled and hum.WalkSpeed ~= KX.WSVal then hum.WalkSpeed = KX.WSVal end
    if KX.JumpPowerEnabled and hum.JumpPower ~= KX.JPVal then hum.JumpPower = KX.JPVal end
    if KX.HipHeight > 0 and hum.HipHeight ~= KX.HipHeight then hum.HipHeight = KX.HipHeight end
    if KX.NoClip then hum.PlatformStand = true end
    if KX.NoFall then hum.FallDamage = false end
    if KX.AntiDrown and hum.Health > 0 then
        local root = getRoot(player)
        if root and root.Position.Y < -50 then root.Velocity = Vector3.new(0,100,0) end
    end
    if KX.WalkWater then
        local root = getRoot(player)
        if root then
            local w = workspace:FindPartOnRayWithWhitelist(Ray.new(root.Position, Vector3.new(0,-10,0)), {workspace.Terrain})
            if w then
                if root.Position.Y < -2 then root.Velocity = Vector3.new(root.Velocity.X, 15, root.Velocity.Z) end
            end
        end
    end
end)

PlayerTab:AddToggle({"Walk on Water", false, function(v)
    KX.WalkWater = v
end})

PlayerTab:AddButton({"Kill Me (Respawn)", function()
    if player.Character then player.Character:BreakJoints() end
end})

-- ============================================================
-- TELEPORT TAB (ORIGINAL)
-- ============================================================
local locs = {
    {"Casa 1", CFrame.new(88, 22, 84)},
    {"Casa 2", CFrame.new(130, 22, 84)},
    {"Casa 3", CFrame.new(190, 22, 84)},
    {"Casa 4", CFrame.new(88, 22, 150)},
    {"Casa 5", CFrame.new(130, 22, 150)},
    {"Casa 6", CFrame.new(190, 22, 150)},
    {"Casa 7", CFrame.new(88, 22, 210)},
    {"Casa 8", CFrame.new(130, 22, 210)},
    {"Casa 9", CFrame.new(190, 22, 210)},
    {"Casa 10", CFrame.new(88, 22, 270)},
    {"Casa 11", CFrame.new(130, 22, 270)},
    {"Casa 12", CFrame.new(190, 22, 270)},
    {"Casa 13", CFrame.new(88, 22, 330)},
    {"Casa 14", CFrame.new(130, 22, 330)},
    {"Casa 15", CFrame.new(190, 22, 330)},
    {"Casa 16", CFrame.new(88, 22, 390)},
    {"Casa 17", CFrame.new(130, 22, 390)},
    {"Casa 18", CFrame.new(190, 22, 390)},
    {"Escola", CFrame.new(417, 21, 103)},
    {"Hospital", CFrame.new(417, 21, 218)},
    {"Delegacia", CFrame.new(378, 21, 330)},
    {"Banco", CFrame.new(338, 21, 410)},
    {"Supermercado", CFrame.new(287, 21, 410)},
    {"Restaurante", CFrame.new(382, 21, 130)},
    {"Parque", CFrame.new(452, 21, 340)},
    {"Praca", CFrame.new(442, 21, 410)},
    {"Loja de Carros", CFrame.new(596, 21, 141)},
    {"Concessionaria", CFrame.new(514, 21, 263)},
    {"Hotel", CFrame.new(378, 21, 460)},
    {"Igreja", CFrame.new(457, 21, 184)},
    {"Posto de Gasolina", CFrame.new(304, 21, 234)},
    {"Academia", CFrame.new(443, 21, 119)},
    {"Praia", CFrame.new(155, 5, 576)},
    {"Pier", CFrame.new(373, 5, 544)},
    {"Floresta", CFrame.new(650, 28, 404)},
    {"Fazenda", CFrame.new(647, 26, 504)},
    {"Ponte", CFrame.new(340, 19, 84)},
    {"Estacionamento", CFrame.new(456, 21, 80)},
}

TeleportTab:AddSection({"Locais"})
local tpNames = {}
for _, loc in ipairs(locs) do table.insert(tpNames, loc[1]) end

TeleportTab:AddDropdown({"Teleportar para", tpNames, function(v)
    for _, loc in ipairs(locs) do
        if loc[1] == v then tpTo(loc[2]); notify("Teleportado para "..v); break end
    end
end})

TeleportTab:AddButton({"Spawn (Ponto Inicial)", function()
    local spawns = workspace:FindFirstChild("SpawnLocations")
    if spawns then
        local s = spawns:GetChildren()
        if #s > 0 then tpTo(s[1].CFrame * CFrame.new(0,3,0)) end
    end
end})

TeleportTab:AddSection({"Loop Teleport"})
TeleportTab:AddToggle({"Loop Teleport", false, function(v)
    KX.LoopTP = v
    if v then
        task.spawn(function()
            local idx = 1
            while KX.LoopTP do
                tpTo(locs[idx][2])
                idx = idx % #locs + 1
                task.wait(0.5)
            end
        end)
        notify("Loop Teleport ativado!")
    else
        notify("Loop Teleport desativado!")
    end
end})

-- ============================================================
-- VISUAL TAB (ORIGINAL)
-- ============================================================
VisualTab:AddSection({"Camera"})

VisualTab:AddSlider({"FOV", 1, 120, 70, function(v)
    KX.FovVal = v
    if workspace.CurrentCamera then workspace.CurrentCamera.FieldOfView = v end
end})

VisualTab:AddToggle({"Lock FOV", false, function(v)
    KX.FovEnabled = v
end})

VisualTab:AddSlider({"Zoom Distance", 1, 100000, 100000, function(v)
    KX.ZoomVal = v
end})

VisualTab:AddToggle({"Max Zoom", false, function(v)
    KX.ZoomEnabled = v
end})

-- ESP
local function clearESP()
    for _, obj in ipairs(KX.ESPOpjs) do pcall(function() obj:Destroy() end) end
    KX.ESPOpjs = {}
end

local function updateESP()
    clearESP()
    if not KX.ESP then return end
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr ~= player and plr.Character then
            local root = plr.Character:FindFirstChild("HumanoidRootPart") or plr.Character:FindFirstChild("Head")
            if root then
                local hl = Instance.new("Highlight")
                hl.FillColor = Color3.fromRGB(255, 50, 50)
                hl.OutlineColor = Color3.fromRGB(255, 255, 255)
                hl.FillTransparency = 0.5
                hl.Adornee = plr.Character
                hl.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
                hl.Parent = plr.Character
                table.insert(KX.ESPOpjs, hl)
                
                local bill = Instance.new("BillboardGui")
                bill.Size = UDim2.new(0, 200, 0, 50)
                bill.StudsOffset = Vector3.new(0, 3, 0)
                bill.AlwaysOnTop = true
                bill.Adornee = root
                local txt = Instance.new("TextLabel")
                txt.Size = UDim2.new(1, 0, 1, 0)
                txt.BackgroundTransparency = 1
                txt.Text = plr.Name .. " [KX]"
                txt.TextColor3 = Color3.fromRGB(255, 50, 50)
                txt.TextScaled = true
                txt.Font = Enum.Font.GothamBold
                txt.Parent = bill
                bill.Parent = root
                table.insert(KX.ESPOpjs, bill)
            end
        end
    end
end

Players.PlayerAdded:Connect(function()
    if KX.ESP then task.wait(1); updateESP() end
end)
Players.PlayerRemoving:Connect(function()
    if KX.ESP then task.wait(0.5); updateESP() end
end)

VisualTab:AddToggle({"ESP (Destaque)", false, function(v)
    KX.ESP = v
    if v then updateESP() else clearESP() end
end})

VisualTab:AddButton({"Atualizar ESP", updateESP})

VisualTab:AddSection({"Efeitos"})
VisualTab:AddToggle({"Fullbright", false, function(v)
    KX.Fullbright = v
    if v then
        for _, child in ipairs(Lighting:GetChildren()) do
            if child:IsA("Sky") then child.Enabled = false end
        end
        Lighting.Ambient = Color3.fromRGB(255,255,255)
        Lighting.Brightness = 2
        Lighting.ClockTime = 14
        Lighting.FogEnd = 1e5
        Lighting.GlobalShadows = false
        Lighting.OutdoorAmbient = Color3.fromRGB(255,255,255)
    else
        for _, child in ipairs(Lighting:GetChildren()) do
            if child:IsA("Sky") then child.Enabled = true end
        end
        Lighting.Ambient = Color3.fromRGB(0,0,0)
        Lighting.Brightness = 1
        Lighting.FogEnd = 100000
        Lighting.GlobalShadows = true
        Lighting.OutdoorAmbient = Color3.fromRGB(128,128,128)
    end
end})

VisualTab:AddButton({"No Sky", function()
    for _, child in ipairs(Lighting:GetChildren()) do
        if child:IsA("Sky") then child:Destroy() end
    end
    notify("Sky removido!")
end})

-- ============================================================
-- VEHICLE TAB (ORIGINAL + MELHORIAS)
-- ============================================================
VehicleTab:AddSection({"Velocidade"})
VehicleTab:AddToggle({"Velocidade Maxima", false, function(v)
    KX.VehSpeed = v
end})

VehicleTab:AddSlider({"Velocidade", 10, 500, 100, function(v)
    KX.VehSpeedVal = v
end})

RunService.Heartbeat:Connect(function()
    if KX.VehSpeed then
        for _, v in ipairs(workspace:GetDescendants()) do
            if v:IsA("VehicleSeat") then
                local veh = v:FindFirstAncestorOfClass("Model")
                if veh and veh.PrimaryPart then
                    local root = veh.PrimaryPart
                    local vel = root.Velocity
                    local dir = vel.Magnitude > 0 and vel.Unit or root.CFrame.LookVector
                    local targetVel = dir * KX.VehSpeedVal
                    root.Velocity = Vector3.new(targetVel.X, vel.Y, targetVel.Z)
                end
            end
        end
    end
end)

VehicleTab:AddSection({"Spawn Veiculos"})
local vehicleModels = {}
for _, child in ipairs(workspace:GetDescendants()) do
    if child:IsA("VehicleSeat") then
        local model = child:FindFirstAncestorOfClass("Model")
        if model and not vehicleModels[model.Name] then
            vehicleModels[model.Name] = model
        end
    end
end

local vehList = {}
for name, _ in pairs(vehicleModels) do table.insert(vehList, name) end

if #vehList > 0 then
    VehicleTab:AddDropdown({"Teleportar para Veiculo", vehList, function(v)
        if vehicleModels[v] and vehicleModels[v].PrimaryPart then
            tpTo(vehicleModels[v].PrimaryPart.CFrame * CFrame.new(0,5,0))
            notify("Teleportado para "..v)
        end
    end})
end

VehicleTab:AddButton({"Destruir Veiculo Atual", function()
    for _, v in ipairs(workspace:GetDescendants()) do
        if v:IsA("VehicleSeat") and v.Occupant then
            local model = v:FindFirstAncestorOfClass("Model")
            if model then pcall(function() model:Destroy() end); notify("Veiculo destruido!"); break end
        end
    end
end})

VehicleTab:AddButton({"Flutuar Veiculo", function()
    for _, v in ipairs(workspace:GetDescendants()) do
        if v:IsA("VehicleSeat") and v.Occupant and v.Occupant:FindFirstChild("SeatPart") then
            local seat = v.Occupant.SeatPart
            if seat then
                pcall(function()
                    local bv = Instance.new("BodyVelocity")
                    bv.MaxForce = Vector3.new(0, 9e9, 0)
                    bv.Velocity = Vector3.new(0, 0, 0)
                    bv.Parent = seat
                    task.wait(0.5)
                    bv:Destroy()
                end)
            end
            break
        end
    end
    notify("Veiculo flutuando!")
end})

VehicleTab:AddSection({"Reparar"})
VehicleTab:AddButton({"Reparar Veiculo", function()
    local hum = getHum(player)
    if hum then
        local seat = hum.SeatPart
        if seat then
            local model = seat:FindFirstAncestorOfClass("Model")
            if model then
                for _, part in ipairs(model:GetDescendants()) do
                    if part:IsA("BasePart") then
                        part.BrickColor = part.BrickColor
                        pcall(function() part:ClearAllChildren() end)
                    end
                end
                notify("Veiculo reparado!")
            end
        end
    end
end})

-- NOVO: Kill Car
VehicleTab:AddSection({"Kill/Trazer Carro"})
VehicleTab:AddButton({"Matar Carro (Kill)", function()
    local hum = getHum(player)
    if hum then
        local seat = hum.SeatPart
        if seat then
            local model = seat:FindFirstAncestorOfClass("Model")
            if model then
                pcall(function() model:BreakJoints() end)
                notify("Carro destruido!")
            end
        end
    end
end})

VehicleTab:AddButton({"Trazer Carro (Bring)", function()
    local hum = getHum(player)
    if hum then
        local seat = hum.SeatPart
        if seat then
            local model = seat:FindFirstAncestorOfClass("Model")
            if model and model.PrimaryPart then
                model.PrimaryPart.CFrame = getRoot(player).CFrame * CFrame.new(0, 3, -5)
                notify("Carro trazido!")
            end
        end
    end
end})

-- NOVO: RGB Veiculo
VehicleTab:AddSection({"RGB Veiculo"})
VehicleTab:AddToggle({"RGB Veiculo", false, function(v)
    if v then
        local hue = 0
        KX.vehicleRgbConnection = RunService.RenderStepped:Connect(function()
            hue = (hue + 0.005) % 1
            local color = Color3.fromHSV(hue, 1, 1)
            local hum = getHum(player)
            if hum and hum.SeatPart then
                local model = hum.SeatPart:FindFirstAncestorOfClass("Model")
                if model then
                    for _, part in ipairs(model:GetDescendants()) do
                        if part:IsA("BasePart") then
                            part.Color = color
                        end
                    end
                end
            end
        end)
        notify("RGB Veiculo ativado!")
    else
        if KX.vehicleRgbConnection then
            KX.vehicleRgbConnection:Disconnect()
            KX.vehicleRgbConnection = nil
        end
        notify("RGB Veiculo desativado!")
    end
end})

-- ============================================================
-- WORLD TAB (ORIGINAL)
-- ============================================================
WorldTab:AddSection({"Tempo"})
WorldTab:AddButton({"Dia", function()
    Lighting.ClockTime = 14; Lighting.FogEnd = 100000; Lighting.Brightness = 1; notify("Dia ativado!")
end})
WorldTab:AddButton({"Noite", function()
    Lighting.ClockTime = 0; Lighting.FogEnd = 100000; Lighting.Brightness = 0.5; notify("Noite ativada!")
end})
WorldTab:AddButton({"Por do Sol", function()
    Lighting.ClockTime = 18; Lighting.FogEnd = 80000; Lighting.Brightness = 0.75; notify("Por do Sol ativado!")
end})
WorldTab:AddSlider({"Horario", 0, 24, 14, function(v) Lighting.ClockTime = v end})

WorldTab:AddSection({"Clima"})
WorldTab:AddButton({"Limpar", function() Lighting.FogEnd = 100000; Lighting.Brightness = 1; notify("Clima limpo!") end})
WorldTab:AddButton({"Nevoa", function() Lighting.FogEnd = 5000; Lighting.FogColor = Color3.fromRGB(200,200,200); notify("Nevoa ativada!") end})
WorldTab:AddButton({"Chuva (Efeito)", function()
    for _, child in ipairs(workspace:GetDescendants()) do
        if child:IsA("Part") and (child.Name:lower():find("rain") or child.Name:lower():find("chuva")) then
            child.Transparency = 0
        end
    end
    notify("Chuva ativada!")
end})

WorldTab:AddSection({"Gravidade"})
WorldTab:AddButton({"Gravidade Normal", function() workspace.Gravity = 196.2; notify("Gravidade normal!") end})
WorldTab:AddButton({"Gravidade Baixa", function() workspace.Gravity = 50; notify("Gravidade baixa!") end})
WorldTab:AddButton({"Gravidade Zero", function() workspace.Gravity = 10; notify("Gravidade zero!") end})
WorldTab:AddSlider({"Custom", 1, 500, 196, function(v) workspace.Gravity = v end})

WorldTab:AddSection({"Outros"})
WorldTab:AddButton({"Destruir Todas as Trancas", function()
    for _, v in ipairs(workspace:GetDescendants()) do
        if v:IsA("Part") and (v.Name:lower():find("lock") or v.Name:lower():find("tranca") or v.Name:lower():find("door")) then
            pcall(function() v:Destroy() end)
        end
    end
    notify("Trancas destruidas!")
end})
WorldTab:AddButton({"Destruir Cercas", function()
    for _, v in ipairs(workspace:GetDescendants()) do
        if v:IsA("Part") and (v.Name:lower():find("fence") or v.Name:lower():find("cerca") or v.Name:lower():find("barrier")) then
            pcall(function() v:Destroy() end)
        end
    end
    notify("Cercas destruidas!")
end})
WorldTab:AddButton({"Destruir Portas", function()
    for _, v in ipairs(workspace:GetDescendants()) do
        if v:IsA("Part") and (v.Name:lower():find("door") or v.Name:lower():find("porta")) then
            pcall(function() v:Destroy() end)
        end
    end
    notify("Portas destruidas!")
end})

-- ============================================================
-- MUSIC TAB (NÃO MEXIDA - IDÊNTICA AO ORIGINAL)
-- ============================================================

local function createMusicDropdown(title, musicOptions)
    local musicNames = {}
    local categoryMap = {}
    for category, sounds in pairs(musicOptions) do
        for _, music in ipairs(sounds) do
            if music.name ~= "" then
                table.insert(musicNames, music.name)
                categoryMap[music.name] = {id = music.id, category = category}
            end
        end
    end

    MusicTab:AddDropdown({
        Name = title,
        Description = "all",
        Default = "Option 1",
        Multi = false,
        Options = musicNames,
        Callback = function(selectedSound)
            if selectedSound and categoryMap[selectedSound] then
                local soundId = categoryMap[selectedSound].id
                if soundId and soundId ~= "" then
                    tocarMusica(tostring(soundId))
                end
            end
        end
    })
end

createMusicDropdown("Forro", {
    ["forro"] = {
        {name = "ja que me essino a beber", id = "102593134121793"},
        {name = "lembranças", id = "111551362636063"},
        {name = "Passinho do barão", id = "127786586963377"},
        {name = "Bloquinho Macumbeira", id = "138345050819224"},
        {name = "eu já tava bem", id = "93590122047380"},
        {name = "PISEIRO ESTOURADO (20 sgds de intro)", id = "133190351316780"},
        {name = "forro ja cansou", id = "74812784884330"},
        {name = "GRELO E O FE", id = "72200166265935"},
        {name = "lenbro ate hoje", id = "71531533552899"},
        {name = "escolha certa", id = "107088620814881"},
        {name = "forro da rezenha", id = "120973520531216"},
        {name = "forro dudu", id = "74404168179733"},
        {name = "forro sao joao", id = "106364874935196"},
        {name = "forro engraçado paia", id = "76524290482399"},
        {name = "100% forro vaquejada", id = "92295159623916"},
        {name = "PASTOR MIRIM E A LÍNGUA DOS ANJOS", id = "71153532555470"},
        {name = "PARA NÃO ESQUECER QUEM SOMOS", id = "88937498361674"},
        {name = "Uno zero", id = "112959083808887"},
        {name = "Iate do neymar", id = "135738534706063"},
        {name = "Batidao na aldeia", id = "79953696595578"},
    }
})

createMusicDropdown("Musicas e Memes Aleatorio", {
    ["memes"] = {
        {name = "desca dai seu corno", id = "119738878921996"},
        {name = "GTA ESTOURADO", id = "109337680029292"},
        {name = "ANXIETY (Amapiano Re-fix)", id = "101483901475189"}, 
        {name = "Meu corpo, minhas regras", id = "127587901595282"},
        {name = "Megalovania but its only the melodies", id = "104500091160463"},
        {name = "androphono strikes back", id = "78312089943968"},
        {name = "Bamm Bamm", id = "128730685516895"},
        {name = "longe de mais", id = "124478512057763"},
        {name = "Garoto de Copacabana", id = "135648634110254"},
        {name = "CELL!", id = "117634275895085"},
        {name = "Boa vibe em Ubatuba", id = "139059061493558"},
        {name = "SLIP AWAY", id = "126152928520174"},
        {name = "Alone in Motion", id = "122379348696948"},
        {name = "Fade Away", id = "81002139735874"},
        {name = "Wounds & Wishes", id = "109347979566607"},
        {name = "Ascensão do Monarca", id = "101864243033211"},
        {name = "carro do ovo", id = "3148329638"},
        {name = "ingles bus (fling ou kill bus)", id = "123268013026823"},
        {name = "MIKU MIKU HATSUNE", id = "112783541496955"},
        {name = "Escalando a Seleção Brasileira para a Copa", id = "116546457407236"},
    }
})

createMusicDropdown("Funk", {
    ["Funk"] = {
        {name = "EX", id = "139081830944037"},
        {name = "MACONHA", id = "77654661905802"},
        {name = "TURQUIA DJ C4", id = "80937607674721"},
        {name = "SEU ZE", id = "82889452939550"},
        {name = "tuturu", id = "83929954510410"},
        {name = "vai rebola", id = "120075559226752"},
        {name = "saia", id = "104226699513043"},
        {name = "meia noite", id = "86617433885915"},
        {name = "bonde", id = "132706975762383"},
        {name = "sla", id = "75531002354210"},
        {name = "arabe", id = "131441995313231"},
        {name = "dim dim dom", id = "135194449370589"},
        {name = "ritimada", id = "128354328768039"},
        {name = "XECHE MATE", id = "129902784040741"},
        {name = "come cu no uno", id = "75839538917529"},
        {name = "comer novinha", id = "84434631780133"},
        {name = "eu não sou gay", id = "82816587043443"},
        {name = "porta calcinha", id = "135005299702467"},
        {name = "quem gosta de bucetão", id = "84434631780133"},
        {name = "vai mamar o bonde", id = "137888824649807"},
        {name = "sla", id = "92524227941055"},
        {name = "TA", id = "100723668752455"},
        {name = "TE", id = "136923848139722"},
        {name = "ch", id = "127615454743173"},
        {name = "montagem", id = "90570459800891"},
        {name = "cretina", id = "75531002354210"},
        {name = "Uniao Flasco", id = "81628621752701"},
        {name = "tapa", id = "114345007529009"},
        {name = "sacanagem", id = "124054822886984"},
        {name = "achei que bebeia bem", id = "111551362636063"},
        {name = "Amor Hospitalar", id = "96259351729049"},
        {name = "chupa piroka", id = "94214367115154"},
        {name = "ela", id = "120373931922938"},
        {name = "cvlt", id = "123045007438309"},
        {name = "eu gosto de tu fy", id = "73937969824874"},
        {name = "o bagulho mudo", id = "135750430892149"},
        {name = "seda preta", id = "87195083268833"},
        {name = "ou ou ou", id = "126196231406971"},
        {name = "meca", id = "108226178439659"},
        {name = "antares", id = "122938948937941"},
        {name = "Piranha Piranha", id = "123238370098753"},
        {name = "Batida do Tal Do Tbt", id = "91007045451630"},
        {name = "comeno uma prkinha", id = "94214367115154"},
        {name = "soca na danada", id = "100337717591420"},
        {name = "desce talarica", id = "110363768678499"},
        {name = "RITMADA DE VILAO", id = "121405804171398"},
        {name = "Paredao morcegao", id = "138120757806690"},
        {name = "Jogo", id = "73198805524530"},
        {name = "BEM VINDO AO HELIPA", id = "94672348312515"},
        {name = "de sainha bem curtinha (40s intro)", id = "140655042547224"},
        {name = "Ajoelha", id = "127052251825619"},
        {name = "Eu não nasci pra trabalhar", id = "95197852052116"},
        {name = "BITCH!", id = "103288558732219"},
        {name = "arabe funk", id = "93451391025129"},
        {name = "PUXANDO CBL", id = "78631447496051"},
        {name = "REBOLA", id = "121046655523341"},
        {name = "JOGA NO PAI", id = "128011871344522"},
        {name = "RADINHO", id = "139693447546059"},
        {name = "ESTOURADAO KKKK", id = "86839065790068"},
        {name = "TIPO NINO", id = "140336018782383"},
        {name = "NINO PT2", id = "97708834121472"},
        {name = "EXCITADINHA? KKKK", id = "110176270788146"},
        {name = "BERIMBAU KK", id = "77712236704085"},
        {name = "NAT FUNK", id = "107416893652681"},
        {name = "MTG EXPLODE", id = "81384105684889"},
        {name = "envolvidão", id = "127775034804421"},
        {name = "RAIL GRIND ESTOURADOOO", id = "135958179501280"},
        {name = "CLYXAL X NYT", id = "100258273816054"},
        {name = "SENTA E RBL", id = "107513285979080"},
        {name = "chairy", id = "130071638363509"},
        {name = "Seu Pedreiro", id = "116272171755349"},
        {name = "fuga na viatura", id = "131891110268352"},
        {name = "funkphonk fumando verde", id = "112143944982807"},
        {name = "que que sharke", id = "129546408528391"},
        {name = "pre treino", id = "136869502216760"},
        {name = "CVRL", id = "124244582950595"},
        {name = "batida Brega Violino (Beat Brega Funk)", id = "99399643204701"},
        {name = "Dança do Canguru (Pke Gaz1nh)", id = "86876136192157"},
        {name = "MONTAGEM ARABIANA (Pke Gaz1nh)", id = "78076624091098"},
        {name = "Manda o papo (NGI)", id = "132642647937688"},
        {name = "Viver bem", id = "82805460494325"},
        {name = "Faixa estronda", id = "121187736532042"},
        {name = "Ritmo Pixelado", id = "93928823862203"},
        {name = "Viagem Sonora", id = "79349174602261"},
        {name = "Melodia Virtual", id = "139147474886402"},
        {name = "Melodia Serena", id = "97011217688307"},
        {name = "SENTA", id = "124085422276732"},
        {name = "crazy-lol", id = "106958630419629"},
        {name = "V7", id = "80348640826643"},
        {name = "UIUAH", id = "82894376737849"},
        {name = "meta ritmo", id = "110091098283354"},
        {name = "CAPPUCCINO ASSASSINO (SPEDUP)", id = "132733033157915"},
        {name = "haha (NGI)", id = "122114766584918"},
    }
})

createMusicDropdown("Phonk", {
    ["phonk"] = {
        {name = "wyles", id = "85385155970460"},
        {name = "Vai Que E No Vapor!", id = "94845998956451"},
        {name = "phonk kawai", id = "91502410121438"},
        {name = "querendo da a bucet@", id = "72720721570850"},
        {name = "vem no pocpoc", id = "102333419023382"},
        {name = "tatiu wim", id = "122871512353520"},
        {name = "novinha sapeca", id = "111668097052966"},
        {name = "novinha representa", id = "93786060174790"},
        {name = "phonk1", id = "77501611905348"},
        {name = "phonk2", id = "126887144190812"},
        {name = "phonk sarra", id = "132436320685732"},
        {name = "phonk3", id = "90323407842935"},
        {name = "novinha dançapanpa", id = "132245626038510"},
        {name = "phonk sexoagreçivo", id = "111995323199676"},
        {name = "phonk4", id = "115016589376700"},
        {name = "phonk5", id = "118740708757685"},
        {name = "phonk6", id = "139435437308948"},
        {name = "phonk chapaquente", id = "109189438638906"},
        {name = "phonk rajada", id = "105126065014034"},
        {name = "rede globo", id = "138487820505005"},
        {name = "phonk indiano", id = "87968531262747"},
        {name = "vapo do vapo", id = "106317184644394"},
        {name = "tutatatutata", id = "112068892721408"},
        {name = "phonk slower", id = "122852029094656"},
        {name = "phonk9", id = "91760524161503"},
        {name = "phonk10", id = "73140398421340"},
        {name = "phonk11", id = "137962454483542"},
        {name = "phonk12", id = "84733736048142"},
        {name = "phonk13", id = "106322173003761"},
        {name = "phonk14", id = "94604796823780"},
        {name = "phonk15", id = "118063577904953"},
        {name = "phonk16", id = "115567432786512"},
        {name = "phonk toq", id = "71304501822029"},
        {name = "phonk hey", id = "132218979961283"},
        {name = "phonk17", id = "102708912256857"},
        {name = "phonk18", id = "140642559093189"},
        {name = "phonk neve", id = "13530439660"},
        {name = "phonk19", id = "87863924786534"},
        {name = "phonk20", id = "133135085604736"},
        {name = "phonk lento", id = "97258811783169"},
        {name = "phonk21", id = "92308400487695"},
        {name = "tipo wym", id = "88064647826500"},
        {name = "estouradassa1", id = "92175624643620"},
        {name = "estouradassa2", id = "108099943758978"},
        {name = "trem", id = "114608169341947"},
        {name = "eoropa", id = "111346133543699"},
        {name = "atimosphekika", id = "77857496821844"},
        {name = "phonk ALL THE TIME", id = "123809083385992"},
        {name = "Automotivo Blondie (Pke Gaz1nh)", id = "74564219749776"},
        {name = "Unknown v2", id = "118225359190317"},
        {name = "MTG TU VAI SENTAR (Pke Gaz1nh)", id = "115317874112657"},
        {name = "Catuquanvan", id = "88038595663211"},
        {name = "F-D-1 (slowed)", id = "124958445624871"},
        {name = "Sucessagem", id = "88551699463723"},
        {name = "ILOVE phonksla", id = "82148953715595"},
        {name = "SPEED SLIDE", id = "118959437310311"},
        {name = "TOMA FUNK PHONK", id = "126291069838831"},
        {name = "PASSO BEM SOLTO X NEW JAZZ", id = "122706595087279"},
        {name = "MONTAGEM BIONICA DIAMANTE", id = "122338822665007"},
        {name = "BALA SELVAGEM!", id = "96180057167470"},
        {name = "COMO TU", id = "86928685812280"},
        {name = "MONTAGEM SOLAR TROPICANO (SPEED UP)", id = "116461681407294"},
        {name = "MONTAGEM SOLAR TROPICANO (SLOWED)", id = "109308273341422"},
        {name = "YO DE TI", id = "125181345407169"},
        {name = "Beauty, (Phonk), Super sped up", id = "71123357599630"},
        {name = "BRAZIL DO FUNK", id = "133498554139200"},
        {name = "FUNK DO RAVE 1.0", id = "137135395010424"},
        {name = "Portao Funk", id = "70900514961735"},
        {name = "FUTABA", id = "91834632690710"},
        {name = "Melódica Explosão De Melodia", id = "98371771055411"},
        {name = "HIPNOTIZA", id = "117668905142866"},
        {name = "CRISTAL NOTURNO", id = "103695219371872"},
        {name = "SKY HIGH", id = "123517126955383"},
        {name = "GOTH FUNK", id = "97662362226511"},
        {name = "SUBURBANA", id = "139825057894568"},
        {name = "STORYMODECOOL", id = "87115976125426"},
        {name = "KOBALT", id = "79381341943021"},
        {name = "andante bacterial", id = "105882833374061"},
        {name = "ANGEL Speed Up", id = "139593870988593"},
        {name = "MALDITA", id = "133814632960968"},
        {name = "MIDZUKI speed up", id = "129151948619922"},
        {name = "CRISTAL", id = "103445348511856"},
    }
})

MusicTab:AddSection({"Tocar por ID"})
MusicTab:AddTextBox({
    Name = "ID da musica",
    PlaceholderText = "Digite o ID e pressione Enter",
    Callback = function(v)
        if v and v ~= "" then
            tocarMusica(tostring(v))
            notify("Tocando ID: "..v)
        end
    end
})

MusicTab:AddButton({
    Name = "Stop",
    Description = "ALL music",
    Callback = function()
        tocarMusica("")
        notify("Musica parada!")
    end
})

MusicTab:AddButton({"Boom Box Spam", function()
    local ids = {"3148329638","94410505324605","112783541496955","138345050819224","106412079335663"}
    for _, id in ipairs(ids) do
        task.spawn(function() tocarMusica(id) end)
        task.wait(0.08)
    end
    notify("Boom Box Spam!")
end})

MusicTab:AddSection({"All Music (Para Todos)"})
MusicTab:AddParagraph({"Funcao:", "Toca musica para TODOS os jogadores"})

MusicTab:AddTextBox({
    Name = "ID (Todos)",
    PlaceholderText = "Digite o ID e pressione Enter",
    Callback = function(v)
        if v and v ~= "" then
            tocarMusicaParaTodos(tostring(v))
            notify("Tocando para todos! ID: "..v)
        end
    end
})

MusicTab:AddButton({
    Name = "Stop All",
    Description = "Para musica de todos",
    Callback = function()
        tocarMusicaParaTodos("")
        notify("Musica de todos parada!")
    end
})

MusicTab:AddButton({"Boom Box Spam (Todos)", function()
    local ids = {"3148329638","94410505324605","112783541496955","138345050819224","106412079335663"}
    for _, id in ipairs(ids) do
        task.spawn(function() tocarMusicaParaTodos(id) end)
        task.wait(0.08)
    end
    notify("Boom Box Spam para todos!")
end})-- ============================================================
-- SHADERS TAB (COMPLETO DO DARK HUB)
-- ============================================================
ShadersTab:AddSection({"Shaders"})
ShadersTab:AddSection({"Type 1 (Client-Sided)"})

ShadersTab:AddButton({
    Name = "Enable Shaders (Irreversible)",
    Callback = function()
        local workspace = game:GetService("Workspace")
        local Lighting = game:GetService("Lighting")
        local RunService = game:GetService("RunService")
        local Debris = game:GetService("Debris")
        local TweenService = game:GetService("TweenService")
        local SoundService = game:GetService("SoundService")
        local Players = game:GetService("Players")
        local player = Players.LocalPlayer
        local model = workspace:FindFirstChild("Model")
        
        if model then
            local function setMat(obj)
                for _, c in pairs(obj:GetChildren()) do
                    if c:IsA("BasePart") then
                        c.Material = Enum.Material.Basalt
                    elseif c:IsA("Model") or c:IsA("Folder") then
                        setMat(c)
                    end
                end
            end
            if model:FindFirstChild("001_SnowStreet") then setMat(model["001_SnowStreet"]) end
            if model:FindFirstChild("Street") then
                for _, o in pairs(model.Street:GetDescendants()) do
                    if o:IsA("BasePart") then o.Material = Enum.Material.Basalt end
                end
            end
            for _, o in pairs(model:GetChildren()) do
                if o:IsA("BasePart") and (o.Name == "Sidewalk" or o.Name == "Wedge") and o.Material == Enum.Material.SmoothPlastic then
                    o.Material = Enum.Material.Cobblestone
                end
            end
            model.ChildAdded:Connect(function(obj)
                if obj:IsA("BasePart") and (obj.Name == "Sidewalk" or obj.Name == "Wedge") and obj.Material == Enum.Material.SmoothPlastic then
                    obj.Material = Enum.Material.Cobblestone
                end
            end)
        end
        
        local soundPart = Instance.new("Part")
        soundPart.Size = Vector3.new(1,1,1); soundPart.Transparency = 1; soundPart.Anchored = true; soundPart.CanCollide = false
        soundPart.Parent = workspace
        local character = player.Character or player.CharacterAdded:Wait()
        local hrp = character:WaitForChild("HumanoidRootPart")
        
        local birdSound = Instance.new("Sound")
        birdSound.Name = "BirdsSound"; birdSound.SoundId = "rbxassetid://1237969272"; birdSound.Looped = true
        birdSound.Volume = 0.05; birdSound.Parent = soundPart
        
        local wolfSound = Instance.new("Sound")
        wolfSound.SoundId = "rbxassetid://6654360741"; wolfSound.Volume = 0.05; wolfSound.Looped = false
        wolfSound.Parent = workspace
        
        RunService.Heartbeat:Connect(function()
            if hrp and hrp.Parent then soundPart.Position = hrp.Position + Vector3.new(0,10,0) end
        end)
        
        local function isNight()
            local t = Lighting.ClockTime
            return (t >= 18 or t <= 6)
        end
        
        task.spawn(function()
            while true do
                if isNight() then
                    if birdSound.IsPlaying then birdSound:Stop() end
                    if wolfSound.IsPlaying then wolfSound:Stop() end
                    wolfSound:Play()
                else
                    if wolfSound.IsPlaying then wolfSound:Stop() end
                    if not birdSound.IsPlaying then birdSound:Play() end
                end
                wait(20)
            end
        end)
        
        -- Fonte
        local fountainPart = Instance.new("Part")
        fountainPart.Anchored = true; fountainPart.CanCollide = false; fountainPart.Transparency = 1
        fountainPart.Size = Vector3.new(1,1,1); fountainPart.Position = Vector3.new(-27,19,15)
        fountainPart.Parent = workspace
        
        local attachment = Instance.new("Attachment")
        attachment.Position = Vector3.new(-27,19,15); attachment.Parent = fountainPart
        
        local fountainSound = Instance.new("Sound")
        fountainSound.Name = "FountainSound"; fountainSound.SoundId = "rbxassetid://4766793559"
        fountainSound.Looped = true; fountainSound.Volume = 0.03; fountainSound.EmitterSize = 10
        fountainSound.RollOffMode = Enum.RollOffMode.Linear; fountainSound.MaxDistance = 100
        fountainSound.Parent = attachment; fountainSound:Play()
        
        local customSound = Instance.new("Sound")
        customSound.Name = "MyCustomSound"; customSound.SoundId = "rbxassetid://9048659736"
        customSound.Volume = 0.01; customSound.Looped = true; customSound.Parent = workspace; customSound:Play()
        
        local active = false
        local stars = {}
        local shootingStarsFolder = Instance.new("Folder",workspace)
        shootingStarsFolder.Name = "ShootingStars"
        local STAR_COUNT = 300; local SHOOTING_STAR_CHANCE = 0.3; local SHOOTING_STAR_MAX = 12; local shootingStarCooldown = 0.1
        
        local spaceSound = Instance.new("Sound",workspace)
        spaceSound.SoundId = "rbxassetid://1843520836"; spaceSound.Volume = 0.3; spaceSound.Looped = true
        spaceSound.Name = "SpaceAmbience"
        
        local function createStar()
            local star = Instance.new("Part")
            local size = math.random(1,3)*0.5
            star.Size = Vector3.new(size,size,size)
            star.Position = Vector3.new(math.random(-1000,1000),math.random(300,700),math.random(-1000,1000))
            star.Anchored = true; star.CanCollide = false; star.Material = Enum.Material.Neon
            local colors = {Color3.fromRGB(255,255,255),Color3.fromRGB(255,255,180),Color3.fromRGB(180,200,255)}
            star.Color = colors[math.random(1,#colors)]; star.Name = "Star"; star.Parent = workspace
            local light = Instance.new("PointLight",star)
            light.Brightness = 2 + math.random()*1.5; light.Range = 12
            spawn(function()
                while star.Parent and active do
                    star.Transparency = 0.2 + math.sin(tick()*math.random(2,5))*0.2
                    RunService.Heartbeat:Wait()
                end
                if star.Parent then star:Destroy() end
            end)
            table.insert(stars,star)
        end
        
        local function createShootingStar()
            if not active then return end
            local startPos = Vector3.new(math.random(-1000,1000),math.random(350,600),math.random(-1000,1000))
            local dir = Vector3.new(math.random(-1,1),math.random(-0.1,0.1),math.random(-1,1)).Unit
            local speed = math.random(350,550)
            local isFire = math.random() <= SHOOTING_STAR_CHANCE
            local color = isFire and Color3.fromRGB(255,50,50) or Color3.fromRGB(255,255,220)
            local trailColor = isFire and ColorSequence.new(Color3.fromRGB(255,120,0),Color3.fromRGB(255,230,50)) or ColorSequence.new(Color3.fromRGB(255,255,255),Color3.fromRGB(255,255,180))
            local star = Instance.new("Part")
            star.Size = Vector3.new(0.5,0.5,3); star.Position = startPos; star.Anchored = true; star.CanCollide = false
            star.Material = Enum.Material.Neon; star.Color = color; star.Name = "ShootingStar"
            star.Parent = shootingStarsFolder
            local att0 = Instance.new("Attachment",star); local att1 = Instance.new("Attachment",star)
            att1.Position = Vector3.new(0,0,-3)
            local trail = Instance.new("Trail",star)
            trail.Attachment0 = att0; trail.Attachment1 = att1; trail.Lifetime = 0.35; trail.Color = trailColor
            trail.LightEmission = 1; trail.WidthScale = NumberSequence.new({NumberSequenceKeypoint.new(0,1),NumberSequenceKeypoint.new(1,0)})
            local light = Instance.new("PointLight",star)
            light.Brightness = isFire and 12 or 7; light.Range = 35; light.Color = color
            if isFire then
                local fire = Instance.new("Fire",star)
                fire.Heat = 15; fire.Size = 3.5; fire.Color = Color3.fromRGB(255,110,0); fire.SecondaryColor = Color3.fromRGB(255,210,0)
            end
            local lifetime = math.random(1,1.5); local timePassed = 0; local moveConn
            moveConn = RunService.Heartbeat:Connect(function(dt)
                if not active then moveConn:Disconnect(); if star.Parent then star:Destroy() end; return end
                timePassed = timePassed + dt
                if timePassed >= lifetime then moveConn:Disconnect(); if star.Parent then star:Destroy() end; return end
                local curve = math.sin(timePassed*20)*0.5
                star.Position = star.Position + (dir+Vector3.new(0,curve,0)).Unit*speed*dt
            end)
            Debris:AddItem(star,4)
        end
        
        local function updateSky()
            local hour = Lighting.ClockTime
            local shouldBeActive = hour >= 18 or hour < 6
            if shouldBeActive and not active then
                active = true
                Lighting.FogColor = Color3.fromRGB(10,10,30); Lighting.FogEnd = 5000; Lighting.Brightness = 2
                for _,s in ipairs(stars) do if s and s.Parent then s:Destroy() end end; stars = {}
                for _,p in ipairs(shootingStarsFolder:GetChildren()) do p:Destroy() end
                for i=1,STAR_COUNT do createStar() end; spaceSound:Play()
            elseif not shouldBeActive and active then
                active = false
                for _,s in ipairs(stars) do if s and s.Parent then s:Destroy() end end; stars = {}
                for _,p in ipairs(shootingStarsFolder:GetChildren()) do p:Destroy() end; spaceSound:Stop()
                Lighting.FogColor = Color3.fromRGB(192,192,192); Lighting.FogEnd = 100000; Lighting.Brightness = 2
            end
        end
        
        task.spawn(function()
            while true do
                if active then for i=1,SHOOTING_STAR_MAX do createShootingStar(); task.wait(shootingStarCooldown) end
                else task.wait(1) end
            end
        end)
        
        task.spawn(function() while true do updateSky(); task.wait(1) end end)
        
        local rainFolder = Instance.new("Folder",workspace); rainFolder.Name = "FakeRain"; local isRaining = false
        
        local birds = Instance.new("Sound",SoundService); birds.SoundId = "rbxassetid://9111139882"
        birds.Volume = 0.2; birds.Looped = true; birds:Play()
        local rainSound = Instance.new("Sound",SoundService); rainSound.SoundId = "rbxassetid://9118823106"
        rainSound.Volume = 0.3; rainSound.Looped = true; rainSound:Play()
        local thunder = Instance.new("Sound",SoundService); thunder.SoundId = "rbxassetid://9120018695"; thunder.Volume = 0.4
        
        local function updateBirdSound() birds.Volume = isRaining and 0 or 0.2 end
        
        local function spawnRain()
            isRaining = true; updateBirdSound()
            for i=1,120 do
                local drop = Instance.new("Part"); drop.Size = Vector3.new(0.1,2,0.1); drop.Anchored = true
                drop.CanCollide = false; drop.Material = Enum.Material.Glass; drop.Transparency = 0.5
                drop.Color = Color3.fromRGB(160,160,255); drop.Position = Vector3.new(math.random(-150,150),100,math.random(-150,150))
                drop.Parent = rainFolder
                local tween = TweenService:Create(drop,TweenInfo.new(1),{Position=drop.Position-Vector3.new(0,60,0)})
                tween:Play(); Debris:AddItem(drop,1.5)
            end
            wait(1.5); isRaining = false; updateBirdSound()
        end
        
        local function lightningStrike()
            local flash = Instance.new("Part"); flash.Size = Vector3.new(1,1000,1); flash.Anchored = true
            flash.CanCollide = false; flash.Transparency = 0.4; flash.Material = Enum.Material.Neon; flash.Color = Color3.new(1,1,1)
            flash.Position = Vector3.new(math.random(-100,100),500,math.random(-100,100)); flash.Parent = workspace
            Lighting.Brightness = Lighting.Brightness + 1.5; thunder:Play(); wait(0.1)
            Lighting.Brightness = Lighting.Brightness - 1.5; flash:Destroy()
        end
        
        for _,part in pairs(workspace:GetDescendants()) do
            if part:IsA("BasePart") and part.Material == Enum.Material.SmoothPlastic then
                part.Reflectance = 0.25
            end
        end
        
        task.spawn(function() while true do spawnRain(); if math.random() < 0.2 then lightningStrike() end; wait(1) end end)
        
        Lighting.Brightness = 2; Lighting.GlobalShadows = true; Lighting.OutdoorAmbient = Color3.fromRGB(70, 70, 70)
        Lighting.FogColor = Color3.fromRGB(120, 130, 140); Lighting.FogStart = 80; Lighting.FogEnd = 600
        Lighting.EnvironmentSpecularScale = 1; Lighting.EnvironmentDiffuseScale = 0.5
        
        local sky = Instance.new("Sky"); sky.SkyboxBk = "rbxassetid://159454299"; sky.SkyboxDn = "rbxassetid://159454296"
        sky.SkyboxFt = "rbxassetid://159454293"; sky.SkyboxLf = "rbxassetid://159454286"; sky.SkyboxRt = "rbxassetid://159454300"
        sky.SkyboxUp = "rbxassetid://159454304"; sky.Parent = Lighting
        
        local color = Instance.new("ColorCorrectionEffect", Lighting); color.Brightness = 0.03; color.Contrast = 0.15
        color.Saturation = 0.05; color.TintColor = Color3.fromRGB(255, 240, 220)
        
        local bloom = Instance.new("BloomEffect", Lighting); bloom.Intensity = 0.8; bloom.Size = 56; bloom.Threshold = 0.9
        local sunRays = Instance.new("SunRaysEffect", Lighting); sunRays.Intensity = 0.05; sunRays.Spread = 0.8
        local blur = Instance.new("BlurEffect", Lighting); blur.Size = 0
    end
})

-- ============================================================
-- GAMEPASS TAB (COMPLETO)
-- ============================================================
GamepassTab:AddSection("Effects Avatar")

local effectList = {
   {name = "Corações Amarelos", id = "18635672195", code = "001HeartsYellow"},
   {name = "Corações Verdes", id = "18635727693", code = "002HeartsGreen"},
   {name = "Corações Azuis", id = "18635732186", code = "003HeartsBlue"},
   {name = "Corações Roxos", id = "18635723426", code = "004HeartsPurple"},
   {name = "Corações Rosas", id = "18635726250", code = "005HeartsPink"},
   {name = "Corações Vermelhos", id = "18635729673", code = "006HeartsRed"},
   {name = "Pontos Laranjas", id = "18637252424", code = "010DotsOrange"},
   {name = "Pontos Amarelos", id = "18637263004", code = "011DotsYellow"},
   {name = "Pontos Verdes", id = "18637265264", code = "013DotsGreen"},
   {name = "Pontos Azuis", id = "18637256859", code = "014DotsBlue"},
   {name = "Pontos Roxos", id = "18637261058", code = "015DotsPurple"},
   {name = "Pontos Rosas", id = "18637259328", code = "016DotsPink"},
   {name = "Pontos Vermelhos", id = "18637267290", code = "017DotsRed"},
   {name = "Brilho Branco", id = "18637115654", code = "020TwinkleWhite"},
   {name = "Brilho Amarelo", id = "18637118923", code = "021TwinkleYellow"},
   {name = "Brilho Verde", id = "18637151114", code = "022TwinkleGreen"},
   {name = "Brilho Roxo", id = "18637153880", code = "023TwinklePurple"},
   {name = "Brilho Rosa", id = "18637157071", code = "024TwinklePink"},
   {name = "Brilho Vermelho", id = "18637155247", code = "025TwinkleRed"},
   {name = "Fogo Branco", id = "18637074370", code = "030FireWhite"},
   {name = "Fogo Laranja", id = "18637025451", code = "031FireOrange"},
   {name = "Fogo Verde", id = "18637078598", code = "032FireGreen"},
   {name = "Fogo Azul", id = "18637076370", code = "033FireBlue"},
   {name = "Fogo Roxo", id = "18637070174", code = "034FirePurple"},
   {name = "Fogo Preto", id = "18637072603", code = "035FireBlack"},
   {name = "Corações Pequenos Amarelos", id = "18637339451", code = "040SmallHeartsYellow"},
   {name = "Corações Pequenos Verdes", id = "18637337576", code = "041SmallHeartsGreen"},
   {name = "Corações Pequenos Azuis", id = "18637345162", code = "042SmallHeartsBlue"},
   {name = "Corações Pequenos Roxos", id = "18637335865", code = "043SmallHeartsPurple"},
   {name = "Corações Pequenos Rosas", id = "18637343416", code = "044SmallHeartsPink"},
   {name = "Corações Pequenos Vermelhos", id = "18637341847", code = "045SmallHeartsRed"},
   {name = "Faíscas Brancas", id = "18637383085", code = "050SparksWhite"},
   {name = "Faíscas Verdes", id = "18637385236", code = "051SparksGreen"},
   {name = "Faíscas Azuis", id = "18637386856", code = "052SparksBlue"},
   {name = "Faíscas Roxas", id = "18637442447", code = "053SparksPurple"},
   {name = "Faíscas Rosas", id = "18637445897", code = "054SparksPink"},
   {name = "Faíscas Vermelhas", id = "18637447550", code = "055SparksRed"},
   {name = "Bolhas Verdes", id = "18637493072", code = "061BubbleGreen"},
   {name = "Bolhas Azuis", id = "18637499282", code = "062BubbleBlue"},
   {name = "Bolhas Roxas", id = "18637497343", code = "063BubblePurple"},
   {name = "Bolhas Vermelhas", id = "18637500927", code = "064BubbleRed"},
   {name = "Música Branca", id = "18637675173", code = "070MusicWhite"},
   {name = "Música Verde", id = "18637677789", code = "071MusicGreen"},
   {name = "Música Azul", id = "18637680960", code = "072MusicBlue"},
   {name = "Música Roxa", id = "18637679384", code = "073MusicPurple"},
   {name = "Música Vermelha", id = "18637672698", code = "074MusicRed"},
   {name = "Fumaça Branca", id = "18637791748", code = "080SmokeWhite"},
   {name = "Fumaça Amarela", id = "18637800482", code = "081SmokeYellow"},
   {name = "Fumaça Laranja", id = "18637793920", code = "082SmokeOrange"},
   {name = "Fumaça Verde", id = "18637789299", code = "083SmokeGreen"},
   {name = "Fumaça Azul", id = "18637803021", code = "084SmokeBlue"},
   {name = "Fumaça Roxa", id = "18637813360", code = "085SmokePurple"},
   {name = "Fumaça Vermelha", id = "18637796598", code = "086SmokeRed"},
   {name = "Fumaça Preta", id = "18637798529", code = "087SmokeBlack"},
   {name = "Estrela Branca", id = "18637942956", code = "090StarWhite"},
   {name = "Estrela Laranja", id = "18637946172", code = "091StarOrange"},
   {name = "Estrela Verde", id = "18637934500", code = "092StarGreen"},
   {name = "Estrela Azul", id = "18637940338", code = "093StarBlue"},
   {name = "Estrela Roxa", id = "18637944796", code = "094StarPurple"},
   {name = "Estrela Rosa", id = "18637947820", code = "095StarPink"},
   {name = "Estrela Vermelha", id = "18637949457", code = "096StarRed"}
}

local selectedEffect = effectList[1]
local dropdownOptions = {}
for _, effect in ipairs(effectList) do table.insert(dropdownOptions, effect.name) end

local Dropdown = GamepassTab:AddDropdown({
   Name = "Select Effects",
   Options = dropdownOptions,
   Default = effectList[1].name,
   Callback = function(option)
      for _, effect in ipairs(effectList) do
        if effect.name == option then selectedEffect = effect; break end
      end
   end
})

GamepassTab:AddButton({Name = "Equip Effects", Callback = function()
    game:GetService("ReplicatedStorage").Remotes.ApplyEmmiter:InvokeServer(selectedEffect.id, selectedEffect.code)
end})

GamepassTab:AddSection({"Fires"})

local FireTypes = {
   ["Vermelho"] = {id = "18637500927", emitter = "064BubbleRed"},
   ["Roxo"] = {id = "18637497343", emitter = "063BubblePurple"},
   ["Azul"] = {id = "18637499282", emitter = "062BubbleBlue"},
   ["Verde"] = {id = "18637493072", emitter = "061BubbleGreen"}
}

local selectedFire = "Verde"

GamepassTab:AddDropdown({Name = "Select Fire", Options = {"Vermelho", "Roxo", "Azul", "Verde"}, Default = "Verde", Callback = function(option) selectedFire = option end})

GamepassTab:AddToggle({Name = "Active Fire", Default = false, Callback = function(value)
    KX.fireEnabled = value
    if KX.fireEnabled then
        local fireData = FireTypes[selectedFire]
        game:GetService("ReplicatedStorage"):WaitForChild("Remotes"):WaitForChild("ApplyEmmiter"):InvokeServer(fireData.id, fireData.emitter)
        wait(0.5)
        KX.fireLoop = task.spawn(function()
            while KX.fireEnabled do
                pcall(function()
                    game:GetService("ReplicatedStorage").Remotes.SaveOutfit:InvokeServer(25, "Outfit 25")
                    game:GetService("ReplicatedStorage").Remotes.LoadOutfit:InvokeServer(25)
                end)
                wait(0.1)
            end
        end)
    else
        KX.fireEnabled = false
        if KX.fireLoop then task.cancel(KX.fireLoop); KX.fireLoop = nil end
    end
end})

GamepassTab:AddSection("Fires and Smokes")

GamepassTab:AddDropdown({Name = "Fire Colors", Options = {"White", "Orange", "Green", "Blue", "Purple", "Black"}, Default = "White", Callback = function(Value)
    KX.selectedColor = Value
end})

GamepassTab:AddButton({Name = "Equip Fire Color", Callback = function()
    local fireColors = {
        ["White"] = {id = "18637074370", code = "030FireWhite"},
        ["Orange"] = {id = "18637025451", code = "031FireOrange"},
        ["Green"] = {id = "18637078598", code = "032FireGreen"},
        ["Blue"] = {id = "18637076370", code = "033FireBlue"},
        ["Purple"] = {id = "18637070174", code = "034FirePurple"},
        ["Black"] = {id = "18637072603", code = "035FireBlack"}
    }
    if KX.selectedColor and fireColors[KX.selectedColor] then
        local colorData = fireColors[KX.selectedColor]
        game:GetService("ReplicatedStorage").Remotes.ApplyEmmiter:InvokeServer(colorData.id, colorData.code)
    end
end})

GamepassTab:AddDropdown({Name = "Smoke Colors", Options = {"White", "Yellow", "Orange", "Green", "Blue", "Purple", "Red", "Black"}, Default = "White", Callback = function(Value)
    KX.selectedSmokeColor = Value
end})

GamepassTab:AddButton({Name = "Equip Smoke Color", Callback = function()
    local smokeColors = {
        ["White"] = {id = "18637791748", code = "080SmokeWhite"},
        ["Yellow"] = {id = "18637800482", code = "081SmokeYellow"},
        ["Orange"] = {id = "18637793920", code = "082SmokeOrange"},
        ["Green"] = {id = "18637789299", code = "083SmokeGreen"},
        ["Blue"] = {id = "18637803021", code = "084SmokeBlue"},
        ["Purple"] = {id = "18637813360", code = "085SmokePurple"},
        ["Red"] = {id = "18637796598", code = "086SmokeRed"},
        ["Black"] = {id = "18637798529", code = "087SmokeBlack"}
    }
    if KX.selectedSmokeColor and smokeColors[KX.selectedSmokeColor] then
        local colorData = smokeColors[KX.selectedSmokeColor]
        game:GetService("ReplicatedStorage").Remotes.ApplyEmmiter:InvokeServer(colorData.id, colorData.code)
    end
end})

-- ============================================================
-- ANIMAÇÕES TAB (COMPLETO)
-- ============================================================
AnimationsTab:AddSection({"All You Want Animations"})

local function applyAnimation(animations)
    local plr = game.Players.LocalPlayer
    local function replaceAnim(char)
        local humanoid = char:WaitForChild("Humanoid"); local animate = char:WaitForChild("Animate")
        animate.Disabled = true
        for _, track in ipairs(humanoid:GetPlayingAnimationTracks()) do track:Stop() end
        for animationType, animationId in pairs(animations) do
            if animate:FindFirstChild(animationType) then
                for _, anim in ipairs(animate[animationType]:GetChildren()) do
                    if anim:IsA("Animation") then anim.AnimationId = animationId end
                end
            end
        end
        if animations.idleAlt and animate:FindFirstChild("idle") then
            local animAlt = animate.idle:FindFirstChild("Animation2")
            if animAlt then animAlt.AnimationId = animations.idleAlt end
        end
        humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        animate.Disabled = false
    end
    if plr.Character then replaceAnim(plr.Character) end
    plr.CharacterAdded:Connect(function(char) char:WaitForChild("Humanoid"); char:WaitForChild("Animate"); task.wait(0.5); replaceAnim(char) end)
end

AnimationsTab:AddButton({Name = "Adidas Animation", Callback = function()
    applyAnimation({
        idle = "rbxassetid://18537376492", idleAlt = "rbxassetid://18537371272", walk = "rbxassetid://18537392113",
        run = "rbxassetid://18537384940", jump = "rbxassetid://18537380791", fall = "rbxassetid://18537367238",
        swim = "rbxassetid://18537389531", swimIdle = "rbxassetid://18537387180", climb = "rbxassetid://18537378510"
    })
    notify("Adidas Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Vampire Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=1083445855", idleAlt = "http://www.roblox.com/asset/?id=1083450166",
        walk = "http://www.roblox.com/asset/?id=1083473930", run = "http://www.roblox.com/asset/?id=1083462077",
        jump = "http://www.roblox.com/asset/?id=1083455352", climb = "http://www.roblox.com/asset/?id=1083439238",
        fall = "http://www.roblox.com/asset/?id=1083443587"
    })
    notify("Vampire Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Hero Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=616111295", idleAlt = "http://www.roblox.com/asset/?id=616113536",
        walk = "http://www.roblox.com/asset/?id=616122287", run = "http://www.roblox.com/asset/?id=616117076",
        jump = "http://www.roblox.com/asset/?id=616115533", climb = "http://www.roblox.com/asset/?id=616104706",
        fall = "http://www.roblox.com/asset/?id=616108001"
    })
    notify("Hero Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Zombie Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=616158929", idleAlt = "http://www.roblox.com/asset/?id=616160636",
        walk = "http://www.roblox.com/asset/?id=616168032", run = "http://www.roblox.com/asset/?id=616163682",
        jump = "http://www.roblox.com/asset/?id=616161997", climb = "http://www.roblox.com/asset/?id=616156119",
        fall = "http://www.roblox.com/asset/?id=616157476"
    })
    notify("Zombie Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Mage Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=707742142", idleAlt = "http://www.roblox.com/asset/?id=707855907",
        walk = "http://www.roblox.com/asset/?id=707897309", run = "http://www.roblox.com/asset/?id=707861613",
        jump = "http://www.roblox.com/asset/?id=707853694", climb = "http://www.roblox.com/asset/?id=707826056",
        fall = "http://www.roblox.com/asset/?id=707829716"
    })
    notify("Mage Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Ghost Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=616006778", idleAlt = "http://www.roblox.com/asset/?id=616008087",
        walk = "http://www.roblox.com/asset/?id=616010382", run = "http://www.roblox.com/asset/?id=616013216",
        jump = "http://www.roblox.com/asset/?id=616008936", climb = "http://www.roblox.com/asset/?id=616003713",
        fall = "http://www.roblox.com/asset/?id=616005863"
    })
    notify("Ghost Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Elder Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=845397899", idleAlt = "http://www.roblox.com/asset/?id=845400520",
        walk = "http://www.roblox.com/asset/?id=845403856", run = "http://www.roblox.com/asset/?id=845386501",
        jump = "http://www.roblox.com/asset/?id=845398858", climb = "http://www.roblox.com/asset/?id=845392038",
        fall = "http://www.roblox.com/asset/?id=845396048"
    })
    notify("Elder Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Levitation Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=616006778", idleAlt = "http://www.roblox.com/asset/?id=616008087",
        walk = "http://www.roblox.com/asset/?id=616013216", run = "http://www.roblox.com/asset/?id=616010382",
        jump = "http://www.roblox.com/asset/?id=616008936", climb = "http://www.roblox.com/asset/?id=616003713",
        fall = "http://www.roblox.com/asset/?id=616005863"
    })
    notify("Levitation Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Toy Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=782841498", idleAlt = "http://www.roblox.com/asset/?id=782845736",
        walk = "http://www.roblox.com/asset/?id=782843345", run = "http://www.roblox.com/asset/?id=782842708",
        jump = "http://www.roblox.com/asset/?id=782847020", climb = "http://www.roblox.com/asset/?id=782843869",
        fall = "http://www.roblox.com/asset/?id=782846423"
    })
    notify("Toy Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Ninja Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=656117400", idleAlt = "http://www.roblox.com/asset/?id=656118341",
        walk = "http://www.roblox.com/asset/?id=656121766", run = "http://www.roblox.com/asset/?id=656118852",
        jump = "http://www.roblox.com/asset/?id=656117878", climb = "http://www.roblox.com/asset/?id=656114359",
        fall = "http://www.roblox.com/asset/?id=656115606"
    })
    notify("Ninja Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Cartoon Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=742637544", idleAlt = "http://www.roblox.com/asset/?id=742638445",
        walk = "http://www.roblox.com/asset/?id=742640026", run = "http://www.roblox.com/asset/?id=742638842",
        jump = "http://www.roblox.com/asset/?id=742637942", climb = "http://www.roblox.com/asset/?id=742636889",
        fall = "http://www.roblox.com/asset/?id=742637151"
    })
    notify("Cartoon Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Pirate Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=750781874", idleAlt = "http://www.roblox.com/asset/?id=750782770",
        walk = "http://www.roblox.com/asset/?id=750785693", run = "http://www.roblox.com/asset/?id=750783738",
        jump = "http://www.roblox.com/asset/?id=750782230", climb = "http://www.roblox.com/asset/?id=750779899",
        fall = "http://www.roblox.com/asset/?id=750780242"
    })
    notify("Pirate Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Knight Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=657595757", idleAlt = "http://www.roblox.com/asset/?id=657568135",
        walk = "http://www.roblox.com/asset/?id=657552124", run = "http://www.roblox.com/asset/?id=657564596",
        jump = "http://www.roblox.com/asset/?id=658409194", climb = "http://www.roblox.com/asset/?id=658360781",
        fall = "http://www.roblox.com/asset/?id=657600338"
    })
    notify("Knight Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Sneaky Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=1132473842", idleAlt = "http://www.roblox.com/asset/?id=1132477671",
        walk = "http://www.roblox.com/asset/?id=1132510133", run = "http://www.roblox.com/asset/?id=1132494274",
        jump = "http://www.roblox.com/asset/?id=1132489853", climb = "http://www.roblox.com/asset/?id=1132461372",
        fall = "http://www.roblox.com/asset/?id=1132469004"
    })
    notify("Sneaky Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Werewolf Animation", Callback = function()
    applyAnimation({
        idle = "http://www.roblox.com/asset/?id=1083195517", idleAlt = "http://www.roblox.com/asset/?id=1083214717",
        walk = "http://www.roblox.com/asset/?id=1083178339", run = "http://www.roblox.com/asset/?id=1083216690",
        jump = "http://www.roblox.com/asset/?id=1083218792", climb = "http://www.roblox.com/asset/?id=1083182000",
        fall = "http://www.roblox.com/asset/?id=1083189019"
    })
    notify("Werewolf Animation aplicada!")
end})

AnimationsTab:AddButton({Name = "Reset Animations", Callback = function()
    local plr = game.Players.LocalPlayer
    if plr.Character then
        local animate = plr.Character:FindFirstChild("Animate")
        if animate then animate:Destroy() end
        local humanoid = plr.Character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            local newAnimate = Instance.new("LocalScript")
            newAnimate.Name = "Animate"
            newAnimate.Parent = plr.Character
        end
    end
    notify("Animações resetadas!")
end})

-- ============================================================
-- AVATAR TAB
-- ============================================================
AvatarTab:AddSection({"Copiar Avatar"})
AvatarTab:AddButton({Name = "Copiar Avatar de um Player", Callback = function()
    local closestPlayer = nil
    local closestDist = math.huge
    local root = getRoot(player)
    if root then
        for _, plr in ipairs(Players:GetPlayers()) do
            if plr ~= player and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
                local dist = (root.Position - plr.Character.HumanoidRootPart.Position).Magnitude
                if dist < closestDist then
                    closestDist = dist
                    closestPlayer = plr
                end
            end
        end
    end
    if closestPlayer then
        pcall(function()
            local humanoid = closestPlayer.Character:FindFirstChildOfClass("Humanoid")
            if humanoid then
                local description = humanoid:GetAppliedDescription()
                local myHumanoid = getHum(player)
                if myHumanoid then
                    myHumanoid:ApplyDescription(description)
                    notify("Avatar copiado de " .. closestPlayer.Name)
                end
            end
        end)
    else
        notify("Nenhum player próximo encontrado!")
    end
end})

AvatarTab:AddSection({"Heads"})
AvatarTab:AddButton({Name = "Head Freddy Fazbear", Callback = function()
    pcall(function()
        local args = {
            [1] = "http://www.roblox.com/asset/?id=16079702019",
            [2] = "2162154434"
        }
        game:GetService("ReplicatedStorage").RE["1Play1erHa1t"]:FireServer(unpack(args))
    end)
end})

AvatarTab:AddButton({Name = "Head Alien", Callback = function()
    pcall(function()
        local args = {
            [1] = "http://www.roblox.com/asset/?id=15873844270",
            [2] = "2162154434"
        }
        game:GetService("ReplicatedStorage").RE["1Play1erHa1t"]:FireServer(unpack(args))
    end)
end})

AvatarTab:AddButton({Name = "Head Dragon", Callback = function()
    pcall(function()
        local args = {
            [1] = "http://www.roblox.com/asset/?id=16079728663",
            [2] = "2162154434"
        }
        game:GetService("ReplicatedStorage").RE["1Play1erHa1t"]:FireServer(unpack(args))
    end)
end})

AvatarTab:AddButton({Name = "Head Robot", Callback = function()
    pcall(function()
        local args = {
            [1] = "http://www.roblox.com/asset/?id=14561091494",
            [2] = "2162154434"
        }
        game:GetService("ReplicatedStorage").RE["1Play1erHa1t"]:FireServer(unpack(args))
    end)
end})

AvatarTab:AddButton({Name = "Head Skull", Callback = function()
    pcall(function()
        local args = {
            [1] = "http://www.roblox.com/asset/?id=16079743018",
            [2] = "2162154434"
        }
        game:GetService("ReplicatedStorage").RE["1Play1erHa1t"]:FireServer(unpack(args))
    end)
end})

AvatarTab:AddButton({Name = "Head Clown", Callback = function()
    pcall(function()
        local args = {
            [1] = "http://www.roblox.com/asset/?id=16079751199",
            [2] = "2162154434"
        }
        game:GetService("ReplicatedStorage").RE["1Play1erHa1t"]:FireServer(unpack(args))
    end)
end})

-- ============================================================
-- TROLL TAB (COMPLETO - TODOS OS FLINGS)
-- ============================================================
TrollTab:AddSection({"Fogo"})
TrollTab:AddButton({"Fogo em Mim", function()
    if player.Character then
        local r = getRoot(player)
        if r then local f = Instance.new("Fire"); f.Size = 12; f.Heat = 12; f.Parent = r; Debris:AddItem(f, 15) end
    end
end})
TrollTab:AddButton({"Fogo em Todos", function()
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr.Character then
            local r = plr.Character:FindFirstChild("HumanoidRootPart") or plr.Character:FindFirstChild("Head")
            if r then local f = Instance.new("Fire"); f.Size = 10; f.Heat = 10; f.Parent = r; Debris:AddItem(f, 20) end
        end
    end
    notify("Fogo em todos!")
end})
TrollTab:AddButton({"Fogo + Fumaca em Todos", function()
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr.Character then
            local r = plr.Character:FindFirstChild("HumanoidRootPart") or plr.Character:FindFirstChild("Head")
            if r then
                local f = Instance.new("Fire"); f.Size = 15; f.Heat = 15; f.Parent = r
                local s = Instance.new("Smoke"); s.Size = 10; s.RiseVelocity = 5; s.Parent = r
                Debris:AddItem(f, 30); Debris:AddItem(s, 30)
            end
        end
    end
    notify("Fogo + Fumaca!")
end})

TrollTab:AddSection({"Som"})
TrollTab:AddButton({"Som Alto (Todos)", function()
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr.Character and plr.Character:FindFirstChild("Head") then
            local s = Instance.new("Sound"); s.SoundId = "rbxassetid://9120385986"; s.Volume = 10
            s.Parent = plr.Character.Head; s:Play(); Debris:AddItem(s, 5)
        end
    end
end})
TrollTab:AddButton({"Alarme (Todos)", function()
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr.Character and plr.Character:FindFirstChild("Head") then
            local s = Instance.new("Sound"); s.SoundId = "rbxassetid://5375332180"; s.Volume = 10; s.Looped = true
            s.Parent = plr.Character.Head; s:Play(); Debris:AddItem(s, 10)
        end
    end
end})

TrollTab:AddSection({"ForceField"})
TrollTab:AddButton({"ForceField em Mim", function()
    if player.Character then local ff = Instance.new("ForceField"); ff.Parent = player.Character; Debris:AddItem(ff, 15) end
end})
TrollTab:AddButton({"ForceField em Todos", function()
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr.Character then local ff = Instance.new("ForceField"); ff.Parent = plr.Character; Debris:AddItem(ff, 15) end
    end
    notify("ForceField em todos!")
end})

TrollTab:AddSection({"Troll Básico"})
TrollTab:AddButton({"Lancar Jogadores p/ Cima", function()
    for _, plr in ipairs(Players:GetPlayers()) do
        if plr ~= player and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
            plr.Character.HumanoidRootPart.Velocity = Vector3.new(0, 500, 0)
        end
    end
    notify("Jogadores lancados!")
end})
TrollTab:AddButton({"Prender Jogadores", function()
    local r = getRoot(player)
    if r then
        for _, plr in ipairs(Players:GetPlayers()) do
            if plr ~= player and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
                plr.Character.HumanoidRootPart.CFrame = r.CFrame * CFrame.new(math.random(-2,2), 0, math.random(-2,2))
            end
        end
        notify("Jogadores presos!")
    end
end})

TrollTab:AddSection({"Explosao"})
TrollTab:AddButton({"Explosao em Mim", function()
    local r = getRoot(player)
    if r then
        local exp = Instance.new("Explosion"); exp.BlastRadius = 10; exp.BlastPressure = 50000
        exp.Position = r.Position; exp.Parent = workspace; Debris:AddItem(exp, 5)
    end
end})
TrollTab:AddButton({"Explosao Gigante", function()
    local r = getRoot(player)
    if r then
        local exp = Instance.new("Explosion"); exp.BlastRadius = 100; exp.BlastPressure = 100000
        exp.Position = r.Position; exp.Parent = workspace; Debris:AddItem(exp, 5)
    end
end})

-- ============================================================
-- TROLL TAB - FLINGS (COMPLETO DO DARK HUB/COQUETTE)
-- ============================================================
TrollTab:AddSection({"Flings - English Bus"})

TrollTab:AddToggle({"English Fling (Bus)", false, function(v)
    KX.englishFlingActive = v
    if v then
        task.spawn(function()
            while KX.englishFlingActive do
                pcall(function()
                    local args = {
                        [1] = "ToolMusicText",
                        [2] = "123268013026823"
                    }
                    ReplicatedStorage.RE["PlayerToolEvent"]:FireServer(unpack(args))
                end)
                task.wait(0.1)
            end
        end)
        notify("English Fling ativado!")
    else
        notify("English Fling desativado!")
    end
end})

TrollTab:AddSection({"Flings - Brazilian Fling (Boat)"})

TrollTab:AddToggle({"Brazilian Fling (Boat)", false, function(v)
    KX.brazilianFlingActive = v
    if v then
        task.spawn(function()
            while KX.brazilianFlingActive do
                pcall(function()
                    local args = {
                        [1] = "PickingCarMusicText",
                        [2] = "123268013026823"
                    }
                    ReplicatedStorage.RE["1Player1sCa1r"]:FireServer(unpack(args))
                end)
                task.wait(0.1)
            end
        end)
        notify("Brazilian Fling ativado!")
    else
        notify("Brazilian Fling desativado!")
    end
end})

TrollTab:AddSection({"Flings - Couch"})

TrollTab:AddToggle({"Fling Couch", false, function(v)
    KX.flingCouchActive = v
    if v then
        task.spawn(function()
            while KX.flingCouchActive do
                pcall(function()
                    local args = {
                        [1] = "PickHouseMusicText",
                        [2] = "123268013026823"
                    }
                    ReplicatedStorage.RE["1Player1sHous1e"]:FireServer(unpack(args))
                end)
                task.wait(0.1)
            end
        end)
        notify("Fling Couch ativado!")
    else
        notify("Fling Couch desativado!")
    end
end})

TrollTab:AddToggle({"Fling Couch Fast", false, function(v)
    KX.flingCouchFastActive = v
    if v then
        task.spawn(function()
            while KX.flingCouchFastActive do
                pcall(function()
                    local args = {
                        [1] = "PickHouseMusicText",
                        [2] = "123268013026823"
                    }
                    ReplicatedStorage.RE["1Player1sHous1e"]:FireServer(unpack(args))
                    ReplicatedStorage.RE["1Player1sHous1e"]:FireServer(unpack(args))
                end)
                task.wait(0.05)
            end
        end)
        notify("Fling Couch Fast ativado!")
    else
        notify("Fling Couch Fast desativado!")
    end
end})

TrollTab:AddSection({"Flings - Auto Fling"})

TrollTab:AddToggle({"Auto Fling", false, function(v)
    KX.autoFlingActive = v
    if v then
        task.spawn(function()
            while KX.autoFlingActive do
                pcall(function()
                    local id = tostring(math.random(1000000000, 9999999999))
                    local args = {[1] = "ToolMusicText", [2] = id}
                    ReplicatedStorage.RE["PlayerToolEvent"]:FireServer(unpack(args))
                end)
                task.wait(0.05)
            end
        end)
        notify("Auto Fling ativado!")
    else
        notify("Auto Fling desativado!")
    end
end})

TrollTab:AddSection({"Flings - Touched Fling"})

TrollTab:AddToggle({"Touched Fling", false, function(v)
    KX.touchedFlingActive = v
    if v then
        task.spawn(function()
            while KX.touchedFlingActive do
                pcall(function()
                    local id = tostring(math.random(1000000000, 9999999999))
                    local args = {
                        [1] = "PickingScooterMusicText",
                        [2] = id
                    }
                    ReplicatedStorage.RE["1NoMoto1rVehicle1s"]:FireServer(unpack(args))
                end)
                task.wait(0.05)
            end
        end)
        notify("Touched Fling ativado!")
    else
        notify("Touched Fling desativado!")
    end
end})

TrollTab:AddSection({"Shield Ball"})

TrollTab:AddButton({"Criar Shield Ball", function()
    if KX.shieldBall then pcall(function() KX.shieldBall:Destroy() end) end
    if KX.shieldLoop then KX.shieldLoop:Disconnect() end
    
    KX.shieldBall = Instance.new("Part")
    KX.shieldBall.Size = Vector3.new(5, 5, 5)
    KX.shieldBall.Shape = Enum.PartType.Ball
    KX.shieldBall.Anchored = false
    KX.shieldBall.CanCollide = true
    KX.shieldBall.Material = Enum.Material.Neon
    KX.shieldBall.Color = Color3.fromRGB(255, 50, 50)
    KX.shieldBall.Transparency = 0.3
    KX.shieldBall.Parent = workspace
    
    local mesh = Instance.new("SpecialMesh")
    mesh.MeshType = Enum.MeshType.Sphere
    mesh.Parent = KX.shieldBall
    
    local bodyPosition = Instance.new("BodyPosition")
    bodyPosition.MaxForce = Vector3.new(9e9, 9e9, 9e9)
    bodyPosition.D = 100
    bodyPosition.P = 1000
    bodyPosition.Parent = KX.shieldBall
    
    KX.shieldLoop = RunService.Heartbeat:Connect(function()
        local root = getRoot(player)
        if root and KX.shieldBall then
            bodyPosition.Position = root.Position + Vector3.new(0, 3, 0)
        end
    end)
    
    notify("Shield Ball criado!")
end})

TrollTab:AddButton({"Destruir Shield Ball", function()
    if KX.shieldBall then pcall(function() KX.shieldBall:Destroy() end); KX.shieldBall = nil end
    if KX.shieldLoop then KX.shieldLoop:Disconnect(); KX.shieldLoop = nil end
    notify("Shield Ball destruido!")
end})

TrollTab:AddSection({"Glitch Fling Couch All"})

TrollTab:AddToggle({"Glitch Fling Couch (All)", false, function(v)
    KX.glitchFlingCouchActiveAll = v
    if v then
        task.spawn(function()
            while KX.glitchFlingCouchActiveAll do
                for _, plr in ipairs(Players:GetPlayers()) do
                    pcall(function()
                        local args = {
                            [1] = "PickHouseMusicText",
                            [2] = tostring(math.random(1000000000, 9999999999))
                        }
                        ReplicatedStorage.RE["1Player1sHous1e"]:FireServer(unpack(args))
                    end)
                end
                task.wait(0.05)
            end
        end)
        notify("Glitch Fling Couch ativado!")
    else
        notify("Glitch Fling Couch desativado!")
    end
end})

TrollTab:AddSection({"Loop TP Fling"})

TrollTab:AddToggle({"Loop TP Fling", false, function(v)
    KX.loopTPfling = v
    if v then
        task.spawn(function()
            while KX.loopTPfling do
                for _, loc in ipairs(locs) do
                    if not KX.loopTPfling then break end
                    tpTo(loc[2])
                    pcall(function()
                        local args = {
                            [1] = "ToolMusicText",
                            [2] = "123268013026823"
                        }
                        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer(unpack(args))
                    end)
                    task.wait(0.3)
                end
            end
        end)
        notify("Loop TP Fling ativado!")
    else
        notify("Loop TP Fling desativado!")
    end
end})

-- ============================================================
-- PROPS TAB (COMPLETO)
-- ============================================================
PropsTab:AddSection({"Fling Props"})

PropsTab:AddToggle({"Fling Props", false, function(v)
    if v then
        KX.FlingConnection = RunService.Heartbeat:Connect(function()
            pcall(function()
                local id = tostring(math.random(1000000000, 9999999999))
                local args = {[1] = "ToolMusicText", [2] = id}
                ReplicatedStorage.RE["PlayerToolEvent"]:FireServer(unpack(args))
            end)
        end)
        notify("Fling Props ativado!")
    else
        if KX.FlingConnection then KX.FlingConnection:Disconnect(); KX.FlingConnection = nil end
        notify("Fling Props desativado!")
    end
end})

PropsTab:AddToggle({"Bring Props", false, function(v)
    if v then
        KX.BringConnection = RunService.Heartbeat:Connect(function()
            pcall(function()
                local id = tostring(math.random(1000000000, 9999999999))
                local args = {[1] = "PickHouseMusicText", [2] = id}
                ReplicatedStorage.RE["1Player1sHous1e"]:FireServer(unpack(args))
            end)
        end)
        notify("Bring Props ativado!")
    else
        if KX.BringConnection then KX.BringConnection:Disconnect(); KX.BringConnection = nil end
        notify("Bring Props desativado!")
    end
end})

PropsTab:AddToggle({"Kill Props", false, function(v)
    if v then
        KX.KillConnection = RunService.Heartbeat:Connect(function()
            pcall(function()
                local id = tostring(math.random(1000000000, 9999999999))
                local args = {[1] = "PickingCarMusicText", [2] = id}
                ReplicatedStorage.RE["1Player1sCa1r"]:FireServer(unpack(args))
            end)
        end)
        notify("Kill Props ativado!")
    else
        if KX.KillConnection then KX.KillConnection:Disconnect(); KX.KillConnection = nil end
        notify("Kill Props desativado!")
    end
end})

PropsTab:AddSection({"RGB Props"})

PropsTab:AddToggle({"RGB Props", false, function(v)
    KX.PropsRGBEnabled = v
    if v then
        local hue = 0
        KX.RGBConnection = RunService.RenderStepped:Connect(function()
            if not KX.PropsRGBEnabled then return end
            hue = (hue + 0.005) % 1
            local color = Color3.fromHSV(hue, 1, 1)
            pcall(function()
                local args = {[1] = "PickingRPNameColor", [2] = color}
                ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer(unpack(args))
            end)
        end)
        notify("RGB Props ativado!")
    else
        if KX.RGBConnection then KX.RGBConnection:Disconnect(); KX.RGBConnection = nil end
        notify("RGB Props desativado!")
    end
end})

PropsTab:AddToggle({"Orbit Props", false, function(v)
    if v then
        KX.OrbitConnection = RunService.Heartbeat:Connect(function()
            pcall(function()
                local id = tostring(math.random(1000000000, 9999999999))
                local args = {[1] = "PickingScooterMusicText", [2] = id}
                ReplicatedStorage.RE["1NoMoto1rVehicle1s"]:FireServer(unpack(args))
            end)
        end)
        notify("Orbit Props ativado!")
    else
        if KX.OrbitConnection then KX.OrbitConnection:Disconnect(); KX.OrbitConnection = nil end
        notify("Orbit Props desativado!")
    end
end})

PropsTab:AddButton({"Parar Todos os Props", function()
    if KX.FlingConnection then KX.FlingConnection:Disconnect(); KX.FlingConnection = nil end
    if KX.BringConnection then KX.BringConnection:Disconnect(); KX.BringConnection = nil end
    if KX.KillConnection then KX.KillConnection:Disconnect(); KX.KillConnection = nil end
    if KX.RGBConnection then KX.RGBConnection:Disconnect(); KX.RGBConnection = nil end
    if KX.OrbitConnection then KX.OrbitConnection:Disconnect(); KX.OrbitConnection = nil end
    KX.PropsRGBEnabled = false
    notify("Todos os Props parados!")
end})

-- ============================================================
-- FUN TAB
-- ============================================================
FunTab:AddSection({"Anti Tools"})

FunTab:AddToggle({"Loop Anti Tools (Mim)", false, function(v)
    KX.loopAtivo = v
    if v then
        task.spawn(function()
            while KX.loopAtivo do
                pcall(function()
                    local args = {
                        [1] = "ToolMusicText",
                        [2] = ""
                    }
                    ReplicatedStorage.RE["PlayerToolEvent"]:FireServer(unpack(args))
                end)
                task.wait(0.5)
            end
        end)
        notify("Loop Anti Tools ativado!")
    else
        notify("Loop Anti Tools desativado!")
    end
end})

FunTab:AddToggle({"Loop Anti Tools (Todos)", false, function(v)
    KX.loopTodosAtivo = v
    if v then
        task.spawn(function()
            while KX.loopTodosAtivo do
                for _, plr in ipairs(Players:GetPlayers()) do
                    pcall(function()
                        local args = {
                            [1] = "ToolMusicText",
                            [2] = ""
                        }
                        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer(unpack(args))
                    end)
                end
                task.wait(0.5)
            end
        end)
        notify("Loop Anti Tools (Todos) ativado!")
    else
        notify("Loop Anti Tools (Todos) desativado!")
    end
end})

FunTab:AddSection({"Placa"})
FunTab:AddTextBox({
    Name = "Texto da Placa",
    PlaceholderText = "Digite o texto e pressione Enter",
    Callback = function(v)
        if v and v ~= "" then
            pcall(function()
                local args = {
                    [1] = "ToolMusicText",
                    [2] = v
                }
                ReplicatedStorage.RE["PlayerToolEvent"]:FireServer(unpack(args))
            end)
            notify("Placa atualizada: " .. v)
        end
    end
})

FunTab:AddButton({"Limpar Placa", function()
    pcall(function()
        local args = {
            [1] = "ToolMusicText",
            [2] = ""
        }
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer(unpack(args))
    end)
    notify("Placa limpa!")
end})

-- ============================================================
-- NAME & BIO TAB
-- ============================================================
NameBioTab:AddSection({"Nome & Bio"})

NameBioTab:AddTextBox({
    Name = "Alterar Nome RP",
    PlaceholderText = "Digite o nome e pressione Enter",
    Callback = function(v)
        if v and v ~= "" then
            pcall(function()
                ReplicatedStorage.RE["1RPNam1eTex1t"]:FireServer("RolePlayName", v)
            end)
            notify("Nome alterado para: " .. v)
        end
    end
})

NameBioTab:AddTextBox({
    Name = "Alterar Bio RP",
    PlaceholderText = "Digite a bio e pressione Enter",
    Callback = function(v)
        if v and v ~= "" then
            pcall(function()
                ReplicatedStorage.RE["1RPNam1eTex1t"]:FireServer("RolePlayBio", v)
            end)
            notify("Bio alterada para: " .. v)
        end
    end
})

NameBioTab:AddSection({"RGB Nome & Bio"})

NameBioTab:AddToggle({"RGB Nome", false, function(v)
    if v then
        local hue = 0
        KX.RGBConnection = RunService.RenderStepped:Connect(function()
            if not v then KX.RGBConnection:Disconnect(); return end
            hue = (hue + 0.005) % 1
            local color = Color3.fromHSV(hue, 1, 1)
            pcall(function()
                ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPNameColor", color)
            end)
        end)
    else
        if KX.RGBConnection then KX.RGBConnection:Disconnect(); KX.RGBConnection = nil end
    end
end})

NameBioTab:AddToggle({"RGB Bio", false, function(v)
    if v then
        local hue = 0
        local bioConn = RunService.RenderStepped:Connect(function()
            if not v then bioConn:Disconnect(); return end
            hue = (hue + 0.005) % 1
            local color = Color3.fromHSV(hue, 1, 1)
            pcall(function()
                ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPBioColor", color)
            end)
        end)
    else
        -- Não precisa desconectar, o if not v cuida
    end
end})

NameBioTab:AddSection({"Bicicleta"})
NameBioTab:AddButton({"Spawn Bicicleta", function()
    pcall(function()
        ReplicatedStorage.RE["1NoMoto1rVehicle1s"]:FireServer("PickingScooter", true)
    end)
    notify("Bicicleta spawnada!")
end})

NameBioTab:AddButton({"Remover Bicicleta", function()
    pcall(function()
        ReplicatedStorage.RE["1NoMoto1rVehicle1s"]:FireServer("PickingScooter", false)
    end)
    notify("Bicicleta removida!")
end})

NameBioTab:AddSection({"Radio"})
NameBioTab:AddButton({"Ligar Radio (Tool)", function()
    pcall(function()
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer("ToolMusicText", "3148329638")
    end)
    notify("Radio ligado!")
end})
NameBioTab:AddButton({"Desligar Radio", function()
    pcall(function()
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer("ToolMusicText", "")
    end)
    notify("Radio desligado!")
end})

-- ============================================================
-- HOUSE TAB
-- ============================================================
HouseTab:AddSection({"Casa"})

HouseTab:AddToggle({"RGB Casa", false, function(v)
    KX.rgbHouse = v
    if v then
        local hue = 0
        KX.rgbHouseConnection = RunService.RenderStepped:Connect(function()
            if not KX.rgbHouse then return end
            hue = (hue + 0.005) % 1
            local color = Color3.fromHSV(hue, 1, 1)
            pcall(function()
                local args = {
                    [1] = "PickingHouseColor",
                    [2] = color
                }
                ReplicatedStorage.RE["1Player1sHous1e"]:FireServer(unpack(args))
            end)
        end)
        notify("RGB Casa ativado!")
    else
        if KX.rgbHouseConnection then KX.rgbHouseConnection:Disconnect(); KX.rgbHouseConnection = nil end
        notify("RGB Casa desativado!")
    end
end})

HouseTab:AddToggle({"RGB Text Casa", false, function(v)
    KX.houseTextRgb = v
    if v then
        local hue = 0
        KX.houseTextConnection = RunService.RenderStepped:Connect(function()
            if not KX.houseTextRgb then return end
            hue = (hue + 0.005) % 1
            local color = Color3.fromHSV(hue, 1, 1)
            pcall(function()
                local args = {
                    [1] = "PickingHouseTextColor",
                    [2] = color
                }
                ReplicatedStorage.RE["1Player1sHous1e"]:FireServer(unpack(args))
            end)
        end)
        notify("RGB Text Casa ativado!")
    else
        if KX.houseTextConnection then KX.houseTextConnection:Disconnect(); KX.houseTextConnection = nil end
        notify("RGB Text Casa desativado!")
    end
end})

HouseTab:AddToggle({"Hacked Text", false, function(v)
    KX.hackedHouseText = v
    if v then
        task.spawn(function()
            while KX.hackedHouseText do
                pcall(function()
                    ReplicatedStorage.RE["1Player1sHous1e"]:FireServer("PickHouseMusicText", "")
                end)
                task.wait(0.1)
            end
        end)
        notify("Hacked Text ativado!")
    else
        notify("Hacked Text desativado!")
    end
end})

HouseTab:AddToggle({"Loop Garage", false, function(v)
    KX.loopGarage = v
    if v then
        task.spawn(function()
            local garages = {"1", "2", "3", "4", "5", "6", "7", "8", "9", "10", "11", "12", "13", "14", "15", "16", "17", "18"}
            while KX.loopGarage do
                for _, garage in ipairs(garages) do
                    if not KX.loopGarage then break end
                    pcall(function()
                        ReplicatedStorage.RE["1Player1sHous1e"]:FireServer("Garage" .. garage, true)
                    end)
                    task.wait(0.5)
                end
            end
        end)
        notify("Loop Garage ativado!")
    else
        notify("Loop Garage desativado!")
    end
end})

HouseTab:AddSection({"Remover Ban"})
HouseTab:AddButton({"Remover Ban da Casa", function()
    pcall(function()
        ReplicatedStorage.RE["1Player1sHous1e"]:FireServer("UnbanAll", true)
    end)
    notify("Ban removido!")
end})

HouseTab:AddButton({"Remover Ban (Force)", function()
    pcall(function()
        ReplicatedStorage.RE["1Player1sHous1e"]:FireServer("UnbanAll", false)
        ReplicatedStorage.RE["1Player1sHous1e"]:FireServer("UnbanAll", true)
    end)
    notify("Ban removido (force)!")
end})

-- ============================================================
-- ITENS TAB
-- ============================================================
ItensTab:AddSection({"Ferramentas"})
ItensTab:AddButton({"Spawn Picareta", function()
    pcall(function()
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer("ToolPickaxe", true)
    end)
    notify("Picareta spawnada!")
end})
ItensTab:AddButton({"Spawn Machado", function()
    pcall(function()
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer("ToolAxe", true)
    end)
    notify("Machado spawnado!")
end})
ItensTab:AddButton({"Spawn Vara de Pesca", function()
    pcall(function()
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer("ToolFishingRod", true)
    end)
    notify("Vara de pesca spawnada!")
end})
ItensTab:AddButton({"Spawn Lanterna", function()
    pcall(function()
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer("ToolFlashlight", true)
    end)
    notify("Lanterna spawnada!")
end})
ItensTab:AddButton({"Spawn Binóculos", function()
    pcall(function()
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer("ToolBinoculars", true)
    end)
    notify("Binóculos spawnados!")
end})

ItensTab:AddSection({"Remover Itens"})
ItensTab:AddButton({"Remover Todos Itens", function()
    pcall(function()
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer("ToolMusicText", "")
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer("ToolPickaxe", false)
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer("ToolAxe", false)
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer("ToolFishingRod", false)
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer("ToolFlashlight", false)
        ReplicatedStorage.RE["PlayerToolEvent"]:FireServer("ToolBinoculars", false)
    end)
    notify("Itens removidos!")
end})

-- ============================================================
-- SCRIPTS TAB
-- ============================================================
ScriptsTab:AddSection({"Scripts Úteis"})
ScriptsTab:AddButton({"Infinite Yield", function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"))()
    notify("Infinite Yield carregado!")
end})
ScriptsTab:AddButton({"CMD-X", function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/CMD-X/CMD-X/master/Source"))()
    notify("CMD-X carregado!")
end})
ScriptsTab:AddButton({"Dex Explorer", function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/InfinityMacro/DexExplorer/main/DexExplorer.lua"))()
    notify("Dex Explorer carregado!")
end})
ScriptsTab:AddButton({"Remote Spy", function()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/exxtremestuffs/SimpleSpySource/master/SimpleSpy.lua"))()
    notify("Remote Spy carregado!")
end})

-- ============================================================
-- PROTEÇÃO TAB (COMPLETA)
-- ============================================================
ProtectionTab:AddSection({"Anti Fling"})

ProtectionTab:AddToggle({"Anti Fling Veiculos", false, function(v)
    KX.AntiFlingVehicles = v
    if v then
        task.spawn(function()
            while KX.AntiFlingVehicles do
                pcall(function()
                    for _, v in ipairs(workspace:GetDescendants()) do
                        if v:IsA("VehicleSeat") then
                            local model = v:FindFirstAncestorOfClass("Model")
                            if model and model.PrimaryPart then
                                model.PrimaryPart.Velocity = Vector3.new(0, 0, 0)
                                model.PrimaryPart.RotVelocity = Vector3.new(0, 0, 0)
                            end
                        end
                    end
                end)
                task.wait(0.5)
            end
        end)
        notify("Anti Fling Veiculos ativado!")
    else
        notify("Anti Fling Veiculos desativado!")
    end
end})

ProtectionTab:AddToggle({"Anti Fling Canoas/Jets/Helis", false, function(v)
    KX.AntiFlingBalls = v
    if v then
        task.spawn(function()
            while KX.AntiFlingBalls do
                pcall(function()
                    for _, v in ipairs(workspace:GetDescendants()) do
                        if v:IsA("Part") and (v.Name:lower():find("canoa") or v.Name:lower():find("jet") or v.Name:lower():find("heli") or v.Name:lower():find("boat") or v.Name:lower():find("barco")) then
                            v.Velocity = Vector3.new(0, 0, 0)
                            v.RotVelocity = Vector3.new(0, 0, 0)
                        end
                    end
                end)
                task.wait(0.5)
            end
        end)
        notify("Anti Fling Canoas/Jets/Helis ativado!")
    else
        notify("Anti Fling Canoas/Jets/Helis desativado!")
    end
end})

ProtectionTab:AddToggle({"Anti Fling Portas", false, function(v)
    KX.AntiFlingPortas = v
    if v then
        task.spawn(function()
            while KX.AntiFlingPortas do
                pcall(function()
                    for _, v in ipairs(workspace:GetDescendants()) do
                        if v:IsA("Part") and (v.Name:lower():find("door") or v.Name:lower():find("porta")) then
                            v.Velocity = Vector3.new(0, 0, 0)
                            v.RotVelocity = Vector3.new(0, 0, 0)
                        end
                    end
                end)
                task.wait(0.5)
            end
        end)
        notify("Anti Fling Portas ativado!")
    else
        notify("Anti Fling Portas desativado!")
    end
end})

ProtectionTab:AddToggle({"Anti Fling Bloco", false, function(v)
    KX.AntiFlingBloco = v
    if v then
        task.spawn(function()
            while KX.AntiFlingBloco do
                pcall(function()
                    for _, v in ipairs(workspace:GetDescendants()) do
                        if v:IsA("Part") and v.Name:lower():find("bloco") then
                            v.Velocity = Vector3.new(0, 0, 0)
                            v.RotVelocity = Vector3.new(0, 0, 0)
                        end
                    end
                end)
                task.wait(0.5)
            end
        end)
        notify("Anti Fling Bloco ativado!")
    else
        notify("Anti Fling Bloco desativado!")
    end
end})

ProtectionTab:AddSection({"Anti Lag"})
ProtectionTab:AddButton({"Anti Lag (Remover Decks)", function()
    pcall(function()
        for _, v in ipairs(workspace:GetDescendants()) do
            if v:IsA("Part") and (v.Name:lower():find("deck") or v.Name:lower():find("piso") or v.Name:lower():find("floor")) then
                v.Transparency = 1
            end
        end
    end)
    notify("Anti Lag ativado!")
end})

ProtectionTab:AddSection({"Remover Itens Proibidos"})
ProtectionTab:AddButton({"Remover Balls", function()
    pcall(function()
        for _, v in ipairs(workspace:GetDescendants()) do
            if v:IsA("Part") and (v.Name:lower():find("ball") or v.Name:lower():find("bola") or v.Name:lower():find("esfera")) then
                if v.Shape == Enum.PartType.Ball then
                    v:Destroy()
                end
            end
        end
    end)
    notify("Balls removidas!")
end})

ProtectionTab:AddButton({"Remover Blocos Suspeitos", function()
    pcall(function()
        for _, v in ipairs(workspace:GetDescendants()) do
            if v:IsA("Part") and (v.Name:lower():find("bloco") or v.Name:lower():find("block")) then
                v:Destroy()
            end
        end
    end)
    notify("Blocos suspeitos removidos!")
end})

-- ============================================================
-- RGB TAB
-- ============================================================
RGBTab:AddSection({"Cores Dinâmicas"})
RGBTab:AddParagraph({"Efeito:", "Nome e Bio em RGB"})
RGBTab:AddToggle({"RGB Ativo", false, function(v)
    KX.RGB = v
    if v then
        rgbLoop()
        notify("RGB ativado!")
    else
        if KX.RGBConn then KX.RGBConn:Disconnect(); KX.RGBConn = nil end
        pcall(function()
            ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPNameColor", Color3.new(1,0,0))
            ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPBioColor", Color3.new(1,1,1))
        end)
        notify("RGB desativado!")
    end
end})

RGBTab:AddSlider({"Velocidade RGB", 1, 20, 5, function(v) KX.RGBSpeed = v end})

RGBTab:AddSection({"Presets"})
RGBTab:AddButton({"Vermelho", function()
    if KX.RGB then KX.RGB = false; if KX.RGBConn then KX.RGBConn:Disconnect(); KX.RGBConn = nil end end
    pcall(function()
        ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPNameColor", Color3.new(1,0,0))
        ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPBioColor", Color3.new(1,0,0))
    end)
    notify("Cor: Vermelho!")
end})
RGBTab:AddButton({"Azul", function()
    if KX.RGB then KX.RGB = false; if KX.RGBConn then KX.RGBConn:Disconnect(); KX.RGBConn = nil end end
    pcall(function()
        ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPNameColor", Color3.new(0,0,1))
        ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPBioColor", Color3.new(0,0,1))
    end)
    notify("Cor: Azul!")
end})
RGBTab:AddButton({"Verde", function()
    if KX.RGB then KX.RGB = false; if KX.RGBConn then KX.RGBConn:Disconnect(); KX.RGBConn = nil end end
    pcall(function()
        ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPNameColor", Color3.new(0,1,0))
        ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPBioColor", Color3.new(0,1,0))
    end)
    notify("Cor: Verde!")
end})
RGBTab:AddButton({"Branco", function()
    if KX.RGB then KX.RGB = false; if KX.RGBConn then KX.RGBConn:Disconnect(); KX.RGBConn = nil end end
    pcall(function()
        ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPNameColor", Color3.new(1,1,1))
        ReplicatedStorage.RE["1RPNam1eColo1r"]:FireServer("PickingRPBioColor", Color3.new(1,1,1))
    end)
    notify("Cor: Branco!")
end})

-- ============================================================
-- FARM TAB
-- ============================================================
FarmTab:AddSection({"Auto Farm"})

FarmTab:AddButton({"Iniciar Auto Farm (30s)", function()
    if KX.FarmActive then notify("Ja ativo!"); return end
    KX.FarmActive = true
    local c = 0
    KX.FarmConn = RunService.Heartbeat:Connect(function()
        c = c + 1
        if c >= 1800 then
            KX.FarmConn:Disconnect(); KX.FarmConn = nil
            KX.FarmActive = false; notify("Farm finalizado!"); return
        end
        if player.Character then
            local h = getHum(player); local r = getRoot(player)
            if h and r then
                h:MoveTo(r.Position + Vector3.new(math.random(-25,25), 0, math.random(-25,25)))
            end
            pcall(function() VirtualUser:CaptureController(); VirtualUser:ClickButton1(Vector2.new(0,0)) end)
        end
    end)
    notify("Auto Farm 30s ativado!")
end})

FarmTab:AddButton({"Parar Auto Farm", function()
    if KX.FarmConn then KX.FarmConn:Disconnect(); KX.FarmConn = nil end
    KX.FarmActive = false; notify("Farm parado!")
end})

FarmTab:AddSection({"Farm Turbo"})
FarmTab:AddButton({"Farm + Teleport Loop (60s)", function()
    local c = 0
    local conn = RunService.Heartbeat:Connect(function()
        c = c + 1
        if c >= 3600 then conn:Disconnect(); notify("Farm turbo finalizado!"); return end
        if player.Character then
            local h = getHum(player); local r = getRoot(player)
            if h and r then
                h:MoveTo(r.Position + Vector3.new(math.random(-35,35), 0, math.random(-35,35)))
                if c % 60 == 0 then r.CFrame = CFrame.new(locs[math.random(#locs)][2]) end
            end
            pcall(function() VirtualUser:CaptureController(); VirtualUser:ClickButton1(Vector2.new(0,0)) end)
        end
    end)
    task.wait(60); conn:Disconnect()
    notify("Farm turbo 60s concluido!")
end})

-- ============================================================
-- SETTINGS TAB
-- ============================================================
SettingsTab:AddSection({"UI"})

SettingsTab:AddButton({"Destruir UI", function()
    KX.TempoRunning = false
    if KX.FarmConn then KX.FarmConn:Disconnect() end
    if KX.FlyConn then KX.FlyConn:Disconnect(); toggleFly(false) end
    if KX.AntiSitHum then KX.AntiSitHum:Disconnect() end
    if KX.AntiSitChair then KX.AntiSitChair:Disconnect() end
    if KX.WalkWaterConn then KX.WalkWaterConn:Disconnect() end
    if KX.RGBConn then KX.RGBConn:Disconnect() end
    if KX.FlingConnection then KX.FlingConnection:Disconnect() end
    if KX.BringConnection then KX.BringConnection:Disconnect() end
    if KX.KillConnection then KX.KillConnection:Disconnect() end
    if KX.RGBConnection then KX.RGBConnection:Disconnect() end
    if KX.OrbitConnection then KX.OrbitConnection:Disconnect() end
    if KX.vehicleRgbConnection then KX.vehicleRgbConnection:Disconnect() end
    if KX.rgbHouseConnection then KX.rgbHouseConnection:Disconnect() end
    if KX.houseTextConnection then KX.houseTextConnection:Disconnect() end
    if KX.hackedConnection then KX.hackedConnection:Disconnect() end
    if KX.shieldLoop then KX.shieldLoop:Disconnect() end
    if KX.shieldBall then KX.shieldBall:Destroy() end
    clearESP(); disableAntiSit(); task.wait(1); Window:Destroy()
end})

SettingsTab:AddButton({"Rejoin", function()
    TeleportService:TeleportToPlaceInstance(game.PlaceId, game.JobId, player)
end})
SettingsTab:AddButton({"Server Hop", serverHop})

SettingsTab:AddSection({"Tecla Abrir/Fechar"})
SettingsTab:AddParagraph({"Tecla:", "RightControl (RCtrl)"})
SettingsTab:AddParagraph({"Funcao:", "Mostra/Esconde o Hub"})
SettingsTab:AddButton({"Definir Tecla (F4)", function()
    KX.ToggleKey = Enum.KeyCode.F4; notify("Tecla alterada para F4!")
end})

SettingsTab:AddSection({"Sobre"})
SettingsTab:AddParagraph({"KingerX Hub v6.0", "Ultimate Complete"})
SettingsTab:AddParagraph({"Key:", "kingerxstudio"})
SettingsTab:AddParagraph({"Developer:", "Julainorei"})
SettingsTab:AddParagraph({"Colaborador:", "xicoooo73"})
SettingsTab:AddParagraph({"Team:", "KingerX Studio"})

-- ============================================================
-- SISTEMA DE ABRIR/FECHAR (TOGGLE UI)
-- ============================================================
KX.ToggleKey = Enum.KeyCode.RightControl

UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    if input.KeyCode == KX.ToggleKey then
        KX.UIHidden = not KX.UIHidden
        if Window then
            pcall(function()
                if KX.UIHidden then Window:Toggle(false) else Window:Toggle(true) end
            end)
        end
    end
end)

-- ============================================================
-- LOOP PRINCIPAL
-- ============================================================
task.spawn(function()
    while KX.TempoRunning do
        task.wait(0.1)
        KX.Tempo = KX.Tempo + 1
        
        local cam = workspace.CurrentCamera
        if KX.FovEnabled and cam and cam.FieldOfView ~= KX.FovVal then
            cam.FieldOfView = KX.FovVal
        end
        
        if KX.ZoomEnabled and cam then
            pcall(function()
                if cam.CameraSubject then
                    local z = cam.CameraSubject:FindFirstChild("CameraMaxZoomDistance")
                    if not z then
                        z = Instance.new("NumberValue")
                        z.Name = "CameraMaxZoomDistance"
                        z.Value = KX.ZoomVal
                        z.Parent = cam.CameraSubject
                    else
                        z.Value = KX.ZoomVal
                    end
                end
            end)
        end
    end
end)

-- ============================================================
-- NOTIFICACAO FINAL
-- ============================================================
task.wait(2)
notify("KingerX Hub v6.0 carregado!")
notify("Developer: Julainorei | Colab: xicoooo73")
notify("Pressione RCtrl para abrir/fechar!")

end -- Fim da função startHub()
