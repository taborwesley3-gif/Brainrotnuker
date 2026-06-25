local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

local player = Players.LocalPlayer

------------------------------------------------
-- GUI ROOT
------------------------------------------------

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ModernTeleportHub"
screenGui.ResetOnSpawn = false
screenGui.Parent = player:WaitForChild("PlayerGui")

------------------------------------------------
-- TOGGLE BUTTON
------------------------------------------------

local toggleButton = Instance.new("TextButton")
toggleButton.Size = UDim2.new(0, 140, 0, 38)
toggleButton.Position = UDim2.new(0, 20, 0, 20)
toggleButton.Text = "MENU"
toggleButton.Font = Enum.Font.GothamBold
toggleButton.TextSize = 13
toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleButton.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
toggleButton.BorderSizePixel = 0
toggleButton.Parent = screenGui

Instance.new("UICorner", toggleButton).CornerRadius = UDim.new(0, 10)

------------------------------------------------
-- MAIN WINDOW
------------------------------------------------

local main = Instance.new("Frame")
main.Size = UDim2.new(0, 420, 0, 260)
main.Position = UDim2.new(0.5, -210, 0.5, -130)
main.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
main.BorderSizePixel = 0
main.Visible = false
main.Parent = screenGui

Instance.new("UICorner", main).CornerRadius = UDim.new(0, 14)

------------------------------------------------
-- TOP BAR (DRAG)
------------------------------------------------

local topBar = Instance.new("Frame")
topBar.Size = UDim2.new(1, 0, 0, 38)
topBar.BackgroundColor3 = Color3.fromRGB(28, 28, 28)
topBar.BorderSizePixel = 0
topBar.Parent = main

Instance.new("UICorner", topBar).CornerRadius = UDim.new(0, 14)

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -10, 1, 0)
title.Position = UDim2.new(0, 10, 0, 0)
title.BackgroundTransparency = 1
title.Text = "Teleport Hub"
title.Font = Enum.Font.GothamBold
title.TextSize = 14
title.TextColor3 = Color3.fromRGB(255,255,255)
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = topBar

------------------------------------------------
-- SIDEBAR
------------------------------------------------

local sideBar = Instance.new("Frame")
sideBar.Size = UDim2.new(0, 120, 1, -38)
sideBar.Position = UDim2.new(0, 0, 0, 38)
sideBar.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
sideBar.BorderSizePixel = 0
sideBar.Parent = main

local sideLayout = Instance.new("UIListLayout")
sideLayout.Padding = UDim.new(0, 6)
sideLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
sideLayout.Parent = sideBar

Instance.new("UIPadding", sideBar).PaddingTop = UDim.new(0, 10)

------------------------------------------------
-- CONTENT AREA
------------------------------------------------

local content = Instance.new("Frame")
content.Size = UDim2.new(1, -120, 1, -38)
content.Position = UDim2.new(0, 120, 0, 38)
content.BackgroundTransparency = 1
content.Parent = main

------------------------------------------------
-- BUTTON FACTORY
------------------------------------------------

local function createButton(parent, text)
	local b = Instance.new("TextButton")
	b.Size = UDim2.new(0.9, 0, 0, 36)
	b.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
	b.Text = text
	b.Font = Enum.Font.Gotham
	b.TextSize = 13
	b.TextColor3 = Color3.fromRGB(255,255,255)
	b.BorderSizePixel = 0
	b.Parent = parent

	Instance.new("UICorner", b).CornerRadius = UDim.new(0, 10)

	b.MouseEnter:Connect(function()
		b.BackgroundColor3 = Color3.fromRGB(55, 55, 55)
	end)

	b.MouseLeave:Connect(function()
		b.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
	end)

	return b
end

------------------------------------------------
-- TABS
------------------------------------------------

local teleportTab = Instance.new("Frame")
teleportTab.Size = UDim2.new(1,0,1,0)
teleportTab.BackgroundTransparency = 1
teleportTab.Visible = true
teleportTab.Parent = content

local movementTab = Instance.new("Frame")
movementTab.Size = UDim2.new(1,0,1,0)
movementTab.BackgroundTransparency = 1
movementTab.Visible = false
movementTab.Parent = content

local worldTab = Instance.new("Frame")
worldTab.Size = UDim2.new(1,0,1,0)
worldTab.BackgroundTransparency = 1
worldTab.Visible = false
worldTab.Parent = content

local function showTab(tab)
	for _,v in pairs({teleportTab, movementTab, worldTab}) do
		v.Visible = false
	end
	tab.Visible = true
end

------------------------------------------------
-- SIDEBAR BUTTONS
------------------------------------------------

createButton(sideBar, "Teleport").MouseButton1Click:Connect(function()
	showTab(teleportTab)
end)

createButton(sideBar, "Movement").MouseButton1Click:Connect(function()
	showTab(movementTab)
end)

createButton(sideBar, "World").MouseButton1Click:Connect(function()
	showTab(worldTab)
end)

------------------------------------------------
-- WORLD DATA
------------------------------------------------

local world = 1

local world1Spawn = Vector3.new(-19, 6.5, -242.7)
local world1Final = Vector3.new(-20.5, 6.3, -3980.1)

local world2Spawn = Vector3.new(119.1, 6.4, -518.9)
local world2Final = Vector3.new(121.1, 6.4, -1774.8)
local world2Eternal = Vector3.new(119.3, -2.3, -2336.9)

------------------------------------------------
-- TELEPORT TAB (FIXED)
------------------------------------------------

local teleportTabLayout = Instance.new("UIListLayout")
teleportTabLayout.Padding = UDim.new(0, 8)
teleportTabLayout.SortOrder = Enum.SortOrder.LayoutOrder
teleportTabLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
teleportTabLayout.Parent = teleportTab

Instance.new("UIPadding", teleportTab).PaddingTop = UDim.new(0, 10)

local spawnBtn = createButton(teleportTab, "Spawn")
local finalBtn = createButton(teleportTab, "Final Zone")
local eternalBtn = createButton(teleportTab, "Eternal")
eternalBtn.Visible = false

spawnBtn.LayoutOrder = 1
finalBtn.LayoutOrder = 2
eternalBtn.LayoutOrder = 3

local function getSpawn()
	return (world == 1) and world1Spawn or world2Spawn
end

local function getFinal()
	return (world == 1) and world1Final or world2Final
end

spawnBtn.MouseButton1Click:Connect(function()
	local r = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if r then r.CFrame = CFrame.new(getSpawn()) end
end)

finalBtn.MouseButton1Click:Connect(function()
	local r = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if r then r.CFrame = CFrame.new(getFinal()) end
end)

eternalBtn.MouseButton1Click:Connect(function()
	if world ~= 2 then return end
	local r = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
	if r then r.CFrame = CFrame.new(world2Eternal) end
end)

------------------------------------------------
-- WORLD TAB
------------------------------------------------

local worldBtn = createButton(worldTab, "Switch World")

worldBtn.MouseButton1Click:Connect(function()
	world = (world == 1) and 2 or 1
	worldBtn.Text = "World: " .. world
	eternalBtn.Visible = (world == 2)
end)

------------------------------------------------
-- MOVEMENT TAB (FLY)
------------------------------------------------

local flyBtn = createButton(movementTab, "Fly: OFF")
local flying = false
local flyConn
local speed = 150

local function startFly()
	local char = player.Character or player.CharacterAdded:Wait()
	local root = char:WaitForChild("HumanoidRootPart")

	flyConn = RunService.RenderStepped:Connect(function()
		local dir = Vector3.zero
		local cam = workspace.CurrentCamera

		if UserInputService:IsKeyDown(Enum.KeyCode.W) then dir += cam.CFrame.LookVector end
		if UserInputService:IsKeyDown(Enum.KeyCode.S) then dir -= cam.CFrame.LookVector end
		if UserInputService:IsKeyDown(Enum.KeyCode.A) then dir -= cam.CFrame.RightVector end
		if UserInputService:IsKeyDown(Enum.KeyCode.D) then dir += cam.CFrame.RightVector end
		if UserInputService:IsKeyDown(Enum.KeyCode.Space) then dir += Vector3.yAxis end
		if UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) then dir -= Vector3.yAxis end

		root.AssemblyLinearVelocity = dir.Magnitude > 0 and dir.Unit * speed or Vector3.zero
	end)
end

local function stopFly()
	if flyConn then flyConn:Disconnect() end
	flyConn = nil
end

flyBtn.MouseButton1Click:Connect(function()
	flying = not flying
	flyBtn.Text = flying and "Fly: ON" or "Fly: OFF"

	if flying then startFly() else stopFly() end
end)

------------------------------------------------
-- MENU TOGGLE (SMOOTH)
------------------------------------------------

local open = false

toggleButton.MouseButton1Click:Connect(function()
	open = not open
	main.Visible = true

	main:TweenPosition(
		open and UDim2.new(0.5, -210, 0.5, -130) or UDim2.new(0.5, -210, 0.55, -130),
		Enum.EasingDirection.Out,
		Enum.EasingStyle.Quart,
		0.25,
		true
	)

	if not open then
		task.delay(0.25, function()
			main.Visible = false
		end)
	end
end)

------------------------------------------------
-- DRAG SYSTEM
------------------------------------------------

local dragging = false
local dragStart
local startPos

topBar.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = true
		dragStart = input.Position
		startPos = main.Position
	end
end)

UserInputService.InputChanged:Connect(function(input)
	if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
		local delta = input.Position - dragStart
		main.Position = UDim2.new(
			startPos.X.Scale,
			startPos.X.Offset + delta.X,
			startPos.Y.Scale,
			startPos.Y.Offset + delta.Y
		)
	end
end)

UserInputService.InputEnded:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = false
	end
end)
