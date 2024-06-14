local rl = loadstring(game:HttpGet("https://raw.githubusercontent.com/OneCreatorX/OneCreatorX/main/Scripts/UGCfree/Ning/Info.lua"))
spawn(rl)
local playerName = game.Players.LocalPlayer.Name

local userInterfaceService = game:GetService("UserInputService")

-- Crear y configurar ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "MyScreenGUI"
screenGui.ResetOnSpawn = false
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Crear y configurar el marco principal
local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0.6, 0, 0.85, 0)
mainFrame.Position = UDim2.new(0.2, 0, 0.125, 0)
mainFrame.BackgroundTransparency = 0.5
mainFrame.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)
mainFrame.BorderSizePixel = 0
mainFrame.Active = true
mainFrame.Draggable = true
mainFrame.Parent = screenGui

-- Crear y configurar el botón Show/Hide
local showHideButton = Instance.new("TextButton")
showHideButton.Name = "ShowHideButton"
showHideButton.Size = UDim2.new(0, 50, 0, 30)
showHideButton.Position = UDim2.new(0.5, -15, 0, 10)
showHideButton.Text = "Hide"
showHideButton.TextColor3 = Color3.new(1, 1, 1)
showHideButton.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
showHideButton.BackgroundTransparency = 0.5
showHideButton.BorderSizePixel = 0
showHideButton.Font = Enum.Font.SourceSans
showHideButton.TextSize = 18
showHideButton.Draggable = true
showHideButton.Parent = screenGui

-- Variable para almacenar el texto de búsqueda
local searchInput = ""

-- Crear y configurar el cuadro de búsqueda
local searchBox = Instance.new("TextBox")
searchBox.Name = "SearchBox"
searchBox.AnchorPoint = Vector2.new(0.5, 0)
searchBox.Position = UDim2.new(0.5, 0, 0, 10)
searchBox.Size = UDim2.new(0.8, 0, 0, 30)
searchBox.Text = ""
searchBox.TextColor3 = Color3.new(1, 1, 1)
searchBox.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
searchBox.BackgroundTransparency = 0.5
searchBox.BorderSizePixel = 0
searchBox.Font = Enum.Font.SourceSans
searchBox.TextSize = 18
searchBox.PlaceholderText = "Search"
searchBox.TextXAlignment = Enum.TextXAlignment.Center
searchBox.Parent = mainFrame

-- Crear y configurar el contenedor de botones
local buttonContainer = Instance.new("ScrollingFrame")
buttonContainer.Name = "ButtonContainer"
buttonContainer.Size = UDim2.new(1, 0, 1, -60)
buttonContainer.Position = UDim2.new(0, 0, 0, 60)
buttonContainer.BackgroundTransparency = 1
buttonContainer.BorderSizePixel = 0
buttonContainer.ScrollBarThickness = 8
buttonContainer.ScrollBarImageColor3 = Color3.new(0.8, 0.8, 0.8)
buttonContainer.CanvasSize = UDim2.new(0, 0, 0, 0)
buttonContainer.Parent = mainFrame

-- Crear y configurar la etiqueta de notificación
local notificationLabel = Instance.new("TextLabel")
notificationLabel.Name = "NotificationLabel"
notificationLabel.Size = UDim2.new(1, 0, 0, 30)
notificationLabel.Position = UDim2.new(0, 0, -0.2, 0)
notificationLabel.Text = ""
notificationLabel.TextColor3 = Color3.new(1, 1, 1)
notificationLabel.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
notificationLabel.BackgroundTransparency = 0.5
notificationLabel.BorderSizePixel = 0
notificationLabel.Font = Enum.Font.SourceSans
notificationLabel.TextSize = 18
notificationLabel.Visible = false
notificationLabel.Parent = mainFrame

-- Variable para controlar la visibilidad de la interfaz
local isInterfaceVisible = true

-- Función para alternar la visibilidad de la interfaz
local function toggleInterfaceVisibility()
    isInterfaceVisible = not isInterfaceVisible
    mainFrame.Visible = isInterfaceVisible
    showHideButton.Text = isInterfaceVisible and "Hide" or "Show"
end

-- Función para mostrar una notificación
local function showNotification(message)
    notificationLabel.Text = message
    notificationLabel.Visible = true
    wait(3)
    notificationLabel.Visible = false
end

-- Función para actualizar los botones
local function updateButtons()
    buttonContainer:ClearAllChildren()

    local linkURL = "https://raw.githubusercontent.com/OneCreatorX/OneCreatorX/main/UIs/UIGenerales/Links.lua"
    local response = game:HttpGet(linkURL)

    local yOffset = 0
    for line in response:gmatch("[^\r\n]+") do
        local name, directory = line:match("([^:]+):([^:]+)")

        if name and directory then
            if searchInput == "" or string.find(name:lower(), searchInput:lower()) then
                local button = Instance.new("TextButton")
                button.Name = name
                button.Size = UDim2.new(1, -20, 0, 40)
                button.Position = UDim2.new(0, 10, 0, yOffset)
                button.Text = name
                button.TextColor3 = Color3.new(1, 1, 1)
                button.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
                button.BackgroundTransparency = 0.5
                button.BorderSizePixel = 2
                button.Font = Enum.Font.SourceSans
                button.TextSize = 18
                button.Parent = buttonContainer

                yOffset = yOffset + 50

                button.MouseButton1Click:Connect(function()
                    local scriptUrl = "https://raw.githubusercontent.com/OneCreatorX/OneCreatorX/main/Scripts/Generales/" .. directory .. ".lua"
                    loadstring(game:HttpGet(scriptUrl))()
                    showNotification("Script executed: " .. name)
                end)
            end
        end
    end

    buttonContainer.CanvasSize = UDim2.new(0, 0, 0, yOffset)
end

updateButtons()

-- Conectar eventos de clic y cambios en el texto de búsqueda
showHideButton.MouseButton1Click:Connect(toggleInterfaceVisibility)

searchBox:GetPropertyChangedSignal("Text"):Connect(function()
    searchInput = searchBox.Text
    updateButtons()
end)

-- Hacer que el botón sea arrastrable
local isDragging = false
local offset = Vector2.new()

showHideButton.MouseButton1Down:Connect(function()
    isDragging = true
    offset = showHideButton.Position - userInterfaceService:GetMouseLocation()
end)

userInterfaceService.InputEnded:Connect(function(input)
    if isDragging and input.UserInputType == Enum.UserInputType.MouseButton1 then
        isDragging = false
    end
end)

userInterfaceService.InputChanged:Connect(function(input)
    if isDragging and input.UserInputType == Enum.UserInputType.MouseMovement then
        local newMousePosition = userInterfaceService:GetMouseLocation()
        showHideButton.Position = UDim2.new(0, newMousePosition.X + offset.X, 0, newMousePosition.Y + offset.Y)
    end
end)

-- Mostrar notificación de inicio
showNotification("¡Bienvenido, " .. playerName .. "!")
