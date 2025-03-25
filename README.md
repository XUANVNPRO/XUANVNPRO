loadstring(game:HttpGet("https://raw.githubusercontent.com/Marco8642/science/refs/heads/ok/dead%20rails"))()
task.wait(1)

local p, c = game.Players.LocalPlayer, p.Character or p.CharacterAdded:Wait()
local r, h, g = c:FindFirstChild("HumanoidRootPart"), c:FindFirstChild("Humanoid"), c:FindFirstChild("Revolver") or p.Backpack:FindFirstChild("Revolver")

game:GetService("RunService").Stepped:Connect(function()
    for _, v in pairs(c:GetDescendants()) do 
        if v:IsA("BasePart") then v.CanCollide = false end 
    end
end)

local function shoot(b) 
    if g and b:FindFirstChild("HumanoidRootPart") then 
        local e = g:FindFirstChild("FireEvent") or game.ReplicatedStorage:FindFirstChild("FireEvent")
        if e then e:FireServer(b.HumanoidRootPart.Position + Vector3.new(0, 1.5, 0)) end 
    end 
end

while task.wait(1) do
    for _, b in ipairs(workspace:GetChildren()) do 
        if b:IsA("Model") and b:FindFirstChild("Humanoid") and b ~= c then 
            shoot(b) 
            task.wait(0.5) 
        end 
    end
    task.wait(1)

    local bonds, total = 0, 0
    for _, bond in ipairs(workspace:GetChildren()) do 
        if bond:IsA("Part") and bond.Name == "Bond" and bond.Parent and bond.Parent:IsA("Model") and bond.Parent.Name == "BanditHouse" then
            total = total + 1
            
            bond.CanCollide = false
            bond.Anchored = false
            
            r.CFrame = bond.CFrame + Vector3.new(0, 1, 0)
            task.wait(0.1)
            firetouchinterest(r, bond, 0)
            firetouchinterest(r, bond, 1)

            h:MoveTo(bond.Position + Vector3.new(0, 1, 0))
            task.wait(0.5)
            
            bonds = bonds + 1
            task.wait(0.2)
        end 
    end

    if bonds > 0 and bonds == total and h then 
        task.wait(1) 
        h.Health = 0 
    end
end
