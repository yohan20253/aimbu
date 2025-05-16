--// Configurações
local DISTANCIA_DANO = 10 -- raio em studs ao redor do jogador
local DANO = 20 -- dano por tiro

--// Referências
local tool = script.Parent
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

--// Quando o jogador atira
tool.Activated:Connect(function()
	for _, player in ipairs(Players:GetPlayers()) do
		if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("Humanoid") then
			local alvo = player.Character:FindFirstChild("HumanoidRootPart")
			if alvo then
				local distancia = (alvo.Position - humanoidRootPart.Position).Magnitude
				if distancia <= DISTANCIA_DANO then
					player.Character.Humanoid:TakeDamage(DANO)
				end
			end
		end
	end
end)
