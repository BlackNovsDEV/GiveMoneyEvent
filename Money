-- SERVICES
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local UserInputService = game:GetService("UserInputService")

local player = Players.LocalPlayer

-- EVENTS
local SellEvent = ReplicatedStorage:WaitForChild("SellCarEvent")
local BuyEvent = ReplicatedStorage:WaitForChild("BuyCarEvent")
local AddXPEvent = ReplicatedStorage:FindFirstChild("AddXPEvent", true)

-- CONFIG
local REQUIRED_KEY = "black23"
local KEY_ATTRIBUTE = "Blacknovs_KeyUnlocked"
local carName = "Koning Ultraspeed - Stock"

-- SAVED VALUES
local sellPrice = player:GetAttribute("SavedSellPrice") or 1
local buyPrice = player:GetAttribute("SavedBuyPrice") or 1000000
local xpAmount = player:GetAttribute("SavedXPAmount") or 1000

local running = false
local minimized = false
local unlocked = false

------------------------------------------------
-- 🔐 KEY SYSTEM (FIXED)
------------------------------------------------
if player:GetAttribute(KEY_ATTRIBUTE) then
	unlocked = true
else
	local keyGui = Instance.new("ScreenGui", player.PlayerGui)
	keyGui.ResetOnSpawn = false

	local kFrame = Instance.new("Frame", keyGui)
	kFrame.Size = UDim2.new(0,260,0,170)
	kFrame.Position = UDim2.new(0.5,-130,0.5,-85)
	kFrame.BackgroundColor3 = Color3.fromRGB(25,25,25)
	Instance.new("UICorner", kFrame)

	local kTitle = Instance.new("TextLabel", kFrame)
	kTitle.Size = UDim2.new(1,0,0,35)
	kTitle.Text = "🔐 Key System"
	kTitle.Font = Enum.Font.GothamBold
	kTitle.TextSize = 20
	kTitle.TextColor3 = Color3.new(1,1,1)
	kTitle.BackgroundTransparency = 1

	local kBox = Instance.new("TextBox", kFrame)
	kBox.Size = UDim2.new(1,-20,0,35)
	kBox.Position = UDim2.new(0,10,0,50)
	kBox.PlaceholderText = "Enter key..."
	kBox.ClearTextOnFocus = false
	kBox.BackgroundColor3 = Color3.fromRGB(40,40,40)
	kBox.TextColor3 = Color3.new(1,1,1)
	Instance.new("UICorner", kBox)

	local kStatus = Instance.new("TextLabel", kFrame)
	kStatus.Size = UDim2.new(1,0,0,20)
	kStatus.Position = UDim2.new(0,0,0,90)
	kStatus.TextColor3 = Color3.fromRGB(255,80,80)
	kStatus.BackgroundTransparency = 1

	local kBtn = Instance.new("TextButton", kFrame)
	kBtn.Size = UDim2.new(1,-20,0,35)
	kBtn.Position = UDim2.new(0,10,0,120)
	kBtn.Text = "Unlock"
	kBtn.BackgroundColor3 = Color3.fromRGB(0,170,0)
	kBtn.TextColor3 = Color3.new(1,1,1)
	Instance.new("UICorner", kBtn)

	kBtn.MouseButton1Click:Connect(function()
		local text = string.lower(string.gsub(kBox.Text, "%s+", ""))
		if text == REQUIRED_KEY then
			player:SetAttribute(KEY_ATTRIBUTE, true)
			unlocked = true
			keyGui:Destroy()
		else
			kStatus.Text = "Invalid key"
		end
	end)
end

repeat task.wait() until unlocked

------------------------------------------------
-- 🚗 AUTO UI
------------------------------------------------
local gui = Instance.new("ScreenGui", player.PlayerGui)
gui.ResetOnSpawn = false

local frame = Instance.new("Frame", gui)
frame.Size = UDim2.new(0,280,0,350)
frame.Position = UDim2.new(0.5,-140,0.5,-175)
frame.BackgroundColor3 = Color3.fromRGB(25,25,25)
frame.Active = true
Instance.new("UICorner", frame)

-- DRAG
do
	local dragging, dragStart, startPos
	frame.InputBegan:Connect(function(i)
		if i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch then
			dragging = true
			dragStart = i.Position
			startPos = frame.Position
		end
	end)

	UserInputService.InputChanged:Connect(function(i)
		if dragging then
			local delta = i.Position - dragStart
			frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
		end
	end)

	UserInputService.InputEnded:Connect(function()
		dragging = false
	end)
end

-- TITLE
local title = Instance.new("TextLabel", frame)
title.Size = UDim2.new(1,-60,0,30)
title.Position = UDim2.new(0,10,0,5)
title.Text = "🚗 Auto UI"
title.Font = Enum.Font.GothamBold
title.TextSize = 18
title.TextColor3 = Color3.new(1,1,1)
title.BackgroundTransparency = 1

local credit = Instance.new("TextLabel", frame)
credit.Size = UDim2.new(1,-20,0,20)
credit.Position = UDim2.new(0,10,0,30)
credit.Text = "@by Blacknovs"
credit.TextSize = 14
credit.TextColor3 = Color3.fromRGB(170,170,170)
credit.BackgroundTransparency = 1

-- MINIMIZE
local minimize = Instance.new("TextButton", frame)
minimize.Size = UDim2.new(0,30,0,30)
minimize.Position = UDim2.new(1,-40,0,10)
minimize.Text = "-"
minimize.BackgroundColor3 = Color3.fromRGB(50,50,50)
minimize.TextColor3 = Color3.new(1,1,1)
Instance.new("UICorner", minimize)

-- SELL
local sellLabel = Instance.new("TextLabel", frame)
sellLabel.Size = UDim2.new(1,-20,0,20)
sellLabel.Position = UDim2.new(0,10,0,55)
sellLabel.Text = "Sell Price"
sellLabel.TextColor3 = Color3.fromRGB(200,200,200)
sellLabel.BackgroundTransparency = 1
sellLabel.TextXAlignment = Enum.TextXAlignment.Left

local sellBox = Instance.new("TextBox", frame)
sellBox.Size = UDim2.new(1,-20,0,30)
sellBox.Position = UDim2.new(0,10,0,75)
sellBox.Text = tostring(sellPrice)
sellBox.BackgroundColor3 = Color3.fromRGB(40,40,40)
sellBox.TextColor3 = Color3.new(1,1,1)
sellBox.ClearTextOnFocus = false
Instance.new("UICorner", sellBox)

-- BUY
local buyLabel = Instance.new("TextLabel", frame)
buyLabel.Size = UDim2.new(1,-20,0,20)
buyLabel.Position = UDim2.new(0,10,0,115)
buyLabel.Text = "Buy Price"
buyLabel.TextColor3 = Color3.fromRGB(200,200,200)
buyLabel.BackgroundTransparency = 1
buyLabel.TextXAlignment = Enum.TextXAlignment.Left

local buyBox = Instance.new("TextBox", frame)
buyBox.Size = UDim2.new(1,-20,0,30)
buyBox.Position = UDim2.new(0,10,0,135)
buyBox.Text = tostring(buyPrice)
buyBox.BackgroundColor3 = Color3.fromRGB(40,40,40)
buyBox.TextColor3 = Color3.new(1,1,1)
buyBox.ClearTextOnFocus = false
Instance.new("UICorner", buyBox)

-- XP
local xpLabel = Instance.new("TextLabel", frame)
xpLabel.Size = UDim2.new(1,-20,0,20)
xpLabel.Position = UDim2.new(0,10,0,175)
xpLabel.Text = "XP Amount"
xpLabel.TextColor3 = Color3.fromRGB(200,200,200)
xpLabel.BackgroundTransparency = 1
xpLabel.TextXAlignment = Enum.TextXAlignment.Left

local xpBox = Instance.new("TextBox", frame)
xpBox.Size = UDim2.new(1,-20,0,30)
xpBox.Position = UDim2.new(0,10,0,195)
xpBox.Text = tostring(xpAmount)
xpBox.BackgroundColor3 = Color3.fromRGB(40,40,40)
xpBox.TextColor3 = Color3.new(1,1,1)
xpBox.ClearTextOnFocus = false
Instance.new("UICorner", xpBox)

-- XP BUTTON
local xpButton = Instance.new("TextButton", frame)
xpButton.Size = UDim2.new(1,-20,0,35)
xpButton.Position = UDim2.new(0,10,0,235)
xpButton.Text = AddXPEvent and "Send XP" or "XP Event not found"
xpButton.BackgroundColor3 = AddXPEvent and Color3.fromRGB(0,120,200) or Color3.fromRGB(80,80,80)
xpButton.TextColor3 = Color3.new(1,1,1)
xpButton.AutoButtonColor = AddXPEvent
Instance.new("UICorner", xpButton)

-- TOGGLE
local toggle = Instance.new("TextButton", frame)
toggle.Size = UDim2.new(1,-20,0,40)
toggle.Position = UDim2.new(0,10,0,280)
toggle.Text = "OFF"
toggle.TextSize = 22
toggle.BackgroundColor3 = Color3.fromRGB(170,0,0)
toggle.TextColor3 = Color3.new(1,1,1)
Instance.new("UICorner", toggle)

-- SAVE INPUTS
sellBox.FocusLost:Connect(function()
	local v = tonumber(sellBox.Text)
	if v then
		sellPrice = v
		player:SetAttribute("SavedSellPrice", v)
	end
end)

buyBox.FocusLost:Connect(function()
	local v = tonumber(buyBox.Text)
	if v then
		buyPrice = v
		player:SetAttribute("SavedBuyPrice", v)
	end
end)

xpBox.FocusLost:Connect(function()
	local v = tonumber(xpBox.Text)
	if v then
		xpAmount = v
		player:SetAttribute("SavedXPAmount", v)
	end
end)

-- MINIMIZE
minimize.MouseButton1Click:Connect(function()
	minimized = not minimized
	for _,v in ipairs({sellLabel,sellBox,buyLabel,buyBox,xpLabel,xpBox,xpButton,toggle}) do
		v.Visible = not minimized
	end
	minimize.Text = minimized and "+" or "-"
	frame.Size = minimized and UDim2.new(0,280,0,60) or UDim2.new(0,280,0,350)
end)

-- TOGGLE SELL / BUY
toggle.MouseButton1Click:Connect(function()
	running = not running
	toggle.Text = running and "ON" or "OFF"
	toggle.BackgroundColor3 = running and Color3.fromRGB(0,170,0) or Color3.fromRGB(170,0,0)
end)

-- XP RÁFAGA
xpButton.MouseButton1Click:Connect(function()
	if not AddXPEvent then return end
	xpButton.Text = "Sending..."
	xpButton.Active = false

	task.spawn(function()
		for i = 1, 50 do
			AddXPEvent:FireServer(xpAmount)
			task.wait(0.1)
		end
		xpButton.Text = "Send XP"
		xpButton.Active = true
	end)
end)

-- LOOP SELL / BUY
task.spawn(function()
	while true do
		if running then
			SellEvent:FireServer(carName, sellPrice)
			BuyEvent:FireServer(carName, buyPrice)
		end
		task.wait(0.3)
	end
end)
