-- Variáveis para o Reach
local reachEnabled = false
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local tool = nil  -- Defina a ferramenta que o player está usando, se aplicável
local originalReach = 10  -- Altere para o alcance normal
local increasedReach = 50  -- Altere para o alcance aumentado

-- Acessando o botão
local screenGui = player:WaitForChild("PlayerGui"):WaitForChild("ScreenGui")
local button = screenGui:WaitForChild("TextButton")

-- Função para alternar o alcance
local function toggleReach()
    reachEnabled = not reachEnabled
    if reachEnabled then
        -- Modifique o alcance da ferramenta ou personagem
        if tool then
            tool.Reach = increasedReach  -- Aqui você altera o alcance da ferramenta, se aplicável
        else
            -- Se não houver ferramenta, altere o alcance do personagem
            character.Humanoid.HipWidth = increasedReach  -- Modifique conforme necessário
        end
    else
        -- Restaura o alcance original
        if tool then
            tool.Reach = originalReach
        else
            character.Humanoid.HipWidth = originalReach
        end
    end
end

-- Conectando a função ao clique do botão
button.MouseButton1Click:Connect(function()
    toggleReach()  -- Alterna o alcance
end)
