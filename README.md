-- Khởi tạo ScreenGui
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local UICorner = Instance.new("UICorner")
local UIStroke = Instance.new("UIStroke")
local Title = Instance.new("TextLabel")
local ScrollingFrame = Instance.new("ScrollingFrame")
local UIPadding = Instance.new("UIPadding")
local UIListLayout = Instance.new("UIListLayout")

-- Cấu hình chính
ScreenGui.Name = "k00pkidd770_f3x_gui_root"
ScreenGui.Parent = game:GetService("CoreGui")
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
MainFrame.Position = UDim2.new(0.5, -300, 0.5, -200)
MainFrame.Size = UDim2.new(0, 600, 0, 400)
MainFrame.Active = true
MainFrame.Draggable = true

UICorner.CornerRadius = UDim.new(0, 12); UICorner.Parent = MainFrame
UIStroke.Color = Color3.fromRGB(255, 255, 255); UIStroke.Thickness = 3; UIStroke.Parent = MainFrame

Title.Parent = MainFrame; Title.BackgroundTransparency = 1; Title.Position = UDim2.new(0, 0, 0, 10)
Title.Size = UDim2.new(1, 0, 0, 40); Title.Font = Enum.Font.GothamBold
Title.Text = "k00pkidd770 gui f3x"; Title.TextColor3 = Color3.fromRGB(255, 255, 255); Title.TextSize = 24

ScrollingFrame.Parent = MainFrame; ScrollingFrame.BackgroundTransparency = 1
ScrollingFrame.Position = UDim2.new(0, 10, 0, 60); ScrollingFrame.Size = UDim2.new(1, -20, 1, -70)
ScrollingFrame.CanvasSize = UDim2.new(0, 0, 0, 0); ScrollingFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
ScrollingFrame.ScrollBarThickness = 4

-- Sắp xếp các nhóm theo chiều dọc
UIListLayout.Parent = ScrollingFrame; UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder; UIListLayout.Padding = UDim.new(0, 10)
UIPadding.Parent = ScrollingFrame; UIPadding.PaddingLeft = UDim.new(0, 5); UIPadding.PaddingTop = UDim.new(0, 5)

-- Hàm tạo khung lưới cho nút
local function CreateGridFrame(name, order)
    local Frame = Instance.new("Frame")
    local Grid = Instance.new("UIGridLayout")
    Frame.Name = name; Frame.Parent = ScrollingFrame; Frame.BackgroundTransparency = 1
    Frame.Size = UDim2.new(1, 0, 0, 0); Frame.AutomaticSize = Enum.AutomaticSize.Y
    Frame.LayoutOrder = order
    Grid.Parent = Frame; Grid.CellSize = UDim2.new(0, 132, 0, 40); Grid.CellPadding = UDim2.new(0, 10, 0, 10)
    return Frame
end

-- Hàm tạo nút
local function AddBtn(parent, text, callback)
    local btn = Instance.new("TextButton")
    local corner = Instance.new("UICorner")
    btn.Parent = parent; btn.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    btn.Font = Enum.Font.GothamBold; btn.Text = text; btn.TextColor3 = Color3.fromRGB(255, 255, 255); btn.TextSize = 12
    corner.CornerRadius = UDim.new(0, 6); corner.Parent = btn
    btn.MouseButton1Click:Connect(callback)
end

-- --- NHÓM 1: CHỨC NĂNG ---
local AdminGrid = CreateGridFrame("AdminGrid", 1)

AddBtn(AdminGrid, "Decal Spam", function()
local player = game.Players.LocalPlayer
		local char = player.Character
		local tool
		for i,v in player:GetDescendants() do
			if v.Name == "SyncAPI" then
				tool = v.Parent
			end
		end
		for i,v in game.ReplicatedStorage:GetDescendants() do
			if v.Name == "SyncAPI" then
				tool = v.Parent
			end
		end
		--craaa
		remote = tool.SyncAPI.ServerEndpoint
		function _(args)
			remote:InvokeServer(unpack(args))
		end
		function SetCollision(part,boolean)
			local args = {
				[1] = "SyncCollision",
				[2] = {
					[1] = {
						["Part"] = part,
						["CanCollide"] = boolean
					}
				}
			}
			_(args)
		end
		function SetAnchor(boolean,part)
			local args = {
				[1] = "SyncAnchor",
				[2] = {
					[1] = {
						["Part"] = part,
						["Anchored"] = boolean
					}
				}
			}
			_(args)
		end
		function CreatePart(cf,parent)
			local args = {
				[1] = "CreatePart",
				[2] = "Normal",
				[3] = cf,
				[4] = parent
			}
			_(args)
		end
		function DestroyPart(part)
			local args = {
				[1] = "Remove",
				[2] = {
					[1] = part
				}
			}
			_(args)
		end
		function MovePart(part,cf)
			local args = {
				[1] = "SyncMove",
				[2] = {
					[1] = {
						["Part"] = part,
						["CFrame"] = cf
					}
				}
			}
			_(args)
		end
		function Resize(part,size,cf)
			local args = {
				[1] = "SyncResize",
				[2] = {
					[1] = {
						["Part"] = part,
						["CFrame"] = cf,
						["Size"] = size
					}
				}
			}
			_(args)
		end
		function AddMesh(part)
			local args = {
				[1] = "CreateMeshes",
				[2] = {
					[1] = {
						["Part"] = part
					}
				}
			}
			_(args)
		end
	
		function SetMesh(part,meshid)
			local args = {
				[1] = "SyncMesh",
				[2] = {
					[1] = {
						["Part"] = part,
						["MeshId"] = "rbxassetid://"..meshid
					}
				}
			}
			_(args)
		end
		function SetTexture(part, texid)
			local args = {
				[1] = "SyncMesh",
				[2] = {
					[1] = {
						["Part"] = part,
						["TextureId"] = "rbxassetid://"..texid
					}
				}
			}
			_(args)
		end
		function SetName(part, stringg)
			local args = {
				[1] = "SetName",
				[2] = {
					[1] = part
				},
				[3] = stringg
			}
	
			_(args)
		end
		function MeshResize(part,size)
			local args = {
				[1] = "SyncMesh",
				[2] = {
					[1] = {
						["Part"] = part,
						["Scale"] = size
					}
				}
			}
			_(args)
		end
		function Weld(part1, part2,lead)
			local args = {
				[1] = "CreateWelds",
				[2] = {
					[1] = part1,
					[2] = part2
				},
				[3] = lead
			}
			_(args)
	
		end
		function SetLocked(part,boolean)
			local args = {
				[1] = "SetLocked",
				[2] = {
					[1] = part
				},
				[3] = boolean
			}
			_(args)
		end
		function SetTrans(part,int)
			local args = {
				[1] = "SyncMaterial",
				[2] = {
					[1] = {
						["Part"] = part,
						["Transparency"] = int
					}
				}
			}
			_(args)
		end
		function CreateSpotlight(part)
			local args = {
				[1] = "CreateLights",
				[2] = {
					[1] = {
						["Part"] = part,
						["LightType"] = "SpotLight"
					}
				}
			}
			_(args)
		end
		function SyncLighting(part,brightness)
			local args = {
				[1] = "SyncLighting",
				[2] = {
					[1] = {
						["Part"] = part,
						["LightType"] = "SpotLight",
						["Brightness"] = brightness
					}
				}
			}
			_(args)
		end
		function Color(part,color)
			local args = {
				[1] = "SyncColor",
				[2] = {
					[1] = {
						["Part"] = part,
						["Color"] = color --[[Color3]],
						["UnionColoring"] = false
					}
				}
			}
			_(args)
		end
		function SpawnDecal(part,side)
			local args = {
				[1] = "CreateTextures",
				[2] = {
					[1] = {
						["Part"] = part,
						["Face"] = side,
						["TextureType"] = "Decal"
					}
				}
			}
	
			_(args)
		end
		function AddDecal(part,asset,side)
			local args = {
				[1] = "SyncTexture",
				[2] = {
					[1] = {
						["Part"] = part,
						["Face"] = side,
						["TextureType"] = "Decal",
						["Texture"] = "rbxassetid://".. asset
					}
				}
			}
			_(args)
		end
	
		function spam(id)
			for i,v in game.workspace:GetDescendants() do
				if v:IsA("BasePart") then
					spawn(function()
						SetLocked(v,false)
						SpawnDecal(v,Enum.NormalId.Front)
						AddDecal(v,id,Enum.NormalId.Front)
	
						SpawnDecal(v,Enum.NormalId.Back)
						AddDecal(v,id,Enum.NormalId.Back)
	
						SpawnDecal(v,Enum.NormalId.Right)
						AddDecal(v,id,Enum.NormalId.Right)
	
						SpawnDecal(v,Enum.NormalId.Left)
						AddDecal(v,id,Enum.NormalId.Left)
	
						SpawnDecal(v,Enum.NormalId.Bottom)
						AddDecal(v,id,Enum.NormalId.Bottom)
	
						SpawnDecal(v,Enum.NormalId.Top)
						AddDecal(v,id,Enum.NormalId.Top)
					end)
				end
			end 
		end
		spam(99698372156633)
end)

AddBtn(AdminGrid, "Decal Spam 2", function()
local player = game.Players.LocalPlayer
		local char = player.Character
		local tool
		for i,v in player:GetDescendants() do
			if v.Name == "SyncAPI" then
				tool = v.Parent
			end
		end
		for i,v in game.ReplicatedStorage:GetDescendants() do
			if v.Name == "SyncAPI" then
				tool = v.Parent
			end
		end
		--craaa
		remote = tool.SyncAPI.ServerEndpoint
		function _(args)
			remote:InvokeServer(unpack(args))
		end
		function SetCollision(part,boolean)
			local args = {
				[1] = "SyncCollision",
				[2] = {
					[1] = {
						["Part"] = part,
						["CanCollide"] = boolean
					}
				}
			}
			_(args)
		end
		function SetAnchor(boolean,part)
			local args = {
				[1] = "SyncAnchor",
				[2] = {
					[1] = {
						["Part"] = part,
						["Anchored"] = boolean
					}
				}
			}
			_(args)
		end
		function CreatePart(cf,parent)
			local args = {
				[1] = "CreatePart",
				[2] = "Normal",
				[3] = cf,
				[4] = parent
			}
			_(args)
		end
		function DestroyPart(part)
			local args = {
				[1] = "Remove",
				[2] = {
					[1] = part
				}
			}
			_(args)
		end
		function MovePart(part,cf)
			local args = {
				[1] = "SyncMove",
				[2] = {
					[1] = {
						["Part"] = part,
						["CFrame"] = cf
					}
				}
			}
			_(args)
		end
		function Resize(part,size,cf)
			local args = {
				[1] = "SyncResize",
				[2] = {
					[1] = {
						["Part"] = part,
						["CFrame"] = cf,
						["Size"] = size
					}
				}
			}
			_(args)
		end
		function AddMesh(part)
			local args = {
				[1] = "CreateMeshes",
				[2] = {
					[1] = {
						["Part"] = part
					}
				}
			}
			_(args)
		end
	
		function SetMesh(part,meshid)
			local args = {
				[1] = "SyncMesh",
				[2] = {
					[1] = {
						["Part"] = part,
						["MeshId"] = "rbxassetid://"..meshid
					}
				}
			}
			_(args)
		end
		function SetTexture(part, texid)
			local args = {
				[1] = "SyncMesh",
				[2] = {
					[1] = {
						["Part"] = part,
						["TextureId"] = "rbxassetid://"..texid
					}
				}
			}
			_(args)
		end
		function SetName(part, stringg)
			local args = {
				[1] = "SetName",
				[2] = {
					[1] = part
				},
				[3] = stringg
			}
	
			_(args)
		end
		function MeshResize(part,size)
			local args = {
				[1] = "SyncMesh",
				[2] = {
					[1] = {
						["Part"] = part,
						["Scale"] = size
					}
				}
			}
			_(args)
		end
		function Weld(part1, part2,lead)
			local args = {
				[1] = "CreateWelds",
				[2] = {
					[1] = part1,
					[2] = part2
				},
				[3] = lead
			}
			_(args)
	
		end
		function SetLocked(part,boolean)
			local args = {
				[1] = "SetLocked",
				[2] = {
					[1] = part
				},
				[3] = boolean
			}
			_(args)
		end
		function SetTrans(part,int)
			local args = {
				[1] = "SyncMaterial",
				[2] = {
					[1] = {
						["Part"] = part,
						["Transparency"] = int
					}
				}
			}
			_(args)
		end
		function CreateSpotlight(part)
			local args = {
				[1] = "CreateLights",
				[2] = {
					[1] = {
						["Part"] = part,
						["LightType"] = "SpotLight"
					}
				}
			}
			_(args)
		end
		function SyncLighting(part,brightness)
			local args = {
				[1] = "SyncLighting",
				[2] = {
					[1] = {
						["Part"] = part,
						["LightType"] = "SpotLight",
						["Brightness"] = brightness
					}
				}
			}
			_(args)
		end
		function Color(part,color)
			local args = {
				[1] = "SyncColor",
				[2] = {
					[1] = {
						["Part"] = part,
						["Color"] = color --[[Color3]],
						["UnionColoring"] = false
					}
				}
			}
			_(args)
		end
		function SpawnDecal(part,side)
			local args = {
				[1] = "CreateTextures",
				[2] = {
					[1] = {
						["Part"] = part,
						["Face"] = side,
						["TextureType"] = "Decal"
					}
				}
			}
	
			_(args)
		end
		function AddDecal(part,asset,side)
			local args = {
				[1] = "SyncTexture",
				[2] = {
					[1] = {
						["Part"] = part,
						["Face"] = side,
						["TextureType"] = "Decal",
						["Texture"] = "rbxassetid://".. asset
					}
				}
			}
			_(args)
		end
	
		function spam(id)
			for i,v in game.workspace:GetDescendants() do
				if v:IsA("BasePart") then
					spawn(function()
						SetLocked(v,false)
						SpawnDecal(v,Enum.NormalId.Front)
						AddDecal(v,id,Enum.NormalId.Front)
	
						SpawnDecal(v,Enum.NormalId.Back)
						AddDecal(v,id,Enum.NormalId.Back)
	
						SpawnDecal(v,Enum.NormalId.Right)
						AddDecal(v,id,Enum.NormalId.Right)
	
						SpawnDecal(v,Enum.NormalId.Left)
						AddDecal(v,id,Enum.NormalId.Left)
	
						SpawnDecal(v,Enum.NormalId.Bottom)
						AddDecal(v,id,Enum.NormalId.Bottom)
	
						SpawnDecal(v,Enum.NormalId.Top)
						AddDecal(v,id,Enum.NormalId.Top)
					end)
				end
			end 
		end
		spam(94781978913748)
end)

AddBtn(AdminGrid, "Skybox", function()
local player = game.Players.LocalPlayer
local char = player.Character
local tool

for i,v in player:GetDescendants() do
	if v.Name == "SyncAPI" then
		tool = v.Parent
	end
end

for i,v in game.ReplicatedStorage:GetDescendants() do
	if v.Name == "SyncAPI" then
		tool = v.Parent
	end
end

remote = tool.SyncAPI.ServerEndpoint
function _(args)
	remote:InvokeServer(unpack(args))
end

function SetCollision(part,boolean)
	local args = {
		[1] = "SyncCollision",
		[2] = {
			[1] = {
				["Part"] = part,
				["CanCollide"] = boolean
			}
		}
	}
	_(args)
end

function SetAnchor(boolean,part)
	local args = {
		[1] = "SyncAnchor",
		[2] = {
			[1] = {
				["Part"] = part,
				["Anchored"] = boolean
			}
		}
	}
	_(args)
end

function CreatePart(cf,parent)
	local args = {
		[1] = "CreatePart",
		[2] = "Normal",
		[3] = cf,
		[4] = parent
	}
	_(args)
end

function DestroyPart(part)
	local args = {
		[1] = "Remove",
		[2] = {
			[1] = part
		}
	}
	_(args)
end

function MovePart(part,cf)
	local args = {
		[1] = "SyncMove",
		[2] = {
			[1] = {
				["Part"] = part,
				["CFrame"] = cf
			}
		}
	}
	_(args)
end

function Resize(part,size,cf)
	local args = {
		[1] = "SyncResize",
		[2] = {
			[1] = {
				["Part"] = part,
				["CFrame"] = cf,
				["Size"] = size
			}
		}
	}
	_(args)
end

function AddMesh(part)
	local args = {
		[1] = "CreateMeshes",
		[2] = {
			[1] = {
				["Part"] = part
			}
		}
	}
	_(args)
end

function SetMesh(part,meshid)
	local args = {
		[1] = "SyncMesh",
		[2] = {
			[1] = {
				["Part"] = part,
				["MeshId"] = "rbxassetid://"..meshid
			}
		}
	}
	_(args)
end

function SetTexture(part, texid)
	local args = {
		[1] = "SyncMesh",
		[2] = {
			[1] = {
				["Part"] = part,
				["TextureId"] = "rbxassetid://"..texid
			}
		}
	}
	_(args)
end

function SetName(part, stringg)
	local args = {
		[1] = "SetName",
		[2] = {
			[1] = part
		},
		[3] = stringg
	}
	_(args)
end

function MeshResize(part,size)
	local args = {
		[1] = "SyncMesh",
		[2] = {
			[1] = {
				["Part"] = part,
				["Scale"] = size
			}
		}
	}
	_(args)
end

function Weld(part1, part2,lead)
	local args = {
		[1] = "CreateWelds",
		[2] = {
			[1] = part1,
			[2] = part2
		},
		[3] = lead
	}
	_(args)
end

function SetLocked(part,boolean)
	local args = {
		[1] = "SetLocked",
		[2] = {
			[1] = part
		},
		[3] = boolean
	}
	_(args)
end

function SetTrans(part,int)
	local args = {
		[1] = "SyncMaterial",
		[2] = {
			[1] = {
				["Part"] = part,
				["Transparency"] = int
			}
		}
	}
	_(args)
end

function CreateSpotlight(part)
	local args = {
		[1] = "CreateLights",
		[2] = {
			[1] = {
				["Part"] = part,
				["LightType"] = "SpotLight"
			}
		}
	}
	_(args)
end

function SyncLighting(part,brightness)
	local args = {
		[1] = "SyncLighting",
		[2] = {
			[1] = {
				["Part"] = part,
				["LightType"] = "SpotLight",
				["Brightness"] = brightness
			}
		}
	}
	_(args)
end

function Color(part,color)
	local args = {
		[1] = "SyncColor",
		[2] = {
			[1] = {
				["Part"] = part,
				["Color"] = color,
				["UnionColoring"] = false
			}
		}
	}
	_(args)
end

function SpawnDecal(part,side)
	local args = {
		[1] = "CreateTextures",
		[2] = {
			[1] = {
				["Part"] = part,
				["Face"] = side,
				["TextureType"] = "Decal"
			}
		}
	}
	_(args)
end

function AddDecal(part,asset,side)
	local args = {
		[1] = "SyncTexture",
		[2] = {
			[1] = {
				["Part"] = part,
				["Face"] = side,
				["TextureType"] = "Decal",
				["Texture"] = "rbxassetid://".. asset
			}
		}
	}
	_(args)
end

function Sky(id)
	local root = char:WaitForChild("HumanoidRootPart")
	local pos = root.CFrame + Vector3.new(0, 6, 0)
	CreatePart(pos, workspace)
	task.wait(0.2)
	local skyPart
	for _, v in workspace:GetChildren() do
		if v:IsA("BasePart") and (v.Position - pos.Position).magnitude < 1 then
			skyPart = v
			break
		end
	end
	if skyPart then
		SetName(skyPart, "Sky")
		AddMesh(skyPart)
		SetMesh(skyPart, "111891702759441")
		SetTexture(skyPart, id)
		MeshResize(skyPart, Vector3.new(5000, 5000, 5000))
		SetLocked(skyPart, true)
		SetAnchor(true, skyPart)
		
		-- Hiệu ứng quay trippy với tốc độ chậm
		local startTime = tick()
		game:GetService("RunService").Heartbeat:Connect(function()
			local elapsedTime = tick() - startTime
			
			-- Tốc độ quay chậm: 1 vòng trong 20 giây = 18 độ/giây
			local baseSpeed = 18 -- độ/giây (giảm từ 72 xuống 18)
			
			-- Tạo các hiệu ứng trippy nhưng chậm hơn
			local trippyFactor = 1 -- Hệ số trippy nhỏ hơn
			
			-- Góc quay cơ bản cho mỗi trục (chậm hơn)
			local angleX = elapsedTime * (baseSpeed * 0.5) -- Trục X quay rất chậm
			local angleY = elapsedTime * baseSpeed        -- Trục Y quay chậm
			local angleZ = elapsedTime * (baseSpeed * 0.3) -- Trục Z quay rất chậm
			
			-- Thêm các hiệu ứng trippy dao động chậm
			local trippyX = math.sin(elapsedTime * 0.3) * 15 * trippyFactor  -- Tần số thấp
			local trippyY = math.cos(elapsedTime * 0.2) * 20 * trippyFactor  -- Tần số thấp
			local trippyZ = math.sin(elapsedTime * 0.25) * 10 * trippyFactor -- Tần số thấp
			
			-- Thêm hiệu ứng lắc lư (wobble) chậm
			local wobbleX = math.sin(elapsedTime * 0.5) * 8   -- Chậm
			local wobbleY = math.cos(elapsedTime * 0.4) * 10  -- Chậm
			local wobbleZ = math.sin(elapsedTime * 0.6) * 6   -- Chậm
			
			-- Kết hợp tất cả các hiệu ứng
			local finalAngleX = angleX + trippyX + wobbleX
			local finalAngleY = angleY + trippyY + wobbleY
			local finalAngleZ = angleZ + trippyZ + wobbleZ
			
			-- Tạo CFrame quay trippy chậm
			local rotationCFrame = CFrame.Angles(
				math.rad(finalAngleX),
				math.rad(finalAngleY),
				math.rad(finalAngleZ)
			)
			
			-- Thêm hiệu ứng scale nhịp nhàng rất chậm
			local pulse = math.sin(elapsedTime * 0.4) * 0.03 + 1 -- Dao động rất nhẹ và chậm
			local currentScale = Vector3.new(5000, 5000, 5000) * pulse
			
			-- Cập nhật kích thước skybox
			MeshResize(skyPart, currentScale)
			
			-- Di chuyển skybox với rotation trippy chậm
			MovePart(skyPart, pos * rotationCFrame)
		end)
	end
end

Sky("99698372156633")
end)

AddBtn(AdminGrid, "Skybox 2", function()
local player = game.Players.LocalPlayer
local char = player.Character
local tool

for i,v in player:GetDescendants() do
	if v.Name == "SyncAPI" then
		tool = v.Parent
	end
end

for i,v in game.ReplicatedStorage:GetDescendants() do
	if v.Name == "SyncAPI" then
		tool = v.Parent
	end
end

remote = tool.SyncAPI.ServerEndpoint
function _(args)
	remote:InvokeServer(unpack(args))
end

function SetCollision(part,boolean)
	local args = {
		[1] = "SyncCollision",
		[2] = {
			[1] = {
				["Part"] = part,
				["CanCollide"] = boolean
			}
		}
	}
	_(args)
end

function SetAnchor(boolean,part)
	local args = {
		[1] = "SyncAnchor",
		[2] = {
			[1] = {
				["Part"] = part,
				["Anchored"] = boolean
			}
		}
	}
	_(args)
end

function CreatePart(cf,parent)
	local args = {
		[1] = "CreatePart",
		[2] = "Normal",
		[3] = cf,
		[4] = parent
	}
	_(args)
end

function DestroyPart(part)
	local args = {
		[1] = "Remove",
		[2] = {
			[1] = part
		}
	}
	_(args)
end

function MovePart(part,cf)
	local args = {
		[1] = "SyncMove",
		[2] = {
			[1] = {
				["Part"] = part,
				["CFrame"] = cf
			}
		}
	}
	_(args)
end

function Resize(part,size,cf)
	local args = {
		[1] = "SyncResize",
		[2] = {
			[1] = {
				["Part"] = part,
				["CFrame"] = cf,
				["Size"] = size
			}
		}
	}
	_(args)
end

function AddMesh(part)
	local args = {
		[1] = "CreateMeshes",
		[2] = {
			[1] = {
				["Part"] = part
			}
		}
	}
	_(args)
end

function SetMesh(part,meshid)
	local args = {
		[1] = "SyncMesh",
		[2] = {
			[1] = {
				["Part"] = part,
				["MeshId"] = "rbxassetid://"..meshid
			}
		}
	}
	_(args)
end

function SetTexture(part, texid)
	local args = {
		[1] = "SyncMesh",
		[2] = {
			[1] = {
				["Part"] = part,
				["TextureId"] = "rbxassetid://"..texid
			}
		}
	}
	_(args)
end

function SetName(part, stringg)
	local args = {
		[1] = "SetName",
		[2] = {
			[1] = part
		},
		[3] = stringg
	}
	_(args)
end

function MeshResize(part,size)
	local args = {
		[1] = "SyncMesh",
		[2] = {
			[1] = {
				["Part"] = part,
				["Scale"] = size
			}
		}
	}
	_(args)
end

function Weld(part1, part2,lead)
	local args = {
		[1] = "CreateWelds",
		[2] = {
			[1] = part1,
			[2] = part2
		},
		[3] = lead
	}
	_(args)
end

function SetLocked(part,boolean)
	local args = {
		[1] = "SetLocked",
		[2] = {
			[1] = part
		},
		[3] = boolean
	}
	_(args)
end

function SetTrans(part,int)
	local args = {
		[1] = "SyncMaterial",
		[2] = {
			[1] = {
				["Part"] = part,
				["Transparency"] = int
			}
		}
	}
	_(args)
end

function CreateSpotlight(part)
	local args = {
		[1] = "CreateLights",
		[2] = {
			[1] = {
				["Part"] = part,
				["LightType"] = "SpotLight"
			}
		}
	}
	_(args)
end

function SyncLighting(part,brightness)
	local args = {
		[1] = "SyncLighting",
		[2] = {
			[1] = {
				["Part"] = part,
				["LightType"] = "SpotLight",
				["Brightness"] = brightness
			}
		}
	}
	_(args)
end

function Color(part,color)
	local args = {
		[1] = "SyncColor",
		[2] = {
			[1] = {
				["Part"] = part,
				["Color"] = color,
				["UnionColoring"] = false
			}
		}
	}
	_(args)
end

function SpawnDecal(part,side)
	local args = {
		[1] = "CreateTextures",
		[2] = {
			[1] = {
				["Part"] = part,
				["Face"] = side,
				["TextureType"] = "Decal"
			}
		}
	}
	_(args)
end

function AddDecal(part,asset,side)
	local args = {
		[1] = "SyncTexture",
		[2] = {
			[1] = {
				["Part"] = part,
				["Face"] = side,
				["TextureType"] = "Decal",
				["Texture"] = "rbxassetid://".. asset
			}
		}
	}
	_(args)
end

function Sky(id)
	local root = char:WaitForChild("HumanoidRootPart")
	local pos = root.CFrame + Vector3.new(0, 6, 0)
	CreatePart(pos, workspace)
	task.wait(0.2)
	local skyPart
	for _, v in workspace:GetChildren() do
		if v:IsA("BasePart") and (v.Position - pos.Position).magnitude < 1 then
			skyPart = v
			break
		end
	end
	if skyPart then
		SetName(skyPart, "Sky")
		AddMesh(skyPart)
		SetMesh(skyPart, "111891702759441")
		SetTexture(skyPart, id)
		MeshResize(skyPart, Vector3.new(5000, 5000, 5000))
		SetLocked(skyPart, true)
		SetAnchor(true, skyPart)
		
		-- Hiệu ứng quay trippy với tốc độ chậm
		local startTime = tick()
		game:GetService("RunService").Heartbeat:Connect(function()
			local elapsedTime = tick() - startTime
			
			-- Tốc độ quay chậm: 1 vòng trong 20 giây = 18 độ/giây
			local baseSpeed = 18 -- độ/giây (giảm từ 72 xuống 18)
			
			-- Tạo các hiệu ứng trippy nhưng chậm hơn
			local trippyFactor = 1 -- Hệ số trippy nhỏ hơn
			
			-- Góc quay cơ bản cho mỗi trục (chậm hơn)
			local angleX = elapsedTime * (baseSpeed * 0.5) -- Trục X quay rất chậm
			local angleY = elapsedTime * baseSpeed        -- Trục Y quay chậm
			local angleZ = elapsedTime * (baseSpeed * 0.3) -- Trục Z quay rất chậm
			
			-- Thêm các hiệu ứng trippy dao động chậm
			local trippyX = math.sin(elapsedTime * 0.3) * 15 * trippyFactor  -- Tần số thấp
			local trippyY = math.cos(elapsedTime * 0.2) * 20 * trippyFactor  -- Tần số thấp
			local trippyZ = math.sin(elapsedTime * 0.25) * 10 * trippyFactor -- Tần số thấp
			
			-- Thêm hiệu ứng lắc lư (wobble) chậm
			local wobbleX = math.sin(elapsedTime * 0.5) * 8   -- Chậm
			local wobbleY = math.cos(elapsedTime * 0.4) * 10  -- Chậm
			local wobbleZ = math.sin(elapsedTime * 0.6) * 6   -- Chậm
			
			-- Kết hợp tất cả các hiệu ứng
			local finalAngleX = angleX + trippyX + wobbleX
			local finalAngleY = angleY + trippyY + wobbleY
			local finalAngleZ = angleZ + trippyZ + wobbleZ
			
			-- Tạo CFrame quay trippy chậm
			local rotationCFrame = CFrame.Angles(
				math.rad(finalAngleX),
				math.rad(finalAngleY),
				math.rad(finalAngleZ)
			)
			
			-- Thêm hiệu ứng scale nhịp nhàng rất chậm
			local pulse = math.sin(elapsedTime * 0.4) * 0.03 + 1 -- Dao động rất nhẹ và chậm
			local currentScale = Vector3.new(5000, 5000, 5000) * pulse
			
			-- Cập nhật kích thước skybox
			MeshResize(skyPart, currentScale)
			
			-- Di chuyển skybox với rotation trippy chậm
			MovePart(skyPart, pos * rotationCFrame)
		end)
	end
end

Sky("94781978913748")
end)

AddBtn(AdminGrid, "k00pkidd decal", function()
local player = game.Players.LocalPlayer
		local char = player.Character
		local tool
		for i,v in player:GetDescendants() do
			if v.Name == "SyncAPI" then
				tool = v.Parent
			end
		end
		for i,v in game.ReplicatedStorage:GetDescendants() do
			if v.Name == "SyncAPI" then
				tool = v.Parent
			end
		end
		--craaa
		remote = tool.SyncAPI.ServerEndpoint
		function _(args)
			remote:InvokeServer(unpack(args))
		end
		function SetCollision(part,boolean)
			local args = {
				[1] = "SyncCollision",
				[2] = {
					[1] = {
						["Part"] = part,
						["CanCollide"] = boolean
					}
				}
			}
			_(args)
		end
		function SetAnchor(boolean,part)
			local args = {
				[1] = "SyncAnchor",
				[2] = {
					[1] = {
						["Part"] = part,
						["Anchored"] = boolean
					}
				}
			}
			_(args)
		end
		function CreatePart(cf,parent)
			local args = {
				[1] = "CreatePart",
				[2] = "Normal",
				[3] = cf,
				[4] = parent
			}
			_(args)
		end
		function DestroyPart(part)
			local args = {
				[1] = "Remove",
				[2] = {
					[1] = part
				}
			}
			_(args)
		end
		function MovePart(part,cf)
			local args = {
				[1] = "SyncMove",
				[2] = {
					[1] = {
						["Part"] = part,
						["CFrame"] = cf
					}
				}
			}
			_(args)
		end
		function Resize(part,size,cf)
			local args = {
				[1] = "SyncResize",
				[2] = {
					[1] = {
						["Part"] = part,
						["CFrame"] = cf,
						["Size"] = size
					}
				}
			}
			_(args)
		end
		function AddMesh(part)
			local args = {
				[1] = "CreateMeshes",
				[2] = {
					[1] = {
						["Part"] = part
					}
				}
			}
			_(args)
		end
	
		function SetMesh(part,meshid)
			local args = {
				[1] = "SyncMesh",
				[2] = {
					[1] = {
						["Part"] = part,
						["MeshId"] = "rbxassetid://"..meshid
					}
				}
			}
			_(args)
		end
		function SetTexture(part, texid)
			local args = {
				[1] = "SyncMesh",
				[2] = {
					[1] = {
						["Part"] = part,
						["TextureId"] = "rbxassetid://"..texid
					}
				}
			}
			_(args)
		end
		function SetName(part, stringg)
			local args = {
				[1] = "SetName",
				[2] = {
					[1] = part
				},
				[3] = stringg
			}
	
			_(args)
		end
		function MeshResize(part,size)
			local args = {
				[1] = "SyncMesh",
				[2] = {
					[1] = {
						["Part"] = part,
						["Scale"] = size
					}
				}
			}
			_(args)
		end
		function Weld(part1, part2,lead)
			local args = {
				[1] = "CreateWelds",
				[2] = {
					[1] = part1,
					[2] = part2
				},
				[3] = lead
			}
			_(args)
	
		end
		function SetLocked(part,boolean)
			local args = {
				[1] = "SetLocked",
				[2] = {
					[1] = part
				},
				[3] = boolean
			}
			_(args)
		end
		function SetTrans(part,int)
			local args = {
				[1] = "SyncMaterial",
				[2] = {
					[1] = {
						["Part"] = part,
						["Transparency"] = int
					}
				}
			}
			_(args)
		end
		function CreateSpotlight(part)
			local args = {
				[1] = "CreateLights",
				[2] = {
					[1] = {
						["Part"] = part,
						["LightType"] = "SpotLight"
					}
				}
			}
			_(args)
		end
		function SyncLighting(part,brightness)
			local args = {
				[1] = "SyncLighting",
				[2] = {
					[1] = {
						["Part"] = part,
						["LightType"] = "SpotLight",
						["Brightness"] = brightness
					}
				}
			}
			_(args)
		end
		function Color(part,color)
			local args = {
				[1] = "SyncColor",
				[2] = {
					[1] = {
						["Part"] = part,
						["Color"] = color --[[Color3]],
						["UnionColoring"] = false
					}
				}
			}
			_(args)
		end
		function SpawnDecal(part,side)
			local args = {
				[1] = "CreateTextures",
				[2] = {
					[1] = {
						["Part"] = part,
						["Face"] = side,
						["TextureType"] = "Decal"
					}
				}
			}
	
			_(args)
		end
		function AddDecal(part,asset,side)
			local args = {
				[1] = "SyncTexture",
				[2] = {
					[1] = {
						["Part"] = part,
						["Face"] = side,
						["TextureType"] = "Decal",
						["Texture"] = "rbxassetid://".. asset
					}
				}
			}
			_(args)
		end
	
		function spam(id)
			for i,v in game.workspace:GetDescendants() do
				if v:IsA("BasePart") then
					spawn(function()
						SetLocked(v,false)
						SpawnDecal(v,Enum.NormalId.Front)
						AddDecal(v,id,Enum.NormalId.Front)
	
						SpawnDecal(v,Enum.NormalId.Back)
						AddDecal(v,id,Enum.NormalId.Back)
	
						SpawnDecal(v,Enum.NormalId.Right)
						AddDecal(v,id,Enum.NormalId.Right)
	
						SpawnDecal(v,Enum.NormalId.Left)
						AddDecal(v,id,Enum.NormalId.Left)
	
						SpawnDecal(v,Enum.NormalId.Bottom)
						AddDecal(v,id,Enum.NormalId.Bottom)
	
						SpawnDecal(v,Enum.NormalId.Top)
						AddDecal(v,id,Enum.NormalId.Top)
					end)
				end
			end 
		end
		spam(9422866248)
end)

AddBtn(AdminGrid, "Realm", function()
    local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
	RequestCommand:InvokeServer(";btools me")
    RequestCommand:InvokeServer(";fogcolor black")
	wait(0.4)
	RequestCommand:InvokeServer(";punish all")
	wait(0.1)
	local player = game.Players.LocalPlayer
	local char = player.Character
	local backpack = player.Backpack

	local function getf3x()
		for _, v in ipairs(backpack:GetChildren()) do
			if v:FindFirstChild("SyncAPI") then
				return v
			end
		end
		for _, v in ipairs(char:GetChildren()) do
			if v:FindFirstChild("SyncAPI") then
				return v
			end
		end

		return nil
	end
	local f3x = getf3x()
	if not f3x then
		warn("you dont have f3x skid")
	end
	local syncapi = f3x.SyncAPI
	local serverendpoint = syncapi.ServerEndpoint

	local function delete(part)
		local args = {
			[1] = "Remove",
			[2] = {
				[1] = part
			}
		}
		serverendpoint:InvokeServer(unpack(args))
	end

	local function deleteall()
		for _, v in ipairs(workspace:GetDescendants()) do
			if v:IsA("BasePart") or v:IsA("UnionOperation") then
				spawn(function()
					delete(v)
				end)
			end
		end
	end

	deleteall()

	local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent
	RequestCommand:InvokeServer(";fogcolor black ;time")
	local player = game.Players.LocalPlayer
	local char = player.Character
	local backpack = player.Backpack

	local function getf3x()
		for _, v in ipairs(backpack:GetChildren()) do
			if v:FindFirstChild("SyncAPI") then
				return v
			end
		end
		for _, v in ipairs(char:GetChildren()) do
			if v:FindFirstChild("SyncAPI") then
				return v
			end
		end

		return nil
	end
	local f3x = getf3x()
	if not f3x then
		warn("you dont have f3x skid")
	end
	local syncapi = f3x.SyncAPI
	local serverendpoint = syncapi.ServerEndpoint

	local function resize(part,size,cf)
		local args = {
			[1] = "SyncResize",
			[2] = {
				[1] = {
					["Part"] = part,
					["CFrame"] = cf,
					["Size"] = size
				}
			}
		}
		serverendpoint:InvokeServer(unpack(args))
	end

	local function syncmaterial(part,mate,trans)
		local args = {
			[1] = "SyncMaterial",
			[2] = {
				[1] = {
					["Part"] = part,
					["Material"] = mate
				}
			}
		}
		serverendpoint:InvokeServer(unpack(args))
	end
	local function transparency(part,trans)
		local args = {
			[1] = "SyncMaterial",
			[2] = {
				[1] = {
					["Part"] = part,
					["Transparency"] = trans
				}
			}
		}
		serverendpoint:InvokeServer(unpack(args))
	end

	local function color(part, color)
		local args = {
			[1] = "SyncColor",
			[2] = {
				[1] = {
					["Part"] = part,
					["Color"] = color --[[Color3]],
					["UnionColoring"] = false
				}
			}
		}
		serverendpoint:InvokeServer(unpack(args))
	end

	local function syncmeshid(part, id)
		local args = {
			[1] = "SyncMesh",
			[2] = {
				[1] = {
					["Part"] = part,
					["MeshId"] = "rbxassetid://"..id
				}
			}
		}
		serverendpoint:InvokeServer(unpack(args))
	end

	local function makemesh(part)
		local args = {
			[1] = "CreateMeshes",
			[2] = {
				[1] = {
					["Part"] = part
				}
			}
		}
		serverendpoint:InvokeServer(unpack(args))
	end

	local function syncmeshsize(part, vectora)
		local args = {
			[1] = "SyncMesh",
			[2] = {
				[1] = {
					["Part"] = part,
					["Scale"] = vectora
				}
			}
		}
		serverendpoint:InvokeServer(unpack(args))
	end

	local function syncmeshtexture(part, id)
		local args = {
			[1] = "SyncMesh",
			[2] = {
				[1] = {
					["Part"] = part,
					["TextureId"] =	"rbxassetid://"..id
				}
			}
		}
		serverendpoint:InvokeServer(unpack(args))
	end

	local function name(part, stringa)
		local args = {
			[1] = "SetName",
			[2] = {
				[1] = part
			},
			[3] = stringa
		}
		serverendpoint:InvokeServer(unpack(args))
	end

	local function lock(part, boolean)
		local args = {
			[1] = "SetLocked",
			[2] = {
				[1] = part
			},
			[3] = boolean
		}
		serverendpoint:InvokeServer(unpack(args))
	end

	local function setcollision(part, booleana)
		local args = {
			[1] = "SyncCollision",
			[2] = {
				[1] = {
					["Part"] = part,
					["CanCollide"] = booleana
				}
			}
		}
		serverendpoint:InvokeServer(unpack(args))
	end

	local function setanchor(part, boolean)
		local args = {
			[1] = "SyncAnchor",
			[2] = {
				[1] = {
					["Part"] = part,
					["Anchored"] = boolean
				}
			}
		}
		serverendpoint:InvokeServer(unpack(args))
	end

	local function createdecal(part, side)
		local args = {
			[1] = "CreateTextures",
			[2] = {
				[1] = {
					["Part"] = part,
					["Face"] = side,
					["TextureType"] = "Decal"
				}
			}
		}
		serverendpoint:InvokeServer(unpack(args))
	end
	local function setdecal(part, asset, side)
		local args = {
			[1] = "SyncTexture",
			[2] = {
				[1] = {
					["Part"] = part,
					["Face"] = side,
					["TextureType"] = "Decal",
					["Texture"] = "rbxassetid://".. asset
				}
			}
		}
		serverendpoint:InvokeServer(unpack(args))
	end

	local function makerealmbase()
		local position = CFrame.new(0, 5, 0)
		local base = serverendpoint:InvokeServer("CreatePart", "Normal", position, workspace)
		resize(base, Vector3.new(512, 16, 512), position)
		syncmaterial(base, Enum.Material.Concrete)
		color(base, Color3.new(0.513725, 0.513725, 0.513725))
		name(base, "loltroll")
		lock(base, true)

		local spawnpos = CFrame.new(34.5, 8.1, -26)
		local spawna = serverendpoint:InvokeServer("CreatePart", "Spawn", spawnpos, workspace)
		resize(spawna, Vector3.new(20, 10, 20), spawnpos)
		name(spawna, "SpawnLocation")
		lock(spawna, true)

		createdecal(spawna, Enum.NormalId.Top)
		setdecal(spawna, "89145710208026", Enum.NormalId.Top) -- ganti decalnya pake decal lu
		transparency(spawna, 1)

		local pos = CFrame.new(74.143, 24, -25.232)

		local rules = serverendpoint:InvokeServer("CreatePart", "Normal", pos, workspace)

		transparency(rules, 0)
		setcollision(rules, false)
		createdecal(rules, Enum.NormalId.Left)
		setdecal(rules, "84413878812178", Enum.NormalId.Left)
		color(rules, Color3.new(1, 1, 1))
		resize(rules, Vector3.new(4, 23, 37), pos)


		local pos = CFrame.new(1.143, 24, -25.232)

		local bad = serverendpoint:InvokeServer("CreatePart", "Normal", pos, workspace)

		transparency(bad, 1)
		setcollision(bad, false)
		createdecal(bad, Enum.NormalId.Right)
		setdecal(bad, "99698372156633", Enum.NormalId.Right)
		resize(bad, Vector3.new(4, 23, 37), pos)

	end

	local function sky()
		local position = CFrame.new(0, 5, 0)
		local sky = serverendpoint:InvokeServer("CreatePart", "Normal", position, workspace)

		makemesh(sky)
		syncmeshid(sky, "111891702759441")
		syncmeshtexture(sky, "99698372156633")
		syncmeshsize(sky, Vector3.new(99999, 99999, 99999))
		lock(sky, true)
		name(sky, "k00pkidd770 hacked")
		setcollision(sky, false)
	end





	local function unanchorall()
		for _, v in ipairs(workspace:GetDescendants()) do
			if v:IsA("BasePart") or v:IsA("UnionOperation") then
				spawn(function()
					setanchor(v, false)
				end)
			end
		end
	end

	local function realm()
		sky()
		makerealmbase()
	end

	realm()

	RequestCommand:InvokeServer(";res all")
	wait(0.3)
	RequestCommand:InvokeServer(";r6 all")
	RequestCommand:InvokeServer(";time 17")
	wait(0.7)
	RequestCommand:InvokeServer(";music 1847661821 ;volume inf  ;savemap")
end)

AddBtn(AdminGrid, "k00pkidd skybox", function()
local player = game.Players.LocalPlayer
local char = player.Character
local tool

for i,v in player:GetDescendants() do
	if v.Name == "SyncAPI" then
		tool = v.Parent
	end
end

for i,v in game.ReplicatedStorage:GetDescendants() do
	if v.Name == "SyncAPI" then
		tool = v.Parent
	end
end

remote = tool.SyncAPI.ServerEndpoint
function _(args)
	remote:InvokeServer(unpack(args))
end

function SetCollision(part,boolean)
	local args = {
		[1] = "SyncCollision",
		[2] = {
			[1] = {
				["Part"] = part,
				["CanCollide"] = boolean
			}
		}
	}
	_(args)
end

function SetAnchor(boolean,part)
	local args = {
		[1] = "SyncAnchor",
		[2] = {
			[1] = {
				["Part"] = part,
				["Anchored"] = boolean
			}
		}
	}
	_(args)
end

function CreatePart(cf,parent)
	local args = {
		[1] = "CreatePart",
		[2] = "Normal",
		[3] = cf,
		[4] = parent
	}
	_(args)
end

function DestroyPart(part)
	local args = {
		[1] = "Remove",
		[2] = {
			[1] = part
		}
	}
	_(args)
end

function MovePart(part,cf)
	local args = {
		[1] = "SyncMove",
		[2] = {
			[1] = {
				["Part"] = part,
				["CFrame"] = cf
			}
		}
	}
	_(args)
end

function Resize(part,size,cf)
	local args = {
		[1] = "SyncResize",
		[2] = {
			[1] = {
				["Part"] = part,
				["CFrame"] = cf,
				["Size"] = size
			}
		}
	}
	_(args)
end

function AddMesh(part)
	local args = {
		[1] = "CreateMeshes",
		[2] = {
			[1] = {
				["Part"] = part
			}
		}
	}
	_(args)
end

function SetMesh(part,meshid)
	local args = {
		[1] = "SyncMesh",
		[2] = {
			[1] = {
				["Part"] = part,
				["MeshId"] = "rbxassetid://"..meshid
			}
		}
	}
	_(args)
end

function SetTexture(part, texid)
	local args = {
		[1] = "SyncMesh",
		[2] = {
			[1] = {
				["Part"] = part,
				["TextureId"] = "rbxassetid://"..texid
			}
		}
	}
	_(args)
end

function SetName(part, stringg)
	local args = {
		[1] = "SetName",
		[2] = {
			[1] = part
		},
		[3] = stringg
	}
	_(args)
end

function MeshResize(part,size)
	local args = {
		[1] = "SyncMesh",
		[2] = {
			[1] = {
				["Part"] = part,
				["Scale"] = size
			}
		}
	}
	_(args)
end

function Weld(part1, part2,lead)
	local args = {
		[1] = "CreateWelds",
		[2] = {
			[1] = part1,
			[2] = part2
		},
		[3] = lead
	}
	_(args)
end

function SetLocked(part,boolean)
	local args = {
		[1] = "SetLocked",
		[2] = {
			[1] = part
		},
		[3] = boolean
	}
	_(args)
end

function SetTrans(part,int)
	local args = {
		[1] = "SyncMaterial",
		[2] = {
			[1] = {
				["Part"] = part,
				["Transparency"] = int
			}
		}
	}
	_(args)
end

function CreateSpotlight(part)
	local args = {
		[1] = "CreateLights",
		[2] = {
			[1] = {
				["Part"] = part,
				["LightType"] = "SpotLight"
			}
		}
	}
	_(args)
end

function SyncLighting(part,brightness)
	local args = {
		[1] = "SyncLighting",
		[2] = {
			[1] = {
				["Part"] = part,
				["LightType"] = "SpotLight",
				["Brightness"] = brightness
			}
		}
	}
	_(args)
end

function Color(part,color)
	local args = {
		[1] = "SyncColor",
		[2] = {
			[1] = {
				["Part"] = part,
				["Color"] = color,
				["UnionColoring"] = false
			}
		}
	}
	_(args)
end

function SpawnDecal(part,side)
	local args = {
		[1] = "CreateTextures",
		[2] = {
			[1] = {
				["Part"] = part,
				["Face"] = side,
				["TextureType"] = "Decal"
			}
		}
	}
	_(args)
end

function AddDecal(part,asset,side)
	local args = {
		[1] = "SyncTexture",
		[2] = {
			[1] = {
				["Part"] = part,
				["Face"] = side,
				["TextureType"] = "Decal",
				["Texture"] = "rbxassetid://".. asset
			}
		}
	}
	_(args)
end

function Sky(id)
	local root = char:WaitForChild("HumanoidRootPart")
	local pos = root.CFrame + Vector3.new(0, 6, 0)
	CreatePart(pos, workspace)
	task.wait(0.2)
	local skyPart
	for _, v in workspace:GetChildren() do
		if v:IsA("BasePart") and (v.Position - pos.Position).magnitude < 1 then
			skyPart = v
			break
		end
	end
	if skyPart then
		SetName(skyPart, "Sky")
		AddMesh(skyPart)
		SetMesh(skyPart, "111891702759441")
		SetTexture(skyPart, id)
		MeshResize(skyPart, Vector3.new(5000, 5000, 5000))
		SetLocked(skyPart, true)
		SetAnchor(true, skyPart)
		
		-- Hiệu ứng quay trippy với tốc độ chậm
		local startTime = tick()
		game:GetService("RunService").Heartbeat:Connect(function()
			local elapsedTime = tick() - startTime
			
			-- Tốc độ quay chậm: 1 vòng trong 20 giây = 18 độ/giây
			local baseSpeed = 18 -- độ/giây (giảm từ 72 xuống 18)
			
			-- Tạo các hiệu ứng trippy nhưng chậm hơn
			local trippyFactor = 1 -- Hệ số trippy nhỏ hơn
			
			-- Góc quay cơ bản cho mỗi trục (chậm hơn)
			local angleX = elapsedTime * (baseSpeed * 0.5) -- Trục X quay rất chậm
			local angleY = elapsedTime * baseSpeed        -- Trục Y quay chậm
			local angleZ = elapsedTime * (baseSpeed * 0.3) -- Trục Z quay rất chậm
			
			-- Thêm các hiệu ứng trippy dao động chậm
			local trippyX = math.sin(elapsedTime * 0.3) * 15 * trippyFactor  -- Tần số thấp
			local trippyY = math.cos(elapsedTime * 0.2) * 20 * trippyFactor  -- Tần số thấp
			local trippyZ = math.sin(elapsedTime * 0.25) * 10 * trippyFactor -- Tần số thấp
			
			-- Thêm hiệu ứng lắc lư (wobble) chậm
			local wobbleX = math.sin(elapsedTime * 0.5) * 8   -- Chậm
			local wobbleY = math.cos(elapsedTime * 0.4) * 10  -- Chậm
			local wobbleZ = math.sin(elapsedTime * 0.6) * 6   -- Chậm
			
			-- Kết hợp tất cả các hiệu ứng
			local finalAngleX = angleX + trippyX + wobbleX
			local finalAngleY = angleY + trippyY + wobbleY
			local finalAngleZ = angleZ + trippyZ + wobbleZ
			
			-- Tạo CFrame quay trippy chậm
			local rotationCFrame = CFrame.Angles(
				math.rad(finalAngleX),
				math.rad(finalAngleY),
				math.rad(finalAngleZ)
			)
			
			-- Thêm hiệu ứng scale nhịp nhàng rất chậm
			local pulse = math.sin(elapsedTime * 0.4) * 0.03 + 1 -- Dao động rất nhẹ và chậm
			local currentScale = Vector3.new(5000, 5000, 5000) * pulse
			
			-- Cập nhật kích thước skybox
			MeshResize(skyPart, currentScale)
			
			-- Di chuyển skybox với rotation trippy chậm
			MovePart(skyPart, pos * rotationCFrame)
		end)
	end
end

Sky("9422866248")
end)

AddBtn(AdminGrid, "Btools", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";btools")
end)

AddBtn(AdminGrid, "Shutdown", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";shutdown")
end)

AddBtn(AdminGrid, "Re All", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";re all")
end)

AddBtn(AdminGrid, "Char All", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";char all k00pkidd770")
end)

AddBtn(AdminGrid, "Title All", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";title all join team k00pkid770 today!!!")
end)

AddBtn(AdminGrid, "Title Me", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";title me k00pkidd770")
end)

AddBtn(AdminGrid, "Message", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";sm join teamk00pkidd770 today!!!")
end)

AddBtn(AdminGrid, "Hint", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";sh join team k00pkidd770 today!!!") 
end)

AddBtn(AdminGrid, "Dummy", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";clone me")
end)

AddBtn(AdminGrid, "Fire All", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";fire all")
end)

AddBtn(AdminGrid, "Disco", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";disco")
end)

AddBtn(AdminGrid, "Save Map", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";savemap")
end)

AddBtn(AdminGrid, "Kill All", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";kill all")
end)

AddBtn(AdminGrid, "Theme", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";music 1847661821 ;volume inf")
end)

AddBtn(AdminGrid, "Sword", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";sword") 
end)

-- --- PHẦN 2: CHỮ MUSIC ---
local MusicLabel = Instance.new("TextLabel")
MusicLabel.Parent = ScrollingFrame; MusicLabel.LayoutOrder = 2
MusicLabel.BackgroundTransparency = 1; MusicLabel.Size = UDim2.new(1, 0, 0, 60)
MusicLabel.Font = Enum.Font.GothamBold; MusicLabel.Text = "MUSIC"; MusicLabel.TextColor3 = Color3.fromRGB(255, 255, 255); MusicLabel.TextSize = 35

-- --- PHẦN 3: NÚT NHẠC ---
local MusicGrid = CreateGridFrame("MusicGrid", 3)

AddBtn(MusicGrid, "Jumpstyle", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";music 1839246711 ;volume inf")
end)

AddBtn(MusicGrid, "Toxic", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";music 86412047196482 ;volume inf")
end)

AddBtn(MusicGrid, "Wtf Gooby", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";music 113548699544058 ;volume inf ;pitch 0.1") 
end)

AddBtn(MusicGrid, "C00lkidd", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";music 77484784570543 ;volume inf ;pitch 0.1")
end)

AddBtn(MusicGrid, "Gooby", function() 
local ReplicatedStorage = game:GetService("ReplicatedStorage")
	local RequestCommand = ReplicatedStorage:WaitForChild("HDAdminHDClient").Signals.RequestCommandSilent

	RequestCommand:InvokeServer(";music 1847661821 ;volume inf")
end)

-- --- PHẦN 4: ẢNH DECOR ---
local DecorationImage = Instance.new("ImageLabel")
DecorationImage.Parent = ScrollingFrame; DecorationImage.LayoutOrder = 4
DecorationImage.BackgroundTransparency = 1; DecorationImage.Size = UDim2.new(0, 400, 0, 250)
DecorationImage.Image = "rbxassetid://84413878812178"; DecorationImage.ScaleType = Enum.ScaleType.Fit
