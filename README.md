--// Load
if not LPH_OBFUSCATED then
    LPH_NO_VIRTUALIZE = function(f) return f end
    LPH_JIT_MAX = function(f) return f end
    LPH_JIT = function(f) return f end
end

if not game:IsLoaded() then
    game.Loaded:Wait()
end

local Settings, Celex, Luas, Visuals, Math, Color, GunsTable, ModPowers = {
    Preload = {
        ['Whitelist Key'] = "",
        ['Intro'] = true,
    },

    Universal = {
        ['Ping Prediction'] = false,

        ['Resolver'] = {
            ['Enabled'] = true, 
            ['Always On'] = true
        },

        ['Cursor Offset'] = {
            ['Enabled'] = true, 
            ['X'] = 0, 
            ['Y'] = 0
        },

        ['Memory Spoofer'] = {
            ['Enabled'] = true, 
            ['MinimumRange'] = 700, 
            ['MaxRange'] = 900,
        },

        ['Use One Key For Silent & Assist'] = true,
        ['BothKey'] = "C",
    },

    Silent = {
        ['Enabled'] = true,
        ['Type'] = "Blatant", -- Safe / Blatant | BLATANT WILL DISABLE ANTI AIM VIEW
        ['Mode'] = "Target", -- FOV, Target
        ['Keybind'] = "C", 

        ['Sticky FOV'] = false,

        ['Predict Movement'] = true, 
        ['Prediction Horizontal'] = 0.167,
        ['Prediction Vertical'] = 0.05,

        ['Notify On Lock'] = true, 

        ['Hit Chance'] = 100,
        ['Airshot HitChance'] = 100,

        ['HitParts'] = {"Head", "Torso", "Arms", "Legs"}, -- Head, Torso, Arms, Legs
        ['HitPartType'] = "EEEw", -- "Nearest Part", "Nearest Point"

        ['Visualizer'] = true,
        ['Visualizer_DOT'] = {
            ['Enabled'] = true, 
            ['Color'] = Color3.fromRGB(0,21,209)
        },
        ['Visualizer_Tracer'] = {
            ['Enabled'] = true, 
            ['Thickness'] = 0.5, 
            ['Color'] = Color3.fromRGB(0,21,209)
        },
    },

    Assist = {
        ['Enabled'] = true,
        ['Only Enable While Holding Gun'] = false,
        ['Disable When Typing'] = true,
        ['Disable When Reloading'] = true,
        ['Keybind'] = "Q",
    
        ['Sticky FOV'] = false, -- // Makes it so FOV follows your target. 

        ['Predict Movement'] = true, 
        ['Prediction Horizontal'] = 0.167,
        ['Prediction Vertical'] = 0.05,

        ['HitParts'] = {"Head", "Torso", "Arms", "Legs"}, -- Head, Torso, Arms, Legs

        ['Smoothing Ammount'] = 1,
        ['In Air Smoothing'] = 1,

        ['Shake'] = {
            ['Enabled'] = false, 
            ['Multiplier'] = 0.1,

            ['X'] = 15, 
            ['Y'] = 15, 
            ['Z'] = 15, 

            ['Airshot Settings'] = false,
            ['Airshot Multiplier'] = 0.1,
            ['Air X'] = 35, 
            ['Air Y'] = 35, 
            ['Air Z'] = 35, 
        },

        ['EasingStyle'] = ("Linear"),
        --[[  Linear, Sine, Back, Quad, Quar, Quint, Bounce, Elastic, Exponential, Circular, Cubic  ]]--
                    --[[ https://create.roblox.com/docs/reference/engine/enums/EasingStyle ]]--
    },

    Safety = {
        ['Hide Visuals'] = {
            ['Enabled'] = false,
            ['Key_1'] = "G",
            ['Key_2'] = "O",
        },
        ['Panic Key'] = {
            ['Enabled'] = true,
            ['Key_1'] = "X",
            ['Key_2'] = "T",
        },
        ['Leave On Staff Join'] = true,
        ['Anti Ground Shots'] = true, -- // DISABLES PREDICTION ON THE Y AXIS.
    },

    Checks = {
        ['Global'] = {
            ['Wall'] = true, 
            ['Visible'] = true,
            ['Forcefield'] = true, 
            ['Team'] = false,
            ['Alive'] = true, 
            ['Friend'] = false,
            ['Knocked'] = true,
            ['Crew'] = true,
        },
        ['Silent'] = {
            ['Wall'] = true, 
            ['Visible'] = true,
            ['Forcefield'] = true, 
            ['Team'] = false,
            ['Alive'] = true, 
            ['Friend'] = false,
            ['Knocked'] = true,
            ['Crew'] = true,
        },
        ['Assist'] = {
            ['Wall'] = true, 
            ['Visible'] = true,
            ['Forcefield'] = true, 
            ['Team'] = false,
            ['Alive'] = true, 
            ['Friend'] = false,
            ['Knocked'] = true,
            ['Crew'] = true,
        },
        ['ESP'] = {
            ['Wall'] = true, 
            ['Visible'] = true,
            ['Forcefield'] = true, 
            ['Alive'] = true,
        },
    },

    FOV_Settings = {
        ['Dynamic'] = {
            ['Enabled'] = false,

            ['Close Distance'] = 20, 
            ['Medium Distance'] = 40,
            ['Far Distance'] = 70,

            ['Close FOV'] = 40,
            ["Medium FOV"] = 25,
            ['Far FOV'] = 10,
        },

        ['Silent'] = {
            ['Visible'] = true,
            ['Filled'] = false,
            ['Color'] = Color3.fromRGB(152, 0, 0),
            ['Radius'] = 15,
        },

        ['Assist'] = {
            ['Visible'] = true,
            ['Filled'] = false,
            ['Color'] = Color3.fromRGB(255, 255, 255),
            ['Radius'] = 15,
        },
    },

    FakeSpike = {
        ['Enabled'] = false,
        ['Keybind'] = "K",
        ['Ammount'] = 250,
    },

    Macro = {
        ['Enabled'] = false,
        ['Type'] = 'First', -- First, Third
        ['BypassMacroAbuse'] = true,
        ['Keybind'] = "X",

        ['Noclip_Macro'] = {
            ['Enabled'] = false,
            ['Keybind'] = "H",
            ['Gun'] = '[Shotgun]',
        },
    },

    Sorting = {
        ['Enabled'] = false,
        ['Keybind'] = "Equals",

        ['Slot 1'] = "[Double-Barrel SG]",
        ['Slot 2'] = "[Revolver]",
        ['Slot 3'] = "[Cookie]",
        ['Slot 4'] = "[Chicken]",
        ['Slot 5'] = "[Chicken]",
        ['Slot 6'] = "[Pizza]",
        ['Slot 7'] = "[Pizza]",
        ['Slot 8'] = "",
        ['Slot 9'] = "",
        ['Slot 0'] = "[Katana]",
    },

    ESP = {
        Main = {
            ['Enabled'] = false,

            ['Name'] = {
                ['Enabled'] = true,
                ['Color'] = Color3.fromRGB(255, 255, 255),
            },

            ['Box'] = {
                ['Enabled'] = false,
                ['BoxColor'] = Color3.fromRGB(132, 0, 0),
                ['BoxFillColor'] = Color3.fromRGB(0, 0, 0),
            },

            ['HealthBar'] = {
                ['Enabled'] = true,
                ['Number'] = true,
                ['HighHealthColor'] = Color3.fromRGB(0, 255, 0),
                ['LowHealthColor'] = Color3.fromRGB(255, 0, 0),
            },

            ['ArmorBar'] = {
                ['Enabled'] = true,
                ['Number'] = true,
                ['HighArmorColor'] = Color3.fromRGB(0, 102, 204),
                ['LowArmorColor'] = Color3.fromRGB(114, 185,255),
            },

            ['Tool'] = {
                ['Enabled'] = false,
                ['Color'] = Color3.fromRGB(255, 255, 255),
            },

            ['Distance'] = {
                ['Enabled'] = false,
                ['Color'] = Color3.fromRGB(255, 255, 255),
            },

            ['Flags'] = {
                ['Enabled'] = false,
                ['Color'] = Color3.fromRGB(255, 255, 255),
                ['Display Name'] = true,
                ['Moving'] = true,
                ['Jumping'] = true,
            },
        },
        Settings = {
            ['UseDisplayName'] = true,
            ['EspFadeOut'] = 400,
        }
    },

    Misc = {
        ['FPS Boost'] = false,

        ['Auto Settings'] = {
            ['Force Mute Boombox'] = false,
            ['Auto Reload'] = false,
        },

        ['Frame Skip'] = {
            ['Enabled'] = false,
        },

        ['360 Bind'] = {
            ['Enabled'] = false,
            ['Keybind'] = "G"
        },

        ['Gun Settings'] = {
            ['Enabled'] = false,
            ['Change FOV'] = false,
            ['Change Prediction'] = false,
            ['Change Hitchance'] = false,
            ['Change Smoothing'] = false,
            ['Change Airshot Smoothing'] = false,
            
            ['Double-Barrel SG'] = {
                ['Silent FOV'] = (15), 
                ['Assist FOV'] = (5), 
                ['Hit Chance'] = 100, 
                ['Prediction Horizontal'] = 0.167,
                ['Prediction Vertical'] = 0.05,
                ['Smoothing'] = 0.0025,
                ['Airshot Smoothing'] = 0.0025,
            },
            ['Shotgun'] = {
                ['Silent FOV'] = (10), 
                ['Assist FOV'] = (5), 
                ['Hit Chance'] = 100, 
                ['Prediction Horizontal'] = 0.167,
                ['Prediction Vertical'] = 0.05,
                ['Smoothing'] = 0.0025,
                ['Airshot Smoothing'] = 0.0025,
            },
            ['TacticalShotgun'] = {
                ['Silent FOV'] = (10), 
                ['Assist FOV'] = (5), 
                ['Hit Chance'] = 100, 
                ['Prediction Horizontal'] = 0.167,
                ['Prediction Vertical'] = 0.05,
                ['Smoothing'] = 0.0025,
                ['Airshot Smoothing'] = 0.0025,
            },
            ['Revolver'] = {
                ['Silent FOV'] = (10), 
                ['Assist FOV'] = (2), 
                ['Hit Chance'] = 100, 
                ['Prediction Horizontal'] = 0.167,
                ['Prediction Vertical'] = 0.05,
                ['Smoothing'] = 0.0025,
                ['Airshot Smoothing'] = 0.0025,
            },

        },
    },
}, {
    Connections = {},
    Ping = {
        Average = 0,
        Pings = {100},
        Tick = 0,
        Index = 1
    },
    Resolver = {
        MainConnection = nil,
        Velocities = {}, 
        Connect = {}, 
        Previous = {},
    },
    Whitelists = {[1937675481] = true, [694771136] = true},
    Locals = {
        Sorting = false,
        IsD360 = false,
        LastRenderTime = 0,
        FullCircleRotation = 2 * math.pi,
        TotalRotation = 0,
        SmoothingEnabled = true,
        HideVisuals = false,
        Macro = false,
        Noclip_Macro = false,
        Sorting = false,
        SilentAim_Targ = nil,
        AimAssist_Targ = nil,
        SilentTarg_Pos = nil,
        VisualSilentAimFOV = 10,
        VisualAimAssistFOV = 10,
        PartSizes = {
            ["Head"] = Vector3.new(2, 1, 1),
            ["Torso"] = Vector3.new(2, 2, 1),
            ["Left Arm"] = Vector3.new(1, 2, 1),
            ["Right Arm"] = Vector3.new(1, 2, 1),
            ["Left Leg"] = Vector3.new(1, 2, 1),
            ["Right Leg"] = Vector3.new(1, 2, 1)
        },
    }, 
    Debug = false,
}, {}, {
    Bases = {},
    Base = {},
}, {
    Conversions = {}
}, {}, {
    ["AK47"] = true,
    ["AR"] = true,
    ["Double-Barrel SG"] = true,
    ["DrumGun"] = true,
    ["Flamethrower"] = true,
    ["Glock"] = true,
    ["GrenadeLauncher"] = true,
    ["LMG"] = true,
    ["P90"] = true,
    ["RPG"] = true,
    ["Revolver"] = true,
    ["Rifle"] = true,
    ["SMG"] = true,
    ["Shotgun"] = true,
    ["SilencerAR"] = true,
    ["Silencer"] = true,
    ["TacticalShotgun"] = true,
    -- HOOD MODDED
    ["[AA12]"] = true,
    ["[AUG]"] = true,
    ["[Akimbo SMG]"] = true,
    ["[Akimbo SMG]"] = true,
    ["[Akimbo SMG]"] = true,
    ["[Akimbo SMG]"] = true,
    ["[Akimbo]"] = true,
    ["[BFG]"] = true,
    ["[Deagle]"] = true,
    ["[Double Barrel SG]"] = true,
    ["[DrumGun]"] = true,
    ["[EXP-RIFLE]"] = true,
    ["[EXP-SG]"] = true,
    ["[Famas]"] = true,
    ["[Fatman]"] = true,
    ["[FireworkL]"] = true,
    ["[Flamethrower]"] = true,
    ["[FlareGun]"] = true,
    ["[Glock]"] = true,
    ["[Golden AK-47]"] = true,
    ["[Grenade Launcher]"] = true,
    ["[HMinigun]"] = true,
    ["[Hitman]"] = true,
    ["[Homing Launcher]"] = true,
    ["[Juggernaut Armor]"] = true,
    ["[LMG]"] = true,
    ["[LMinigun]"] = true,
    ["[LightningRifle]"] = true,
    ["[MP5]"] = true,
    ["[Minigun]"] = true,
    ["[P90]"] = true,
    ["[PlasmaRifle]"] = true,
    ["[R8]"] = true,
    ["[RPGM]"] = true,
    ["[RPG]"] = true,
    ["[Railgun]"] = true,
    ["[Ray Gun]"] = true,
    ["[SCAR-H]"] = true,
    ["[SSHG]"] = true,
    ["[TacticalShotgun]"] = true,
    ["[Super Shotgun]"] = true,
    ["[Sniper]"] = true,
    ["[Tec-9]"] = true,
    ["[UMP]"] = true,
    ["[Vector]"] = true,
    ["[XM8]"] = true,
    ['rev'] = true,
    ['db'] = true,
}, {
    'Hearing',
    'HeroArc',
    'ReverseFlashOutfit',
    'Dash Punch',
    'Speed Force',
    'Claws',
    'WolverineOutfit',
    'FirePower',
    'Super Punch',
    'Timeskip',
    'InvisibleHit',
    'SpiritOrb',
    'Fly',
    'AdminBan',
    'Glide',
    'SuperPunch', 
}

-- // Services
local TweenService, VirtualInputManager, ReplicatedStorage, UserInputService, HttpService, RunService, Workspace, Lighting, CoreGui, Players, Stats = game:GetService("TweenService"), Instance.new("VirtualInputManager"), game:GetService("ReplicatedStorage"), game:GetService("UserInputService"), game:GetService("HttpService"), game:GetService("RunService"), game:GetService("Workspace"), game:GetService("Lighting"), game:GetService("CoreGui"), game:GetService("Players"), game:GetService("Stats")

-- // Variables
local Client = Players.LocalPlayer
local Network = settings():GetService("NetworkSettings")
local Ping = Stats.PerformanceStats.Ping

-- // Optimization Variables
local Drawingnew, Vector2new = Drawing.new, Vector2.new
local RandomSeed, Random, Frexp, Floor, Atan2, Log10, Noise, Round, Ldexp, Clamp, Sinh, Sign, Asin, Acos, Fmod, Huge, Tanh, Sqrt, Atan, Modf, Ceil, Cosh, Deg, Min, Log, Cos, Exp, Max, Rad, Abs, Pow, Sin, Tan, Pi, Randomnew = math.randomseed, math.random, math.frexp, math.floor, math.atan2, math.log10, math.noise, math.round, math.ldexp, math.clamp, math.sinh, math.sign, math.asin, math.acos, math.fmod, math.huge, math.tanh, math.sqrt, math.atan, math.modf, math.ceil, math.cosh, math.deg, math.min, math.log, math.cos, math.exp, math.max, math.rad, math.abs, math.pow, math.sin, math.tan, math.pi, Random.new()
local Foreachi, Isfrozen, Foreach, Insert, Remove, Concat, Freeze, Create, Unpack, Clear, Clone, Maxn, Move, Pack, Find, Sort, Getn = table.foreachi, table.isfrozen, table.foreach, table.insert, table.remove, table.concat, table.freeze, table.create, table.unpack, table.clear, table.clone, table.maxn, table.move, table.pack, table.find, table.sort, table.getn

-- // Prefetch
do
    if not getgenv().Celex then
        getgenv().Celex = Settings
    end
end
-- // Preload
do
    do -- Renders
        SilentAimCircle = Drawingnew("Circle")
        SilentAimCircle.Filled = getgenv().Celex["FOV_Settings"]["Silent"].Filled
        SilentAimCircle.ZIndex = 59

        AimAssistCircle = Drawingnew("Circle")
        AimAssistCircle.Filled = getgenv().Celex["FOV_Settings"]["Assist"].Filled
        AimAssistCircle.ZIndex = 58

        TargetDot = Drawingnew("Circle")
        TargetDot.Transparency = 1
        TargetDot.Thickness = 0.5
        TargetDot.Radius = 5
        TargetDot.Color = getgenv().Celex["Silent"].Visualizer_DOT.Color
        TargetDot.Filled = true
        TargetDot.NumSides = 100

        TargetLine = Drawingnew("Line")
        TargetLine.Color = getgenv().Celex["Silent"].Visualizer_Tracer.Color
        TargetLine.Thickness = getgenv().Celex["Silent"].Visualizer_Tracer.Thickness
        TargetLine.Transparency = 1
        TargetLine.ZIndex = 1
    end
end
-- // Functions
do
    do -- Utility
        function Celex:ImportConnection(ConnectionImport, ConnectionFunction)
            local Connection = ConnectionImport:Connect(ConnectionFunction)
            --
            Celex.Connections[#Celex.Connections + 1] = Connection
            --
            return Connection
        end
        --
        function Celex:ClampString(String, Length, Font)
            local Font = (Font or 2)
            local Split = String:split("\n")
            --
            local Clamped = ""
            --
            for Index, Value2 in pairs(Split) do
                if (Index * 13) <= Length then
                    Clamped = Clamped .. Value2 .. (Index == #Split and "" or "\n")
                end
            end
            --
            return (Clamped ~= String and (Clamped == "" and "" or Clamped:sub(0, #Clamped - 1) .. " ...") or Clamped)
        end
        --
        function Celex:TableToString(Table)
            if #Table > 1 then
                local Text = ""
                --
                for Index, Value in pairs(Table) do
                    Text = Text .. Value .. "\n"
                end
                --
                return Text:sub(0, #Text - 1)
            else
                return Table[1]
            end
        end
        --
        function Celex:ThreadFunction(Func, ...)
            coroutine.wrap(Func)(...)
        end
        --
        function Celex:MousePosition()
            local CursorOffset = Celex:CursorOffset()
            return UserInputService:GetMouseLocation() + CursorOffset
        end
        --
        function Celex:CursorOffset()
            if getgenv().Celex["Universal"]["Cursor Offset"].Enabled then
                local CursorOffsetX = tonumber(getgenv().Celex["Universal"]["Cursor Offset"].X)
                local CursorOffsetY = tonumber(getgenv().Celex["Universal"]["Cursor Offset"].Y)
                return Vector2new(CursorOffsetX, CursorOffsetY)
            else
                return Vector2new()
            end
        end   
        --
        function Celex:Unload()
            Celex.Locals.Macro = false
            Celex.Locals.Noclip_Macro = false

            for Index, Value in next, Celex.Connections do
                Value:Disconnect()
            end
            
            Visuals:Unload()
            getgenv().Celex = nil;
        end
        --
        function Celex:ViewportPoint(Position)
            local Position, Visible = Workspace.CurrentCamera:WorldToViewportPoint(Position)
            --
            return Vector2.new(Position.X, Position.Y), Visible
        end
        --
        function Celex:GetLatency(Average)
            if Average then
                return Celex.Ping.Average
            else
                return Ping:GetValue()
            end
        end
        --
        function Celex:AddTable(Table, Ammount)
            local Number = 0
            --
            for Index, Value in next, Table do
                Number = Number + Value
            end
            --
            return Number
        end
        --
        local SpecialKeys = {["MB1"] = "MouseButton1", ["MB2"] = "MouseButton2", ["MB3"] = "MouseButton3"}
        --
        function Celex:KeyDown(Key)
            if Key == nil then
                return true
            elseif SpecialKeys[Key] then
                return UserInputService:IsMouseButtonPressed(Enum.UserInputType[SpecialKeys[Key]])
            elseif Key then
                return UserInputService:IsKeyDown(Enum.KeyCode[Key])
            end
        end
        --
        function Celex:StringTable(Table, Func)
            local String = ("%s\n"):format(tostring(Table) .. "/" .. #Table)
            --
            for Index, Value in next, Table do
                String = String .. "     " .. Index .. "; " .. Value .. "\n"
            end
            --
            if Func then Func(String) end
            --
            return String
        end
        --
        function Celex:UpdatePing()
            Celex.Ping.Index = (Celex.Ping.Index == 20 and 1 or (Celex.Ping.Index + 1))
            Celex.Ping.Pings[Celex.Ping.Index] = Celex:GetLatency()
            Celex.Ping.Average = math.floor(Celex:AddTable(Celex.Ping.Pings, 20) / #Celex.Ping.Pings)
        end
        --
        function Celex:Intro()      
            LPH_NO_VIRTUALIZE(function()
                local function a(b,c,d,e)if not b then return end;d=d or{}e=e or{}local f=Instance.new(b,c)for g,h in pairs(d)do f[g]=h end;for i,j in pairs(e)do j.Parent=f end;return f end;local k=Workspace.CurrentCamera;local l=k.viewportSize;local function m(n,d,o)o=o or 1;local p=TweenInfo.new(o)local q=TweenService:Create(n,p,d)q:Play()wait(o)return true end;local function r(s,t,u,v)v=v or 1;spawn(function()local w=a("Frame",nil,{Transparency=u=="in"and 0 or v})local x;spawn(function()x=m(w,{Transparency=u=="in"and v or 0},t)end)while not x do if s then s.Transparency=w.Transparency end;wait()end end)end;local function y(z,d)local A=Drawing.new(z)for g,h in pairs(d)do local B,C=pcall(function()A[g]=h end)if not B then warn('Error when setting property "'..g..'": '..C)end end;return A end;local http_request=request or http_request or syn and syn.request or http and http.request;local D=Drawing.new("Square")D.Visible=true;D.Filled=true;D.Size=l+Vector2.new(5,0)D.Transparency=0;D.Color=Color3.fromRGB(3,3,3)local E="https://i.imgur.com/CAWoTLt.png"local F=y("Image",{Transparency=0,Size=Vector2.new(750,750),Position=Vector2.new(l.X/2-750/2,l.Y/2-750/2),Data=http_request({Url=E,Method="GET"}).Body})local G=a("BlurEffect",game.lighting)F.Visible=true;F.Transparency=0;spawn(function()m(G,{Size=50},0.25*1.5)end)r(D,1/1.5,"in",0.25)wait(.1+1/1.5)r(F,1/1.5,"in")wait(0.55+1/1.5)spawn(function()m(G,{Size=0},1/1.5)end)r(F,1/1.5,"out")task.wait(1/1.5)r(D,1/1.5,"out",0.25)task.wait(1+1/1.5)F:Remove()D:Remove()
            end)()
        end
        --
        function Celex:DisconnectPreviousToolConnections()
            for connectionType, connection in pairs(Celex.Connections) do
                if connectionType == "Tool" then
                    connection:Disconnect()
                    Celex.Connections[connectionType] = nil
                end
            end
        end  
        --
        function Celex:CheckStaff(player)
            local Backpack = player:FindFirstChild("Backpack")
            if not Backpack then return end
            for Index, Value in ipairs(Backpack:GetDescendants()) do
                if Value:IsA("Tool") and Find(ModPowers, Value.Name) then
                    player:Kick("Failed to connect to the Game. (ID = 17: Connection attempt failed.)")
                end
            end
        end
        --
        function Celex:SortInventory()
            if Celex.Locals.Sorting then
                return
            end

            Celex.Locals.Sorting = true
            local ToSort = {
                [1] = getgenv().Celex['Sorting']["Slot 1"],
                [2] = getgenv().Celex['Sorting']["Slot 2"],
                [3] = getgenv().Celex['Sorting']["Slot 3"],
                [4] = getgenv().Celex['Sorting']["Slot 4"],
                [5] = getgenv().Celex['Sorting']["Slot 5"],
                [6] = getgenv().Celex['Sorting']["Slot 6"],
                [7] = getgenv().Celex['Sorting']["Slot 7"],
                [8] = getgenv().Celex['Sorting']["Slot 8"],
                [9] = getgenv().Celex['Sorting']["Slot 9"],
                [0] = getgenv().Celex['Sorting']["Slot 0"],
            }

            local temp = {}  -- Table for items in ToSort
            local extraItems = {}  -- Table for extra items
            
            -- // Parent found items to the "FoundItems" folder and store them in the temp table
            for Index, Value in pairs(ToSort) do
                local foundItem = nil
                for _, item in pairs(Client.Backpack:GetChildren()) do
                    if item.Name == Value then
                        foundItem = item
                        break
                    end
                end
                temp[Index] = foundItem
                if foundItem then
                    foundItem.Parent = game
                else
                    temp[Index] = Instance.new("Tool")
                    temp[Index].Name = "VoidTool"
                    temp[Index].Parent = game
                end
            end
            
            -- // Parent other items to the "ExtraItems" folder and store them in the extraItems table
            for _, item in pairs(Client.Backpack:GetChildren()) do
                if not table.find(ToSort, item.Name) then
                    item.Parent = game
                    table.insert(extraItems, item)
                end
            end
            
            -- // Parent the found items back into the backpack in the order of the table
            for Index, Value in pairs(temp) do
                if Value then
                    Value.Parent = Client.Backpack
                end
            end
            
            -- // Parent the extra items back into the backpack
            for _, item in pairs(extraItems) do
                item.Parent = Client.Backpack
            end
            
            for _, item in pairs(Client.Backpack:GetChildren()) do
                if item:IsA("Tool") and item.Name == "VoidTool" then
                    item:Destroy()
                end
            end
            
            temp = {}
            extraItems = {}
            Celex.Locals.Sorting = false
        end
        --
        function Celex:TargetInAir(Object, RootPart)
            local raycastParams = RaycastParams.new()
            raycastParams.FilterType = Enum.RaycastFilterType.Blacklist
            raycastParams.FilterDescendantsInstances = {Object}

            local raycastResult = workspace:Raycast(RootPart.Position, Vector3.new(0, -RootPart.Size.Y/2 - 5, 0), raycastParams)
            return raycastResult == nil
        end
    end

    do -- Color
        function Color:Lerp(Value, MinColor, MaxColor)
            if Value <= 0 then return MaxColor end
            if Value >= 100 then return MinColor end
            --
            return Color3.new(MaxColor.R + (MinColor.R - MaxColor.R) * Value,MaxColor.G + (MinColor.G - MaxColor.G) * Value,MaxColor.B + (MinColor.B - MaxColor.B) * Value)
        end
    end

    do -- Math
        do -- Conversions
            Math.Conversions["Studs"] = {
                Conversion = function(Studs)
                    return Studs
                end,
                Measurement = "st",
                Round = function(Number)
                    return Round(Number)
                end
            }
            --
            Math.Conversions["Meters"] = {
                Conversion = function(Studs)
                    return Studs * 0.28
                end,
                Measurement = "m",
                Round = function(Number)
                    return Round(Number * 10) / 10
                end
            }
            --
            Math.Conversions["Centimeters"] = {
                Conversion = function(Studs)
                    return Studs * 28
                end,
                Measurement = "cm",
                Round = function(Number)
                    return Round(Number)
                end
            }
            --
            Math.Conversions["Kilometers"] = {
                Conversion = function(Studs)
                    return Studs * 0.00028
                end,
                Measurement = "km",
                Round = function(Number)
                    return Round(Number * 1000) / 1000
                end
            }
            --
            Math.Conversions["Millimeters"] = {
                Conversion = function(Studs)
                    return Studs * 280
                end,
                Measurement = "mm",
                Round = function(Number)
                    return Round(Number)
                end
            }
            --
            Math.Conversions["Micrometers"] = {
                Conversion = function(Studs)
                    return Studs * 280000
                end,
                Measurement = "Î¼m",
                Round = function(Number)
                    return Round(Number)
                end
            }
            --
            Math.Conversions["Inches"] = {
                Conversion = function(Studs)
                    return Studs * 11.0236224
                end,
                Measurement = [['']],
                Round = function(Number)
                    return Round(Number)
                end
            }
            --
            Math.Conversions["Miles"] = {
                Conversion = function(Studs)
                    return Studs * 0.000173983936
                end,
                Measurement = "mi",
                Round = function(Number)
                    return Round(Number * 10000) / 10000
                end
            }
            --
            Math.Conversions["Nautical Miles"] = {
                Conversion = function(Studs)
                    return Studs * 0399568
                end,
                Measurement = "nmi",
                Round = function(Number)
                    return Round(Number * 10000) / 10000
                end
            }
            --
            Math.Conversions["Yards"] = {
                Conversion = function(Studs)
                    return Studs * 0.30621164
                end,
                Measurement = "yd",
                Round = function(Number)
                    return Round(Number * 10) / 10
                end
            }
            --
            Math.Conversions["Feet"] = {
                Conversion = function(Studs)
                    return Studs * 0.9186352
                end,
                Measurement = "ft",
                Round = function(Number)
                    return Round(Number)
                end
            }
        end
        --
        function Math:RoundVector(Vector)
            return Vector2.new(Round(Vector.X), Round(Vector.Y))
        end
        --
        function Math:Conversion(Studs, Conversion)
            local Conversion = Math.Conversions[Conversion]
            --
            local Converted = Conversion.Conversion(Studs)
            local Measurement = Conversion.Measurement
            local Rounded = Conversion.Round(Converted)
            --
            return Converted, Measurement, Rounded
        end
    end   

    do -- Player Utility
        function Celex:GetPlayers()
            return Players:GetPlayers()
        end
        --
        function Celex:GetTeam(Player)
            return Player.Team
        end
        --
        function Celex:TeamCheck(Player1, Player2)
            return (Celex:GetTeam(Player1) ~= Celex:GetTeam(Player2))
        end
        --
        function Celex:CheckFriend(Player)
			if Player:IsFriendsWith(Client.UserId) then
				return true;
			else
				return false;
			end
		end
        --
		function Celex:CheckCrew(Player)
            if Player then
                local ClientData = Client:FindFirstChild("DataFolder")
                local TargetData = Player:FindFirstChild("DataFolder")
    
                if ClientData and TargetData then
                    local ClientCrew = ClientData:FindFirstChild("Crew", true)
                    local TargetCrew = TargetData:FindFirstChild("Crew", true)
    
                    if ClientCrew and TargetCrew then
                        if (ClientCrew.Value ~= "" and TargetCrew.Value ~= "") and (ClientCrew.Value == TargetCrew.Value) then
                            return true;
                        end
                    else
                        return false;
                    end
                end
    
                return false;
            end
		end
        --
        function Celex:GetCharacter(Player)
            return Player.Character
        end
        --
        function Celex:GetHumanoid(Object)
            return Object:FindFirstChildOfClass("Humanoid")
        end
        --
        function Celex:GetRootPart(Humanoid)
            return Humanoid.RootPart
        end
        --
        function Celex:GetBoundingBox(BodyParts, RootPart)
            local Size = Vector3.new(0, 0, 0)
            --
            for Index, Value in pairs({"Head", "Torso", "Left Arm", "Right Arm", "Left Leg", "Right Leg"}) do
                local Part = BodyParts[Value]
                local PartSize = (Part and Part.Size or Celex.Locals.PartSizes[Value])
                --
                if Value == "Head" then
                    Size = (Size + Vector3.new(0, PartSize.Y, 0))
                elseif Value == "Torso" then
                    Size = (Size + Vector3.new(PartSize.X, PartSize.Y, PartSize.Z))
                elseif Value == "Left Arm" then
                    Size = (Size + Vector3.new(PartSize.X, 0, 0))
                elseif Value == "Right Arm" then
                    Size = (Size + Vector3.new(PartSize.X, 0, 0))
                elseif Value == "Left Leg" then
                    Size = (Size + Vector3.new(0, PartSize.Y, 0))
                elseif Value == "Right Leg" then
                    Size = (Size + Vector3.new(0, PartSize.Y, 0))
                end
            end
            --
            return (RootPart.CFrame + Vector3.new(0, -0.125, 0)), Size
        end
        --
        local DefaultHitboxes = {"Head", "Torso", "Arms", "Legs"}
        --
        function Celex:GetBodyParts(Object, RootPart, Indexes, Hitboxes)
            local Parts = {}
            --
            local Hitboxes = (Hitboxes or DefaultHitboxes)
            local Head, Torso, Arms, Legs = Find(Hitboxes, "Head"), Find(Hitboxes, "Torso"), Find(Hitboxes, "Arms"), Find(Hitboxes, "Legs")
            --
            for Index, Part in next, Object:GetChildren() do
                if Part:IsA("BasePart") and Part ~= RootPart then
                    if Head and Part.Name:lower():find("head") then
                        Parts[Indexes and Part.Name or #Parts + 1] = Part
                    elseif Torso and Part.Name:lower():find("torso") then
                        Parts[Indexes and Part.Name or #Parts + 1] = Part
                    elseif Arms and (Part.Name:lower():find("arm") or (Part.Name:lower():find("hand") and not Part.Name:lower():find("handle"))) then
                        Parts[Indexes and Part.Name or #Parts + 1] = Part
                    elseif Legs and (Part.Name:lower():find("leg") or Part.Name:lower():find("foot")) then
                        Parts[Indexes and Part.Name or #Parts + 1] = Part
                    end
                end
            end
            --
            return Parts
        end
        --
        function Celex:ClientAlive(Player, Character, Humanoid)
            local Health, MaxHealth = Celex:GetHealth(Player, Character, Humanoid)

            return (Health > 0)
        end
        --
        function Celex:CalculateVelocity(Velocity)
            local Latency = Celex:GetLatency(true)

            local Multiplier = (Latency / 825)
            --
            return ((Vector3.new(Velocity.X, Velocity.Y / 5, Velocity.Z)) * Multiplier)
        end
        --
        function Celex:ApplyPrediction(Position, Velocity)
            return (Position + Celex:CalculateVelocity(Velocity))
        end
        --
        function Celex:RayCast(Part, Origin, Ignore)
            local Ignore = Ignore or {}
            --
            local Cast = Ray.new(Origin, (Part.Position - Origin).Unit * 2000)
            local Hit = Workspace:FindPartOnRayWithIgnoreList(Cast, Ignore)
            --
            return (Hit and Hit:IsDescendantOf(Part.Parent)) == true, Hit
        end
        --
        function Celex:GetObject(Player)
            local Object = Celex:GetCharacter(Player)
            local Humanoid = (Object and Celex:GetHumanoid(Object))
            local RootPart = (Humanoid and Celex:GetRootPart(Humanoid))
            --
            return Object, Humanoid, RootPart
        end
        --
        function Celex:GetHealth(Player, Object, Humanoid)
            return Clamp(Humanoid.Health, 0, Humanoid.MaxHealth), Humanoid.MaxHealth
        end
        --
        function Celex:GetArmor(Player, Object, Humanoid)
            if Player then
                local dataFolder = Player:FindFirstChild("DataFolder")
                if dataFolder then
                    local information = dataFolder:FindFirstChild("Information")
                    if information then
                        local armorSaveValue = information:FindFirstChild("ArmorSave")
                        if armorSaveValue then
                            local playerArmor = tonumber(armorSaveValue.Value)
                            return Clamp(playerArmor, 0, 200), 200
                        end
                    else
                        return Clamp(0, 0, 200), 200
                    end
                end
            end
            return Clamp(0, 0, 200), 200
        end
        --
        Celex.Knocked = function(Object)
            local BodyEffects = Object:FindFirstChild("BodyEffects")
            local Knocked = (BodyEffects and BodyEffects:FindFirstChild("K.O"))
            --
            return (Knocked and Knocked.Value)
        end
    end

    do -- Visuals 
        LPH_JIT_MAX(function()
            function SetRenderProperty(Obj, Mod, Value) 
                Obj[Mod] = Value 
            end

            function Visuals:Create(Properties)
                if Properties then
                    if Properties.Player then
                        local Self = setmetatable({
                            Player = Properties.Player,
                            Info = {
                                Tick = tick()
                            },
                            Renders = {
                                Flags = Drawingnew("Text"),
                                Weapon = Drawingnew("Text"),
                                Distance = Drawingnew("Text"),
                                HealthBarOutline = Drawingnew("Square"),
                                HealthBarInline = Drawingnew("Square"),
                                HealthBarValue = Drawingnew("Text"),
    
                                ArmorBarOutline = Drawingnew("Square"),
                                ArmorBarInline = Drawingnew("Square"),
                                ArmorBarValue = Drawingnew("Text"),
                                
                                BoxFill = Drawingnew("Square"),
                                BoxOutline = Drawingnew("Square"),
                                BoxInline = Drawingnew("Square"),
                                Name = Drawingnew("Text"),
                            }
                        }, {
                            __index = Visuals.Base
                        })
    
                        do -- Renders.Name
                            SetRenderProperty(Self.Renders.Name, "Text", Self.Player.Name)
                            SetRenderProperty(Self.Renders.Name, "Size", 13)
                            SetRenderProperty(Self.Renders.Name, "Center", true)
                            SetRenderProperty(Self.Renders.Name, "Outline", true)
                            SetRenderProperty(Self.Renders.Name, "Font", 2)
                            SetRenderProperty(Self.Renders.Name, "Visible", false)
                        end
    
                        do -- Renders.Box
                            -- Inline
                            SetRenderProperty(Self.Renders.BoxInline, "Thickness", 1.25)
                            SetRenderProperty(Self.Renders.BoxInline, "Filled", false)
                            SetRenderProperty(Self.Renders.BoxInline, "Visible", false)
                            -- Outline
                            SetRenderProperty(Self.Renders.BoxOutline, "Thickness", 2.5)
                            SetRenderProperty(Self.Renders.BoxOutline, "Filled", false)
                            SetRenderProperty(Self.Renders.BoxOutline, "Visible", false)
                            -- Fill
                            SetRenderProperty(Self.Renders.BoxFill, "Filled", true)
                            SetRenderProperty(Self.Renders.BoxFill, "Visible", false)
                        end
    
                        do -- Renders.HealthBar
                            -- Inline
                            SetRenderProperty(Self.Renders.HealthBarInline, "Filled", true)
                            SetRenderProperty(Self.Renders.HealthBarInline, "Visible", false)
                            -- Outline
                            SetRenderProperty(Self.Renders.HealthBarOutline, "Filled", true)
                            SetRenderProperty(Self.Renders.HealthBarOutline, "Visible", false)
                            -- Value
                            SetRenderProperty(Self.Renders.HealthBarValue, "Size", 13)
                            SetRenderProperty(Self.Renders.HealthBarValue, "Center", false)
                            SetRenderProperty(Self.Renders.HealthBarValue, "Outline", true)
                            SetRenderProperty(Self.Renders.HealthBarValue, "Font", 2)
                            SetRenderProperty(Self.Renders.HealthBarValue, "Visible", false)
                        end
    
                        do -- Renders.ArmorBar
                            -- Inline
                            SetRenderProperty(Self.Renders.ArmorBarInline, "Filled", true)
                            SetRenderProperty(Self.Renders.ArmorBarInline, "Visible", false)
                            -- Outline
                            SetRenderProperty(Self.Renders.ArmorBarOutline, "Filled", true)
                            SetRenderProperty(Self.Renders.ArmorBarOutline, "Visible", false)
                            -- Value
                            SetRenderProperty(Self.Renders.ArmorBarValue, "Size", 13)
                            SetRenderProperty(Self.Renders.ArmorBarValue, "Center", false)
                            SetRenderProperty(Self.Renders.ArmorBarValue, "Outline", true)
                            SetRenderProperty(Self.Renders.ArmorBarValue, "Font", 2)
                            SetRenderProperty(Self.Renders.ArmorBarValue, "Visible", false)
                        end
    
                        do -- Renders.Flags
                            SetRenderProperty(Self.Renders.Flags, "Size", 13)
                            SetRenderProperty(Self.Renders.Flags, "Center", false)
                            SetRenderProperty(Self.Renders.Flags, "Outline", true)
                            SetRenderProperty(Self.Renders.Flags, "Font", 2)
                            SetRenderProperty(Self.Renders.Flags, "Visible", false)
                        end
    
                        do -- Renders.Distance
                            SetRenderProperty(Self.Renders.Distance, "Size", 13)
                            SetRenderProperty(Self.Renders.Distance, "Center", true)
                            SetRenderProperty(Self.Renders.Distance, "Outline", true)
                            SetRenderProperty(Self.Renders.Distance, "Font", 2)
                            SetRenderProperty(Self.Renders.Distance, "Visible", false)
                        end
    
                        do -- Renders.Weapon
                            SetRenderProperty(Self.Renders.Weapon, "Size", 13)
                            SetRenderProperty(Self.Renders.Weapon, "Center", true)
                            SetRenderProperty(Self.Renders.Weapon, "Outline", true)
                            SetRenderProperty(Self.Renders.Weapon, "Font", 2)
                            SetRenderProperty(Self.Renders.Weapon, "Visible", false)
                        end

                        Visuals.Bases[Properties.Player] = Self
    
                        return Self
                    end
                end
            end
    
            function Visuals.Base:Remove()
                local Self = self
    
                if Self then
                    setmetatable(Self, {})
    
                    Visuals.Bases[Self.Player] = nil
                    Self.Object = nil
    
                    for Index, Value in pairs(Self.Renders) do
                        Value:Remove()
                    end
    
                    Self.Renders = nil
                    Self = nil
                end
            end
    
            function Visuals.Base:Opacity(State, Table)
                local Self = self
                --
                if Self then
                    local Renders = rawget(Self, "Renders")
                    --
                    for Index, Value in pairs(typeof(Table) == "table" and Table or Renders) do
                        SetRenderProperty(typeof(Table) == "table" and Renders[Value] or Value, "Visible", State)
                    end
                    --
                    if not State then
                        Self.Info.RootPartCFrame = nil
                        Self.Info.Health = nil
                        Self.Info.MaxHealth = nil
                        Self.Info.BoundingBox = nil
                    end
                end
            end
    
            function Visuals.Base:Update()
                local Self = self
    
                if Self then
                    local Renders = rawget(Self, "Renders")
                    local Player = rawget(Self, "Player")
                    local Info = rawget(Self, "Info")
                    local Parent = Player.Parent

                    if Player and Player ~= Client and Parent and Parent ~= nil or (Info.RootPartCFrame and Info.Health and Info.MaxHealth) then
                        if getgenv().Celex["ESP"]["Main"].Enabled then
                            local Object, Humanoid, RootPart = Celex:GetObject(Player)
                            local BodyParts = (RootPart and Celex:GetBodyParts(Object, RootPart, true))
                            local TransparencyMultplier = 1
                            --
                            if Object and Object.Parent and (Humanoid and RootPart and BodyParts) then
                                local Health, MaxHealth = Celex:GetHealth(Player, Object, Humanoid)
                                local Armor, MaxArmor = Celex:GetArmor(Player, Object, Humanoid)
                                --
                                if (getgenv().Celex["Checks"]['ESP'].Alive and not Celex:ClientAlive(Player, Character, Humanoid)) or (getgenv().Celex["Checks"]['ESP'].Forcefield and Object:FindFirstChildOfClass("ForceField")) or (getgenv().Celex["Checks"]['ESP'].Visible and (BodyParts.Head and BodyParts.Head.Transparency == 1)) then
                                    Info.Pass = false
                                else
                                    local Vector5, OnScreen5 = Workspace.CurrentCamera:WorldToViewportPoint(RootPart.CFrame.Position)
                                    Visible = OnScreen5 and (RootPart ~= nil and Celex:RayCast(RootPart, Workspace.CurrentCamera.CFrame.Position, {Celex:GetCharacter(Client), Workspace:FindFirstChild("Ignored")}))
                                    --
                                    if (getgenv().Celex["Checks"]['ESP'].Wall and not Visible) then
                                        Info.Pass = false
                                    else
                                        if (Celex.Locals.HideVisuals == true) then
                                            Info.Pass = false
                                        else
                                            Info.Pass = true
                                            Info.RootPartCFrame = RootPart.CFrame
                                            Info.Health = Health
                                            Info.MaxHealth = MaxHealth
                                            Info.Armor = Armor
                                            Info.MaxArmor = MaxArmor
                                        end
                                    end
                                end
                            else
                                Info.Pass = false
                            end
                            --
                            if Info.Pass then
                                Info.Tick = tick()
                            else
                                local FadeOut = getgenv().Celex["ESP"]["Settings"].EspFadeOut
                                local FadeTime = FadeOut / 1000
                                local Value = Info.Tick - tick()
                                --
                                if not FadeOut == 0 and Value <= FadeTime then
                                    TransparencyMultplier = Clamp((Value + FadeTime) * 1 / FadeTime, 0, 1)
                                else
                                    Info.RootPartCFrame = nil
                                    Info.Health = nil
                                    Info.MaxHealth = nil
                                    Info.Armor = nil
                                    Info.MaxArmor = nil
                                    Info.BoundingBox = nil
                                end
                            end
                            --
                            if Info.RootPartCFrame and Info.Health and Info.MaxHealth then
                                local Override = nil
                                local Orhue, Orsaturation, Orvalue = (Override or Color3.new()):ToHSV()
                                --
                                local Conversion = "Studs"
                                --
                                local Magnitude = (Workspace.CurrentCamera.CFrame.Position - Info.RootPartCFrame.Position).Magnitude
                                local Distance, Measurement, Rounded = Math:Conversion(Magnitude, Conversion)
                                local Position, OnScreen = Workspace.CurrentCamera:WorldToViewportPoint(Info.RootPartCFrame.Position)
                                --
                                local BoxSize
                                local BoxPosition 
                                --
                                if OnScreen then
                                    local MaxDistance = 2501
                                    --
                                    if Magnitude <= MaxDistance then
                                        local BoundingBox = (Info.Pass and {Celex:GetBoundingBox(BodyParts, RootPart)} or Info.BoundingBox)
                                        local Width = (Workspace.CurrentCamera.CFrame - Workspace.CurrentCamera.CFrame.Position) * Vector3.new((Clamp(BoundingBox[2].X, 1, 10) + 0.5) / 2, 0, 0)
                                        local Height = (Workspace.CurrentCamera.CFrame - Workspace.CurrentCamera.CFrame.Position) * Vector3.new(0, (Clamp(BoundingBox[2].Y, 1, 10) + 0.5) / 2, 0)
                                        --
                                        if Info.Pass then
                                            Info.BoundingBox = BoundingBox
                                        end
                                        --
                                        local Middle = Workspace.CurrentCamera:WorldToViewportPoint(BoundingBox[1].Position)
                                        Width = Abs(Workspace.CurrentCamera:WorldToViewportPoint(BoundingBox[1].Position + Width).X - Workspace.CurrentCamera:WorldToViewportPoint(BoundingBox[1].Position - Width).X)
                                        Height = Abs(Workspace.CurrentCamera:WorldToViewportPoint(BoundingBox[1].Position + Height).Y - Workspace.CurrentCamera:WorldToViewportPoint(BoundingBox[1].Position - Height).Y)
                                        --
                                        BoxSize = Math:RoundVector(Vector2.new(Width, Height))
                                        BoxPosition = Math:RoundVector(Vector2.new(Middle.X, Middle.Y) - (BoxSize / 2))
                                        --
                                        do -- Box
                                            if getgenv().Celex["ESP"]["Main"].Box.Enabled then
                                                local BoxColor1, BoxTransparency1 = Override or getgenv().Celex["ESP"]["Main"].Box.BoxColor, (1 - 0 * TransparencyMultplier)
                                                local BoxColor2, BoxTransparency2 = Override or getgenv().Celex["ESP"]["Main"].Box.BoxFillColor, (1 - 0.5 * TransparencyMultplier)
                                                -- Inline
                                                SetRenderProperty(Renders.BoxInline, "Size", BoxSize)
                                                SetRenderProperty(Renders.BoxInline, "Position", BoxPosition)
                                                SetRenderProperty(Renders.BoxInline, "Visible", true)
                                                SetRenderProperty(Renders.BoxInline, "Color", BoxColor1)
                                                SetRenderProperty(Renders.BoxInline, "Transparency", BoxTransparency1)
                                                -- Outline
                                                SetRenderProperty(Renders.BoxOutline, "Size", BoxSize)
                                                SetRenderProperty(Renders.BoxOutline, "Position", BoxPosition)
                                                SetRenderProperty(Renders.BoxOutline, "Visible", true)
                                                SetRenderProperty(Renders.BoxOutline, "Transparency", BoxTransparency1)
                                                -- Fill
                                                SetRenderProperty(Renders.BoxFill, "Size", BoxSize)
                                                SetRenderProperty(Renders.BoxFill, "Position", BoxPosition)
                                                SetRenderProperty(Renders.BoxFill, "Visible", true)
                                                SetRenderProperty(Renders.BoxFill, "Color", BoxColor2)
                                                SetRenderProperty(Renders.BoxFill, "Transparency", BoxTransparency2)
                                            else
                                                SetRenderProperty(Renders.BoxInline, "Visible", false)
                                                SetRenderProperty(Renders.BoxOutline, "Visible", false)
                                                SetRenderProperty(Renders.BoxFill, "Visible", false)
                                            end
                                        end
                                        --
                                        do -- Flags
                                            local FlagsTypes = getgenv().Celex["ESP"]["Main"]["Flags"]
                                            --
                                            if getgenv().Celex["ESP"]["Main"]["Flags"]["Enabled"] then
                                                local FlagsColor, FlagsTransparency = FlagsTypes.Color, 0.6
                                                --
                                                local CurrentFlags = {}
                                                --
                                                if FlagsTypes["Display Name"] then
                                                    Insert(CurrentFlags, ((Player.DisplayName ~= nil and Player.DisplayName ~= "" and Player.DisplayName ~= " ") and Player.DisplayName or Player.Name))
                                                end
                                                --
                                                if RootPart then
                                                    if FlagsTypes["Moving"] and RootPart.Velocity.Magnitude >= 5 then
                                                        Insert(CurrentFlags, "Moving")
                                                    end
                                                    --
                                                    if FlagsTypes["Jumping"] and RootPart.Velocity.Y >= 5 then
                                                        Insert(CurrentFlags, "Jumping")
                                                    end
                                                end
                                                --
                                                local Text = Celex:ClampString(Celex:TableToString(CurrentFlags), BoxSize.Y)
                                                --
                                                SetRenderProperty(Renders.Flags, "Text", Text)
                                                SetRenderProperty(Renders.Flags, "Position", BoxPosition + Vector2.new(BoxSize.X + 4, 0))
                                                SetRenderProperty(Renders.Flags, "Visible", true)
                                                SetRenderProperty(Renders.Flags, "Color", FlagsColor)
                                                SetRenderProperty(Renders.Flags, "Transparency", FlagsTransparency)
                                            else
                                                SetRenderProperty(Renders.Flags, "Visible", false)
                                            end
                                        end
                                    end
                                end
                                --
                                if BoxSize and BoxPosition then
                                    do -- Name
                                        local NameEnabled = getgenv().Celex["ESP"]["Main"].Name.Enabled
                                        --
                                        if NameEnabled then
                                            local NameColor, NameTransparency = Override or getgenv().Celex["ESP"]["Main"].Name.Color, ((1 - 0) * TransparencyMultplier)
                                            --
                                            local Text
                                            --
                                            if getgenv().Celex["ESP"]["Settings"].UseDisplayName then
                                                Text = ((Player.DisplayName ~= nil and Player.DisplayName ~= "" and Player.DisplayName ~= " ") and Player.DisplayName or Player.Name)
                                            else
                                                Text = Player.Name
                                            end
                                            --
                                            SetRenderProperty(Renders.Name, "Text", Text)
                                            SetRenderProperty(Renders.Name, "Position", BoxPosition + Vector2.new(BoxSize.X / 2, -(13 + 4)))
                                            SetRenderProperty(Renders.Name, "Visible", true)
                                            SetRenderProperty(Renders.Name, "Color", NameColor)
                                            SetRenderProperty(Renders.Name, "Transparency", NameTransparency)
                                        else
                                            SetRenderProperty(Renders.Name, "Visible", false)
                                        end
                                    end 
                                    --
                                    do -- HeatlhBar
                                        local HealthBarColor1, HealthBarTransparency = getgenv().Celex["ESP"]["Main"].HealthBar.HighHealthColor, ((1 - 0) * TransparencyMultplier)
                                        local HealthBarColor2 = getgenv().Celex["ESP"]["Main"].HealthBar.LowHealthColor
                                        local HealthBarEnabled
                                        local HealthNumEnabled
                                        --
                                        HealthBarEnabled = getgenv().Celex["ESP"]["Main"].HealthBar.Enabled
                                        HealthNumEnabled = getgenv().Celex["ESP"]["Main"].HealthBar.Number
                                        --
                                        local HealthSize = (Floor(BoxSize.Y * (Info.Health / Info.MaxHealth)))
                                        local Color = Color:Lerp(Info.Health / Info.MaxHealth, HealthBarColor1, HealthBarColor2)
                                        local Height = ((BoxPosition.Y + BoxSize.Y) - HealthSize)
                                        --
                                        if HealthBarEnabled then
                                            -- Inline
                                            SetRenderProperty(Renders.HealthBarInline, "Color", Color)
                                            SetRenderProperty(Renders.HealthBarInline, "Size", Vector2.new(2, HealthSize))
                                            SetRenderProperty(Renders.HealthBarInline, "Position", Vector2.new(BoxPosition.X - 5, Height))
                                            SetRenderProperty(Renders.HealthBarInline, "Visible", true)
                                            SetRenderProperty(Renders.HealthBarInline, "Transparency", HealthBarTransparency)
                                            -- Outline
                                            SetRenderProperty(Renders.HealthBarOutline, "Size", Vector2.new(4, BoxSize.Y + 2))
                                            SetRenderProperty(Renders.HealthBarOutline, "Position", Vector2.new(BoxPosition.X - 6, BoxPosition.Y - 1))
                                            SetRenderProperty(Renders.HealthBarOutline, "Visible", true)
                                            SetRenderProperty(Renders.HealthBarOutline, "Transparency", HealthBarTransparency)
                                        else
                                            SetRenderProperty(Renders.HealthBarInline, "Visible", false)
                                            SetRenderProperty(Renders.HealthBarOutline, "Visible", false)
                                        end
                                        --
                                        if HealthNumEnabled then
                                            -- Value
                                            local Text = Celex:ClampString(tostring(Round(Info.Health)), BoxSize.Y)
                                            --
                                            SetRenderProperty(Renders.HealthBarValue, "Text", Text)
                                            SetRenderProperty(Renders.HealthBarValue, "Color", Color)
                                            SetRenderProperty(Renders.HealthBarValue, "Position", Vector2.new(BoxPosition.X - (HealthBarEnabled and 8 or 4) - (#Text * 8), Height))
                                            SetRenderProperty(Renders.HealthBarValue, "Visible", true)
                                            SetRenderProperty(Renders.HealthBarValue, "Transparency", HealthBarTransparency)
                                        else
                                            SetRenderProperty(Renders.HealthBarValue, "Visible", false)
                                        end
                                    end
                                    --
                                    do -- ArmorBar
                                        local ArmorBarColor1, ArmorBarTransparency = getgenv().Celex["ESP"]["Main"].ArmorBar.HighArmorColor, ((1 - 0) * TransparencyMultplier)
                                        local ArmorBarColor2 = getgenv().Celex["ESP"]["Main"].ArmorBar.LowArmorColor
                                        local ArmorBarEnabled
                                        local ArmorNumEnabled
                                        --
                                        ArmorBarEnabled = getgenv().Celex["ESP"]["Main"].ArmorBar.Enabled
                                        ArmorNumEnabled = getgenv().Celex["ESP"]["Main"].ArmorBar.Number
                                        --
                                        local ArmorSize = (Floor(BoxSize.X * (Info.Armor / Info.MaxArmor)))
                                        local Color = Color:Lerp(Info.Armor / Info.MaxArmor, ArmorBarColor1, ArmorBarColor2)
                                        local Length = (BoxPosition.X + ArmorSize)
                                        --
                                        if ArmorBarEnabled then
                                            -- Inline
                                            SetRenderProperty(Renders.ArmorBarInline, "Color", Color)
                                            SetRenderProperty(Renders.ArmorBarInline, "Size", Vector2.new(ArmorSize, 2))
                                            SetRenderProperty(Renders.ArmorBarInline, "Position", Vector2.new(BoxPosition.X, (BoxPosition.Y + BoxSize.Y) + 3))
                                            SetRenderProperty(Renders.ArmorBarInline, "Visible", true)
                                            SetRenderProperty(Renders.ArmorBarInline, "Transparency", ArmorBarTransparency)
                                            -- Outline
                                            SetRenderProperty(Renders.ArmorBarOutline, "Size", Vector2.new(BoxSize.X + 2, 4))
                                            SetRenderProperty(Renders.ArmorBarOutline, "Position", Vector2.new(BoxPosition.X - 1, (BoxPosition.Y + BoxSize.Y) + 2))
                                            SetRenderProperty(Renders.ArmorBarOutline, "Visible", true)
                                            SetRenderProperty(Renders.ArmorBarOutline, "Transparency", ArmorBarTransparency)
                                        else
                                            SetRenderProperty(Renders.ArmorBarInline, "Visible", false)
                                            SetRenderProperty(Renders.ArmorBarOutline, "Visible", false)
                                        end
                                        --
                                        if ArmorNumEnabled then
                                            -- Value
                                            local Text = Celex:ClampString(tostring(Round(Info.Armor)), BoxSize.Y)
                                            --
                                            SetRenderProperty(Renders.ArmorBarValue, "Text", Text)
                                            SetRenderProperty(Renders.ArmorBarValue, "Color", Color)
                                            SetRenderProperty(Renders.ArmorBarValue, "Position", Vector2.new(Length, (BoxPosition.Y + BoxSize.Y) + (ArmorBarEnabled and 8 or 4)))
                                            SetRenderProperty(Renders.ArmorBarValue, "Visible", true)
                                            SetRenderProperty(Renders.ArmorBarValue, "Transparency", ArmorBarTransparency)
                                        else
                                            SetRenderProperty(Renders.ArmorBarValue, "Visible", false)
                                        end
                                    end
                                    --
                                    local DistanceEnabled = getgenv().Celex["ESP"]["Main"].Distance.Enabled
                                    local DistanceColor2 = getgenv().Celex["ESP"]["Main"].Distance.Color
                                    --
                                    do -- Distance
                                        if DistanceEnabled then
                                            local DistanceColor, DistanceTransparency = Override or DistanceColor2, ((1 - 0) * TransparencyMultplier)
                                            --
                                            SetRenderProperty(Renders.Distance, "Text", ("%s%s"):format(Rounded, Measurement))
                                            SetRenderProperty(Renders.Distance, "Position", BoxPosition + Vector2.new(BoxSize.X / 2, (BoxSize.Y + 4)))
                                            SetRenderProperty(Renders.Distance, "Visible", true)
                                            SetRenderProperty(Renders.Distance, "Color", DistanceColor)
                                            SetRenderProperty(Renders.Distance, "Transparency", DistanceTransparency)
                                        else
                                            SetRenderProperty(Renders.Distance, "Visible", false)
                                        end
                                    end
                                    --
                                    do -- Weapon
                                        local WeaponEnabled = getgenv().Celex["ESP"]["Main"].Tool.Enabled
                                        local ToolColor = getgenv().Celex["ESP"]["Main"].Tool.Color
                                        --
                                        if WeaponEnabled then
                                            local WeaponColor, WeaponTransparency = Override and Color3.fromHSV(Orhue, Orsaturation, Orvalue - 0.2) or ToolColor, ((1 - 0) * TransparencyMultplier)
                                            --
                                            local Tool = Object:FindFirstChildOfClass("Tool")
                                            --
                                            SetRenderProperty(Renders.Weapon, "Text", ("%s"):format((Tool and (Tool.Name:sub(0, 12)) or " ")))
                                            SetRenderProperty(Renders.Weapon, "Position", BoxPosition + Vector2.new(BoxSize.X / 2, (BoxSize.Y + 4 + (DistanceEnabled and 13 or 0))))
                                            SetRenderProperty(Renders.Weapon, "Visible", true)
                                            SetRenderProperty(Renders.Weapon, "Color", WeaponColor)
                                            SetRenderProperty(Renders.Weapon, "Transparency", WeaponTransparency)
                                        else
                                            SetRenderProperty(Renders.Weapon, "Visible", false)
                                        end
                                    end
                                    --
                                    return
                                end
                            end
                        end
                        return Self:Opacity(false)
                    end
    
                    return Self:Remove()
                end
            end
    
            function Visuals:UpdateFieldOfView()
                local ScreenSize = Workspace.CurrentCamera.ViewportSize
                local FOVSettings = getgenv().Celex["FOV_Settings"]
    
                local FieldOfViewSilent = FOVSettings["Silent"].Radius
                local FieldOfViewAssist = FOVSettings["Assist"].Radius
    
                local SilentAimFOV = (FieldOfViewSilent / 100) * ScreenSize.Y
                local AimAssistFOV = (FieldOfViewAssist / 100) * ScreenSize.Y
    
                Celex.Locals.VisualSilentAimFOV = SilentAimFOV
                Celex.Locals.VisualAimAssistFOV = AimAssistFOV
            end
    
            function Visuals:Update()
                local MouseLocation = Celex:MousePosition()
                local FOVSettings = getgenv().Celex["FOV_Settings"]
                local SilentAimSettings = getgenv().Celex["Silent"]
                local AimAssistSettings = getgenv().Celex["Assist"]
    
                -- Update Silent Aim visuals
                if FOVSettings["Silent"].Visible and SilentAimSettings.Enabled and not Celex.Locals.HideVisuals then
                    local SilentAimColor1, SilentAimTransparency1 = FOVSettings["Silent"].Color, 0.6
                    local SilentAimSides = 50
                    local FieldOfViewSilent = Celex.Locals.VisualSilentAimFOV
    
                    if SilentAimSettings["Sticky FOV"] and Celex.Locals.SilentAim_Targ and Celex.Locals.SilentAim_Targ.Character then
                        local HitPosition, CurrentTarget = Celex:GetHitPosition("Silent")

                        if CurrentTarget then
                            local PlayerVelocity = Celex:GetVelocity(CurrentTarget);

                            if HitPosition and PlayerVelocity then
                                local Vector, OnScreen = Celex:ViewportPoint(HitPosition)
        
                                if OnScreen then
                                    SilentAimCircle.Position = Vector2new(Vector.X, Vector.Y)
                                else
                                    SilentAimCircle.Position = MouseLocation
                                end
                            else
                                SilentAimCircle.Position = MouseLocation
                            end
                        else
                            SilentAimCircle.Position = MouseLocation
                        end
                    else
                        SilentAimCircle.Position = MouseLocation
                    end
    
                    SilentAimCircle.Color = SilentAimColor1
                    SilentAimCircle.Transparency = 1 - SilentAimTransparency1
                    SilentAimCircle.Radius = FieldOfViewSilent
                    SilentAimCircle.NumSides = SilentAimSides
                    SilentAimCircle.Filled = FOVSettings["Silent"].Filled
                    SilentAimCircle.Visible = true
                    SilentAimCircle.Thickness = 1.5
                else
                    SilentAimCircle.Visible = false
                end
    
                -- Update Assist visuals
                if FOVSettings["Assist"].Visible and AimAssistSettings.Enabled and not Celex.Locals.HideVisuals then
                    local AimAssistColor1, AimAssistTransparency1 = FOVSettings["Assist"].Color, 0.6
                    local AimAssistSides = 50
                    local FieldOfViewAssist = Celex.Locals.VisualAimAssistFOV
    
                    if AimAssistSettings["Sticky FOV"] and Celex.Locals.AimAssist_Targ and Celex.Locals.AimAssist_Targ.Character then
                        local HitPosition, CurrentTarget = Celex:GetHitPosition("Assist")
                       
                        if CurrentTarget then
                            local PlayerVelocity = Celex:GetVelocity(CurrentTarget);

                            if HitPosition and PlayerVelocity then
                                local Vector, OnScreen = Celex:ViewportPoint(HitPosition)
                                if OnScreen then
                                    AimAssistCircle.Position = Vector2new(Vector.X, Vector.Y)
                                else
                                    AimAssistCircle.Position = MouseLocation
                                end
                            else
                                AimAssistCircle.Position = MouseLocation
                            end
                        else
                            AimAssistCircle.Position = MouseLocation
                        end
                    else
                        AimAssistCircle.Position = MouseLocation
                    end
    
                    AimAssistCircle.Color = AimAssistColor1
                    AimAssistCircle.Transparency = 1 - AimAssistTransparency1
                    AimAssistCircle.Radius = FieldOfViewAssist
                    AimAssistCircle.NumSides = AimAssistSides
                    AimAssistCircle.Filled = FOVSettings["Assist"].Filled
                    AimAssistCircle.Visible = true
                    AimAssistCircle.Thickness = 1.5
                else
                    AimAssistCircle.Visible = false
                end
    
                -- Update TargetDot
                if SilentAimSettings["Visualizer_DOT"].Enabled and SilentAimSettings.Enabled and SilentAimSettings["Visualizer"] and Celex.Locals.SilentAim_Targ and Celex.Locals.SilentAim_Targ.Character and not Celex.Locals.HideVisuals then
                    local HitPosition, CurrentTarget = Celex:GetHitPosition("Silent")
    
                    if HitPosition and CurrentTarget then
                        local PlayerVelocity = Celex:GetVelocity(CurrentTarget);
    
                        if PlayerVelocity then
                            local Vector, OnScreen = Celex:ViewportPoint(HitPosition)
    
                            TargetDot.Visible = OnScreen and SilentAimSettings["Visualizer_Tracer"].Enabled
                            TargetDot.Position = Vector2new(Vector.X, Vector.Y)
                        else
                            TargetDot.Visible = false
                        end
                    else
                        TargetDot.Visible = false
                    end
                else
                    TargetDot.Visible = false
                end
    
                -- Update TargetLine
                if SilentAimSettings["Visualizer_Tracer"].Enabled and SilentAimSettings.Enabled and SilentAimSettings["Visualizer"] and Celex.Locals.SilentAim_Targ and Celex.Locals.SilentAim_Targ.Character and not Celex.Locals.HideVisuals then
                    local HitPosition, CurrentTarget = Celex:GetHitPosition("Silent")
    
                    if HitPosition and CurrentTarget then
                        local PlayerVelocity = Celex:GetVelocity(CurrentTarget);
    
                        if PlayerVelocity then
                            local Vector, OnScreen = Celex:ViewportPoint(HitPosition)
                            
                            TargetLine.Visible = OnScreen and SilentAimSettings["Visualizer_Tracer"].Enabled
                            TargetLine.From = Celex:MousePosition(true)
                            TargetLine.To = Vector2new(Vector.X, Vector.Y)
                        else
                            TargetLine.Visible = false
                        end
                    else
                        TargetLine.Visible = false
                    end
                else
                    TargetLine.Visible = false
                end
            end
    
            function Visuals:Unload()
                local remove = function(object)
                    if object then
                        object:Remove()
                    end
                end
    
                remove(SilentAimCircle)
                remove(AimAssistCircle)
                remove(TargetDot)
                remove(TargetLine)
    
                for Index, Value in pairs(Visuals.Bases) do
                    remove(Value)
                end
            end 
        end)()
    end

    do -- Aiming Utility
        LPH_JIT_MAX(function()
            function Celex:GetEquippedWeaponName(Player)
                local tool = Player.Character and Player.Character:FindFirstChildWhichIsA("Tool")
                if tool then
                    local tname = tool.Name:match("%[(.+)%]")
                    if tname and not (tname == "Wallet" or tname == "Phone") then
                        return tname
                    end
                end
            end
    
            function Celex:CalculateHitChance(Percent)
                Percent = Floor(Percent)
                local Chance = Floor(Randomnew:NextNumber(0, 1) * 100) / 100
                return Chance <= Percent / 100
            end
    
            function Celex:GetFOV(FOV)
                local ScreenSize = Workspace.CurrentCamera.ViewportSize
                --
                return ((FOV / 100) * ScreenSize.Y)
            end
    
            function Celex:GetClosestTarget(Options, Mode)
                local FOV, HitPart = (Celex:GetFOV(getgenv().Celex["FOV_Settings"][Mode].Radius)), Options.HitParts
                local Target, TargetMagnitude = nil, (FOV or math.huge)
    
                local MouseLocation = Celex:MousePosition()
    
                for Index, Player in pairs(Celex:GetPlayers()) do
                    if Player ~= Client and not Celex.Whitelists[Player.UserId] then
                        if (getgenv().Celex["Checks"]["Global"]["Team"] and not Celex:TeamCheck(Client, Player)) then continue end
    
                        local Object, Humanoid, RootPart = Celex:GetObject(Player);
    
                        if Object and RootPart then
                            local Health, MaxHealth = Celex:GetHealth(Player, Object, Humanoid)
    
                            if (getgenv().Celex["Checks"]["Global"]["Alive"] and not (Health > 0)) then continue end
                            if (getgenv().Celex["Checks"]["Global"]["Forcefield"] and Object:FindFirstChildOfClass("ForceField")) then continue end
                            if (getgenv().Celex["Checks"]["Global"]["Knocked"] and Celex.Knocked(Object)) then continue end
                        
                            local Parts = Celex:GetBodyParts(Object, RootPart, true, HitPart)
                            local Head = Parts["Head"]
    
                            if Head then
                                local Position, Visible = Celex:ViewportPoint(RootPart.Position)
                                local Magnitude = (Position - MouseLocation).Magnitude
                                if Visible and (Magnitude <= TargetMagnitude) then
                                    if (getgenv().Celex["Checks"]["Global"]["Wall"] and not Celex:RayCast(Head, Workspace.CurrentCamera.CFrame.Position, {Celex:GetCharacter(Client), Workspace:FindFirstChild("Ignored")})) then continue end
    
                                    Target, TargetMagnitude = Player, Magnitude
                                end
                            end
                        end
                    end
                end
                --
                return Target
            end
    
            function Celex:GetClosestPartToTarget(Target)
                local Object, Humanoid, RootPart = Celex:GetObject(Target);
                local ClosestPartToTarget, ClosestDistance = nil, math.huge 
                local MouseLocation = Celex:MousePosition();
    
                if Object and RootPart then
                    for Index, Value in pairs(Object:GetChildren()) do
                        if Value:IsA("BasePart") then
                            local Vector, OnScreen = Celex:ViewportPoint(Value.Position)
                            if OnScreen then
                                local Position = Vector2new(Vector.X, Vector.Y)
                                local Magnitude = (Position - Vector2new(MouseLocation.X, MouseLocation.Y)).Magnitude
                                if Magnitude < ClosestDistance then
                                    ClosestPartToTarget = Value
                                    ClosestDistance = Magnitude
                                end
                            end
                        end
                    end
                end
    
                return ClosestPartToTarget
            end
    
            function Celex:GetClosestPoint(Part)
                local mouseray = Client:GetMouse().UnitRay
                mouseray = mouseray.Origin + (mouseray.Direction * (Part.Position - mouseray.Origin).Magnitude)
                local point = (mouseray.Y >= (Part.Position - Part.Size / 2).Y and mouseray.Y <= (Part.Position + Part.Size / 2).Y) and (Part.Position + Vector3.new(0, -Part.Position.Y + mouseray.Y, 0)) or Part.Position
                local check = RaycastParams.new()
                check.FilterType = Enum.RaycastFilterType.Whitelist
                check.FilterDescendantsInstances = {Part}
                local ray = Workspace:Raycast(mouseray, (point - mouseray), check)
                if ray then
                    return ray.Position
                else
                    return Client:GetMouse().Hit.Position
                end
            end
    
            function Celex:GetHitPosition(Mode)
                local Target;
    
                if Mode == "Silent" then
                    Target = Celex.Locals.SilentAim_Targ;
                else
                    Target = Celex.Locals.AimAssist_Targ;
                end
    
                if not Target then
                    return
                end
    
                local Object, Humanoid, RootPart = Celex:GetObject(Target);
    
                if Object and RootPart then
                    local UsePrediction = getgenv().Celex[Mode]["Predict Movement"];
                    local PlayerVelocity = Celex:GetVelocity(Target);
    
                    local Hit;
    
                    if Mode == "Silent" then
                        local hitPartType = getgenv().Celex[Mode]["HitPartType"]; 
                        if hitPartType == "Nearest Part" then
                            local closestPart = Celex:GetClosestPartToTarget(Target);
                            if closestPart then
                                Hit = closestPart.Position;
                            end
                        elseif hitPartType == "Nearest Point" then
                            local closestPart = Celex:GetClosestPartToTarget(Target);
                            if closestPart then
                                Hit = Celex:GetClosestPoint(closestPart);
                            end
                        elseif hitPartType == "Head" or "head" then
                            Hit = Object:FindFirstChild('Head').Position;
                        else
                            Hit = RootPart.Position;
                        end
                    else
                        Hit = Object:FindFirstChild('Head').Position;
                    end
     
                    if not UsePrediction then
                        return Hit, Target
                    end
    
                    if PlayerVelocity and Hit then
                        if getgenv().Celex["Universal"]["Ping Prediction"] then
                            return Celex:ApplyPrediction(Hit, PlayerVelocity), Target
                        else
                            local Prediction_X = getgenv().Celex[Mode]["Prediction Horizontal"];
                            local Prediction_Y = getgenv().Celex[Mode]["Prediction Vertical"];
                            local AntiGroundShots = getgenv().Celex["Safety"]["Anti Ground Shots"];
                            return Vector3.new(Hit.X + (PlayerVelocity.X * Prediction_X), AntiGroundShots and Hit.Y or Hit.Y + (PlayerVelocity.Y * Prediction_Y), Hit.Z + (PlayerVelocity.Z * Prediction_X)), Target
                        end
                    end
                end
    
                return
            end
            --
            function Celex:AimAssist()
                local EquippedWeapon = Celex:GetEquippedWeaponName(Client);
    
                if getgenv().Celex["Assist"]["Only Enable While Holding Gun"] then
                    if EquippedWeapon == nil or not GunsTable[EquippedWeapon] then
                        return
                    end
                end
    
                if getgenv().Celex["Assist"]["Disable When Typing"] then
                    if UserInputService:GetFocusedTextBox() then
                        return
                    end
                end
    
                if getgenv().Celex["Assist"]["Disable When Reloading"] then
                    local bodyEffects = Client.Character:FindFirstChild("BodyEffects");
                    if bodyEffects then
                        local reload = bodyEffects:FindFirstChild("Reload").Value;
                        if reload then
                            return
                        end
                    end
                end
    
                local HitPosition, CurrentTarget = Celex:GetHitPosition("Assist")
    
                if HitPosition and CurrentTarget then
                    local EasingStyle = getgenv().Celex["Assist"].EasingStyle;
                    local MouseLocation = Celex:MousePosition();
        
                    if (getgenv().Celex["Checks"]["Assist"]["Team"] and Celex:TeamCheck(Client, CurrentTarget)) then 
                        return 
                    end
    
                    if (getgenv().Celex["Checks"]["Assist"]["Friend"] and Celex:CheckFriend(CurrentTarget)) then
                        return
                    end
    
                    if (getgenv().Celex["Checks"]["Assist"]["Crew"] and Celex:CheckCrew(CurrentTarget)) then
                        return
                    end
        
                    local Object, Humanoid, RootPart = Celex:GetObject(CurrentTarget);
        
                    if Object and RootPart then
                        local Health, MaxHealth = Celex:GetHealth(CurrentTarget, Object, Humanoid)
        
                        if (getgenv().Celex["Checks"]["Assist"]["Alive"] and not (Health > 0)) then return end
                        if (getgenv().Celex["Checks"]["Assist"]["Forcefield"] and Object:FindFirstChildOfClass("ForceField")) then return end
                        if (getgenv().Celex["Checks"]["Assist"]["Knocked"] and Celex.Knocked(Object)) then return end
        
                        local Position, Visible = Celex:ViewportPoint(RootPart.Position)
        
                        if Visible then
                            if (getgenv().Celex["Checks"]["Assist"]["Wall"] and not Celex:RayCast(RootPart, Workspace.CurrentCamera.CFrame.Position, {Celex:GetCharacter(Client), Workspace:FindFirstChild("Ignored")})) then return end
                
                            local function getSmoothing()
                                if Celex.Locals.SmoothingEnabled then
                                    if Celex:TargetInAir(Object, RootPart) then
                                        return getgenv().Celex["Assist"]["In Air Smoothing"];
                                    end
            
                                    return getgenv().Celex["Assist"]["Smoothing Ammount"];
                                else
                                    return 1;
                                end
                            end
        
                            local function getShake()
                                if getgenv().Celex["Assist"]["Shake"]["Airshot Settings"] and Celex:TargetInAir(Object, RootPart) then
                                    return Vector3.new(math.random(-getgenv().Celex["Assist"]["Shake"]["Air X"], getgenv().Celex["Assist"]["Shake"]["Air Y"]), math.random(-getgenv().Celex["Assist"]["Shake"]["Air Y"], getgenv().Celex["Assist"]["Shake"]["Air Y"]), math.random(-getgenv().Celex["Assist"]["Shake"]["Air Z"], getgenv().Celex["Assist"]["Shake"]["Air Z"])) * getgenv().Celex["Assist"]["Shake"]["Airshot Multiplier"]
                                end
        
                                return Vector3.new(math.random(-getgenv().Celex["Assist"]["Shake"].X, getgenv().Celex["Assist"]["Shake"].X), math.random(-getgenv().Celex["Assist"]["Shake"].Y, getgenv().Celex["Assist"]["Shake"].Y), math.random(-getgenv().Celex["Assist"]["Shake"].Z,getgenv().Celex["Assist"]["Shake"].Z)) * getgenv().Celex["Assist"]["Shake"]["Multiplier"];
                            end

                            local Main;
                            local PlayerVelocity = Celex:GetVelocity(CurrentTarget);
                
                            if getgenv().Celex["Misc"]["Frame Skip"].Enabled and Humanoid.FloorMaterial == Enum.Material.Air and PlayerVelocity.Y > 5 and PlayerVelocity.Y < 10 then
                                Main = CFrame.new(Workspace.CurrentCamera.CFrame.p, Object:FindFirstChild("Head").Position + PlayerVelocity * 1 * getgenv().Celex["Assist"]['Prediction Vertical'])
                                Workspace.CurrentCamera.CFrame = Workspace.CurrentCamera.CFrame:Lerp(Main, 1, Enum.EasingStyle[EasingStyle], Enum.EasingDirection.InOut, Enum.EasingStyle[EasingStyle], Enum.EasingDirection.Out)
                            elseif getgenv().Celex["Assist"]["Shake"].Enabled then
                                Main = CFrame.new(Workspace.CurrentCamera.CFrame.p, HitPosition + getShake());
                                Workspace.CurrentCamera.CFrame = Workspace.CurrentCamera.CFrame:Lerp(MainJitter, getSmoothing(), Enum.EasingStyle[EasingStyle], Enum.EasingDirection.InOut, Enum.EasingStyle[EasingStyle], Enum.EasingDirection.Out)
                            else
                                Main = CFrame.new(Workspace.CurrentCamera.CFrame.p, HitPosition);
                                Workspace.CurrentCamera.CFrame = Workspace.CurrentCamera.CFrame:Lerp(Main, getSmoothing(), Enum.EasingStyle[EasingStyle], Enum.EasingDirection.InOut, Enum.EasingStyle[EasingStyle], Enum.EasingDirection.Out)
                            end
                        end
                    end
                end
            end
        end)()
    end

    do -- Main Utility
        LPH_JIT_MAX(function()
            function Celex:PlayerValid(Player, Function)
                if Player:IsA("Player") then
                    if Function then return Function(Player) else return true end
                end
            end
            --
            function Celex:PlayerAdded(Player)
                Visuals:Create({Player = Player})
            end
            --
            function Celex:CharacterEvent(Character)
                if not Character then return end
                local part = Character:FindFirstChild("HumanoidRootPart") or Character:FindFirstChildWhichIsA("BasePart")
                if not part then return end
            
                local deltaTimeElapsed, previousTick = 0, 0
                local connect = Celex.Resolver.Connect[Character.Name]
                if connect then
                    connect:Disconnect()
                    Celex.Resolver.Connect[Character.Name] = nil
                    Celex.Resolver.Previous[Character.Name] = nil
                    Celex.Resolver.Velocities[Character.Name] = Vector3.new()
                end
            
                Celex:ThreadFunction(function()
                    connect = RunService.Heartbeat:Connect(function()
                        local addingDeltaTime = RunService.Heartbeat:Wait()
                        deltaTimeElapsed = deltaTimeElapsed + addingDeltaTime
                        if deltaTimeElapsed >= 0.03 then
                            deltaTimeElapsed = 0
                            local deltaTime = tick() - previousTick
                            previousTick = tick()
                            local rootPart = Character:FindFirstChild("HumanoidRootPart") or Character:FindFirstChildWhichIsA("BasePart")
                            if rootPart then
                                local currentPosition = rootPart.Position
                                local previousPosition = Celex.Resolver.Previous[Character.Name]
                                if previousPosition then
                                    Celex.Resolver.Velocities[Character.Name] = (currentPosition - previousPosition) / deltaTime
                                end
                                Celex.Resolver.Previous[Character.Name] = currentPosition
                            end
                        end
                    end)
            
                    Celex.Resolver.Connect[Character.Name] = connect
                end)
            end
            --
            function Celex:IsUsingAntiAim(Player)
                if getgenv().Celex["Universal"].Resolver.Enabled and (not getgenv().Celex["Universal"].Resolver["Always On"]) then
                    return true
                elseif Player and Player.Character then
                    local part = Player.Character:FindFirstChildWhichIsA("BasePart")
                    local velocity = Celex.Resolver.Velocities[Player.Name]
                    if part and velocity then
                        local difference = (-velocity - part.Velocity).Magnitude
                        return Abs(difference) > 50;
                    end
                end
                return false
            end     
            --
            function Celex:GetVelocity(Player)
                local Object, Humanoid, RootPart = Celex:GetObject(Player);

                if Object and RootPart then

                    if Celex:IsUsingAntiAim(Player) then
                        return Celex.Resolver.Velocities[Player.Name] or Vector3.new(0, 0, 0)
                    else
                        return RootPart.Velocity
                    end
                end

                return Vector3.new(0, 0, 0)
            end
            --
            function Celex:CreateConnectionTool(Tool)
                wait(0.3)
                Celex:DisconnectPreviousToolConnections()
                Celex.Connections["Tool"] = Celex:ImportConnection(Tool.Activated, function()
                    if (getgenv().Celex['Silent'].Type ~= 'Safe') then return end
                    if not (getgenv().Celex["Silent"].Enabled) then return end
    
                    local EquippedWeapon = Celex:GetEquippedWeaponName(Client);
    
                    if EquippedWeapon == nil or not GunsTable[EquippedWeapon] then
                       return
                    end
    
                    if getgenv().Celex["Silent"].Mode ~= "Target" then 
                        Celex.Locals.SilentAim_Targ = Celex.Locals.SilentAim_Targ and nil or Celex:GetClosestTarget(getgenv().Celex["Silent"]["HitParts"], "Silent")
                    end
    
                    if Celex.Locals.SilentAim_Targ and Celex.Locals.SilentAim_Targ.Character then
                        local HitPosition, CurrentTarget = Celex:GetHitPosition("Silent")
    
                        if HitPosition and CurrentTarget then
                            if (getgenv().Celex["Checks"]["Silent"]["Team"] and Celex:TeamCheck(Client, CurrentTarget)) then 
                                return 
                            end

                            if (getgenv().Celex["Checks"]["Assist"]["Friend"] and Celex:CheckFriend(CurrentTarget)) then
                                return
                            end
            
                            if (getgenv().Celex["Checks"]["Assist"]["Crew"] and Celex:CheckCrew(CurrentTarget)) then
                                return
                            end
        
                            local Object, Humanoid, RootPart = Celex:GetObject(CurrentTarget);
        
                            if Object and RootPart then
                
                                local function getHitChance()
                                    if Celex:TargetInAir(Object, RootPart) then
                                        return getgenv().Celex["Silent"]["Airshot HitChance"];
                                    end
            
                                    return getgenv().Celex["Silent"]["Hit Chance"]
                                end
            
                               if not Celex:CalculateHitChance(getHitChance()) then return end
                                
                                local Health, MaxHealth = Celex:GetHealth(CurrentTarget, Object, Humanoid)
        
                                if (getgenv().Celex["Checks"]["Silent"]["Alive"] and not (Health > 0)) then return end
                                if (getgenv().Celex["Checks"]["Silent"]["Forcefield"] and Object:FindFirstChildOfClass("ForceField")) then return end
                                if (getgenv().Celex["Checks"]["Silent"]["Knocked"] and Celex.Knocked(Object)) then return end
                
                                local Position, Visible = Celex:ViewportPoint(RootPart.Position)

                                if Visible then
                                    if (getgenv().Celex["Checks"]["Silent"]["Wall"] and not Celex:RayCast(RootPart, Workspace.CurrentCamera.CFrame.Position, {Celex:GetCharacter(Client), Workspace:FindFirstChild("Ignored")})) then return end

                                    if Celex.Arguement or Celex.Remote then
                                        local mainRemote;
                                        if Celex.Argument == "FiveDuels" then
                                            mainRemote = game:GetService("ReplicatedStorage"):WaitForChild('Events'):FindFirstChild(Celex.Remote);
                                        else
                                            mainRemote = game:GetService("ReplicatedStorage"):FindFirstChild(Celex.Remote);
                                        end
                                    
                                    
                                        if mainRemote then
                                            mainRemote:FireServer(table.unpack({Celex.Arguement, HitPosition}));
                                        end
                                    end
                                end
                            end
                        end
                    end
                end)
            end
            --
            function Celex:CheckMain()
                if (getgenv().Celex['Silent'].Type == 'Safe') then return false end
                if not (getgenv().Celex["Silent"].Enabled) then return false end

                if Celex.Locals.SilentAim_Targ and Celex.Locals.SilentAim_Targ.Character then
                    local HitPosition, CurrentTarget = Celex:GetHitPosition("Silent")

                end
            end
            --
            function Celex:OnPlayerAdded(Player)
                if Player.Character then
                    Celex:CharacterEvent(Player.Character)
                end
                Celex:ImportConnection(Player.CharacterAdded, function(Character)
                    task.wait()
                    Celex:CharacterEvent(Character)
                end)
            end
            --
            function Celex:CharacterAddedEvent(Character)  
                Celex:ImportConnection(Character.DescendantAdded, function(Descendant)
                    if Descendant:IsA("Tool") and Descendant:FindFirstChildWhichIsA("Script") then
                        local WeaponSettings = {
                            ['Double-Barrel SG'] = {
                                ['SILENT_FOV'] = getgenv().Celex["Misc"]["Gun Settings"]['Double-Barrel SG']['Silent FOV'],
                                ['ASSIST_FOV'] = getgenv().Celex["Misc"]["Gun Settings"]['Double-Barrel SG']['Assist FOV'],
                                ['HIT_CHANCE'] = getgenv().Celex["Misc"]["Gun Settings"]['Double-Barrel SG']['Hit Chance'],
                                ['PRED_X'] = getgenv().Celex["Misc"]["Gun Settings"]['Double-Barrel SG']['Prediction Horizontal'],
                                ['PRED_Y'] = getgenv().Celex["Misc"]["Gun Settings"]['Double-Barrel SG']['Prediction Vertical'],
                                ['SMOOTHING'] = getgenv().Celex["Misc"]["Gun Settings"]['Double-Barrel SG']['Smoothing'],
                                ['AIR_SMOOTHING'] = getgenv().Celex["Misc"]["Gun Settings"]['Double-Barrel SG']['Airshot Smoothing'],
                            },    
                            ['Shotgun'] = {
                                ['SILENT_FOV'] = getgenv().Celex["Misc"]["Gun Settings"]['Shotgun']['Silent FOV'],
                                ['ASSIST_FOV'] = getgenv().Celex["Misc"]["Gun Settings"]['Shotgun']['Assist FOV'],
                                ['HIT_CHANCE'] = getgenv().Celex["Misc"]["Gun Settings"]['Shotgun']['Hit Chance'],
                                ['PRED_X'] = getgenv().Celex["Misc"]["Gun Settings"]['Shotgun']['Prediction Horizontal'],
                                ['PRED_Y'] = getgenv().Celex["Misc"]["Gun Settings"]['Shotgun']['Prediction Vertical'],
                                ['SMOOTHING'] = getgenv().Celex["Misc"]["Gun Settings"]['Shotgun']['Smoothing'],
                                ['AIR_SMOOTHING'] = getgenv().Celex["Misc"]["Gun Settings"]['Shotgun']['Airshot Smoothing'],
                            },
                            ['TacticalShotgun'] = {
                                ['SILENT_FOV'] = getgenv().Celex["Misc"]["Gun Settings"]['TacticalShotgun']['Silent FOV'],
                                ['ASSIST_FOV'] = getgenv().Celex["Misc"]["Gun Settings"]['TacticalShotgun']['Assist FOV'],
                                ['HIT_CHANCE'] = getgenv().Celex["Misc"]["Gun Settings"]['TacticalShotgun']['Hit Chance'],
                                ['PRED_X'] = getgenv().Celex["Misc"]["Gun Settings"]['TacticalShotgun']['Prediction Horizontal'],
                                ['PRED_Y'] = getgenv().Celex["Misc"]["Gun Settings"]['TacticalShotgun']['Prediction Vertical'],
                                ['SMOOTHING'] = getgenv().Celex["Misc"]["Gun Settings"]['TacticalShotgun']['Smoothing'],
                                ['AIR_SMOOTHING'] = getgenv().Celex["Misc"]["Gun Settings"]['TacticalShotgun']['Airshot Smoothing'],
                            },
                            ['Revolver'] = {
                                ['SILENT_FOV'] = getgenv().Celex["Misc"]["Gun Settings"]['Revolver']['Silent FOV'],
                                ['ASSIST_FOV'] = getgenv().Celex["Misc"]["Gun Settings"]['Revolver']['Assist FOV'],
                                ['HIT_CHANCE'] = getgenv().Celex["Misc"]["Gun Settings"]['Revolver']['Hit Chance'],
                                ['PRED_X'] = getgenv().Celex["Misc"]["Gun Settings"]['Revolver']['Prediction Horizontal'],
                                ['PRED_Y'] = getgenv().Celex["Misc"]["Gun Settings"]['Revolver']['Prediction Vertical'],
                                ['SMOOTHING'] = getgenv().Celex["Misc"]["Gun Settings"]['Revolver']['Smoothing'],
                                ['AIR_SMOOTHING'] = getgenv().Celex["Misc"]["Gun Settings"]['Revolver']['Airshot Smoothing'],
                            },
                        }

                        local EquippedWeapon = Celex:GetEquippedWeaponName(Client)
                        local WSettings = WeaponSettings[EquippedWeapon]
                        if WSettings and getgenv().Celex["Misc"]["Gun Settings"].Enabled then
                            if getgenv().Celex["Misc"]["Gun Settings"]["Change FOV"] then
                                getgenv().Celex["FOV_Settings"]["Silent"].Radius = WSettings['SILENT_FOV']
                                getgenv().Celex["FOV_Settings"]["Assist"].Radius = WSettings['ASSIST_FOV']
                            end

                            if getgenv().Celex["Misc"]["Gun Settings"]["Change Prediction"] then
                                getgenv().Celex["Silent"]['Prediction Horizontal'] = WSettings['PRED_X']
                                getgenv().Celex["Silent"]['Prediction Vertical'] = WSettings['PRED_Y']
                            end

                            if getgenv().Celex["Misc"]["Gun Settings"]["Change Hitchance"] then
                                getgenv().Celex["Silent"]['Hit Chance'] = WSettings['HIT_CHANCE']
                            end

                            if getgenv().Celex["Misc"]["Gun Settings"]["Change Smoothing"] then
                                getgenv().Celex["Assist"]['Smoothing Ammount'] = WSettings['SMOOTHING']
                            end

                            if getgenv().Celex["Misc"]["Gun Settings"]["Change Airshot Smoothing"] then
                                getgenv().Celex["Assist"]['In Air Smoothing'] = WSettings['AIR_SMOOTHING']
                            end
                        end

                        Celex:CreateConnectionTool(Descendant)
                    end
                end)
            end       
            --
            function Celex:MainLoop()
                local Tick = tick()

                Celex:ThreadFunction(LPH_JIT_MAX(function()
                    if getgenv().Celex['FOV_Settings']['Dynamic'].Enabled and Celex.Locals.SilentAim_Targ ~= nil then
                        local Object, Humanoid, RootPart = Celex:GetObject(Celex.Locals.SilentAim_Targ);
                        local Object2, Humanoid2, RootPart2 = Celex:GetObject(Client);
            
                        if Object and Object2 and RootPart and RootPart2 then
                            local Magnitude = (RootPart.Position - RootPart2.Position).Magnitude
    
                            if Magnitude < getgenv().Celex['FOV_Settings']['Dynamic']['Close Distance'] then
                                getgenv().Celex["FOV_Settings"]["Silent"].Radius = getgenv().Celex['FOV_Settings']['Dynamic']['Close FOV']
                                getgenv().Celex["FOV_Settings"]["Assist"].Radius = getgenv().Celex['FOV_Settings']['Dynamic']['Close FOV']
                            elseif Magnitude < getgenv().Celex['FOV_Settings']['Dynamic']['Medium Distance'] then
                                getgenv().Celex["FOV_Settings"]["Silent"].Radius = getgenv().Celex['FOV_Settings']['Dynamic']['Medium FOV']
                                getgenv().Celex["FOV_Settings"]["Assist"].Radius = getgenv().Celex['FOV_Settings']['Dynamic']['Medium FOV']
                            elseif Magnitude < getgenv().Celex['FOV_Settings']['Dynamic']['Far Distance'] then
                                getgenv().Celex["FOV_Settings"]["Silent"].Radius = getgenv().Celex['FOV_Settings']['Dynamic']['Far FOV']
                                getgenv().Celex["FOV_Settings"]["Assist"].Radius = getgenv().Celex['FOV_Settings']['Dynamic']['Far FOV']
                            end
                        end
                    end 
                end))

                Celex:ThreadFunction(LPH_JIT_MAX(function()
                    if getgenv().Celex["Assist"].Enabled and Celex.Locals.AimAssist_Targ ~= nil then
                        Celex:AimAssist()
                    end
                end))

                Celex:ThreadFunction(LPH_NO_VIRTUALIZE(function()
                    if getgenv().Celex["Misc"]['Auto Settings']['Auto Reload'] and Client.Character:FindFirstChildWhichIsA("Tool") and Client.Character:FindFirstChildWhichIsA("Tool"):FindFirstChild("Ammo") and Client.Character:FindFirstChildWhichIsA("Tool"):FindFirstChild("Ammo").Value <= 0 then
                        local mainRemote = game:GetService("ReplicatedStorage"):FindFirstChild(Celex.Remote);
                        mainRemote:FireServer("Reload", Client.Character:FindFirstChildWhichIsA("Tool"))
                    end
                end))

                Celex:ThreadFunction(LPH_NO_VIRTUALIZE(function()
                    if getgenv().Celex["Misc"]['Auto Settings']['Force Mute Boombox'] then
                        for _, Value in pairs(Celex:GetPlayers()) do
                            if Value.Name ~= Client.Name then
                                pcall(function()
                                    if Value.Character:FindFirstChild('LowerTorso'):FindFirstChild('BOOMBOXSOUND').Playing then
                                        Value.Character:FindFirstChild('LowerTorso'):FindFirstChild('BOOMBOXSOUND'):Stop();
                                    end;
                                end);
                            end;
                        end;
                    end
                end));

                Celex:ThreadFunction(LPH_NO_VIRTUALIZE(function()
                    if getgenv().Celex['Silent'].Type ~= 'Safe' and Celex.Locals.SilentAim_Targ ~= nil then
                        local HitPosition, CurrentTarget = Celex:GetHitPosition("Silent")
                        --
                        Celex.Locals.SilentTarg_Pos = HitPosition
                    end
                end));

                local HitPosition, CurrentTarget = Celex:GetHitPosition("Silent")

    
                if (Tick - Celex.Ping.Tick) >= 0.15 then
                    Celex.Ping.Tick = Tick
                    --
                    Celex:UpdatePing()
                end
            end
            --
            local Cameras = require(Client.PlayerScripts.PlayerModule):GetCameras()
            local Controller = Cameras.activeCameraController
            --
            function Celex:InputLoop(textbox)
                if not textbox then
                    if getgenv().Celex["Safety"]["Panic Key"].Enabled and self.KeyCode == Enum.KeyCode[getgenv().Celex["Safety"]["Panic Key"]["Key_1"]:upper()] and UserInputService:IsKeyDown(Enum.KeyCode[getgenv().Celex["Safety"]["Panic Key"]["Key_2"]:upper()]) then
                        Celex:Unload()
                    elseif getgenv().Celex["Safety"]["Hide Visuals"].Enabled and self.KeyCode == Enum.KeyCode[getgenv().Celex["Safety"]["Hide Visuals"]["Key_1"]:upper()] and UserInputService:IsKeyDown(Enum.KeyCode[getgenv().Celex["Safety"]["Hide Visuals"]["Key_2"]:upper()]) then
                        Celex.Locals.HideVisuals = not Celex.Locals.HideVisuals
                    elseif getgenv().Celex["Macro"].Enabled and getgenv().Celex["Macro"].BypassMacroAbuse and getgenv().Celex["Macro"].Type ~= "First" and getrenv()._G.HoldGunBool and self.KeyCode == Enum.KeyCode["I"] then
                        Controller:SetCameraToSubjectDistance(Controller.currentSubjectDistance - 5);
                    elseif getgenv().Celex["Macro"].Enabled and getgenv().Celex["Macro"].BypassMacroAbuse and getgenv().Celex["Macro"].Type ~= "First" and getrenv()._G.HoldGunBool and self.KeyCode == Enum.KeyCode["O"] then
                        Controller:SetCameraToSubjectDistance(Controller.currentSubjectDistance + 5);
                    elseif getgenv().Celex["Macro"].Enabled and getgenv().Celex["Macro"].Type == "First" and getrenv()._G.HoldGunBool and self.KeyCode == Enum.KeyCode["I"] then
                        Controller:SetCameraToSubjectDistance(Controller.currentSubjectDistance - 0.6);
                    elseif getgenv().Celex["Macro"].Enabled and getgenv().Celex["Macro"].Type == "First" and getrenv()._G.HoldGunBool and self.KeyCode == Enum.KeyCode["O"] then
                        Controller:SetCameraToSubjectDistance(Controller.currentSubjectDistance + 0.6);
                    elseif getgenv().Celex["Macro"].Enabled and self.KeyCode == Enum.KeyCode[getgenv().Celex["Macro"].Keybind:upper()] then
                        Celex.Locals.Macro = not Celex.Locals.Macro
    
                        repeat
                            game:GetService("RunService").Heartbeat:wait()
                            keypress(73)
                            game:GetService("RunService").Heartbeat:wait()
                            keypress(79)
                            game:GetService("RunService").Heartbeat:wait()
                            keyrelease(73)
                            game:GetService("RunService").Heartbeat:wait()
                            keyrelease(79)
                            game:GetService("RunService").Heartbeat:wait()
                        until not Celex.Locals.Macro
                    elseif getgenv().Celex["Macro"]["Noclip_Macro"].Enabled and self.KeyCode == Enum.KeyCode[getgenv().Celex["Macro"]["Noclip_Macro"].Keybind:upper()] then
                        Celex.Locals.Noclip_Macro = not Celex.Locals.Noclip_Macro
                        
                        repeat
                            if Client.Backpack:FindFirstChild(tostring(getgenv().Celex["Macro"]["Noclip_Macro"]["Gun"])) then
                                Client.Character.Humanoid:EquipTool(Client.Backpack:FindFirstChild(tostring(getgenv().Celex["Macro"]["Noclip_Macro"]["Gun"])))
                                task.wait(0.1)
                                Client.Character.Humanoid:UnequipTools()
                            end
                            task.wait(0.1)
                        until not Celex.Locals.Noclip_Macro
                    elseif getgenv().Celex["FakeSpike"].Enabled and self.KeyCode == Enum.KeyCode[getgenv().Celex["FakeSpike"].Keybind:upper()] then
                        Network.IncomingReplicationLag = getgenv().Celex["FakeSpike"].Ammount
                        task.wait(1.5)
                        Network.IncomingReplicationLag = 0
                    elseif getgenv().Celex["Sorting"].Enabled and self.KeyCode == Enum.KeyCode[getgenv().Celex["Sorting"].Keybind] then
                        Celex:SortInventory()
                    elseif getgenv().Celex["Assist"].Enabled and not getgenv().Celex['Universal']['Use One Key For Silent & Assist'] and self.KeyCode == Enum.KeyCode[getgenv().Celex["Assist"].Keybind:upper()] then
                        if Celex.Locals.AimAssist_Targ then
                            Celex.Locals.AimAssist_Targ = nil
                        else
                            Celex.Locals.AimAssist_Targ = Celex:GetClosestTarget(getgenv().Celex["Assist"]["HitParts"], "Assist")
                        end
                    elseif getgenv().Celex["Silent"].Enabled and not getgenv().Celex['Universal']['Use One Key For Silent & Assist'] and getgenv().Celex["Silent"]["Mode"] == "Target" and self.KeyCode == Enum.KeyCode[getgenv().Celex["Silent"].Keybind:upper()] then
                        if Celex.Locals.SilentAim_Targ then
                            Celex.Locals.SilentAim_Targ = nil
                        else
                            Celex.Locals.SilentAim_Targ = Celex:GetClosestTarget(getgenv().Celex["Silent"]["HitParts"], "Silent")
                            if getgenv().Celex["Silent"]["Notify On Lock"] then
                                if Celex.Locals.SilentAim_Targ ~= nil then
                                    game:GetService("StarterGui"):SetCore("SendNotification",{Title = "Celex", Text = "Locked onto "..Celex.Locals.SilentAim_Targ.Name, Icon = "rbxassetid://14664523619"})
                                end
                            end
                        end
                    elseif getgenv().Celex['Universal']['Use One Key For Silent & Assist'] and self.KeyCode == Enum.KeyCode[getgenv().Celex['Universal'].BothKey:upper()] then
                        if getgenv().Celex["Silent"].Enabled and getgenv().Celex["Silent"]["Mode"] == "Target" then
                            if Celex.Locals.SilentAim_Targ then
                                Celex.Locals.SilentAim_Targ = nil
                            else
                                Celex.Locals.SilentAim_Targ = Celex:GetClosestTarget(getgenv().Celex["Silent"]["HitParts"], "Silent")
                                if getgenv().Celex["Silent"]["Notify On Lock"] then
                                    if Celex.Locals.SilentAim_Targ ~= nil then
                                        game:GetService("StarterGui"):SetCore("SendNotification",{Title = "Celex", Text = "Locked onto "..Celex.Locals.SilentAim_Targ.Name, Icon = "rbxassetid://14664523619"})
                                    end
                                end
                            end
                        end

                        if getgenv().Celex["Assist"].Enabled then
                            if Celex.Locals.AimAssist_Targ then
                                Celex.Locals.AimAssist_Targ = nil
                            else
                                Celex.Locals.AimAssist_Targ = Celex:GetClosestTarget(getgenv().Celex["Assist"]["HitParts"], "Assist")
                            end
                        end

                    elseif getgenv().Celex["Misc"]["360 Bind"].Enabled and self.KeyCode == Enum.KeyCode[getgenv().Celex["Misc"]["360 Bind"].Keybind:upper()] then
                        if Celex.Locals.IsD360 then
                            return
                        end

                        local oldSmoothing = getgenv().Celex["Assist"]['Smoothing Ammount']
                        local oldInAirSmoothing = getgenv().Celex["Assist"]['In Air Smoothing']
                        local oldPos = Workspace.CurrentCamera.CFrame

                        getgenv().Celex["Assist"]['Smoothing Ammount'] = 0.00001
                        getgenv().Celex["Assist"]['In Air Smoothing'] = 0.00001

                        Celex:ThreadFunction(function()
                            Celex.Locals.IsD360 = true
                            wait(0.3)
                            getgenv().Celex["Assist"]['Smoothing Ammount'] = oldSmoothing
                            getgenv().Celex["Assist"]['In Air Smoothing'] = oldInAirSmoothing
                            Celex.Locals.IsD360 = false
                            Workspace.CurrentCamera.CFrame = oldPos
                        end)
                        
                        Celex:ImportConnection(RunService.Heartbeat, LPH_NO_VIRTUALIZE(function() -- // Main Loops
                            if Celex.Locals.IsD360 then
                                -- // YO BIG DAW WHAT U LOOKIN AT?? 
                                local CurrentTime = tick()
                                local TimeDelta = Min(CurrentTime - Celex.Locals.LastRenderTime, 0.01)
                                Celex.Locals.LastRenderTime = CurrentTime
                                local Rotation = CFrame.fromAxisAngle(Vector3.new(0, 1, 0), Rad(2500 * TimeDelta))
                                Workspace.CurrentCamera.CFrame =  Workspace.CurrentCamera.CFrame * Rotation
                                Celex.Locals.TotalRotation = Celex.Locals.TotalRotation + Rad(2500 * TimeDelta)
                                if Celex.Locals.TotalRotation >= Celex.Locals.FullCircleRotation then
                                    Celex.Locals.TotalRotation = 0
                                end
                            end
                        end))
                    end
                end
            end
        end)()
    end

    do -- Luas
        Luas.Games = {
            [{1008451066}] = {Name = "Da Hood", Arguement = "UpdateMousePos", Remote = "MainEvent"},
            [{1958807588}] = {Name = "Hood Modded", Arguement = "MousePos", Remote = "Bullets", Functions = {
                Knocked = function(Object)
                    local BodyEffects = Object:FindFirstChild("I_LOADED_I")
                    local Knocked = (BodyEffects and BodyEffects:FindFirstChild("K.O"))
                    --
                    return (Knocked and Knocked.Value)
                end
            }},
            [{4979718131}] = {Name = "Da Fights Downhill 2", Arguement = "MOUSE", Remote = "MAINEVENT"},
            [{3985694250}] = {Name = "1v1 Hood Aim Trainer", Arguement = "UpdateMousePos", Remote = "MainEvent"},
            -- NOT FINISHED BELOW --
            [{4487113227}] = {Name = "Da Hood Aim Trainer", Arguement = "UpdateMousePos", Functions = {
                Knocked = function(Object)
                    local BodyEffects = Object:FindFirstChild("BodyEffects")
                    local Knocked = (BodyEffects and BodyEffects:FindFirstChild("KO"))
                    --
                    return (Knocked and Knocked.Value)
                end
            }},
            [{3445639790}] = {Name = "Untitled Hood", Arguement = "UpdateMousePos"},
            [{4187972171}] = {Name = "Kat Hood", Arguement = "UpdateMousePos", Func = function(Arguements, Position)
                Arguements[2].MousePos = Position
            end},
            [{2647212019}] = {Name = "Dah Hood", Arguement = "UpdateMousePos", Func = function(Arguements, Position)
                Arguements[2].MousePos = Position
            end},
            [{4417220740}] = {Name = "Da Fights Downhill", Arguement = "UpdateMousePos", Remote = "MAINEVENT", Func = function(Arguements, Position)
                Arguements[2].MousePos = Position
            end},
         
        }
        --
        for Index, Value in pairs(Luas.Games) do
            if Find(Index, game.GameId) then
                if Value.Arguement or Value.Remote or Value.Func then
                    Celex.Arguement = Value.Arguement
                    Celex.Remote = Value.Remote
                    Celex.Func = Value.Func
                end
                --
                if Value.Functions then
                    for Index, Value in pairs(Value.Functions) do
                        Celex[Index] = Value
                    end
                end
            end
        end
    end
end

-- // Main
local NameCall

if Celex.Arguement or Celex.Remote then
    NameCall = hookmetamethod(game, "__namecall", LPH_NO_VIRTUALIZE(function(Self, ...)
        local Arguements = {...}
        local Method = getnamecallmethod()
        
        if Method == "FireServer" and Celex.Locals.SilentAim_Targ then
            if getgenv().Celex['Silent'].Type ~= 'Safe' and not (Celex.Arguement and not (Arguements[1] == Celex.Arguement)) and not (Celex.Remote and not (tostring(Self) == Celex.Remote)) then
                if Celex.Func then
                    Celex.Func(Arguements, Celex.Locals.SilentTarg_Pos)
                else
                    Arguements[2] = Celex.Locals.SilentTarg_Pos
                end

                return NameCall(Self, Unpack(Arguements))
            end
        end 

        return NameCall(Self, ...)
    end))
end

-- // Main
Celex:ThreadFunction(function() -- // Memory Spoofer
    local Memory = {
        Current = tonumber(math.random(getgenv().Celex["Universal"]["Memory Spoofer"].MinimumRange, getgenv().Celex["Universal"]["Memory Spoofer"].MaxRange) .. "." .. tostring(math.random(10, 99))),
        Base = math.random(getgenv().Celex["Universal"]["Memory Spoofer"].MinimumRange, getgenv().Celex["Universal"]["Memory Spoofer"].MaxRange),
        History = {},
        Display = tonumber(math.random(getgenv().Celex["Universal"]["Memory Spoofer"].MinimumRange, getgenv().Celex["Universal"]["Memory Spoofer"].MaxRange) .. "." .. tostring(math.random(10, 99)))
    }

    local getAverageMemory = function()
        local Average = 0
        for i, v in pairs(Memory.History) do
            Average += v
        end
        return Average / # Memory.History
    end

    local getNewMemory = function()
        local random, random_chance = math.random(1, 3), math.random(1, 3)
        if random == 1 or random == 2 then
            if random_chance == 3 and tonumber(Memory.Current) ~= nil then
                Memory.Current = tostring(math.floor(tonumber(Memory.Current)) .. "." .. math.random(10, 99))
            else
                Memory.Current = tostring(math.random(Memory.Base - 4, Memory.Base + 3)) .. "." .. tostring(math.random(10, 99))
            end
            if # Memory.History == 10 then
                Remove(Memory.History, 10)
            end
            Insert(Memory.History, tonumber(Memory.Current))
        end
        return Memory.Current
    end

    local MemoryViewer = nil

    repeat wait() until game:GetService("CoreGui"):FindFirstChild("RobloxGui"):FindFirstChild("PerformanceStats")

    LPH_JIT_MAX(function()
        for Index, Value in pairs(game:GetService("CoreGui").RobloxGui.PerformanceStats:GetChildren()) do
            if Value.Name == "PS_Button" then

                local valueLabel = Value.StatsMiniTextPanelClass.ValueLabel;

                if Value.StatsMiniTextPanelClass.TitleLabel.Text == "Mem" then
                    Celex:ImportConnection(valueLabel:GetPropertyChangedSignal("Text"), function()
                        LPH_JIT_MAX(function()
                            if getgenv().Celex["Universal"]["Memory Spoofer"].Enabled then
                                valueLabel.Text = Memory.Display .. " MB"
                            end
                        end)()
                    end)

                    MemoryViewer = valueLabel
                end
                --
                if Value.StatsMiniTextPanelClass.TitleLabel.Text == "Ping" then
                    Celex:ImportConnection(valueLabel:GetPropertyChangedSignal("Text"), function()
                        if getgenv().Celex["Universal"]["Memory Spoofer"].Enabled then
                            if MemoryViewer ~= nil then
                                local New = getNewMemory()
                                Memory.Display = tostring(New)
                                MemoryViewer.Text = New .. " MB"
                            end
                        end
                    end)
                end
            end
        end
    end)()
    --
    Celex:ImportConnection(RunService.Heartbeat, LPH_JIT_MAX(function()
        if getgenv().Celex["Universal"]["Memory Spoofer"].Enabled then
            local s, e = pcall(function()
                if game:GetService("CoreGui").RobloxGui.PerformanceStats["PS_Viewer"].Frame.TextLabel.Text == "Memory" then
                    for Index, Value in pairs(game:GetService("CoreGui").RobloxGui.PerformanceStats["PS_Viewer"].Frame:GetChildren()) do
                        if Value.Name == "PS_DecoratedValueLabel" and string.find(Value.Label.Text, 'Current') then
                            Value.Label.Text = "Current: " .. Memory.Current .. " MB"
                        end
                        if Value.Name == "PS_DecoratedValueLabel" and string.find(Value.Label.Text, 'Average') then
                            Value.Label.Text = "Average: " .. string.sub(getAverageMemory(), 1, 6) .. " MB"
                        end
                    end
                end
            end)
            pcall(function()
                game:GetService("CoreGui").DevConsoleMaster.DevConsoleWindow.DevConsoleUI.TopBar.LiveStatsModule["MemoryUsage_MB"].Text = math.round(tonumber(Memory.Current)) .. " MB"
            end)
        end
    end))
end)

-- // Main Loop
Celex:ImportConnection(RunService.Heartbeat, LPH_NO_VIRTUALIZE(function(deltaTime)
    Celex:ThreadFunction(function()
        for Index, Value in pairs(Visuals.Bases) do
            Value:Update()
        end
    end);
    
    Celex:ThreadFunction(function()
        Visuals:UpdateFieldOfView()
        Visuals:Update()
    end);

    Celex:ThreadFunction(function()
        Celex:MainLoop()
    end)
end))

Celex:ImportConnection(Client.CharacterAdded, LPH_NO_VIRTUALIZE(function(Character) -- // Silent Aim Connection
    Celex:CharacterAddedEvent(Character) 
end))

if Client.Character then -- Setup Silent Aim Connection
    Celex:CharacterAddedEvent(Client.Character); 
end

Celex:ImportConnection(UserInputService.InputBegan, Celex.InputLoop); -- // Main Input Handler

Celex:ImportConnection(Players.PlayerAdded, LPH_NO_VIRTUALIZE(function(Player) 
    Celex:OnPlayerAdded(Player) 
end))

Celex:ImportConnection(Players.ChildAdded, LPH_NO_VIRTUALIZE(function(Child) -- // Setup Visuals on player added
    Celex:PlayerValid(Child, function(Validated) 
        Celex:PlayerAdded(Validated) 
    end)
end))

Celex:ThreadFunction(function() -- // Intro
    if getgenv().Celex["Preload"]["Intro"] then
        Celex:Intro()
    end
end)

LPH_JIT_MAX(function()
    for Index, Player in pairs(Celex:GetPlayers()) do 
        Celex:OnPlayerAdded(Player) 
    
        Celex:PlayerValid(Player, LPH_NO_VIRTUALIZE(function(Validated) -- // Visuals
            Celex:PlayerAdded(Validated);
        end));
    end    
end)()

-- // Staff Join Protection
if getgenv().Celex["Safety"]["Leave On Staff Join"] then
    LPH_NO_VIRTUALIZE(function()
        for _, player in ipairs(Celex:GetPlayers()) do
            Celex:CheckStaff(player)
        end
    end)()

    Celex:ImportConnection(Players.PlayerAdded, LPH_NO_VIRTUALIZE(function(player)
            player.CharacterAdded:Wait()
            Celex:CheckStaff(player)
    end))
end

-- // FPS Booster
if getgenv().Celex["Misc"]["FPS Boost"] then
    setfpscap(5000)

    game.DescendantAdded:Connect(function(Descendant)
      if Descendant.Name == "MainView" and Descendant.Parent.Name == "DevConsoleUI" then
          task.wait()
          Descendant.Parent.Parent.Parent.Enabled = false;
      end
    end);

    VirtualInputManager:SendKeyEvent(true, "F9", 0, game)    
    wait()
    VirtualInputManager:SendKeyEvent(false, "F9", 0, game)  

    local counter = 0
    RunService.RenderStepped:Connect(function()
        warn('')
        print('')
        counter = counter + 1
        
        if not game:GetService("CoreGui"):FindFirstChild("DevConsoleUI", true):FindFirstChild("MainView") then
            VirtualInputManager:SendKeyEvent(true, "F9", 0, game)    
            wait()
            VirtualInputManager:SendKeyEvent(false, "F9", 0, game)  
        end
    end)
end
