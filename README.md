# legends-of-speed-script
legends of speed script


 
-- Initialize the script  
local player = game.Players.LocalPlayer  
local character = player.Character  
local humanoid = character.Humanoid  
  
-- Set up the autofarm variables  
local farmRadius = 10 -- adjust the farm radius to your liking  
local farmDelay = 1 -- adjust the farm delay to your liking  
local resourcesToCollect = {"Speed", "Coins"} -- adjust the resources to collect  
  
-- Function to detect nearby resources  
local function getNearbyResources()  
    local resources = {}  
    for _, obj in pairs(workspace:GetDescendants()) do  
        if obj:IsA("Part") and obj.Name == "Resource" then  
            local distance = (obj.Position - character.HumanoidRootPart.Position).magnitude  
            if distance &lt;= farmRadius then  
                table.insert(resources, obj)  
            end  
        end  
    end  
    return resources  
end  
  
-- Function to collect resources  
local function collectResources(resources)  
    for _, resource in pairs(resources) do  
        humanoid:MoveTo(resource.Position)  
        wait(farmDelay)  
        fireclickdetector(resource.ClickDetector)  
    end  
end  
  
-- Main loop  
while true do  
    local resources = getNearbyResources()  
    collectResources(resources)  
    wait(farmDelay)  
end  
