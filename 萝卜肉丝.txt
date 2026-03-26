


if game:GetService('ContentProvider').RequestQueueSize > 10 then           
    repeat task.wait()
    until game:GetService('ContentProvider').RequestQueueSize <= 10
end


local shared = {
    version = "V3.0.0";
    folders = {
        main = 'IceWare',
        games = 'IceWare/Games',
        analytics = 'IceWare/Analytics',
    };
}

for _, folder in pairs(shared.folders) do
    if not isfolder(folder) then
        print(string.format("[ ICEWARE ] Setting up %s folder", folder))
        makefolder(folder)
    end
end

writefile("IceWare/Discord.txt", "https://discord.gg/sn2Etx6M8G")

local games = {
    [{89851325271396}] = "https://raw.githubusercontent.com/Iceware-RBLX/Roblox/refs/heads/main/Games/ViolenceDistrict/Main.lua"; -- 巨人时代
    [{11653088948}] = "https://raw.githubusercontent.com/VRLNB/GH-BM/refs/heads/main/_Jurassic_square_.txt"; -- 侏罗纪方块
    [{5233782396}] = "https://raw.githubusercontent.com/zxc5558/GHT/refs/heads/main/Sona.txt";
    -- 索里亚世界
}

for ids, url in next, games do
    if table.find(ids, game.PlaceId) then
        task.wait(); loadstring(game:HttpGet(url))()
    end
end


if getgenv().Settings and getgenv().Settings.Analytics then
    game:GetService("LogService").MessageOut:Connect(function(...) 
        appendfile("IceWare/analytics/" .. game:GetService("MarketplaceService"):GetProductInfo(game.PlaceId).Name .. "_" .. os.date("%Y-%m-%d") .. ".log", "[" .. os.date("%H:%M:%S") .. "] [" .. identifyexecutor() .. "] " .. select(1, ...) .. "\n") 
    end)
end
