local PlayerGui = game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui", math.huge)
local CoreGui = game:GetService("CoreGui")
local RunServiceLoop
local Humanoid = nil
local ButtonUI = nil

coroutine.resume(coroutine.create(function()
    while task.wait() do
        for i, v in ipairs(PlayerGui:GetDescendants()) do
            if v:IsA("TextLabel") and v.Text == "Credits: X" then
                local ScreenUI = v.Parent.Parent
                ButtonUI = v.Parent:FindFirstChildOfClass("TextButton")
                ScreenUI.Enabled = true
                ScreenUI.Parent = CoreGui
                if ButtonUI ~= nil and ButtonUI.Text == "Off" then
                    print(ButtonUI.Text)
                    for i, v in pairs(getconnections(ButtonUI.MouseButton1Click)) do
                        print("clicked event")
                        v:Fire()
                    end
                    RunServiceLoop = game:GetService("RunService").RenderStepped:Connect(function()
                        if game:GetService("Players").LocalPlayer.Character ~= nil and game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Humanoid") and Humanoid == nil then
                            Humanoid = game:GetService("Players").LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
                        elseif Humanoid ~= nil then
                            if Humanoid.Health == 0 or Humanoid.Health < 0 and ButtonUI.Text ~= "Off" then
                                for i, v in pairs(getconnections(ButtonUI.MouseButton1Click)) do
                                    print("off")
                                    v:Fire()
                                end
                                print("disconnect")
                                Humanoid = nil
                                RunServiceLoop:Disconnect()
                            end
                        end
                    end)
                end
                break
            end
        end
    end
end))

loadstring(game:HttpGet("https://raw.githubusercontent.com/0Ben1/fe./main/Fling%20GUI"))()
