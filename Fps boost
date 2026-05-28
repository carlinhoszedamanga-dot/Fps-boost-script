-- FPS Booster EXTREMO - Blox Fruits Mobile
-- Para celular com gráfico travado alto

local RunService = game:GetService("RunService")
local Players = game:GetService("Players")
local Lighting = game:GetService("Lighting")
local player = Players.LocalPlayer

-- ========================
-- FORÇAR GRÁFICO NÍVEL 1 CONSTANTEMENTE
-- (Blox Fruits fica resetando, então fica em loop)
-- ========================
RunService.RenderStepped:Connect(function()
    settings().Rendering.QualityLevel = Enum.QualityLevel.Level01
end)

-- ========================
-- FPS CAP
-- ========================
if setfpscap then
    setfpscap(60)
end

-- ========================
-- LIGHTING ZERADO
-- ========================
Lighting.GlobalShadows = false
Lighting.FogEnd = 9e9
Lighting.FogStart = 9e8
Lighting.Brightness = 2
Lighting.ClockTime = 14
Lighting.Ambient = Color3.fromRGB(178, 178, 178)
Lighting.OutdoorAmbient = Color3.fromRGB(178, 178, 178)

-- Destrói todos os efeitos visuais
for _, v in ipairs(Lighting:GetChildren()) do
    if v:IsA("PostEffect") or v:IsA("Atmosphere") or v:IsA("Sky") then
        v:Destroy()
    end
end

-- ========================
-- REMOVER TUDO PESADO NO WORKSPACE
-- ========================
local function limpar(obj)
    pcall(function()
        -- Texturas / Decals
        if obj:IsA("Decal") or obj:IsA("Texture") then
            obj:Destroy(); return
        end
        -- Partículas e efeitos
        if obj:IsA("ParticleEmitter") or obj:IsA("Trail") or
           obj:IsA("Fire") or obj:IsA("Smoke") or obj:IsA("Sparkles") or
           obj:IsA("SelectionBox") or obj:IsA("BillboardGui") then
            obj:Destroy(); return
        end
        -- Simplifica parts
        if obj:IsA("BasePart") then
            obj.Material = Enum.Material.SmoothPlastic
            obj.Reflectance = 0
            obj.CastShadow = false
            if obj.Name ~= "HumanoidRootPart" then
                obj.ReceiveAge = 0
            end
        end
        -- Remove textura de mesh
        if obj:IsA("SpecialMesh") or obj:IsA("MeshPart") then
            pcall(function() obj.TextureId = "" end)
        end
    end)
end

-- Aplica em tudo existente
for _, v in ipairs(workspace:GetDescendants()) do
    limpar(v)
end

-- Aplica em novos objetos (habilidades, npcs, etc)
workspace.DescendantAdded:Connect(function(obj)
    task.defer(limpar, obj)
end)

-- ========================
-- VENTO ZERADO
-- ========================
pcall(function()
    workspace.WindSpeed = 0
    workspace.WindDirection = Vector3.new(0,0,0)
end)

-- ========================
-- OTIMIZAR PERSONAGEM
-- ========================
local function otimizarChar(char)
    task.wait(1)
    for _, v in ipairs(char:GetDescendants()) do
        limpar(v)
    end
end

if player.Character then otimizarChar(player.Character) end
player.CharacterAdded:Connect(otimizarChar)

print("✅ BOOST EXTREMO ATIVADO - Blox Fruits Mobile")
