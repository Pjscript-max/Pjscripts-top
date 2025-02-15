# Pjscripts-top
-- Script para pegar todos os itens no mapa

local player = game.Players.LocalPlayer  -- Obtém o jogador local
local character = player.Character or player.CharacterAdded:Wait()  -- Obtém o personagem do jogador
local backpack = character:WaitForChild("Backpack")  -- Acessa a mochila do jogador

-- Função para pegar todos os itens no mapa
local function collectItems()
    -- Procura por todos os itens no mapa (baseado no nome)
    for _, item in pairs(workspace:GetChildren()) do
        -- Verifica se o item é coletável (por exemplo, se o nome for "Item")
        if item:IsA("Model") and item:FindFirstChild("Item") then
            -- Adiciona o item ao inventário do jogador (apenas um exemplo de como você poderia fazer isso)
            local itemClone = item:Clone()  -- Faz uma cópia do item
            itemClone.Parent = backpack  -- Adiciona ao inventário do jogador

            -- Exibe uma mensagem para informar que o item foi coletado
            print("Item " .. item.Name .. " coletado!")
            
            -- Opcional: Destruir o item no mapa após ser coletado
            item:Destroy()
        end
    end
end

-- Função principal para coletar itens
local function autoCollectItems()
    while true do
        collectItems()  -- Coleta todos os itens
        wait(1)  -- Espera 1 segundo antes de tentar coletar novamente
    end
end

-- Chama a função para iniciar a coleta automática
autoCollectItems()
