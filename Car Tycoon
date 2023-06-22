getgenv().toggleAutoBuild = false
getgenv().toggleAutoFill = false
getgenv().toggleAutoSell = false
getgenv().toggleAutoUpgradeCar = false
getgenv().totalConveyor = 1

local playerTeam = game:GetService("Players").LocalPlayer.Team

function autoBuild()
    spawn(function()
        while getgenv().toggleAutoBuild == true do 
            for i=1, getgenv().totalConveyor do
                game:GetService("ReplicatedStorage").Packages.Knit.Services.TycoonService.RF.SpawnCarSegment:InvokeServer("Conveyor" .. tostring(i))
                wait(1/tonumber(getgenv().totalConveyor))
            end
        end
    end)
end
    
function autoFill()
    spawn(function()
        while getgenv().toggleAutoFill == true do
            for i=1, getgenv().totalConveyor do
                game:GetService("ReplicatedStorage").Packages.Knit.Services.MaterialService.RF.Drop:InvokeServer(workspace.Tycoons:FindFirstChild(tostring(playerTeam)).Model.Lines:FindFirstChild("Conveyor" .. tostring(i)))
                wait(0.15)
                game:GetService("ReplicatedStorage").Packages.Knit.Services.MaterialService.RF.Dispose:InvokeServer()
                wait(0.15)
                game:GetService("ReplicatedStorage").Packages.Knit.Services.MaterialService.RF.Collect:InvokeServer("Metal")
                wait(0.15)
                game:GetService("ReplicatedStorage").Packages.Knit.Services.MaterialService.RF.Drop:InvokeServer(workspace.Tycoons:FindFirstChild(tostring(playerTeam)).Model.Lines:FindFirstChild("Conveyor" .. tostring(i)))
                wait(0.15)
                game:GetService("ReplicatedStorage").Packages.Knit.Services.MaterialService.RF.Dispose:InvokeServer()
                wait(0.15)
                game:GetService("ReplicatedStorage").Packages.Knit.Services.MaterialService.RF.Collect:InvokeServer("Glass")
                wait(0.15)
                game:GetService("ReplicatedStorage").Packages.Knit.Services.MaterialService.RF.Drop:InvokeServer(workspace.Tycoons:FindFirstChild(tostring(playerTeam)).Model.Lines:FindFirstChild("Conveyor" .. tostring(i)))
                wait(0.15)
            end
            wait(0.01)
        end
    end)
end
 

function autoSell()
    spawn(function()
        while getgenv().toggleAutoSell == true do
            game:GetService("ReplicatedStorage").Packages.Knit.Services.TycoonService.RF.AcceptBid:InvokeServer(workspace.Tycoons:FindFirstChild(tostring(playerTeam)).Model.NPCs:FindFirstChild("BidderPrompt"),"1")
            wait(0.75)
        end
    end)
end

function autoUpgradeCar()
    spawn(function()
        while getgenv().toggleAutoUpgradeCar == true do
            for i=0, getgenv().totalConveyor do
                game:GetService("ReplicatedStorage").Packages.Knit.Services.TycoonService.RF.BuyNextCar:InvokeServer("Conveyor" .. tostring(i))
                wait(1)
            end
            wait(0.01)
        end
    end)
end
    
--ui
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()
local Window = OrionLib:MakeWindow({Name = "Car Factory Tycoon", HidePremium = false, SaveConfig = true, ConfigFolder = "By Hexay#4488"})
local Tab = Window:MakeTab({
    Name = "Main Farming",
    Icon = "rbxassetid://4483345998",
	PremiumOnly = false
})

Tab:AddLabel("Made by Hexay#4488")
Tab:AddLabel("Dont buy workers except first worker")
Tab:AddParagraph("Buy worker for first conveyor")
Tab:AddParagraph("and make sure first step isn't bugged, if it is just restart")

local FarmTab = Tab:AddSection({
	Name = "Farming"
})

FarmTab:AddTextbox({
	Name = "Number of Conveyors",
	Default = "",
	TextDisappear = true,
	Callback = function(Value)
		getgenv().totalConveyor = Value
	end	  
})

FarmTab:AddToggle({
	Name = "Auto Fill",
	Default = false,
	Callback = function(Value)
		getgenv().toggleAutoFill = Value
        autoFill()
	end    
})

FarmTab:AddToggle({
	Name = "Auto Build Cars",
	Default = false,
	Callback = function(Value)
		getgenv().toggleAutoBuild = Value
        autoBuild()
	end    
})

FarmTab:AddToggle({
	Name = "Auto Sell Cars",
	Default = false,
	Callback = function(Value)
		getgenv().toggleAutoSell = Value
        autoSell()
	end    
})

FarmTab:AddToggle({
	Name = "Auto Upgrade Car Type",
	Default = false,
	Callback = function(Value)
		getgenv().toggleAutoUpgradeCar = Value
        autoUpgradeCar()
	end    
})
