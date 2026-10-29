local LP=game.Players.LocalPlayer
local PG=LP:WaitForChild("PlayerGui")
if PG:FindFirstChild("JGTP") then PG.JGTP:Destroy() end
local gui=Instance.new("ScreenGui",PG)
gui.Name="JGTP"
local Bola=Instance.new("TextButton",gui)
Bola.Size=UDim2.new(0,55,0,55)
Bola.Position=UDim2.new(0,20,0,100)
Bola.Text="JG"
Bola.TextScaled=true
Bola.BackgroundColor3=Color3.fromRGB(20,20,20)
Bola.TextColor3=Color3.fromRGB(0,170,255)
Instance.new("UICorner",Bola).CornerRadius=UDim.new(1,0)
local Frame=Instance.new("Frame",gui)
Frame.Size=UDim2.new(0,200,0,210)
Frame.Position=UDim2.new(0,20,0,165)
Frame.BackgroundColor3=Color3.fromRGB(25,25,25)
Frame.Visible=false
Instance.new("UICorner",Frame)
local Title=Instance.new("TextLabel",Frame)
Title.Size=UDim2.new(1,0,0,30)
Title.Text="JG TELEPORT"
Title.TextColor3=Color3.new(1,1,1)
Title.BackgroundColor3=Color3.fromRGB(40,40,40)
Instance.new("UICorner",Title)
local function btn(t,y)
local b=Instance.new("TextButton",Frame)
b.Size=UDim2.new(0,180,0,32)
b.Position=UDim2.new(0,10,0,y)
b.Text=t
b.BackgroundColor3=Color3.fromRGB(50,50,50)
b.TextColor3=Color3.new(1,1,1)
Instance.new("UICorner",b)
return b
end
local b1=btn("1. Poner Punto",40)
local b2=btn("2. Ir al Punto",78)
local b3=btn("3. Regresar",116)
local b4=btn("Quitar Punto",154)
local UIS=game:GetService("UserInputService")
local punto=nil
local regreso=nil
local dragging,ds,sp
Title.InputBegan:Connect(function(i) if i.UserInputType==Enum.UserInputType.MouseButton1 or i.UserInputType==Enum.UserInputType.Touch then dragging=true ds=i.Position sp=Frame.Position end end)
Title.InputEnded:Connect(function() dragging=false end)
UIS.InputChanged:Connect(function(i) if dragging and (i.UserInputType==Enum.UserInputType.MouseMovement or i.UserInputType==Enum.UserInputType.Touch) then local d=i.Position-ds Frame.Position=UDim2.new(sp.X.Scale,sp.X.Offset+d.X,sp.Y.Scale,sp.Y.Offset+d.Y) end end)
Bola.MouseButton1Click:Connect(function() Frame.Visible=not Frame.Visible end)
b1.MouseButton1Click:Connect(function()
local c=LP.Character and LP.Character:FindFirstChild("HumanoidRootPart")
if c then punto=c.CFrame b1.Text="Punto Guardado!" task.wait(1) b1.Text="1. Poner Punto" end
end)
b2.MouseButton1Click:Connect(function()
if punto then
local c=LP.Character and LP.Character:FindFirstChild("HumanoidRootPart")
if c then regreso=c.CFrame c.CFrame=punto end
end
end)
b3.MouseButton1Click:Connect(function()
if regreso then
local c=LP.Character and LP.Character:FindFirstChild("HumanoidRootPart")
if c then c.CFrame=regreso end
end
end)
b4.MouseButton1Click:Connect(function() punto=nil regreso=nil b1.Text="1. Poner Punto" end)