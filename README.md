-- This script should be placed in a LocalScript inside an object that the player can interact with,
-- such as a button on the screen (ScreenGui) or an object in the world (ClickDetector).

local function giveWins()
    -- Gets the Players service to access the local player.
    local Players = game:GetService("Players")
    local localPlayer = Players.LocalPlayer

    -- Checks if the local player exists.
    if localPlayer then
        -- Looks for a value within the player to store the wins.
        -- It's common to use an IntValue or NumberValue for this.
        local winsValue = localPlayer:FindFirstChild("Wins")

        -- If the "Wins" value exists, it adds 99999 to it.
        if winsValue then
            winsValue.Value = winsValue.Value + 99999
            print("You received 99999 wins!")
        else
            -- If the "Wins" value doesn't exist, you'll need to create it first
            -- in a Server Script inside the Player when they join the game.
            warn("The 'Wins' value was not found in your character.")
            warn("Make sure to create an IntValue or NumberValue named 'Wins' inside the Player.")
        end
    else
        warn("Local player not found.")
    end
end

-- Example for an on-screen button (ScreenGui):
-- Assuming you have a button named "GiveWinsButton" inside a ScreenGui.
local button = script.Parent:WaitForChild("GiveWinsButton")
if button:IsA("TextButton") or button:IsA("ImageButton") then
    button.MouseButton1Click:Connect(giveWins)
end

-- Example for an object in the world (ClickDetector):
-- Assuming you have an object named "WinObject" with a ClickDetector inside.
local winObject = script.Parent:WaitForChild("WinObject")
local clickDetector = winObject:FindFirstChild("ClickDetector")
if clickDetector then
    clickDetector.MouseClick:Connect(function(player)
        if player == game:GetService("Players").LocalPlayer then
            giveWins()
        end
    end)
end
