-- imad_hub - سكربت رئيسي عربي
local Players = game:GetService("Players")
local Player = Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")

-- إنشاء الواجهة
local GUI = Instance.new("ScreenGui")
GUI.Name = "imad_hub"
GUI.ResetOnSpawn = false
GUI.Parent = PlayerGui

-- الإطار الرئيسي
local Frame = Instance.new("Frame")
Frame.Size = UDim2.new(0, 520, 0, 340)
Frame.Position = UDim2.new(0.5, -260, 0.5, -170)
Frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Frame.BorderSizePixel = 0
Frame.Visible = false
Frame.Parent = GUI

local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 15)
UICorner.Parent = Frame

-- عنوان
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 50)
Title.BackgroundTransparency = 1
Title.Text = "⚡ ايـماد هـاب ⚡"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 28
Title.Parent = Frame

local Line = Instance.new("Frame")
Line.Size = UDim2.new(1, -20, 0, 2)
Line.Position = UDim2.new(0, 10, 0, 55)
Line.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
Line.BorderSizePixel = 0
Line.Parent = Frame

-- زر فتح/إغلاق
local ToggleButton = Instance.new("TextButton")
ToggleButton.Size = UDim2.new(0, 60, 0, 60)
ToggleButton.Position = UDim2.new(0, 20, 0.5, -30)
ToggleButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
ToggleButton.Text = "⚡"
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Font = Enum.Font.GothamBold
ToggleButton.TextSize = 28
ToggleButton.Parent = GUI

local ToggleCorner = Instance.new("UICorner")
ToggleCorner.CornerRadius = UDim.new(1, 0)
ToggleCorner.Parent = ToggleButton

ToggleButton.MouseButton1Click:Connect(function()
    Frame.Visible = not Frame.Visible
end)

-- منطقة الأقسام
local Tabs = Instance.new("Frame")
Tabs.Size = UDim2.new(0, 140, 1, -65)
Tabs.Position = UDim2.new(0, 10, 0, 65)
Tabs.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
Tabs.Parent = Frame

local TabsCorner = Instance.new("UICorner")
TabsCorner.CornerRadius = UDim.new(0, 10)
TabsCorner.Parent = Tabs

local Content = Instance.new("Frame")
Content.Size = UDim2.new(1, -170, 1, -65)
Content.Position = UDim2.new(0, 160, 0, 65)
Content.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Content.Parent = Frame

local ContentCorner = Instance.new("UICorner")
ContentCorner.CornerRadius = UDim.new(0, 10)
ContentCorner.Parent = Content

-- إنشاء الأقسام
local أقسام = {}
local function إنشاءقسم(الاسم, ترتيب)
    local زر = Instance.new("TextButton")
    زر.Size = UDim2.new(1, -10, 0, 40)
    زر.Position = UDim2.new(0, 5, 0, (ترتيب - 1) * 45)
    زر.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    زر.Text = الاسم
    زر.TextColor3 = Color3.fromRGB(255, 255, 255)
    زر.Font = Enum.Font.GothamBold
    زر.TextSize = 18
    زر.Parent = Tabs

    local زرزاوية = Instance.new("UICorner")
    زرزاوية.CornerRadius = UDim.new(0, 8)
    زرزاوية.Parent = زر

    local صفحة = Instance.new("Frame")
    صفحة.Size = UDim2.new(1, 0, 1, 0)
    صفحة.BackgroundTransparency = 1
    صفحة.Visible = false
    صفحة.Parent = Content

    زر.MouseButton1Click:Connect(function()
        for _, قسم in pairs(أقسام) do
            قسم.Visible = false
        end
        صفحة.Visible = true
    end)

    table.insert(أقسام, صفحة)
    return صفحة
end

-- الأقسام
local صفحةتفريم = إنشاءقسم("🗡️ تفريم", 1)
local صفحةلاعب = إنشاءقسم("👤 خصائص اللاعب", 2)
local صفحةرؤية = إنشاءقسم("👁️ رؤية", 3)
local صفحةتيليبورت = إنشاءقسم("🌀 تيليبورت", 4)
local صفحةفواكه = إنشاءقسم("🍎 فواكه", 5)
local صفحةأحداث = إنشاءقسم("🎉 أحداث", 6)
صفحةتفريم.Visible = true

-- زر تشغيل/إيقاف للسكربتات
local function إنشاءزر(النص, ترتيب, رابطالسكربت, ParentFrame)
    local زر = Instance.new("TextButton")
    زر.Size = UDim2.new(0, 200, 0, 40)
    زر.Position = UDim2.new(0, 30, 0, (ترتيب - 1) * 50 + 10)
    زر.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    زر.Text = النص .. " (متوقف)"
    زر.TextColor3 = Color3.fromRGB(255, 255, 255)
    زر.Font = Enum.Font.GothamBold
    زر.TextSize = 18
    زر.Parent = ParentFrame

    local زاوية = Instance.new("UICorner")
    زاوية.CornerRadius = UDim.new(0, 8)
    زاوية.Parent = زر

    local حالة = false
    local اتصال

    زر.MouseButton1Click:Connect(function()
        حالة = not حالة
        if حالة then
            زر.BackgroundColor3 = Color3.fromRGB(0, 170, 0)
            زر.Text = النص .. " (شغال ✅)"
            اتصال = loadstring(game:HttpGet(رابطالسكربت))()
        else
            زر.BackgroundColor3 = Color3.fromRGB(170, 0, 0)
            زر.Text = النص .. " (متوقف)"
            if اتصال and type(اتصال) == "function" then
                pcall(اتصال)
            end
        end
    end)
end

-- إضافة أزرار التفريم
إنشاءزر("🗡️ تلفيل", 1, "https://raw.githubusercontent.com/ThunderZ-HUB/ThunderZ/main/BloxFruits", صفحةتفريم)
إنشاءزر("💀 جمع العظام", 2, "https://raw.githubusercontent.com/ThunderZ-HUB/ThunderZ/main/BonesFarm", صفحةتفريم)
إنشاءزر("🍩 قتل بوس كاتاكوري", 3, "https://raw.githubusercontent.com/ThunderZ-HUB/ThunderZ/main/Katakuri", صفحةتفريم)
إنشاءزر("👹 قتل جميع البوسات", 4, "https://raw.githubusercontent.com/ThunderZ-HUB/ThunderZ/main/BossFarm", صفحةتفريم)
إنشاءزر("⚡ تلفيل فواكه/سيوف/أسلوب", 5, "https://raw.githubusercontent.com/ThunderZ-HUB/ThunderZ/main/Mastery", صفحةتفريم)
إنشاءزر("📦 جمع الصناديق", 6, "https://raw.githubusercontent.com/ThunderZ-HUB/ThunderZ/main/ChestFarm", صفحةتفريم)

-- سحب الإطار
local UserInputService = game:GetService("UserInputService")
local dragging, dragInput, mousePos, framePos

Frame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        mousePos = input.Position
        framePos = Frame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then dragging = false end
        end)
    end
end)

Frame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then dragInput = input end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - mousePos
        Frame.Position = UDim2.new(framePos.X.Scale, framePos.X.Offset + delta.X, framePos.Y.Scale, framePos.Y.Offset + delta.Y)
    end
end)

-- سحب زر الفتح
local draggingButton, buttonDragInput, buttonMousePos, buttonPos
ToggleButton.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        draggingButton = true
        buttonMousePos = input.Position
        buttonPos = ToggleButton.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then draggingButton = false end
        end)
    end
end)

ToggleButton.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then buttonDragInput = input end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == buttonDragInput and draggingButton then
        local delta = input.Position - buttonMousePos
        ToggleButton.Position = UDim2.new(buttonPos.X.Scale, buttonPos.X.Offset + delta.X, buttonPos.Y.Scale, buttonPos.Y.Offset + delta.Y)
    end
end)
