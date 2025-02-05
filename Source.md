**Source:**
```lua
-- IGNORE THIS!! This is just the source! And you have to put this all up ur code.

-- UILibrary Module with animations and smooth UI elements
local UILibrary = {}

-- Services
local TweenService = game:GetService("TweenService")

-- Utility function to create a frame with UI elements like UICorner and UIStroke
local function createFrame(parent, size, position, backgroundColor, borderColor)
    local frame = Instance.new("Frame")
    frame.Size = size
    frame.Position = position
    frame.BackgroundColor3 = backgroundColor or Color3.fromRGB(50, 50, 50)
    frame.BorderColor3 = borderColor or Color3.fromRGB(0, 0, 0)
    frame.Parent = parent
    
    -- Add rounded corners to the frame
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 12) -- Adjust for more or less roundness
    corner.Parent = frame
    
    -- Optional: Add a border effect (stroke)
    local stroke = Instance.new("UIStroke")
    stroke.Thickness = 2
    stroke.Color = borderColor or Color3.fromRGB(0, 0, 0)
    stroke.Parent = frame
    
    return frame
end

-- Function to create a window
function UILibrary:createWindow(parent, title, size, position)
    local window = createFrame(parent, size, position, Color3.fromRGB(60, 60, 60), Color3.fromRGB(0, 0, 0))
    window.Name = title
    
    local titleLabel = Instance.new("TextLabel")
    titleLabel.Size = UDim2.new(1, 0, 0, 30)
    titleLabel.Position = UDim2.new(0, 0, 0, 0)
    titleLabel.Text = title
    titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    titleLabel.TextSize = 18
    titleLabel.TextStrokeTransparency = 0.5
    titleLabel.BackgroundTransparency = 1
    titleLabel.Parent = window
    
    return window
end

-- Function to create a smooth toggle button
function UILibrary:createToggleButton(parent, size, position, text, callback)
    local button = createFrame(parent, size, position, Color3.fromRGB(40, 40, 40), Color3.fromRGB(255, 255, 255))
    
    local buttonText = Instance.new("TextLabel")
    buttonText.Size = UDim2.new(1, 0, 1, 0)
    buttonText.Text = text
    buttonText.TextColor3 = Color3.fromRGB(255, 255, 255)
    buttonText.TextSize = 16
    buttonText.TextStrokeTransparency = 0.5
    buttonText.BackgroundTransparency = 1
    buttonText.Parent = button
    
    -- Toggle animation when clicked
    button.MouseButton1Click:Connect(function()
        -- Animate the toggle button when clicked (smooth transition using sine)
        local goal = { BackgroundColor3 = button.BackgroundColor3 == Color3.fromRGB(40, 40, 40) and Color3.fromRGB(70, 70, 70) or Color3.fromRGB(40, 40, 40) }
        local tweenInfo = TweenInfo.new(0.5, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)
        local tween = TweenService:Create(button, tweenInfo, goal)
        tween:Play()
        
        -- Callback function for toggle button click
        if callback then
            callback()
        end
    end)
    
    return button
end

-- Function to create a button with smooth animations
function UILibrary:createButton(parent, size, position, text, callback)
    local button = createFrame(parent, size, position, Color3.fromRGB(100, 100, 100), Color3.fromRGB(255, 255, 255))
    
    local buttonText = Instance.new("TextLabel")
    buttonText.Size = UDim2.new(1, 0, 1, 0)
    buttonText.Text = text
    buttonText.TextColor3 = Color3.fromRGB(255, 255, 255)
    buttonText.TextSize = 16
    buttonText.TextStrokeTransparency = 0.5
    buttonText.BackgroundTransparency = 1
    buttonText.Parent = button
    
    -- Button click animation with smooth scaling effect
    button.MouseButton1Click:Connect(function()
        local scaleGoal = { Size = UDim2.new(0.95, 0, 0.95, 0) }
        local tweenInfo = TweenInfo.new(0.2, Enum.EasingStyle.Sine, Enum.EasingDirection.Out)
        local tween = TweenService:Create(button, tweenInfo, scaleGoal)
        tween:Play()
        
        tween.Completed:Connect(function()
            -- Reset the size after the animation
            local resetGoal = { Size = UDim2.new(1, 0, 1, 0) }
            local resetTween = TweenService:Create(button, tweenInfo, resetGoal)
            resetTween:Play()
            
            -- Callback function when button is clicked
            if callback then
                callback()
            end
        end)
    end)
    
    return button
end

-- Function to create a slider
function UILibrary:createSlider(parent, size, position, minValue, maxValue, callback)
    local sliderFrame = createFrame(parent, size, position, Color3.fromRGB(70, 70, 70), Color3.fromRGB(255, 255, 255))
    
    local sliderBackground = Instance.new("Frame")
    sliderBackground.Size = UDim2.new(1, 0, 0, 10)
    sliderBackground.Position = UDim2.new(0, 0, 0, 10)
    sliderBackground.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
    sliderBackground.Parent = sliderFrame
    
    local sliderHandle = Instance.new("Frame")
    sliderHandle.Size = UDim2.new(0, 10, 0, 20)
    sliderHandle.Position = UDim2.new(0, 0, 0, -5)
    sliderHandle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    sliderHandle.Parent = sliderFrame
    
    local dragging = false
    
    sliderHandle.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
        end
    end)
    
    sliderHandle.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = false
        end
    end)
    
    game:GetService("UserInputService").InputChanged:Connect(function(input)
        if dragging then
            local mousePos = input.Position.X
            local sliderPos = sliderBackground.AbsolutePosition.X
            local sliderWidth = sliderBackground.AbsoluteSize.X
            local normalizedPos = math.clamp((mousePos - sliderPos) / sliderWidth, 0, 1)
            local value = math.floor(minValue + (maxValue - minValue) * normalizedPos)
            
            -- Update slider handle position
            sliderHandle.Position = UDim2.new(normalizedPos, 0, 0, -5)
            
            -- Callback function when slider value changes
            if callback then
                callback(value)
            end
        end
    end)
    
    return sliderFrame
end

return UILibrary

```
