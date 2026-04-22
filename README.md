# Joey-s-prisonlifey-scriptttt
loadstring([[
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

local player = Players.LocalPlayer
local mouse = player:GetMouse()

local correctKey = "Joethepookie"
local keyVerified = false

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "PrisonLifeScript"
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.ResetOnSpawn = false
screenGui.Parent = player:WaitForChild("PlayerGui")

local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 400, 0, 500)
mainFrame.Position = UDim2.new(0.5, -200, 0.5, -250)
mainFrame.BackgroundColor3 = Color3.fromRGB(30, 0, 50)
mainFrame.BackgroundTransparency = 0.1
mainFrame.BorderSizePixel = 0
mainFrame.Visible = false
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = screenGui

local title = Instance.new("TextLabel")
title.Name = "Title"
title.Size = UDim2.new(1, 0, 0, 40)
title.Position = UDim2.new(0, 0, 0, 0)
title.BackgroundColor3 = Color3.fromRGB(100, 0, 150)
title.Text = "Prison Life Script v1.0"
title.TextColor3 = Color3.white
title.TextSize = 20
title.Font = Enum.Font.GothamBold
title.Parent = mainFrame

local closeButton = Instance.new("TextButton")
closeButton.Name = "CloseButton"
closeButton.Size = UDim2.new(0, 30, 0, 30)
closeButton.Position = UDim2.new(1, -35, 0, 5)
closeButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
closeButton.Text = "X"
closeButton.TextColor3 = Color3.white
closeButton.TextSize = 18
closeButton.Font = Enum.Font.GothamBold
closeButton.Parent = mainFrame

closeButton.MouseButton1Click:Connect(function()
    mainFrame.Visible = false
end)

local keyFrame = Instance.new("Frame")
keyFrame.Name = "KeyFrame"
keyFrame.Size = UDim2.new(0, 300, 0, 150)
keyFrame.Position = UDim2.new(0.5, -150, 0.5, -75)
keyFrame.BackgroundColor3 = Color3.fromRGB(40, 0, 70)
keyFrame.Visible = true
keyFrame.Parent = screenGui

local keyTitle = Instance.new("TextLabel")
keyTitle.Size = UDim2.new(1, 0, 0, 40)
keyTitle.BackgroundColor3 = Color3.fromRGB(80, 0, 120)
keyTitle.Text = "Enter Key"
keyTitle.TextColor3 = Color3.white
keyTitle.TextSize = 18
keyTitle.Font = Enum.Font.GothamBold
keyTitle.Parent = keyFrame

local keyInput = Instance.new("TextBox")
keyInput.Size = UDim2.new(0.8, 0, 0, 40)
keyInput.Position = UDim2.new(0.1, 0, 0.3, 0)
keyInput.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
keyInput.TextColor3 = Color3.white
keyInput.Text = ""
keyInput.PlaceholderText = "Enter key here..."
keyInput.TextSize = 16
keyInput.Parent = keyFrame

local keySubmit = Instance.new("TextButton")
keySubmit.Size = UDim2.new(0.6, 0, 0, 40)
keySubmit.Position = UDim2.new(0.2, 0, 0.7, 0)
keySubmit.BackgroundColor3 = Color3.fromRGB(0, 150, 0)
keySubmit.Text = "Submit"
keySubmit.TextColor3 = Color3.white
keySubmit.TextSize = 18
keySubmit.Font = Enum.Font.GothamBold
keySubmit.Parent = keyFrame

local featuresFrame = Instance.new("ScrollingFrame")
featuresFrame.Name = "FeaturesFrame"
featuresFrame.Size = UDim2.new(1, -20, 1, -100)
featuresFrame.Position = UDim2.new(0, 10, 0, 50)
featuresFrame.BackgroundTransparency = 1
featuresFrame.ScrollBarThickness = 8
featuresFrame.CanvasSize = UDim2.new(0, 0, 0, 800)
featuresFrame.Visible = true
featuresFrame.Parent = mainFrame

local function createFeature(name, defaultState)
    local featureFrame = Instance.new("Frame")
    featureFrame.Size = UDim2.new(1, 0, 0, 40)
    featureFrame.BackgroundColor3 = Color3.fromRGB(50, 0, 80)
    featureFrame.BorderSizePixel = 0
    
    local featureLabel = Instance.new("TextLabel")
    featureLabel.Size = UDim2.new(0.7, 0, 1, 0)
    featureLabel.BackgroundTransparency = 1
    featureLabel.Text = name
    featureLabel.TextColor3 = Color3.white
    featureLabel.TextSize = 16
    featureLabel.TextXAlignment = Enum.TextXAlignment.Left
    featureLabel.Parent = featureFrame
    
    local featureToggle = Instance.new("TextButton")
    featureToggle.Size = UDim2.new(0, 60, 0, 30)
    featureToggle.Position = UDim2.new(0.8, -60, 0.5, -15)
    featureToggle.Text = defaultState and "ON" or "OFF"
    featureToggle.TextColor3 = Color3.white
    featureToggle.TextSize = 14
    featureToggle.Font = Enum.Font.GothamBold
    featureToggle.BackgroundColor3 = defaultState and Color3.fromRGB(0, 150, 0) or Color3.fromRGB(150, 0, 0)
    featureToggle.Parent = featureFrame
    
    local enabled = defaultState
    
    featureToggle.MouseButton1Click:Connect(function()
        enabled = not enabled
        featureToggle.Text = enabled and "ON" or "OFF"
        featureToggle.BackgroundColor3 = enabled and Color3.fromRGB(0, 150, 0) or Color3.fromRGB(150, 0, 0)
        
        print(name .. " " .. (enabled and "enabled" or "disabled"))
    end)
    
    return featureFrame
end

local features = {
    "Aimbot",
    "ESP",
    "Auto Shoot",
    "Auto Handcuff",
    "Walkspeed Boost",
    "Jump Power Boost",
    "Invisible",
    "Spin Bot",
    "Fly",
    "Teleport",
    "Fast Shoot",
    "Spam Jump"
}

for i, feature in ipairs(features) do
    local featureElement = createFeature(feature, false)
    featureElement.Position = UDim2.new(0, 0, 0, (i-1)*45)
    featureElement.Parent = featuresFrame
end

local colorFrame = Instance.new("Frame")
colorFrame.Size = UDim2.new(1, 0, 0, 100)
colorFrame.Position = UDim2.new(0, 0, 0, #features * 45)
colorFrame.BackgroundColor3 = Color3.fromRGB(60, 0, 90)
colorFrame.BorderSizePixel = 0
colorFrame.Parent = featuresFrame

local colorTitle = Instance.new("TextLabel")
colorTitle.Size = UDim2.new(1, 0, 0, 25)
colorTitle.BackgroundTransparency = 1
colorTitle.Text = "Color Customization"
colorTitle.TextColor3 = Color3.white
colorTitle.TextSize = 16
colorTitle.Font = Enum.Font.GothamBold
colorTitle.Parent = colorFrame

local rInput = Instance.new("TextBox")
rInput.Size = UDim2.new(0.3, 0, 0, 30)
rInput.Position = UDim2.new(0.05, 0, 0.4, 0)
rInput.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
rInput.TextColor3 = Color3.white
rInput.Text = "100"
rInput.PlaceholderText = "R"
rInput.TextSize = 14
rInput.Parent = colorFrame

local gInput = Instance.new("TextBox")
gInput.Size = UDim2.new(0.3, 0, 0, 30)
gInput.Position = UDim2.new(0.4, 0, 0.4, 0)
gInput.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
gInput.TextColor3 = Color3.white
gInput.Text = "0"
gInput.PlaceholderText = "G"
gInput.TextSize = 14
gInput.Parent = colorFrame

local bInput = Instance.new("TextBox")
bInput.Size = UDim2.new(0.3, 0, 0, 30)
bInput.Position = UDim2.new(0.75, 0, 0.4, 0)
bInput.BackgroundColor3 = Color3.fromRGB(0, 0, 255)
bInput.TextColor3 = Color3.white
bInput.Text = "150"
bInput.PlaceholderText = "B"
bInput.TextSize = 14
gInput.Parent = colorFrame

local applyColor = Instance.new("TextButton")
applyColor.Size = UDim2.new(0.8, 0, 0, 30)
applyColor.Position = UDim2.new(0.1, 0, 0.8, 0)
applyColor.BackgroundColor3 = Color3.fromRGB(100, 0, 150)
applyColor.Text = "Apply Color"
applyColor.TextColor3 = Color3.white
applyColor.TextSize = 14
applyColor.Font = Enum.Font.GothamBold
applyColor.Parent = colorFrame

applyColor.MouseButton1Click:Connect(function()
    local r = tonumber(rInput.Text) or 100
    local g = tonumber(gInput.Text) or 0
    local b = tonumber(bInput.Text) or 150
    
    mainFrame.BackgroundColor3 = Color3.fromRGB(r, g, b)
end)

local fpsLabel = Instance.new("TextLabel")
fpsLabel.Name = "FPSLabel"
fpsLabel.Size = UDim2.new(0, 100, 0, 30)
fpsLabel.Position = UDim2.new(0, 0, 1, -30)
fpsLabel.BackgroundColor3 = Color3.fromRGB(0, 0, 0, 0.5)
fpsLabel.Text = "FPS: 60"
fpsLabel.TextColor3 = Color3.white
fpsLabel.TextSize = 14
fpsLabel.Font = Enum.Font.Gotham
fpsLabel.Parent = mainFrame

local toggleButton = Instance.new("TextButton")
toggleButton.Name = "ToggleButton"
toggleButton.Size = UDim2.new(0, 80, 0, 30)
toggleButton.Position = UDim2.new(0, 10, 0, 10)
toggleButton.BackgroundColor3 = Color3.fromRGB(100, 0, 150)
toggleButton.Text = "Open GUI"
toggleButton.TextColor3 = Color3.white
toggleButton.TextSize = 14
toggleButton.Font = Enum.Font.GothamBold
toggleButton.Visible = false
toggleButton.Parent = screenGui

toggleButton.MouseButton1Click:Connect(function()
    mainFrame.Visible = not mainFrame.Visible
    toggleButton.Text = mainFrame.Visible and "Close GUI" or "Open GUI"
end)

keySubmit.MouseButton1Click:Connect(function()
    if keyInput.Text == correctKey then
        keyVerified = true
        keyFrame.Visible = false
        mainFrame.Visible = true
        toggleButton.Visible = true
        print("Key verified! GUI loaded.")
    else
        keyInput.Text = ""
        keyInput.PlaceholderText = "Wrong key! Try again..."
        print("Invalid key entered.")
    end
end)

keyInput.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        keySubmit:Activate()
    end
end)

local lastUpdate = tick()
local frameCount = 0
local currentFPS = 60

RunService.RenderStepped:Connect(function()
    frameCount = frameCount + 1
    
    if tick() - lastUpdate >= 1 then
        currentFPS = math.floor(frameCount)
        frameCount = 0
        lastUpdate = tick()
        
        if fpsLabel then
            fpsLabel.Text = "FPS: " .. tostring(currentFPS)
        end
    end
end)

print("Player joined: " .. player.Name)
print("Script loaded for: " .. player.DisplayName)

screenGui.DisplayOrder = 999

print("Script initialized. Enter key: Joethepookie")
print("If key frame doesn't show, check PlayerGui for ScreenGui")
]])()