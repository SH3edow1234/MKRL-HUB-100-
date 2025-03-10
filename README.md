-- Blox Fruits Script Rewok

-- Configurações
local autoFarmEnabled = true
local autoFruitSniperEnabled = true
local autoFarmChestEnabled = true
local fruitRainEnabled = false
local fruitRainDuration = 600 -- 10 minutos
local autoQuestEnabled = true

-- Detecção de Mundo (Blox Fruits)
local currentSea = 1 -- Assumindo que o jogador começa no Sea 1

local function detectSea()
    -- Lógica para detectar o Sea atual (pode envolver verificar a localização do jogador)
    -- Atualize 'currentSea' com o Sea correto
    return 1 -- Exemplo: Retorna Sea 1
end

currentSea = detectSea()

-- Funções Auxiliares (Blox Fruits)
local function findNearest(objects, position)
    local nearest = nil
    local nearestDistance = math.huge
    for _, obj in ipairs(objects) do
        local distance = (obj.PrimaryPart.Position - position).Magnitude
        if distance < nearestDistance then
            nearest = obj
            nearestDistance = distance
        end
    end
    return nearest
end

local function moveTo(position)
    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        player.Character:FindFirstChild("HumanoidRootPart").CFrame = CFrame.new(position)
    end
end

local function attack(target)
    -- Lógica para atacar o alvo (pode envolver usar habilidades de fruta ou ataques de espada)
    -- Exemplo: player.Character.Humanoid:EquipTool(player.Character:FindFirstChildOfClass("Tool"))
    -- player.Character.Humanoid:UseTool()
end

local function collectFruit(fruit)
    -- Lógica para coletar a fruta (pode envolver interagir com a fruta)
    -- Exemplo: fruit:Destroy()
end

local function openChest(chest)
    -- Lógica para abrir o baú (pode envolver interagir com o baú)
    -- Exemplo: chest:Destroy()
end

local function getQuestFromNPC(npcName)
    -- Lógica para pegar a quest do NPC (pode envolver diálogo com o NPC)
    -- Exemplo: local npc = workspace:FindFirstChild(npcName)
    -- moveTo(npc.PrimaryPart.Position)
    -- -- Lógica de diálogo com o NPC
end

local function returnToFarming(monsterName)
    -- Lógica para voltar ao local de farm do monstro
    -- Exemplo: local monster = workspace:FindFirstChild(monsterName)
    -- moveTo(monster.PrimaryPart.Position)
end

-- Lógica de Quest (Blox Fruits)
local Mon, LevelQuest, NameQuest, NameMon, CFrameQuest, CFrameMon

if currentSea == 1 then
    if myLevel >= 1 and myLevel <= 9 then
        Mon = "Bandit"
        LevelQuest = 1
        NameQuest = "BanditQuest1"
        NameMon = "Bandit"
        CFrameQuest = CFrame.new(1059.37195, 15.4495068, 1550.4231, 0.939700544, -0, -0.341998369, 0, 1, -0, 0.341998369, 0, 0.939700544)
        CFrameMon = CFrame.new(1045.962646484375, 27.00250816345215, 1560.8203125)
    elseif myLevel >= 175 and myLevel <= 189 then
        Mon = "Dark Master"
        LevelQuest = 2
        NameQuest = "SkyQuest"
        NameMon = "Dark Master"
        CFrameQuest = CFrame.new(-4839.53027, 716.368591, -2619.44165, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
        CFrameMon = CFrame.new(-4582.47412109375, 786.3787841796875, -2413.513427734375)
    end
elseif currentSea == 2 then
    -- Adicione a lógica de quest para Sea 2 aqui
elseif currentSea == 3 then
    -- Adicione a lógica de quest para Sea 3 aqui
end

-- Auto Farm (Blox Fruits)
if autoFarmEnabled and Mon then
    local monster = workspace:FindFirstChild(NameMon)
    if monster then
        moveTo(monster.PrimaryPart.Position)
        attack(monster)
    end
end

-- Auto Fruit Sniper (Blox Fruits)
if autoFruitSniperEnabled then
    local fruits = workspace:GetDescendants()
    local fruit = findNearest(fruits, player.Character:FindFirstChild("HumanoidRootPart").Position)
    if fruit and fruit:IsA("BasePart") and fruit.Name:lower():find("fruit") then
        moveTo(fruit.Position)
        collectFruit(fruit)
    end
end

-- Auto Farm Chest (Blox Fruits)
if autoFarmChestEnabled then
    local chests = workspace:GetDescendants()
    local chest = findNearest(chests, player.Character:FindFirstChild("HumanoidRootPart").Position)
    if chest and chest:IsA("Model") and chest.Name:lower():find("chest") then
        moveTo(chest.PrimaryPart.Position)
        openChest(chest)
    end
end

-- ESP de Chuva de Frutas (Blox Fruits)
if fruitRainEnabled then
    local endTime = tick() + fruitRainDuration
    while tick() < endTime do
        local fruitName = -- Adicione a lógica para selecionar uma fruta aleatória
        local fruit = Instance.new("Part")
        fruit.Name = fruitName
        fruit.Anchored = true
        fruit.Position = Vector3.new(math.random(-100, 100), 100, math.random(-100, 100))
        fruit.Parent = workspace
        wait(0.5)
    end
end

-- Auto Quest (Blox Fruits)
if autoQuestEnabled then
    getQuestFromNPC(NameMon .. " Quest Giver")
    wait(5)
    returnToFarming(NameMon)
end

-- IU (Blox Fruits)
if player and player.PlayerGui then
    -- ... (IU com botões de alternância)
end

-- Sistema Anti-Detecção (Manter a lógica existente)
-- ...

-- Restante do código (Manter a lógica existente)
-- ...
