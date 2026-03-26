-- 1. شاشة الترحيب (تظهر في البداية)
local introGui = Instance.new("ScreenGui", game:GetService("CoreGui"))
local introImg = Instance.new("ImageLabel", introGui)
introImg.Size = UDim2.new(0, 250, 0, 250) -- تم تعديل الحجم ليتناسب مع الصورة الجديدة
introImg.AnchorPoint = Vector2.new(0.5, 0.5)
introImg.Position = UDim2.new(0.5, 0, 0.5, 0)
introImg.Image = "rbxassetid://133834493769365" -- المعرف الجديد الذي طلبته
introImg.BackgroundTransparency = 1
task.delay(3, function() introGui:Destroy() end)

-- 2. نظام المفتاح (Key System)
local KeySystemGui = Instance.new("ScreenGui", game:GetService("CoreGui"))
local MainFrame = Instance.new("Frame", KeySystemGui)
local TextBox = Instance.new("TextBox", MainFrame)
local SubmitBtn = Instance.new("TextButton", MainFrame)
local Title = Instance.new("TextLabel", MainFrame)

-- تصميم لوحة المفتاح (VOID Style)
MainFrame.Size = UDim2.new(0, 300, 0, 180)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -90)
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0, 15)
local stroke = Instance.new("UIStroke", MainFrame)
stroke.Color = Color3.fromRGB(255, 185, 0)
stroke.Thickness = 2

Title.Size = UDim2.new(1, 0, 0, 50)
Title.Text = "VOID SNIPER | KEY SYSTEM"
Title.TextColor3 = Color3.fromRGB(255, 185, 0)
Title.BackgroundTransparency = 1
Title.Font = Enum.Font.GothamBold
Title.TextSize = 18

TextBox.Size = UDim2.new(0, 240, 0, 40)
TextBox.Position = UDim2.new(0.5, -120, 0.4, 0)
TextBox.PlaceholderText = "Enter Key Here..."
TextBox.Text = ""
TextBox.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
TextBox.TextColor3 = Color3.fromRGB(255, 255, 255)
Instance.new("UICorner", TextBox)

SubmitBtn.Size = UDim2.new(0, 150, 0, 40)
SubmitBtn.Position = UDim2.new(0.5, -75, 0.7, 10)
SubmitBtn.Text = "CHECK KEY"
SubmitBtn.BackgroundColor3 = Color3.fromRGB(255, 185, 0)
SubmitBtn.TextColor3 = Color3.fromRGB(0, 0, 0)
SubmitBtn.Font = Enum.Font.GothamBold
Instance.new("UICorner", SubmitBtn)

-- برمجة التحقق من المفتاح
SubmitBtn.MouseButton1Click:Connect(function()
    local correctKey = "SNIPER X Q"
    if TextBox.Text == correctKey then
        SubmitBtn.Text = "CORRECT!"
        SubmitBtn.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
        task.wait(1)
        KeySystemGui:Destroy()
        
        -- تشغيل السكربت الأصلي بعد المفتاح الصحيح
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Catwljzdyh/Scripts/heads/main/Flamingo"))()
        
        -- تفعيل كود التعديل (تغيير الاسم وحذف الأقسام)
        task.spawn(function()
            local targetName = "VOID SNIPER"
            local gold = Color3.fromRGB(255, 185, 0)
            local black = Color3.fromRGB(15, 15, 15)
            local blacklist = {"misc", "tiktok", "info", "credits", "social", "discord", "youtube"}

            while task.wait(0.5) do
                for _, obj in pairs(game:GetService("CoreGui"):GetDescendants()) do
                    if obj:IsA("GuiObject") then
                        local name = string.lower(obj.Name)
                        local text = (obj:IsA("TextLabel") or obj:IsA("TextButton")) and string.lower(obj.Text) or ""
                        
                        for _, word in pairs(blacklist) do
                            if string.find(name, word) or string.find(text, word) then
                                obj:Destroy()
                            end
                        end

                        if obj:IsA("Frame") or obj:IsA("ScrollingFrame") then
                            obj.BackgroundColor3 = black
                            obj.BorderSizePixel = 0
                            if not obj:FindFirstChild("CleanCorner") then
                                Instance.new("UICorner", obj).Name = "CleanCorner"
                            end
                        end

                        if obj:IsA("TextButton") and obj.Parent ~= MainFrame then
                            obj.BackgroundColor3 = gold
                            obj.TextColor3 = Color3.fromRGB(0, 0, 0)
                            obj.Font = Enum.Font.GothamBold
                        end

                        if obj:IsA("TextLabel") and obj.Parent ~= MainFrame then
                            obj.TextColor3 = Color3.fromRGB(255, 255, 255)
                            obj.Font = Enum.Font.GothamBold
                            if string.find(string.lower(obj.Text), "moai") or string.find(string.lower(obj.Text), "flamingo") then
                                obj.Text = targetName
                            end
                        end
                    end
                end
            end
        end)
    else
        TextBox.Text = ""
        TextBox.PlaceholderText = "WRONG KEY!"
        SubmitBtn.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
        task.wait(1)
        SubmitBtn.BackgroundColor3 = Color3.fromRGB(255, 185, 0)
        SubmitBtn.Text = "CHECK KEY"
    end
end)
