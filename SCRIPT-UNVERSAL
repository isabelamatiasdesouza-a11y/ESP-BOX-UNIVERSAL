local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Camera = workspace.CurrentCamera

local ESP_ENABLED = false
local ESP_OBJECTS = {}

-- UI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "ArthurScriptsUI"
ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")

local Button = Instance.new("TextButton")
Button.Size = UDim2.new(0, 150, 0, 40)
Button.Position = UDim2.new(0, 20, 0, 20)
Button.Text = "Arthur Scripts: OFF"
Button.BackgroundColor3 = Color3.fromRGB(30,30,30)
Button.TextColor3 = Color3.new(1,1,1)
Button.Parent = ScreenGui

-- Função criar ESP
local function createESP(player)
	if player == LocalPlayer then return end
	
	local function onCharacter(char)
		local humanoid = char:WaitForChild("Humanoid")
		local root = char:WaitForChild("HumanoidRootPart")

		-- Highlight (box)
		local highlight = Instance.new("Highlight")
		highlight.FillTransparency = 0.5
		highlight.OutlineColor = Color3.fromRGB(255,255,255)
		highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
		highlight.Enabled = ESP_ENABLED
		highlight.Parent = char

		-- Billboard (nome + vida + distância)
		local billboard = Instance.new("BillboardGui")
		billboard.Size = UDim2.new(0, 200, 0, 50)
		billboard.Adornee = root
		billboard.AlwaysOnTop = true
		billboard.StudsOffset = Vector3.new(0, 3, 0)
		billboard.Enabled = ESP_ENABLED
		billboard.Parent = char

		local label = Instance.new("TextLabel")
		label.Size = UDim2.new(1,0,1,0)
		label.BackgroundTransparency = 1
		label.TextColor3 = Color3.new(1,1,1)
		label.TextStrokeTransparency = 0
		label.TextScaled = true
		label.Parent = billboard

		-- Atualizar info
		task.spawn(function()
			while char.Parent do
				if root and humanoid then
					local distance = (LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") and 
						(LocalPlayer.Character.HumanoidRootPart.Position - root.Position).Magnitude) or 0

					label.Text = player.Name ..
						"\nHP: " .. math.floor(humanoid.Health) ..
						"\nDist: " .. math.floor(distance)

					highlight.Enabled = ESP_ENABLED
					billboard.Enabled = ESP_ENABLED
				end
				task.wait(0.2)
			end
		end)

		ESP_OBJECTS[player] = {highlight, billboard}
	end

	if player.Character then
		onCharacter(player.Character)
	end

	player.CharacterAdded:Connect(onCharacter)
end

-- Aplicar em todos
for _, p in pairs(Players
