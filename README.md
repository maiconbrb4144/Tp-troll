-- Script para teleportar para o final (Gravity ou Speed)

-- Escolha o destino
local destino = workspace:WaitForChild("MainGame"):WaitForChild("EndTower"):WaitForChild("Rewards"):WaitForChild("Gravity"):WaitForChild("ProximityPrompPart")
-- ou use este se quiser o de Speed:
-- local destino = workspace:WaitForChild("MainGame"):WaitForChild("EndTower"):WaitForChild("Rewards"):WaitForChild("Speed"):WaitForChild("ProximityPrompPart")

-- Espera o personagem carregar corretamente
local player = game.Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()
local hrp = char:WaitForChild("HumanoidRootPart")

-- Remove colisão apenas das partes essenciais (mais leve)
for _, v in ipairs(char:GetDescendants()) do
	if v:IsA("BasePart") and v.CanCollide then
		v.CanCollide = false
	end
end

-- Faz uma pequena espera antes do teleporte (evita bugs de carregamento)
task.wait(0.2)

-- Teleporte seguro (levemente acima para não cair)
hrp.CFrame = CFrame.new(destino.Position + Vector3.new(0, 5, 0))
