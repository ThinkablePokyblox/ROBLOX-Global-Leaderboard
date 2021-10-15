--\\Variables//--
--Services--
local Services = require(game.ReplicatedStorage.Modules.Services)
--Variables--
local PlayerDonationAmounts = Services.GameServices.DataStoreService:GetOrderedDataStore("PlayerDonationAmounts")
--\\Local-Functions//--
local function UpdateLeaderboard()
	local Success,Err = pcall(function()
		local Data = PlayerDonationAmounts:GetSortedAsync(false,100)
		local DonationsPage = Data:GetCurrentPage()
		for Rank, Data in ipairs(DonationsPage) do
			local UserName = Services.GameServices.PlayerService:GetNameFromUserIdAsync(string.split(Data.key,"-Donations")[1])
			local Robux = Data.value
			local IsOnLeaderboard = false
			for _, v in pairs(script.Parent.GamepassGui.Frame1.ScrollingFrame:GetChildren()) do
				if (not v:IsA("UIListLayout")) and v.Name == UserName then
					IsOnLeaderboard = true
					break
				end
			end
			if Robux and IsOnLeaderboard == false then
				if Robux > 0 then
					if Rank == 1 then
						script.Parent.Parent.Parent.TopDonators.First.Configuration.userId.Value = string.split(Data.key,"-Donations")[1]
						script.Parent.Parent.Parent.TopDonators.First.Tags.Container.pName.Text = UserName
						local TemplateClone = script.Parent.Templates.First:Clone()
						TemplateClone.TextLabel.Text = "#"..Rank.." "..UserName.." - "..Robux
						TemplateClone.Name = UserName
						TemplateClone.Parent = script.Parent.GamepassGui.Frame1.ScrollingFrame
					elseif Rank == 2 then
						script.Parent.Parent.Parent.TopDonators.Second.Configuration.userId.Value = string.split(Data.key,"-Donations")[1]
						script.Parent.Parent.Parent.TopDonators.Second.Tags.Container.pName.Text = UserName
						local TemplateClone = script.Parent.Templates.Second:Clone()
						TemplateClone.TextLabel.Text = "#"..Rank.." "..UserName.." - "..Robux
						TemplateClone.Name = UserName
						TemplateClone.Parent = script.Parent.GamepassGui.Frame1.ScrollingFrame
					elseif Rank == 3 then
						script.Parent.Parent.Parent.TopDonators.Third.Configuration.userId.Value = string.split(Data.key,"-Donations")[1]
						script.Parent.Parent.Parent.TopDonators.Third.Tags.Container.pName.Text = UserName
						local TemplateClone = script.Parent.Templates.Third:Clone()
						TemplateClone.TextLabel.Text = "#"..Rank.." "..UserName.." - "..Robux
						TemplateClone.Name = UserName
						TemplateClone.Parent = script.Parent.GamepassGui.Frame1.ScrollingFrame
					elseif Rank > 3 and not Rank >= 100 then
						local TemplateClone = script.Parent.Templates.Normal:Clone()
						TemplateClone.TextLabel.Text = "#"..Rank.." "..UserName.." - "..Robux
						TemplateClone.Name = UserName
						TemplateClone.Parent = script.Parent.GamepassGui.Frame1.ScrollingFrame
					end
				end
			end
			print("::Donation_Leaderboard:: \n Added: "..UserName.." To the leaderboard. They have: "..Robux..". And their rank is: "..Rank..".")
		end
	end)
	if Success then
		print("::Donation_Leaderboard:: \n Successfully updated the leaderboard!")
	else
		warn("::Donation_Leaderboard:: \n Failed to update the leaderboard! "..Err)
	end
end
--\\Main-Code//--
while true do
	for _, v in pairs(script.Parent.GamepassGui.Frame1.ScrollingFrame:GetChildren()) do
		if not v:IsA("UIListLayout") then
			v:Destroy()
		end
	end
	UpdateLeaderboard()
	wait(120)
end
