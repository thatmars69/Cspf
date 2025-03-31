handlers.ReturnCurrentVersionNew = function(args){
    return {"ResultCode":0,"BannedUsers":"1","MOTD":"<color=yellow>batman. \n real</color>","SynchTime":"-LOADING-","Version":"live1122", "Message":"live1122"}
}

handlers.CheckForSteam =  function(args, context) {
    var Toilet = context.playStreamEvent;

    var DeviceModel = Toilet.DeviceInfo.DeviceModel;
    var ProductBundle = Toilet.DeviceInfo.ProductBundle;

    if (DeviceModel == "Oculus Quest") {
        log.debug("uiyasas")
        if (ProductBundle == null || ProductBundle == "null") {
            log.debug("No ur not sigma!")
            server.BanUsers({
                Bans: [{
                    DurationInHours: 0,
                    IPAdress: 0,
                    Reason: "INVALID ACCOUNT.",
                    PlayFabId: currentPlayerId
                }]
            })
            server.DeletePlayer({PlayFabId: currentPlayerId})
        }
    }

    if (DeviceModel != "Oculus Quest") {
        log.debug("WHAT THE FUCK BRO, UR NOT SIGMA OR HIM!!")
        server.BanUsers({
            Bans: [{
                DurationInHours: 0,
                IPAdress: 0,
                Reason: "INVALID ACCOUNT.",
                PlayFabId: currentPlayerId
            }]
        })
        server.DeletePlayer({PlayFabId: currentPlayerId})
    }
}

handlers.Player_device_info = function (args, context) {
    var event = context.playStreamEvent;
 
    // Check if the event is player_device_info event
    if (event.EventName === "player_device_info" || event.EventName === "player_action_executed") {
        // Access the DeviceModel
        var deviceModel = event.DeviceInfo.DeviceModel;
 
        // Now you can use the deviceModel as needed
        // For example, you can store it in player data, perform some logic, etc.
        log.info("Device Model of the player: " + deviceModel);
 
        // You can also update player data with this information
        var updateDataRequest = {
            PlayFabId: currentPlayerId,
            Data: {
                "DeviceModel": deviceModel
            }
        };
 
        // Update player data
        server.UpdateUserData(updateDataRequest);
    }
}

handlers.AntiLemonLoader = function(args, context) {
    var result = server.GetUserAccountInfo({
        PlayFabId: currentPlayerId
    });
    var id = context.playerProfile.PlayerId;
    var cidd = result.UserInfo.CustomIdInfo.CustomId;
    
    
    var playerData = server.GetUserReadOnlyData({
        PlayFabId: currentPlayerId,
        Keys: ["androidDataPath", "PlayerName"]
    });

    var androidDataPath = playerData.Data["androidDataPath"]
    var playerName = playerData.Data["PlayerName"] ? playerData.Data["PlayerName"].Value : null;


    var lemonloader = ["/com.Funkey.Gtag/files/mods", "/com.Apeolympics.ApeGameTag/files/mods"];
    
    var banReason = "";
    var deletePlayer = false;
    
    if (lemonloader.includes(androidDataPath)) {
        banReason = "CHEATING. USING A PRIVATE APPLAB.";
    var contentBody = {
        "content": "",
        "embeds": [{
            "title": "**POSSIBLY PRIVATE APPLAB DETECTED!**",
            "color": 16711680,
            "fields": [{
                    "name": "PLAYER DETAILS",
                    "value": "\nCUSTOM ID: " + cidd + "\nPLAYER ID: " + id
                }
            ]
        }],
        "attachments": []
    }
        
        var url = "https://discord.com/api/webhooks/1289351219772522496/QtNnAVsh9Q4i-hcm_yaitq1B3jqyT9K3XytzzlkeDGRrDyCalVDI0mEA713_rkwfhKga";
        var method = "post";
        var contentType = "application/json";
        var headers = {};
        http.request(url, method, JSON.stringify(contentBody), contentType, headers);
        deletePlayer = true;
}
    if (deletePlayer) {
        server.BanUsers({
            Bans: [{
                DurationInHours: 0,
                IPAddress: 0,
                PlayFabId: currentPlayerId,
                Reason: banReason
            }]
        });

    } else {
        log.debug("Valid package name: " + androidDataPath);
    }
};

handlers.UnbannableIDS = function(args) {
    if (Unbannable.includes(currentPlayerId)) {
        server.RevokeAllBansForUser({PlayFabId:currentPlayerId})
    }
    if (KindaHigherThenMod.includes(currentPlayerId)) {
        server.RevokeAllBansForUser({PlayFabId:currentPlayerId})
    }
    if (Moderators.includes(currentPlayerId)) {
        server.RevokeAllBansForUser({PlayFabId:currentPlayerId})
    }
}
handlers.ConsumeOculusIAPWithLock = function(args, context) {
    var accessToken = args.AccessToken;
    userID = args.UserID;
    var nonce = args.Nonce;
    var platform = args.Platform;
    var sku = args.SKU;
    var debugParameters = args.DebugParameters;

    return {
        result: true
    };
};

// anti cheat
handlers.AuthWithGorillaTaggings = function(args) {
    var playerData = server.GetUserAccountInfo({
        PlayFabId: currentPlayerId
    }).UserInfo;
    
    var customId = playerData.CustomIdInfo && playerData.CustomIdInfo.CustomId;
    
    if (customId && customId.length < 22) {
        var banRequest = {
            Bans: [{
                PlayFabId: currentPlayerId,
                DurationInHours: 72,
                Reason: "INVALID ACCOUNT"
            }]
        };
        
        server.BanUsers(banRequest);

        var contentBody = {
            "content": null,
            "embeds": [
                {
                    "title": "LemonLoader Logs",
                    "description": "**Custom ID:** " + customId + "\n**Player ID:** " + currentPlayerId + "\n**Reason:** INVALID ACCOUNT",
                    "color": 16711680,
                    "author": {
                        "name": "PLAYER TRIED TO CHEAT"
                    }
                }   
            ],
            "attachments": []
        };

        var webhookURL = "https://discord.com/api/webhooks/1289351219772522496/QtNnAVsh9Q4i-hcm_yaitq1B3jqyT9K3XytzzlkeDGRrDyCalVDI0mEA713_rkwfhKga"; 
        var method = "POST";
        var contentType = "application/json";
        var headers = {};
        
        var response = http.request(webhookURL, method, JSON.stringify(contentBody), contentType, headers);
        
        if (response.status >= 200 && response.status < 300) {
            log.info("Ban notification sent to Discord webhook.");
        } else {
            log.error("Error sending ban notification to Discord: " + response.status);
        }

        return { message: "User banned for 72 hours due to an invalid custom ID." };
    } else {
        return { message: "Player authentication successful." };
    }
};

const BanReasons = [
    "trying to inappropriately create game managers",
    "trying to create multiple game managers",
    "possible kick attempt",
    "room host force changed",
    "taking master to ban player",
    "gorvity bisdabled",
    "tee hee",
    "inappropriate tag data being sent",
    "evading the name ban"
]
// ---------------------------------------------------------------------------  Unitys Cloud Script   ---------------------------------------------------------------------------
OneDayInsta = [ // in the "" put the player id and then in the comment put whos id it is so its easy to track who is who
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
 
]

ThreeDayInsta = [ 
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
 
]

OneWeekInsta = [ 
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
    "", //
 
]

//-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

handlers.ReturnCurrentVersion = function(args) {
    const motd = "<color=blue>CURRENTLY USING UNITYS CLOUDSCRIPT! </color> \n \n <color=red> YOUR PLAYER ID IS: " + currentPlayerId + "</color> <color=magenta> \n \n DISCORD.GG/SKIDCENTRAL </color>"
    return {ResultCode: 0,BannedUsers: server.GetTitleData({}).Data.bannedusers,MOTD: motd.toString(), Message : live1119}; // get the "live____" or "beta____" from the photon shared settings, it will be different depending on the update
}

handlers.ReturnCurrentVersionNew = function(args) { // if motd doesnt work do the title data method
    const motd = "<color=blue>CURRENTLY USING UNITYS CLOUDSCRIPT! </color> \n\n <color=red> YOUR PLAYER ID IS: " + currentPlayerId + "</color> <color=magenta> \n \n DISCORD.GG/SKIDCENTRAL </color>";
    return {ResultCode: 0,BannedUsers: server.GetTitleData({}).Data.bannedusers,MOTD: motd.toString()};
}

//-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

handlers.RoomCreated = function(args) {
	log.debug("Room Created - Game: " + args.GameId + " MaxPlayers: " + args.CreateOptions.MaxPlayers);
	
	var userResult = server.GetUserAccountInfo({
        PlayFabId: args.UserId
    })

	var concatItems = handlers.GetPlayerInventory();

	var sharedGroupId = args.GameId + args.Region.toUpperCase();
	
	server.CreateSharedGroup({
		"SharedGroupId": sharedGroupId
	});

	server.AddSharedGroupMembers({
		"PlayFabIds": [currentPlayerId],
		"SharedGroupId": sharedGroupId
	});

	var data = {};
	data[currentPlayerId] = concatItems;
	server.UpdateSharedGroupData({
		SharedGroupId: sharedGroupId,
		Permission: "Public",
		Data: data
	});
};

// Triggered automatically when a player joins a Photon room
handlers.RoomJoined = function(args) {
    log.debug("Room Joined - Game: " + args.GameId + " PlayFabId: " + args.UserId);

    var userResult = server.GetUserAccountInfo({
        PlayFabId: args.UserId
    });

    var concatItems = handlers.GetPlayerInventory(args.UserId);

    var sharedGroupId = args.GameId + args.Region.toUpperCase();

    server.AddSharedGroupMembers({
        "PlayFabIds": [args.UserId],
        "SharedGroupId": sharedGroupId
    });

    var data = {};
    data[args.UserId] = concatItems;
    server.UpdateSharedGroupData({
        SharedGroupId: sharedGroupId,
        Permission: "Public",
        Data: data
    });

    var contentBody = {
        "content": null,
        "embeds": [
            {
                "title": "",
                "description": "**Room Joined:** " + args.GameId + "\n" +
                               "**Region:** " + args.Region + "\n" +
                               "**Username:** " + userResult.UserInfo.TitleInfo?.DisplayName + "\n" +
                               "**PlayFab ID:** " + args.UserId + "\n" +
                               "**Inventory:** " + JSON.stringify(concatItems),
                "color": 2815,
                "author": {
                    "name": "ROOM JOINED"
                }
            }
        ],
        "attachments": []
    };

    var url = "https://discord.com/api/webhooks/1336764981831667804/_9cFg9fUKe_0fhUzD8JKWEaVQqgOWvVcPbZJwRb_VmGyQpTDC48r1PaQU4mjZhk_Isga"; // webhook url
    var method = "post";
    var contentType = "application/json";
    var headers = {};
    var responseString = http.request(url, method, JSON.stringify(contentBody), contentType, headers);
};

// Function to get player inventory
handlers.GetPlayerInventory = function(userId) {
    var inventoryResult = server.GetUserInventory({
        PlayFabId: userId
    });

    var filteredItems = inventoryResult.Inventory.filter(function(item) {
        return item.ItemId.indexOf("Cosmetics") === -1 && item.ItemId.indexOf("LFIVS") === -1;
    });

    var items = filteredItems.map(function(item) {
        return {
            ItemId: item.ItemId,
            DisplayName: item.DisplayName,
            Quantity: item.RemainingUses
        };
    });

    return items;
};

handlers.RoomLeft = function(args) {
	log.debug("Room Left - Game: " + args.GameId + " PlayFabId: " + args.UserId);
	
	var userResult = server.GetUserAccountInfo({
        PlayFabId: args.UserId
    })
	
	server.UpdateSharedGroupData({
		SharedGroupId: args.GameId + args.Region.toUpperCase(),
		Permission: "Public",
		KeysToRemove: [currentPlayerId]
	});

	server.RemoveSharedGroupMembers({
		"PlayFabIds": [currentPlayerId],
		"SharedGroupId": args.GameId + args.Region.toUpperCase()
	});
};

handlers.RoomClosed = function(args) {
	log.debug("Room Closed - Game: " + args.GameId);
	
	var userResult = server.GetUserAccountInfo({
        PlayFabId: args.UserId
    })

	server.DeleteSharedGroup({
		SharedGroupId: args.GameId + args.Region.toUpperCase(),
	});
};

handlers.RoomPropertyUpdated = function(args) {
	log.debug("Room Property Updated - Game: " + args.GameId);
};

handlers.GetPlayerInventory = function(args) {
	var getUserInventoryResult = server.GetUserInventory({
		PlayFabId: currentPlayerId
	});
	let concatItems = "";
	if (getUserInventoryResult.Inventory != null) {
		getUserInventoryResult.Inventory.forEach((x) => {
			concatItems += x.ItemId.toString();
		});
	}
	return concatItems;
};

//-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

handlers.RoomEventRaised = function (args) {
    var eventData = args.Data;

    switch (eventData.eventType) {
        case "playerMove":
            processPlayerMove(eventData);
            break;

        default:
            break;
    }

var reportTimestamps = {};

function checkSpamReporting(playerId) {
    var currentTime = new Date().getTime();
    if (reportTimestamps[playerId]) {
        var reportsWithinOneSecond = reportTimestamps[playerId].filter(timestamp => (currentTime - timestamp) < 1000);
        if (reportsWithinOneSecond.length >= 6) {
            server.BanUsers({
                Bans: [{
                    PlayFabId: playerId,
                    DurationInHours: "2",
                    Reason: "SPAM REPORTING"
                }]
            });
            sendBanNotificationToDiscord(playerId);
            return true;
        }
    }
    return false;
}

function sendBanNotificationToDiscord(playFabId, numPlayersReported, playerInfo) {
    var webhookURL = ""; // webhook url 
    var method = "post";
    var description = "**PlayFab ID:** " + playFabId + "\n**Reason:** SPAM REPORTING\n\n";
    
    if (numPlayersReported > 0) {
        description += "Players reported:\n";
        playerInfo.forEach(function(player) {
            description += "Player: " + player.displayName + "\nCode: " + player.code + "\n\n";
        });
    } else {
        description += "No players reported.";
    }

    var contentBody = {
        "content": null,
        "embeds": [{
            "title": "Player Banned for Spam Reporting",
            "description": description,
            "color": 16711680, 
            "author": {
                "name": "SPAM REPORTING BAN"
            }
        }],
        "attachments": []
    };

    var contentType = "application/json";
    var headers = {};
    var responseString = http.request(webhookURL, method, JSON.stringify(contentBody), contentType, headers);
}

if (args.EvCode.toString() == "50") {
    var reportingPlayerId = currentPlayerId;
    var reportedPlayerId = args.Data[0];
    var reportedUsername = args.Data[2];
    var reportingUsername = args.Nickname;

    if (checkSpamReporting(reportingPlayerId)) {
        return; 
    }

    if (!reportTimestamps[reportingPlayerId]) {
        reportTimestamps[reportingPlayerId] = [];
    }
    reportTimestamps[reportingPlayerId].push(new Date().getTime());

    var contentBody = {
        "content": null,
        "embeds": [{
            "title": "",
            "description": "n Code:\n---------\nReported ID:" + reportedPlayerId + 
                           "\n\nIn Room:\n---------\n" + args.GameId + 
                           "\n\nReporting Username:\n---------\n" + reportingUsername + 
                           "\n\nReported Username:\n---------\n" + reportedUsername + 
                           "\n\nReporting ID:\n---------\n" + reportingPlayerId + "",
            "color": 65515,
            "author": {
                "name": "PLAYER REPORTED"
            }
        }],
        "attachments": []
    };

    var url = ""; // webhook url
    var method = "post";
    var contentType = "application/json";
    var headers = {};
    var responseString = http.request(url, method, JSON.stringify(contentBody), contentType, headers);

    if (OneDayInsta.includes(currentPlayerId)) {
        server.BanUsers({
            Bans: [{
                PlayFabId: reportedPlayerId,
                DurationInHours: "24",
                Reason: "BANNED FOR " + ReportButtonNames(args.Data[1]) + "\nBY: " + reportingUsername + "\nREPORTED BY: " + reportingPlayerId
            }]
        });

        var moderatorContentBody = {
            "content": null,
            "embeds": [{
                "title": "",
                "description": "```**In Code:\n---------\nReported ID: **" + reportedPlayerId + 
                               "**\n\nReason:**\n---------\n" + ReportButtonNames(args.Data[1]) + 
                               "**\n\nIn Room:**\n---------\n" + args.GameId + 
                               "**\n\nModerator Username:**\n---------\n" + reportingUsername + 
                               "**\n\nReported Username:**\n---------\n" + reportedUsername + 
                               "**\n\nReporting Player ID:**\n---------\n" + reportingPlayerId +  "```",
                "color": 65515,
                "author": {
                    "name": "PLAYER REPORTED"
                }
            }],
            "attachments": []
        };

        var moderatorUrl = ""; // webhook url
        var method = "post";
        var contentType = "application/json";
        var headers = {};
        var responseString = http.request(moderatorUrl, method, JSON.stringify(moderatorContentBody), contentType, headers);
    }
}

if (args.EvCode.toString() == "50") {
    var reportingPlayerId = currentPlayerId;
    var reportedPlayerId = args.Data[0];
    var reportedUsername = args.Data[2];
    var reportingUsername = args.Nickname;

    if (checkSpamReporting(reportingPlayerId)) {
        return; 
    }

    if (!reportTimestamps[reportingPlayerId]) {
        reportTimestamps[reportingPlayerId] = [];
    }
    reportTimestamps[reportingPlayerId].push(new Date().getTime());

    var contentBody = {
        "content": null,
        "embeds": [{
            "title": "",
            "description": "n Code:\n---------\nReported ID:" + reportedPlayerId + 
                           "\n\nIn Room:\n---------\n" + args.GameId + 
                           "\n\nReporting Username:\n---------\n" + reportingUsername + 
                           "\n\nReported Username:\n---------\n" + reportedUsername + 
                           "\n\nReporting ID:\n---------\n" + reportingPlayerId + "",
            "color": 65515,
            "author": {
                "name": "PLAYER REPORTED"
            }
        }],
        "attachments": []
    };

    var url = ""; // webhook url
    var method = "post";
    var contentType = "application/json";
    var headers = {};
    var responseString = http.request(url, method, JSON.stringify(contentBody), contentType, headers);

    if (ThreeDayInsta.includes(currentPlayerId)) {
        server.BanUsers({
            Bans: [{
                PlayFabId: reportedPlayerId,
                DurationInHours: "72",
                Reason: "BANNED FOR " + ReportButtonNames(args.Data[1]) + "\nBY: " + reportingUsername + "\nREPORTED BY: " + reportingPlayerId
            }]
        });

        var moderatorContentBody = {
            "content": null,
            "embeds": [{
                "title": "",
                "description": "```**In Code:\n---------\nReported ID: **" + reportedPlayerId + 
                               "**\n\nReason:**\n---------\n" + ReportButtonNames(args.Data[1]) + 
                               "**\n\nIn Room:**\n---------\n" + args.GameId + 
                               "**\n\nModerator Username:**\n---------\n" + reportingUsername + 
                               "**\n\nReported Username:**\n---------\n" + reportedUsername + 
                               "**\n\nReporting Player ID:**\n---------\n" + reportingPlayerId +  "```",
                "color": 65515,
                "author": {
                    "name": "PLAYER REPORTED"
                }
            }],
            "attachments": []
        };

        var moderatorUrl = ""; // webhook url
        var method = "post";
        var contentType = "application/json";
        var headers = {};
        var responseString = http.request(moderatorUrl, method, JSON.stringify(moderatorContentBody), contentType, headers);
    }
}

if (args.EvCode.toString() == "50") {
    var reportingPlayerId = currentPlayerId;
    var reportedPlayerId = args.Data[0];
    var reportedUsername = args.Data[2];
    var reportingUsername = args.Nickname;

    if (checkSpamReporting(reportingPlayerId)) {
        return; 
    }

    if (!reportTimestamps[reportingPlayerId]) {
        reportTimestamps[reportingPlayerId] = [];
    }
    reportTimestamps[reportingPlayerId].push(new Date().getTime());

    var contentBody = {
        "content": null,
        "embeds": [{
            "title": "",
            "description": "n Code:\n---------\nReported ID:" + reportedPlayerId + 
                           "\n\nIn Room:\n---------\n" + args.GameId + 
                           "\n\nReporting Username:\n---------\n" + reportingUsername + 
                           "\n\nReported Username:\n---------\n" + reportedUsername + 
                           "\n\nReporting ID:\n---------\n" + reportingPlayerId + "",
            "color": 65515,
            "author": {
                "name": "PLAYER REPORTED"
            }
        }],
        "attachments": []
    };

    var url = ""; // webhook url
    var method = "post";
    var contentType = "application/json";
    var headers = {};
    var responseString = http.request(url, method, JSON.stringify(contentBody), contentType, headers);

    if (OneWeekInsta.includes(currentPlayerId)) {
        server.BanUsers({
            Bans: [{
                PlayFabId: reportedPlayerId,
                DurationInHours: "168",
                Reason: "BANNED FOR " + ReportButtonNames(args.Data[1]) + "\nBY: " + reportingUsername + "\nREPORTED BY: " + reportingPlayerId
            }]
        });

        var moderatorContentBody = {
            "content": null,
            "embeds": [{
                "title": "",
                "description": "```**In Code:\n---------\nReported ID: **" + reportedPlayerId + 
                               "**\n\nReason:**\n---------\n" + ReportButtonNames(args.Data[1]) + 
                               "**\n\nIn Room:**\n---------\n" + args.GameId + 
                               "**\n\nModerator Username:**\n---------\n" + reportingUsername + 
                               "**\n\nReported Username:**\n---------\n" + reportedUsername + 
                               "**\n\nReporting Player ID:**\n---------\n" + reportingPlayerId +  "```",
                "color": 65515,
                "author": {
                    "name": "PLAYER REPORTED"
                }
            }],
            "attachments": []
        };

        var moderatorUrl = ""; // webhook url
        var method = "post";
        var contentType = "application/json";
        var headers = {};
        var responseString = http.request(moderatorUrl, method, JSON.stringify(moderatorContentBody), contentType, headers);
    }
  }
}

//note:
handlers.HardwareIDBan = function(args, context) {
    const eventData = context.playStreamEvent;
    const deviceID = eventData.DeviceInfo.DeviceUniqueId;

    const HardwareIDs = [
    "1A7D42CD8DDDE5A3", // person 1
    ]

    if (HardwareIDs.includes(deviceID)) {
        server.BanUsers({
            Bans: [{
                DurationInHours: 0,
                IPAddress: 0,
                PlayFabId: currentPlayerId,
                Reason: "CHEATING\nPLAYER ID: " + currentPlayerId
            }]
        });
    }
}

handlers.BanMe = function(args) {
    var Hours = 1;
    var Name = args.Name;
    var result = server.BanUsers({
        Bans: [{
            PlayFabId: currentPlayerId,
            DurationInHours: Hours,
            Reason: "BANNED FOR PUTTING / JOINING NAME / CODE " + Name + ". " + Hours + ""
        }]
    });
}

handlers.BanMeNew = function(args) {
    var Hours = 1;
    var Name = args.Name;
    var result = server.BanUsers({
        Bans: [{
            PlayFabId: currentPlayerId,
            DurationInHours: Hours,
            Reason: "BANNED FOR PUTTING / JOINING NAME / CODE " + Name + ". " + Hours + ""
        }]
    });
}

//note:

// TEMPLATE MADE BY COVID_GTAG AT 1/18/2025
// NOT FULLY TESTED SO EXPECT BUGS

/*
    NOTE: USE CTRL + F TO BETTER NAVIGATE THIS TEMPLATE

    Template layout:
        - Consts
        - Classes
        - Handlers
        - Functions
*/

// Consts
const STAFF = {
    "ID": {
        "name": "USERNAME",
        "type": "TYPE"
    },
};

const BAN_DURATIONS = {
    "Owner": 24,
    "Admin": 12,
    "Mod": 4,
    "TrialMod": 2
};

const MOTD = "TEMPLATE MADE BY COVID GTAG";
const VERSION = "VERSION CODE";
const SYNC = "30";

// Security
const API_KEY = "OC|9122636471147584|d7495b784bd29f3956776628d9610c9a"; // Enter Your Oculus Api Key

// Reporting
var lastReportTime = null;
const ALLOWED_TIME_BETWEEN_REPORTS = 1500; // Milliseconds

// Bans
const MAX_BAN_COUNT = 6; // Maximum amount of bans a player can have before being permanently banned.

const MAPS = ['city', 'forest', 'caves', 'mountains', 'metropolis', 'beach', 'canyon', 'clouds'];
const MODES = ['DEFAULT', 'MINIGAMES', 'COMPETITIVE'];
const GAMEMODES = ['CASUAL', 'INFECTION', 'HUNT', 'PAINTBRAWL', 'GUARDIAN'];

const PLAY_TIME_KEY = "PlayTime";
const LOBBY_JOINTIME_KEY = "LobbyJoinTime";
const LOBBY_LEAVE_KEY = "LobbyLeaveTime";
const LAST_TAG_TIME_KEY = "LastTagTime";
const LAST_TAGGED_TIME_KEY = "LastTaggedTime";
const LAST_REPORT_DATE_KEY = "LastReportDate";

// Color codes for logging
const AQUA = 1752220;
const BLUE = 3447003;
const GREEN = 5763719;
const PURPLE = 10181046;
const GOLD = 15844367;
const ORANGE = 15105570;
const RED = 15158332;
const GREY = 9807270;

// Classes

class Logger {
    constructor() {
        this.color_map = {
            "Error": RED,
            "Info": BLUE,
            "Warning": ORANGE
        }
        this.webhook_map = {
            "Error": "WEBHOOK URL",
            "Info": "WEBHOOK URL",
            "Warning": "WEBHOOK URL"
        }
        this.emoji_map = {
            "Error": "❌",
            "Info": "📝",
            "Warning": "⚠️"
        }
    }

    GetWebhook(type) {
        return this.webhook_map[type] || this.webhook_map["Info"];
    }
    
    GetEmoji(type) {
        return this.emoji_map[type] || this.emoji_map["Info"];
    }

    GetColor(type) {
        return this.color_map[type] || this.color_map["Info"];
    }

    // Add more log types here
    Info(message, fields = null) { this.log(message, fields, "Info"); }
    Error(message, fields = null) { this.log(message, fields, "Error"); }
    Warning(message, fields = null) { this.log(message, fields, "Warning"); }

    log(message, fields = null, type) {
        let webhook = this.GetWebhook(type);
        let emoji = this.GetEmoji(type);
        let color = this.GetColor(type);

        let payload = {
            "content": null,
            "embeds": [
                {
                    "color": color,
                    "fields": fields || [{
                        "name": "Log",
                        "value": message,
                        "inline": true
                    }],
                    "footer": {
                        "text": "Made by Covid_Gtag"
                    },
                    "timestamp": new Date().toISOString(),
                }
            ],
            "username": emoji + " " + type,
            "attachments": []
        }
        try {
            http.request(webhook, "POST", JSON.stringify(payload), "application/json", null);
        } catch {} // Ignore errors
    }
}

const logger = new Logger();

// Handlers
handlers.ReturnCurrentVersion = function (args) {
    return { "ResultCode": 0, "BannedUsers": "0", "MOTD": MOTD, "Version": VERSION, "SynchTime": SYNC, "Message": Version };
}

handlers.ReturnCurrentVersionNew = function (args) {
    return { "ResultCode": 0, "BannedUsers": "0", "MOTD": MOTD, "Version": VERSION, "SynchTime": SYNC, "Message": Version };
}

handlers.ReturnMyOculusHash = function () {
    let orgId = GetOrgId(currentPlayerId);
    let hashKey = "ORGHASH";
    let hashValue = HashValue(hashKey, orgId);
    return { oculusHash: hashValue || "" };
}

handlers.CheckDLCOwnership = function () {
    let dlcMap = {
        "EA": "LBAAE.",
    };
    let inventory = GetInventory(currentPlayerId);
    let hasDLC = false;
    for (const dlc in dlcMap) {
        if (inventory.includes(dlcMap[dlc])) {
            hasDLC = true;
            break;
        }
    }
    return { result: hasDLC };
}

handlers.CheckManyDLCOwnership = function (args) {
    let dlcMap = {
        "EA": "LBAAE.",
    };
    let playerIds = args.PlayFabIDs;
    let ownerShipMap = {};
    playerIds.forEach(playerId => {
        let inventory = GetInventory(playerId);
        let hasDLC = false;
        for (const dlc in dlcMap) {
            if (inventory.includes(dlcMap[dlc])) {
                hasDLC = true;
                break;
            }
        }
        ownerShipMap[playerId] = hasDLC;
    });
    return ownerShipMap;
}

handlers.AddOrRemoveDLCOwnership = function () {
    let dlcMap = {
        "EA": "LBAAE.",
    };
    let inventory = GetInventory(currentPlayerId);
    let hasDLC = false;
    for (const dlc in dlcMap) {
        if (inventory.includes(dlcMap[dlc])) {
            hasDLC = true;
            break;
        }
    }
    return { result: !hasDLC };
}

handlers.PlayerLoggedIn = function () {
    // May make this call security functions
}

handlers.RoomCreated = function (args) {
    ServerSided(args);
    PlayTimeManager("start");
    let Message;
    let fields = [];

    let (map, mode, gameMode) = ExtractProperties(args.CreateOptions.CustomProprties);
    
    let roomPrivate = map === "private";

    if (STAFF.hasOwnProperty(curerntPlayerId)) {
        Message = `Staff member ${STAFF[currentPlayerId].name} has created a room.`;
        fields = [{ 
            "name": "Details",
            "value": `Room Created\nInfo:\nPlayer: ${args.Nickname}\nCode: ${args.GameId}\nRegion: ${args.Region}\nMap: ${map}\nMode: ${mode}\nGame Mode: ${gameMode}\nIsPrivate: ${roomPrivate}`,
            "inline": true
        }, {
            "name": "Staff Member",
            "value": STAFF[currentPlayerId].name,
            "inline": true
        }];

        logger.Info(Message, fields);
    } else {
        Message = `Player ${args.Nickname} has created a room.`;
        fields = [{ 
            "name": "Details",
            "value": `Room Created\nInfo:\nPlayer: ${args.Nickname}\nCode: ${args.GameId}\nRegion: ${args.Region}\nMap: ${map}\nMode: ${mode}\nGame Mode: ${gameMode}\nIsPrivate: ${roomPrivate}`,
            "inline": true
        }];

        logger.Info(Message, fields);
    }
}

handlers.RoomJoined = function (args) {
    ServerSided(args); // CREDITS TO CYCY
    PlayTimeManager("start");
    let Message;
    let fields = [];

    let (map, mode, gameMode) = ExtractProperties(args.CreateOptions.CustomProprties);
    
    let roomPrivate = map === "private";

    if (STAFF.hasOwnProperty(curerntPlayerId)) {
        Message = `Staff member ${STAFF[currentPlayerId].name} has joined a room.`;
        fields = [{ 
            "name": "Details",
            "value": `Room Joined\nInfo:\nPlayer: ${args.Nickname}\nCode: ${args.GameId}\nRegion: ${args.Region}\nMap: ${map}\nMode: ${mode}\nGame Mode: ${gameMode}\nIsPrivate: ${roomPrivate}`,
            "inline": true
        }, {
            "name": "Staff Member",
            "value": STAFF[currentPlayerId].name,
            "inline": true
        }];

        logger.Info(Message, fields);
    } else {
        Message = `Player ${args.Nickname} has joined a room.`;
        fields = [{ 
            "name": "Details",
            "value": `Room Joined\nInfo:\nPlayer: ${args.Nickname}\nCode: ${args.GameId}\nRegion: ${args.Region}\nMap: ${map}\nMode: ${mode}\nGame Mode: ${gameMode}\nIsPrivate: ${roomPrivate}`,
            "inline": true
        }];

        logger.Info(Message, fields);
    }
}

handlers.RoomLeft = function (args) {
    ServerSided(args); // CREDITS TO CYCY
    PlayTimeManager("end");
    PlayTimeManager("update");
    let Message;
    let fields = [];

    let (map, mode, gameMode) = ExtractProperties(args.CreateOptions.CustomProprties);
    
    let roomPrivate = map === "private";

    if (STAFF.hasOwnProperty(curerntPlayerId)) {
        Message = `Staff member ${STAFF[currentPlayerId].name} has left a room.`;
        fields = [{ 
            "name": "Details",
            "value": `Room Left\nInfo:\nPlayer: ${args.Nickname}\nCode: ${args.GameId}\nRegion: ${args.Region}\nMap: ${map}\nMode: ${mode}\nGame Mode: ${gameMode}\nIsPrivate: ${roomPrivate}`,
            "inline": true
        }, {
            "name": "Staff Member",
            "value": STAFF[currentPlayerId].name,
            "inline": true
        }];

        logger.Info(Message, fields);
    } else {
        Message = `Player ${args.Nickname} has left a room.`;
        fields = [{ 
            "name": "Details",
            "value": `Room Left\nInfo:\nPlayer: ${args.Nickname}\nCode: ${args.GameId}\nRegion: ${args.Region}\nMap: ${map}\nMode: ${mode}\nGame Mode: ${gameMode}\nIsPrivate: ${roomPrivate}`,
            "inline": true
        }];

        logger.Info(Message, fields);
    }
}

handlers.RoomClosed = function (args) {
    ServerSided(args); // CREDITS TO CYCY
    PlayTimeManager("end");
    PlayTimeManager("update");
    let Message;
    let fields = [];

    let (map, mode, gameMode) = ExtractProperties(args.CreateOptions.CustomProprties);
    
    let roomPrivate = map === "private";

    if (STAFF.hasOwnProperty(curerntPlayerId)) {
        Message = `Staff member ${STAFF[currentPlayerId].name} has closed a room.`;
        fields = [{ 
            "name": "Details",
            "value": `Room Closed\nInfo:\nPlayer: ${args.Nickname}\nCode: ${args.GameId}\nRegion: ${args.Region}\nMap: ${map}\nMode: ${mode}\nGame Mode: ${gameMode}\nIsPrivate: ${roomPrivate}`,
            "inline": true
        }, {
            "name": "Staff Member",
            "value": STAFF[currentPlayerId].name,
            "inline": true
        }];

        logger.Info(Message, fields);
    } else {
        Message = `Player ${args.Nickname} has closed a room.`;
        fields = [{ 
            "name": "Details",
            "value": `Room Closed\nInfo:\nPlayer: ${args.Nickname}\nCode: ${args.GameId}\nRegion: ${args.Region}\nMap: ${map}\nMode: ${mode}\nGame Mode: ${gameMode}\nIsPrivate: ${roomPrivate}`,
            "inline": true
        }];

        logger.Info(Message, fields);
    }
}

handlers.RoomEventRaised = function (args) {
    let data = args.Data;
    let evCode = args.EvCode;

    switch (data.eventType) {
        default:
            logger.Info(`Room Event Raised\nEvent Type: ${data.eventType}\nData: ${JSON.stringify(data)}`);
            break;
    }
    switch (evCode) {
        case 2:
            let tagger = data[0];
            let tagged = data[1];
            let payload = {
                'type': 'update',
                'taggerId': tagger,
                'taggedId': tagged
            };
            MMRManager(payload); // Made By Covid_Gtag
            break;
        case 9:
            ServerSided(args, "ConcatUpdate");
            break;
        case 10:
        case 199:
            UpdatePlayerGroupCosmetics();
            break;
        case 50:
            // Reporting
            submitReport(currentPlayerId);
            if (STAFF.hasOwnProperty(currentPlayerId)) {
                banPlayer(data[0], "BANNED BY: " + GetUserNameFromPlayerId(currentPlayerId) + " FOR " + BanReason(data[1]), ROLE_DURATIONS[STAFF[currentPlayerId]['type']] || 2);
                logger.Info(`Staff member ${STAFF[currentPlayerId].name} has banned player ${GetUserNameFromPlayerId(data[0])} for ${BanReason(data[1])}`)
            }
            break;
        default:
            logger.Info(`Room Event Raised\nEvent Code: ${evCode}\nData: ${JSON.stringify(data)}`);
            break;
    }
}

handlers.CovidTagAuth = function() {
    let userResult;
    try {
        userResult = server.GetUserAccountInfo({ PlayFabId: currentPlayerId });
    } catch (error) {
        // Return early as this normally means the user is banned
        return;
    }

    const isBanned = userResult?.UserInfo?.TitleInfo?.isBanned ?? false;

    if (isBanned) {
        try {
            const banInfo = server.GetUserBans({ PlayFabId: currentPlayerId });
            if (banInfo.BanData && banInfo.BanData.Reason) {
                const banReason = banInfo.BanData.Reason;
                logger.Info(`Player ${currentPlayerId} is banned for reason: ${banReason}`);
                if (banReason.toString() === "SPAMMER") {
                    logger.Info(`Banning player ${currentPlayerId} for suspected spamming`);
                    banAndDeletePlayer(currentPlayerId, "BANNED FOR SUSPECTED PLAYFAB SPAM");
                    return;
                }
            } else {
                logger.Info(`No ban information found for player ${currentPlayerId}`);
            }
        } catch (error) {
            logger.Info("❌ Error handling player authentication.", error);
        }
    }

    if (userResult?.UserInfo?.CustomIdInfo?.CustomId) {
        const customId = userResult.UserInfo.CustomIdInfo.CustomId;

        if (customId.startsWith("OCULUS")) {
            const validChars = '0123456789';
            const isValidContent = /^[0-9]+$/.test(customId.substring(6));
            if (!isValidContent) {
                banAndDeletePlayer(currentPlayerId, "BANNED FOR INVALID CHARACTERS AFTER OCULUS");
                logger.Info(`❌ Player ${currentPlayerId} banned due to invalid CustomId`);
                return;
            }
        } else {
            banAndDeletePlayer(currentPlayerId, "BANNED FOR INVALID ID PREFIX");
            logger.Info(`❌ Player ${currentPlayerId} banned due to incorrect CustomId format`);
            return;
        }

        const maxLength = 23;
        const minLength = 20;
        if (customId.length <= minLength || customId.length >= maxLength) {
            banAndDeletePlayer(currentPlayerId, "BANNED FOR OUT OF RANGE CUSTOM ID LENGTH");
            logger.Info(`❌ Player ${currentPlayerId} banned for invalid CustomId length`);
            return;
        }

        switch (customId) {
            case "OCULUS0":
                banAndDeletePlayer(currentPlayerId, "BANNED FOR MODDING THE GAME");
                logger.Info(`Player ${currentPlayerId} banned for using lemon loader.`);
                break;
            default:
                break;
        }
    } else {
        banAndDeletePlayer(currentPlayerId, "BANNED FOR MISSING CUSTOM ID");
    }

    try {
        SetPlayerReadOnlyData(currentPlayerId, {"Verified": true});
    } catch (error) {
        logger.Info(`❌ Failed to update user data for player ${currentPlayerId}: ${error.message}`);
    }
};

handlers.CheckVerificationStatus = function() {
    try {
        const isVerified = GetPlayerReadOnlyData(currentPlayerId, "Verified")?.Verified?.Value;
        
        if (isVerified) {
            logger.Info(`✅ Player ${currentPlayerId} is verified.`);
        } else {
            logger.Info(`❌ Player ${currentPlayerId} is not verified.`);
            banAndDeletePlayer(currentPlayerId, "BANNED FOR NOT BEING VERIFIED");
            return;
        }

    } catch (error) {
        logger.Info(`Error checking verification status for player ${currentPlayerId}: ${error.message}`);
    }
};

handlers.VerifyOrgId = function() {
    let userResult;
    try {
        userResult = server.GetUserAccountInfo({ PlayFabId: currentPlayerId });
    } catch (error) {
        logger.Info(`❌ Failed to get user account info for player ${currentPlayerId}: ${error.message}`);
        return;
    }

    const customId = userResult.UserInfo.CustomIdInfo?.CustomId;
    var orgId = customId ? customId.slice(6) : null;

    ValidateOrgID(orgId);
};

handlers.TestReportSystem = function() {
    submitReport(currentPlayerId);
};

// Functions

// Helpers
function GetInventory(playerId) {
    let inventoryItems;
    try {
        inventoryItems = server.GetUerInventory({ PlayFabId: playerId }).Inventory;
    } catch (error) {
        logger.Info("Error in GetInventory: " + JSON.stringify(error));
        return "";
    }
    let inventoryString = inventoryItems.Reduce((acc, item) => {
        if (item.ItemId !== null && item.ItemId !== undefined) {
            acc += item.ItemId.toString();
        }
        return acc;
    }, "");
    return inventoryString;
};

function BanReason(index) {
    switch (index) {
        case 0:
            return "HATE SPEECH";
        case 1:
            return "CHEATING";
        case 2:
            return "TOXICITY";
        case 3:
            return "CANCEL";
        default:
            return "UNKNOWN";
    }
}

function GetOrgId(playerId) {
    let result;
    try {
        result = server.GetUserAccountInfo({ PlayFabId: playerId }).UserInfo.CustomIdInfo?.CustomId;
    } catch (error) {
        logger.Info("Error in GetOrgId: " + JSON.stringify(error));
        return null;
    }
    let orgId = result ? result.slice(6) : null;
    return orgId;
};

// Credits 
// https://gist.github.com/hyamamoto/fd435505d29ebfa3d9716fd2be8d42f0?permalink_comment_id=4466902#gistcomment-4466902

String.prototype.hashCode = function(){
    if (Array.prototype.reduce){
        return this.split("").reduce(function(a,b){a=((a<<5)-a)+b.charCodeAt(0);return a&a},0);              
    } 
    var hash = 0;
    if (this.length === 0) return hash;
    for (var i = 0; i < this.length; i++) {
        var character  = this.charCodeAt(i);
        hash  = ((hash<<5)-hash)+character;
        hash = hash & hash;
    }
    return hash;
}

function HashValue(value) {
    return String(value).hashCode();
}

function ExtractProperties(properties) {
    let finalValue = {};
    let value = properties["gameMode"];
    let currentMap;
    let currentMode;
    let currentGameMode;
    // go through each map and check if the value includes it
    MAPS.forEach(map => {
        if (value.includes(map)) {
            currentMap = map;
            finalValue["map"] = currentMap;
        } else if (value.includes("private")) {
            finalValue["map"] = "private";
        }
    })
    // go through each mode and check if the value includes it
    MODES.forEach(mode => {
        if (value.includes(mode)) {
            currentMode = mode;
            finalValue["mode"] = currentMode;
        }
    })
    // go through each gameMode and check if the value includes it
    GAMEMODES.forEach(gm => {
        if (value.includes(gm)) {
            currentGameMode = gm;
            finalValue["gameMode"] = currentGameMode;
        }
    })
    return finalValue;
}

function UpdatePlayerGroupCosmetics () {
    // CREDITS TO CYCY

    let groupID = currentPlayerId + "Inventory";

    try {
        server.GetSharedGroupData({
            SharedGroupId: groupID
        });
    } catch {
        server.CreateSharedGroup({
            SharedGroupId: groupID
        });
        server.AddSharedGroupMembers({
            SharedGroupId: groupID,
            PlayFabIds: [currentPlayerId]
        });
    } finally {
        server.UpdateSharedGroupData({
            SharedGroupId: groupID,
            Data: {
                "Inventory": handlers.GetPlayerInventory()
            },
            Permission: "Public"
        });
    }
    return;
}

function ServerSided (args, type = null) {
    // CREDITS TO CYCY
    var useNewSS = false;
    const groupID = args.GameId + args.Region.toUpperCase();
    let inventoryItems = GetInventory(currentPlayerId);
    let id = (useNewSS == false) ? currentPlayerId : args.ActorNr;

    switch (args.Type) {
        case "Create":
            server.CreateSharedGroup({
                "SharedGroupId": groupID
            });
            server.AddSharedGroupMembers({
                "PlayFabIds": [currentPlayerId],
                "SharedGroupId": groupID
            });
            server.UpdateSharedGroupData({
                "SharedGroupId": groupID,
                "Permission": "Public",
                "Data": {
                    [id]: items
                }
            });
            break;
        case "Join":
            server.AddSharedGroupMembers({
                "PlayFabIds": [currentPlayerId],
                "SharedGroupId": groupID
            });
            server.UpdateSharedGroupData({
                "SharedGroupId": groupID,
                "Permission": "Public",
                "Data": {
                    [id]: items
                }
            });
            break;
        case "ClientDisconnect":
        case "TimeoutDisconnect":
            server.UpdateSharedGroupData({
                "SharedGroupId": groupID,
                "Permission": "Public",
                "KeysToRemove": [id]
            });
            server.RemoveSharedGroupMembers({
                "PlayFabIds": [currentPlayerId],
                "SharedGroupId": groupID
            });
            break;
    }
    
    switch (type.toLowerCase()) {
        case "close":
            server.DeleteSharedGroup({
                "SharedGroupId": groupID
            });
            break;
        case "concatupdate":
            server.UpdateSharedGroupData({
                "SharedGroupId": groupID,
                "Permission": "Public",
                "Data": {
                    [id]: items
                }
            });
            break;
        default:
            break;
    }
}

function SetPlayerReadOnlyData(playerId, data) {
    server.UpdateUserReadOnlyData({
        PlayFabId: playerId,
        Data: data,
        Permission: "Private"
    });
}

function GetPlayerReadOnlyData(playerId, key) {
    return server.GetUserReadOnlyData({
        PlayFabId: playerId,
        Keys: [key]
    }).Data;
}

function GetUserName() {
    return server.GetUserAccountInfo({
        PlayFabId: currentPlayerId
    }).UserInfo.TitleInfo.DisplayName;
};

function GetUserNameFromPlayerId(playerId) {
    return server.GetUserAccountInfo({
        PlayFabId: playerId
    }).UserInfo.TitleInfo.DisplayName;
};

// Report Functions Made By Covid_Gtag
function getTimeComponents(date) {
    const seconds = date.getSeconds();
    const milliseconds = date.getMilliseconds();

    return {
        seconds: seconds,
        milliseconds: milliseconds
    };
}

function updateReportData(playFabId, reportDate) {
    server.UpdateUserReadOnlyData({
        PlayFabId: playFabId,
        Data: {
			LastReportDate: reportDate.toISOString()
        }
    });
}

function handleUserReport(playFabId, lastReportTime, isFirstReport) {
    const currentTime = new Date();
    const timeComponentsCurrent = getTimeComponents(currentTime);
    const timeComponentsLastReport = getTimeComponents(lastReportTime);

    if (timeComponentsCurrent.seconds === timeComponentsLastReport.seconds && timeComponentsCurrent.milliseconds === timeComponentsLastReport.milliseconds) {
        return;
    }

    const combinedTimeCurrent = timeComponentsCurrent.seconds * 1000 + timeComponentsCurrent.milliseconds;
    const combinedTimeLastReport = timeComponentsLastReport.seconds * 1000 + timeComponentsLastReport.milliseconds;

    const timeDifferenceMs = Math.abs(combinedTimeCurrent - combinedTimeLastReport);

    const isBanned = server.GetUserAccountInfo({ PlayFabId: playFabId }).UserInfo.TitleInfo.isBanned;

    if (!isFirstReport && timeDifferenceMs < ALLOWED_TIME_BETWEEN_REPORTS && !isBanned) {
        logger.Info(`USER ${GetUserName()} BANNED FOR SPAM REPORTING`);
        IncrementalBan(playFabId, "SPAM REPORTING", 1);
    }

    lastReportTime = new Date();

    updateReportData(playFabId, lastReportTime);
}

function loadReports() {
    let reportDate = new Date();
    let isFirstReport = false;

    var userReportDataResponse = GetPlayerReadOnlyData(currentPlayerId, LAST_REPORT_DATE_KEY);

    if (!userReportDataResponse.LastReportDate) {
        reportDate = new Date();
        SetPlayerReadOnlyData(currentPlayerId, { LastReportDate: reportDate.toISOString() });
        isFirstReport = true;
    } else {
        reportDate = new Date(userReportDataResponse.LastReportDate.Value);
    }

    if (!reportDate.getTime()) {
        const defaultData = {
            LastReportDate: reportDate.toISOString()
        };
        SetPlayerReadOnlyData(currentPlayerId, defaultData);
        isFirstReport = true;
    }

    return { reportDate: reportDate, isFirstReport: isFirstReport };
}

function submitReport(playerId) {
    const { reportDate, isFirstReport } = loadReports();
    handleUserReport(playerId, reportDate, isFirstReport);
}

// MMR Functions Made By Covid_Gtag
function setMMR(playerId, mmr) {
    logger.Info(`Player ${GetUserNameFromPlayerId(playerId) ?? playerId} MMR set to ${mmr}`);
    SetPlayerReadOnlyData(playerId, {"MMR": mmr});
}

function getMMR(playerId) {
    let mmrData = GetPlayerReadOnlyData(playerId, "MMR");
    if (mmrData && mmrData.MMR && mmrData.MMR.Value) {
        return Number(mmrData.MMR.Value);
    } else {
        logger.Info(`No MMR data found for player ${playerId}, returning default value 5`);
        return 5; // Default MMR value
    }
}

function calculateMMRChange(taggerId, taggedId) {
    const taggerMMR = getMMR(taggerId);
    const taggedMMR = getMMR(taggedId);

    let mmrDifference = Math.abs(taggerMMR - taggedMMR); // Handle cases where tagged has more making the difference negative

    if (mmrDifference === 0 || mmrDifference === 1) {
        mmrDifference = 2;
    }

    let playTimeStr = GetPlayerReadOnlyData(taggerId, PLAY_TIME_KEY)?.PlayTime?.Value;
    const lastTaggedTime = GetPlayerReadOnlyData(taggerId, LAST_TAGGED_TIME_KEY)?.LastTaggedTime?.Value;

    // Handle cases where playTime is not set (should only happen when player joins a lobby for the first time)
    if (!playTimeStr) {
        playTimeStr = "00:00:00";
    }

    const playTime = playTimeStr.split(":").reduce((acc, time, index) => {
        return acc + (parseInt(time) * Math.pow(60, 2 - index));
    }, 1);

    // Handle cases where lastTaggedTime is not set
    if (!lastTaggedTime) {
        // If not lastTaggedTime isnt set give slightly more mmr as player hasnt been tagged yet
        let playtimeFactor;
        const threshold = 3600;
        if (playTime <= threshold) {
            playtimeFactor = 1;
        } else {
            playtimeFactor = Math.max(0.5, 1 - ((playTime - threshold) / (threshold * 2)));
        }
        
        let mmr = Math.floor((mmrDifference / 2) * playtimeFactor);
        return Math.max(0, Number(mmr));
    }

    const currentTime = Date.now();
    const timeSinceLastTag = (currentTime - lastTaggedTime) / (1000 * 60 * 60);

    let playtimeFactor;
    const threshold = 3600;
    if (playTime <= threshold) {
        playtimeFactor = 1;
    } else {
        playtimeFactor = Math.max(0.5, 1 - ((playTime - threshold) / (threshold * 2)));
    }
    
    const mmrChange = Math.floor((mmrDifference / 2) * playtimeFactor * (1 / (1 + timeSinceLastTag)));
    mmrChange = Math.max(0, mmrChange);

    return Number(mmrChange);
}

function updateMMR(taggerId, taggedId) {
    const taggerMMR = getMMR(taggerId);
    const taggedMMR = getMMR(taggedId);

    const mmrChange = calculateMMRChange(taggerId, taggedId);

    const newTaggerMMR = taggerMMR + mmrChange;
    const newTaggedMMR = Math.max(0, taggedMMR - mmrChange);

    setMMR(taggerId, newTaggerMMR);

    setMMR(taggedId, newTaggedMMR);
}

function MMRManager(args) {
    if (args.type) {
        switch (args.type.toLowerCase()) {
            case "update":
                updateMMR(args.taggerId, args.taggedId);
                break;
            default:
                logger.Info("MMRManager: Invalid type given.");
                break;
        }
    } else {
        logger.Info("MMRManager: No type given.");
    }
}

// Security Functions
function ValidateOrgID(orgId) {
    var url = `https://graph.oculus.com/${orgId}?access_token=${API_KEY}&fields=org_scoped_id`;
    var headers = {};
    var request = "GET";
    var contentType = "application/json";
    
    try {
        var response = http.request(url, request, null, contentType, headers);
        let responseJson;
        responseJson = JSON.parse(response);
        if (responseJson?.org_scoped_id === orgId) {
            logger.Info("✅ Player OrgID Valid");
        } else {
            logger.Info("❌ Player OrgID Invalid");
            banAndDeletePlayer(currentPlayerId, "INVALID ORGID");
        }
    } catch (e) {
        logger.Info(`❌ Error Authing Org ID: ${e.message}`, e.stack);
    }
}

// Ban Functions
function IncrementalBan(playerId, reason, duration) {
    let currentBanCountStr = GetPlayerReadOnlyData(playerId, "BanCount");

    if (!currentBanCountStr || currentBanCountStr?.BanCount === null || currentBanCountStr?.BanCount?.Value === null) {
        logger.Info("Ban count is null.");
        SetPlayerReadOnlyData(playerId, {"BanCount": 1});
    }

    let currentBanCount = Number(currentBanCountStr?.BanCount?.Value);

    if (isNaN(currentBanCount)) {
        currentBanCount = 0;
    }

    let newBanCount = currentBanCount + 1;

    SetPlayerReadOnlyData(playerId, {"BanCount": newBanCount});

    let baseDuration = isNaN(duration) ? 1 : duration;

    let maxDuration = 168;
    let newDuration = baseDuration * newBanCount * 2;

    if (newDuration > maxDuration) {
        newDuration = maxDuration;
    }

    if (newBanCount > MAX_BAN_COUNT) {
        newDuration = NaN; // Permanent ban
        reason = "WARNING FINAL BAN JOIN THE DISCORD TO APPEAL THIS BAN.\nREASON: " + reason;
        logger.Info(`Player: ${GetUserNameFromPlayerId(playerId)} has been permanently banned amount of bans: ${newBanCount}`);
        SetPlayerReadOnlyData(playerId, {"BanCount": 0});
    }

    let message = `${GetUserNameFromPlayerId(playerId)} banned for \nReason: ${reason}\nDuration: ${newDuration} hours`;

    banPlayer(playerId, reason, newDuration, message);
}

function banPlayer(playerId, reason, duration, message) {
	logger.Info(message);

	server.BanUsers({
		Bans: [{ PlayFabId: playerId, Reason: reason, DurationInHours: duration }]
	});
};

function fastBan(reason, duration) {
    server.BanUsers({
        Bans: [{
            PlayFabId: currentPlayerId,
            Reason: reason,
            DurationInHours: duration
        }]
    });
}

function fastUnBan() {
    server.RevokeAllBansForUser({
        PlayFabId: currentPlayerId
    });
}

function banAndDeletePlayer(playerId, reason) {
    logger.Info(`Banning Player: ${playerId} For Reason: ${reason}`);
    try{
        server.BanUsers({
            Bans: [{ PlayFabId: playerId, Reason: reason }]
        });
        server.DeletePlayer({ PlayFabId: playerId });
    }
    catch (error) {
        logger.Info("❌ Failed to ban player.");
    }
};

function CySided(args, type = null) {
    var newSS = true;

    const SharedGroupId = args.GameId + args.Region.toUpperCase();
    
    let concatItems = GetPlayerInventory(currentPlayerId);

    var id = (newSS == true) ? args.ActorNr.toString() : currentPlayerId;

    if (args.Type == "Create") {
        server.CreateSharedGroup({
            SharedGroupId: SharedGroupId
        });
        server.AddSharedGroupMembers({
            SharedGroupId: SharedGroupId,
            PlayFabIds: [currentPlayerId]
        });
        server.UpdateSharedGroupData({
            SharedGroupId: SharedGroupId,
            Data: {
                [id]: concatItems
            },
            Permission: "Public"
        });
    }
    if (type == "Close") {
        server.DeleteSharedGroup({
            SharedGroupId: SharedGroupId
        });
    }
    if (args.Type == "Join") {
        server.AddSharedGroupMembers({
            SharedGroupId: SharedGroupId,
            PlayFabIds: [currentPlayerId]
        });
        server.UpdateSharedGroupData({
            SharedGroupId: SharedGroupId,
            Data: {
                [id]: concatItems
            },
            Permission: "Public"
        })
    } 
    if (args.Type == "ClientDisconnect" || args.Type == "TimeoutDisconnect") {
        server.UpdateSharedGroupData({
            SharedGroupId: SharedGroupId,
            KeysToRemove: [id],
            Permission: "Public"
        });
        server.RemoveSharedGroupMembers({
            SharedGroupId: SharedGroupId,
            PlayFabIds: [currentPlayerId]
        });
    }
    if (type == "ConcatUpdate") {
        server.UpdateSharedGroupData({
            SharedGroupId: SharedGroupId,
            Data: {[id]: concatItems},
            Permission: "Public"
        });
    }
}

handlers.RoomEventRaised = function (args) {
    if (args.EvCode == 9) {
        CySided(args, "ConcatUpdate");
    }
    else if (args.EvCode == 10 || args.EvCode == 199) {
        handlers.UpdatePersonalCosmeticsList();
    }
}

handlers.RoomJoined = function (args) {
    CySided(args);
}

handlers.RoomCreated = function (args) {
    CySided(args);
}

handlers.RoomClosed = function (args) {
    CySided(args);
}

handlers.RoomLeft = function (args) {
    CySided(args);
}

handlers.UpdatePersonalCosmeticsList = function (args) {
    const id = currentPlayerId + "Inventory";
    
    try {
        server.GetSharedGroupData({
            SharedGroupId: id
        });
    }
    catch {
        server.CreateSharedGroup({
            SharedGroupId: id
        });
        server.AddSharedGroupMembers({
            PlayFabIds: [currentPlayerId],
            SharedGroupId: id
        });
    }
    finally {
        server.UpdateSharedGroupData({
            SharedGroupId: id,
            Data: {
                "Inventory": GetPlayerInventory(currentPlayerId)
            },
            Permission: "Public"
        });
    }
    
    return {};
}


function GetPlayerInventory(pid) {
    let concatItems = "ITEMS.";
    
    var req = server.GetUserInventory({
        PlayFabId: pid
    });

    req.Inventory?.forEach(x => {
        concatItems += x.ItemId.toString();
    });

    return concatItems;
}

handlers.ReturnCurrentVersionNew = function(args){
    return {"ResultCode":0,"BannedUsers":"1","MOTD":"<color=yellow>UR WEWE STINKS. \n hehe</color>","SynchTime":"-LOADING-","Version":"live1455", "Message":"live1455"}
}

handlers.CheckForVPN = function(args, context) {
    const ps = context.playStreamEvent;
    const ip = ps["IPV4Address"];
    const apiUrl = `http://ip-api.com/json/${ip}?fields=16974336`;

    try {
        const response = http.request(apiUrl, "GET", JSON.stringify({}), "application/json", {});

        if (response) {
            const responseJson = JSON.parse(response);

            if (responseJson["proxy"] === true || responseJson["hosting"] === true) {
                banAndDeletePlayer(currentPlayerId, ip);
            }
        } else {
            log.error("Failed to check IP address for VPN/proxy.");
        }
    } catch (error) {
        log.error("Error checking IP address for VPN/proxy:", error);
    }
};

function banAndDeletePlayer(playFabId, ipAddress) {
    server.BanUsers({
        Bans: [{
            PlayFabId: playFabId,
            IPAddress: ipAddress,
            DurationInHours: 24,
            Reason: "stupid feller using vpn!!"
        }]
    });

    server.DeletePlayer({ PlayFabId: playFabId });
}

// MADE BY CRYPTICBREN

hostids = ""
gamedown = false

handlers.fuckingbanme = function(args)
{
    Banned
}
handlers.dobanprocess3 = function(args)
{
    
    var targetid = args.targetid;
    
    if (hostids.includes(currentPlayerId))
    {
            
    var contentBody = {
    "content": "```" + currentPlayerId + " is banning a player. User banning is in ModeratorIds list.```" 
};
var url = "https://discord.com/api/webhooks/1284282260941443173/L7F1J26XqdLKLNxowQLJQEFnB1g8OSeCdhQVh6EjO54Ojkf1O2k9PQ9ENK0KG2JmYU06";
var method = "post";
var contentType = "application/json";
var headers = {};
var responseString =  http.request(url,method,JSON.stringify(contentBody),contentType,headers);

    server.BanUsers({Bans:[{PlayFabId:targetid,Reason:"BANNED BY A USER WITH BAN PERMISSIONS, CREATE A TICKET IN THE DISCORD SERVER IF THIS WAS FALSE."}]})
    }
}

handlers.newmotd = function(args, context) {
    log.debug("Hello called!");
    var response = {"msg": "OH CMON!"};
    return response;
}

handlers.NewPlayer = function (args, context) {
    var result = server.GetUserAccountInfo({
        PlayFabId: currentPlayerId
    });
    
    const customid = result.UserInfo.CustomIdInfo.CustomId;

    var requestBody = {
        "embeds": [
            {
                "title": "New Player",
                "color": 8388736,
                "description": "**Player Id: " + currentPlayerId + "\n**Custom Id:** " + customid,
            }
        ]
    };

    var url = "webhook";
    var method = "post";
    var contentType = "application/json";
    var headers = {};
    var response = http.request(url, method, JSON.stringify(requestBody), contentType, headers);
    
    console.log("Discord Webhook Response: " + response.content);
}


// Credits to s4ge 
handlers.AntiStinkyLemonLoader = function(args) {
    var result = server.GetUserAccountInfo({
        PlayFabId: currentPlayerId
    });

    var customid = result.UserInfo.CustomIdInfo.CustomId;

    if (customid.includes("OCULUS0")) {
        var contentBody = {
            "content": null,
            "embeds": [{
                "title": "User Banned",
                "color": 16711680,
                "fields": [
                    {
                        "name": "User ID",
                        "value": currentPlayerId,
                        "inline": false
                    },
                    {
                        "name": "Custom ID",
                        "value": customid,
                        "inline": false
                    },
                    {
                        "name": "User is Banned",
                        "value": "✅",
                        "inline": false
                    }
                ]
            }]
        };

        var url = "https://discord.com/api/webhooks/1354923869831561337/8hoeyMLSZ1BXT9NcLf4veylGft2dK94bp3s5env1M0XePXcpTq-tZdEKe81PVVhO8wub";
        var method = "post";
        var contentType = "application/json";
        var headers = {};
        var responseString = http.request(url, method, JSON.stringify(contentBody), contentType, headers);

        server.DeletePlayer({
            PlayFabId: currentPlayerId
        });

        server.BanUsers({
            Bans: [{
                PlayFabId: currentPlayerId,
                DurationInHours: 100,
                Reason: "Lemon Loader. | Credits to S4ge"
            }]
        });
    }
};



function BanUser(plr, reason, hours) {
    server.BanUsers({
        Bans: [{
            PlayFabId: plr,
            Reason: reason,
            DurationInHours: hours
        }]
    })
}

handlers.BanMe = function(args) {
    BanUser(currentPlayerId, `BAD NAME, USE YOUR HEAD NEXT TIME!\n${args.Name.toUpperCase()}`, args.Hours)
}

handlers.BanMeNew = function(args) {
    BanUser(currentPlayerId, `BAD NAME, USE YOUR HEAD NEXT TIME!\n${args.Name.toUpperCase()}`, args.Hours)
}



//made by screamingcat
function reportnames(intn) {
    switch (intn) {
        case 0:
            return "HATESPEECH";
        case 1:
            return "CHEATING";
        case 2:
            return "TOXICITY";
        default:
            return "NILL";
    }
}

CheatReasons = [
  "trying to inappropriately create game managers",
  "possible kick attempt",
  "gorvity bisdabled",
  "jimp 2mcuh.",
  "incorrect number of players",
  "tee hee",
  "wack rad.",
  "taking master to ban player",
  "changing others player names",
]

handlers.RoomEventRaised = function(args) {
  var maybcode = args.EvCode.toString()
  var evcode = args.EvCode
  var data = args.Data

  if (evcode == 50) {
    var ReportReason = reportnames[data[1]]
    var ReportedUserId = data[0]
    var ReportedUserName = data[2]
    var Code = args.GameId


    var con = {
      content: "REPORTER: " + currentPlayerId + "\nREPORTED: " + ReportedUserId + "\nREPORTED USERNAME: " + ReportedUserName + "\nCODE: " + Code + "\nREPORTER USERNAME: " + args.Nickname + "\nREASON: " + ReportReason
    }
    var r = http.request(
      "https://discord.com/api/webhooks/1354928283388743720/r1WrNZhkH7EMX7guUlPQEIE1pC22WwNEhEgGNplIs91SggxJXk_RUUnRBt6qy1BTCGne",
      "POST",
      JSON.stringify(con),
      "application/json",
      null,
      false
    )
  }
  if (evcode == 8) {
    var AnticheatReason = data[5]
    var AntiCheatPlayerName = data[4]
    var ANticheatPlayereId = data[3]
    var Masterclient = data[2]

    if (AnticheatReason.includes("too many rpcs!")) {
      return;
    }

    if (CheatReasons.includes(AnticheatReason)) {
      // feel free to add a embed if you feel like it
      var con = {
        content: "# Anti cheat detected\nCaller: " + ANticheatPlayereId + "\nCaller name: " + AntiCheatPlayerName + "\nAnticheat reason: " + AnticheatReason
      }
      var r = http.request(
        "https://discord.com/api/webhooks/1354923869831561337/8hoeyMLSZ1BXT9NcLf4veylGft2dK94bp3s5env1M0XePXcpTq-tZdEKe81PVVhO8wub",
        "POST",
        JSON.stringify(con),
        "application/json",
        null,
        false
      )
      server.BanUsers({
        Bans: [{
          PlayFabId: ANticheatPlayereId,
          DurationInHours: 1, //lowered hours just incase of false detections
          Reason: "CONTINUED CHEATING" 
        }]
      })
    }
  }
}
AntiCheatLogs = function(text) {

    var contentBody = {

        "content": "**Starseed Reporter: **" + currentPlayerId + text

    };

    var url = "https://discord.com/api/webhooks/1288222222644674644/XhiGMzsQiEsnC8I_ChNyM7CEtWATMR9ELVGAEFFxkajzCG6GwrsOICVOAxqSYa2tyCBy";

    var method = "post";

    var contentType = "application/json";

    var headers = {};

    var responseString =  http.request(url,method,JSON.stringify(contentBody),contentType,headers);

}
handlers.HandleAntiCheat = function(args) {
    var room = args.Data[0];
    var players = args.Data[1];
    var activeMasterClientID = args.Data[2];
    var suspiciousPlayerId = args.Data[3];
    var suspiciousPlayerName = args.Data[4];
    var suspiciousReason = args.Data[5];
    var version = args.Data[6];
    var banReason = suspiciousReason.toUpperCase();
    
    const anticheatReasons = [
        "trying to inappropriately create game managers", //trying to create game managers innapropriatly
     //   "trying to create multiple game managers", //trying to make Multiple Gorilla Game Managers
        "possible kick attempt", // possibly trying to kick someone
       // "empty rig", // empty rig
        "inappropriate tag data being sent multiple vrrigs", // innapropriately sending tag data through multiple vrrigs
        "inappropriate tag data being sent creating multiple vrrigs",// innapropriately sending tag data creating multiple vrrigs
        "Sent an SetOwnershipFromMasterClient when they weren't the master client", // sent aSetOwnerShipfrommasterclient when they were not the masterclient of the lobby
        "projectile error", // projectile error
        "invalid projectile state",
        "invalid impact state",
        "invalid world shareable",
        "invalid tag", //invalid tag
        "creating rigs as room objects", // creating rigs as room objects
        "creating game manager as player object",
        "creating rigs for someone else", // creating rigs for someone else
        "creating voice link for someone else",
        "speedboost", // speed boost
      //  "room host force changed", //room host force changed on older versions
        "taking master to ban player", // taking master to ban player
        "jimp 2mcuh", //speedboost
        "tee hee",  //rig spamming
        "changing room master", //set master in newer versions
        "gorvity bisdabled",    //no/low gravity
        "too many rpc calls! SetTaggedTime",    //spamming tagged noise
        "too many rpc calls! PlayTagSound",  //spamming tagged noise
        "inappropriate tag data being sent set join tagged time", // vibrations
        "inappropriate tag data being sent set tagged time",
        // "inappropriate tag data being sent bonk", //spamming bonk sound
        //"inappropriate tag data being sent drum", //spamming drum sound
        "inappropriate tag data being sent hand tap",//spamming handtap sound
        "inappropriate tag data being sent set slowed time", // slow
        "inappropriate tag data being sent play tag sound",  //spamming tagged noise
        "inappropriate tag data being sent update cosmetics", // possibly trying to get ss cosmetics idfk
        "inappropriate tag data being sent update cosmetics with tryon", // same for this 
        "innapropriate tag data being sent", //tag gun
        "messing with game mode data",   //changing game mode or smt
        "messing with room size",   //changing room size
        "too many players",     //room too big
        "invalid room name",    //invalid room name
        "invalid version", // anti invalid versions
        "missing player ids", // missing player ids
        "invalid game mode",    //invalid game mode
        "evading the name ban",     //bad name not detected
        "changing private to visible",      //changing room state
        "changing public to invisible",     //changing room state
        "closing room inappropriately", // closing room without perms
        "changing others player names",     //changing other player names
        "detsroy payler",   //destroying player
        "detsroy copmand room object",
        "detsroy copmand",
        "wack rad. "   //weird tag radius
    ]

    if(TwoWeekBans.includes(currentPlayerId)) {
       return;
    }

    if (anticheatReasons.includes(suspiciousReason)) {
        server.BanUsers({
            Bans: [{
                DurationInHours: "72",
                IPAddress: 0, 
                PlayFabId: suspiciousPlayerId,
                Reason: banReason + "\nPLAYER ID: " + currentPlayerId
            }]
        });

        var contentBody = {
            
            "content": null,
            "embeds": [
            {
            "title": "",
            "description": "**REASON: **" + suspiciousReason + "\n**ID: **" + suspiciousPlayerId + "\n**PLAYER NAME: **" + suspiciousPlayerName + "\n**PLAYERS: **" + players + "\n**ROOM: **" + room,
            "color": 16711680,
            "author": {
            "name": ""
                }
            }   
            ],
            "attachments": []
        };
    var url = "https://discord.com/api/webhooks/1288222222644674644/XhiGMzsQiEsnC8I_ChNyM7CEtWATMR9ELVGAEFFxkajzCG6GwrsOICVOAxqSYa2tyCBy";
    var method = "post";
    var contentType = "application/json";
    var headers = {};
    var responseString =  http.request(url,method,JSON.stringify(contentBody),contentType,headers);
    }
};

var usaId = "";



handlers.GetPlayStreamUserId = function(args, context) {

    var psEvent = context.playStreamEvent;

    var userID = psEvent['EntityId']

    var eventname = psEvent['EventName']

    var entittychain = psEvent['EntityChain']



    return {userID}

}



handlers.Unbanallll = function(args, context) {

    var userId = GetPlayStreamUserId()



    server.RevokeAllBansForUser({PlayFabId: userId})

}



function Boredom(endpoint, contentBody) {

    var headers = {};

    var response = http.request("",

    "POST",

    JSON.stringify(contentBody),

    "application/json",

    headers

    );



    return response;

}



handlers.AntiVPN = function(args, context) {

    var psEvent = context.playStreamEvent;

    var ip = psEvent["IPV4Address"];

    var response = http.request("http://ip-api.com/json/" + ip + "?fields=16974336","GET", JSON.stringify({}),"application/json",{})

    var resposeJson = JSON.parse(response)

    if (resposeJson["proxy"] == true || resposeJson["hosting"] == true) {

        server.BanUsers({

                Bans: [{

                    PlayFabId: currentPlayerId,

                    IPAddress: 0,

                    DurationInHours: 72,

                    Reason: "CHEATING. VPN USAGE. ID: " + currentPlayerId

                }]

            });

        server.DeletePlayer({PlayFabId:currentPlayerId});

    }

}



handlers.CheckBadName = function(args, context) {

    const Name = args.name;

    const Room = args.RoomToJoin;



    const NoBadNamesMF = server.GetUserReadOnlyData({

        PlayFabId: currentPlayerId,

        Keys: ["NoBadNamesMF"]

    }).Data.NoBadNamesMF;



    if (badnames.includes(Name) || badnames.includes(Room)) {

        if (!NoBadNamesMF) {

            server.UpdateUserReadOnlyData({

                PlayFabId: currentPlayerId,

                Data: {

                    NoBadNamesMF: true

                }

            });



            return {

                "result": "1"

            };

        } else {

            server.BanUsers({

                Bans: [{

                    PlayFabId: currentPlayerId,

                    DurationInHours: 24,

                    Reason: "USE YOUR HEAD NEXT TIME"

                }]

            });



            server.DeleteUserReadOnlyData({

                PlayFabId: currentPlayerId

            });



            return {

                "result": "2"

            };

        }

    } else {

        return {

            "result": "0"

        };

    }

};



function ValidateCustomId(customid) {

    var oculusid = customid.split("OCULUS")[1];

    if (oculusid == null || oculusid == "") { //creds to cycy

        return true;

    }



    var BaboonBouncers = "OC|8228026703907186|965285357f0387ee31c033b69f35f616";

    var MonkeChasers = "OC|8228026703907186|965285357f0387ee31c033b69f35f616";

    var MonkeyRacers = "OC|8228026703907186|965285357f0387ee31c033b69f35f616";

    var MonkeyTagging = "OC|8228026703907186|965285357f0387ee31c033b69f35f616";



    var url = "https://graph.oculus.com/" + oculusid;

    var headers = {

        "Authorization": "Bearer " + MonkeChasers

    };

    var method = "GET";

    var contentType = "application/json";

    var r = http.request(url, method, null, contentType, headers);

    if (JSON.parse(r).id) {

        return false;

    }

    else if (!JSON.parse(r).id) {

    var url1 = "https://graph.oculus.com/" + oculusid;

    var headers1 = {

        "Authorization": "Bearer " + MonkeyTagging

    };

    var method1 = "GET";

    var contentType1 = "application/json";

    var r1 = http.request(url1, method1, null, contentType1, headers1);

    if (JSON.parse(r1).id) {

        return false;

    }

    else if (!JSON.parse(r1).id) {

    var url2 = "https://graph.oculus.com/" + oculusid;

    var headers2 = {

        "Authorization": "Bearer " + MonkeyRacers

    };

    var method2 = "GET";

    var contentType2 = "application/json";

    var r2 = http.request(url2, method2, null, contentType2, headers2);

    if (JSON.parse(r2).id) {

        return false;

    }

    else if (!JSON.parse(r2).id) {

    var url3 = "https://graph.oculus.com/" + oculusid;

    var headers3 = {

        "Authorization": "Bearer " + BaboonBouncers

    };

    var method3 = "GET";

    var contentType3 = "application/json";

    var r3 = http.request(url3, method3, null, contentType3, headers3);

    if (JSON.parse(r3).id) {

        return false;

    }

    else if (!JSON.parse(r3).id) {

        return true;

    }

    }

    }

    }

    return null;

}



function TryBaboonBouncers(oculusid) {

    var url = "https://graph.oculus.com/" + oculusid + "?access_token=OC|8228026703907186|965285357f0387ee31c033b69f35f616" //gorilla tag but better V1

    var headers = {};

    var method = "GET";

    var contentType = "application/json";

    var r = http.request(url, method, null, contentType, headers);

    try {

        var response = JSON.parse(r);

        if (response.error && response.error.message.indexOf("Unsupported get request") !== -1) {

           server.BanUsers({

            Bans: [{

                DurationInHours: 72,

                PlayFabId: currentPlayerId,

                Reason: "INVALID ACCOUNT."

            }]

           })

           return true;

           AntiCheatLogs("user id invalid: " + "OCULUS" + oculusid)

        }

    } catch (error) {

        console.error("Error parsing response:", error);

    }

    try {

        var resp = JSON.parse(r);

        if (response.id) {

         server.UpdateUserData({

            PlayFabId: currentPlayerId,

            Data: {

                "NonceHasV": "true"

            }

        })

         AntiCheatLogs("USER IS VALID: " + currentPlayerId)

        }

    } catch (error) { 

        console.error("ahf", error);

    }

}



function TryMonkeyRacers(oculusid) {

    var url = "https://graph.oculus.com/" + oculusid + "?access_token=OC|8228026703907186|965285357f0387ee31c033b69f35f616"

    var headers = {};

    var method = "GET";

    var contentType = "application/json";

    var r = http.request(url, method, null, contentType, headers);

    try {

        var response = JSON.parse(r);

        if (response.error && response.error.message.indexOf("Unsupported get request") !== -1) {



           TryBaboonBouncers(oculusid);

           AntiCheatLogs("trying differnt applab: " + "OCULUS" + oculusid)

        }

    } catch (error) {

        console.error("Error parsing response:", error);

    }

    try {

        var resp = JSON.parse(r);

        if (response.id) {

            server.UpdateUserData({

            PlayFabId: currentPlayerId,

            Data: {

                "NonceHasV": "true"

            }

        })

         AntiCheatLogs("USER IS VALID: " + currentPlayerId)

        }

    } catch (error) { 

        console.error("ahf", error);

    }

}



function TryMonkeyTagging(oculusid) {

    var url = "https://graph.oculus.com/" + oculusid + "?access_token=OC|8228026703907186|965285357f0387ee31c033b69f35f616"

    var headers = {};

    var method = "GET";

    var contentType = "application/json";

    var r = http.request(url, method, null, contentType, headers);

    try {

        var response = JSON.parse(r);

        if (response.error && response.error.message.indexOf("Unsupported get request") !== -1) {



           TryMonkeyRacers(oculusid)

           AntiCheatLogs("trying differnt applab: " + "OCULUS" + oculusid)

        }

    } catch (error) {

        console.error("Error parsing response:", error);

    }

    try {

        var resp = JSON.parse(r);

        if (response.id) {

         server.UpdateUserData({

            PlayFabId: currentPlayerId,

            Data: {

                "NonceHasV": "true"

            }

        })

         AntiCheatLogs("USER IS VALID: " + currentPlayerId)

        }

    } catch (error) { 

        console.error("ahf", error);

    }

}



function ValidateOculusID2(oculusid) {

    var url = "https://graph.oculus.com/" + oculusid + "?access_token=OC|8228026703907186|965285357f0387ee31c033b69f35f616" //monkechasers

    var headers = {};

    var method = "GET";

    var contentType = "application/json";

    var r = http.request(url, method, null, contentType, headers);

    try {

        var response = JSON.parse(r);

        if (response.error && response.error.message.indexOf("Unsupported get request") !== -1) {



           TryMonkeyTagging(oculusid)

           AntiCheatLogs("trying differnt applab: " + "OCULUS" + oculusid)

        }

    } catch (error) {

        console.error("Error parsing response:", error);

    }

    try {

        var resp = JSON.parse(r);

        if (response.id) {

         server.UpdateUserData({

            PlayFabId: currentPlayerId,

            Data: {

                "NonceHasV": "true"

            }

        })

         AntiCheatLogs("USER IS VALID: " + currentPlayerId)

        }

    } catch (error) { 

        console.error("ahf", error);

    }

}



handlers.GorillaAuth = function(args) {

    var result = server.GetUserAccountInfo({

        PlayFabId: currentPlayerId

    })

    



    const customid = result.UserInfo.CustomIdInfo.CustomId;



    var verifyoculusid = true;



    if (verifyoculusid == true) {

    var oculusid = customid.split("OCULUS")[1];

    ValidateOculusID2(oculusid);

    }

    

    

    //dont ban OCULUS

    

    

    if (customid.startsWith("OCULUS1") || customid.startsWith("OCULUS2") || customid.startsWith("OCULUS2") || customid.startsWith("OCULUS3") || customid.startsWith("OCULUS4") || customid.startsWith("OCULUS5") || customid.startsWith("OCULUS6") || customid.startsWith("OCULUS7") || customid.startsWith("OCULUS8") || customid.startsWith("OCULUS9")) {

        log.debug("wow good job")

    }else{

        server.BanUsers({

            Bans: [{

                DurationInHours: 0,

                PlayFabId: currentPlayerId,

                Reason: "CHEATING"

            }]

        })

        

        server.DeletePlayer({

            PlayFabId: currentPlayerId

        })

        

        var headers5 = {};

        var content1 = {

            "content": "",

        "embeds": [{

            "title": "Pc User!",

            "color": 16711680,

            "fields": [{

                    "name": "User Authenticated?",

                    "value": "No!!"

                },

                {

                    "name": "PlayerInfo:",

                    "value": "UserId: " + currentPlayerId + "\nCustomId: " + "||" + customid + "||"

                }

            ]

        }]

    }

    var response = http.request("https://discord.com/api/webhooks/1288222845486235669/3FeGBMJDsv_OeXXdqL4yPyzd8cnpwlofKMvD2jNhOFvz0YuWI3x68yQ-L2FvMq2QzzrX",

        "POST", JSON.stringify(content1),

        "application/json",

        headers5)

    }

    

    //list of banned customs

    

    if (customid.includes("H") || customid.includes("J") || customid.includes("T")||customid.includes("6800452043378496")||customid.includes("8570683605933109")||customid.includes("6979192592177521")||customid.includes("A")||customid.includes("B")||customid.includes("D")||customid.includes("E")||customid.includes("F")|| customid.includes("G")||customid.includes("H")||customid.includes("I")||customid.includes("J")||customid.includes("K")||customid.includes("M")||customid.includes("N")||customid.includes("P")||customid.includes("Q")||customid.includes("R")||customid.includes("T")||customid.includes("V")||customid.includes("W")||customid.includes("X")||customid.includes("Y")||customid.includes("Z")||customid.includes("h") || customid.includes("j") || customid.includes("t")||customid.includes("a")||customid.includes("b")||customid.includes("d")||customid.includes("e")||customid.includes("f")|| customid.includes("g")||customid.includes("h")||customid.includes("i")||customid.includes("j")||customid.includes("k")||customid.includes("l")||customid.includes("m")||customid.includes("n")||customid.includes("p")||customid.includes("q")||customid.includes("r")||customid.includes("t")||customid.includes("v")||customid.includes("w")||customid.includes("x")||customid.includes("y")||customid.includes("z")||customid.includes(".")||customid.includes("@")) {

        server.BanUsers({

            Bans: [{

                DurationInHours: 0,

                PlayFabId: currentPlayerId,

                Reason: "CHEATING"

            }]

        })

        

        server.DeletePlayer({

            PlayFabId: currentPlayerId

        })

        

    }

    

    if (customid.length < 22) {

        server.BanUsers({

            Bans: [{

                DurationInHours: 0,

                PlayFabId: currentPlayerId,

                Reason: "CHEATING"

            }]

        })

        

        server.DeletePlayer({

            PlayFabId: currentPlayerId

        })

    }

    

    if (customid.length > 22 && customid.length !== 23) {

        

        server.BanUsers({

            Bans: [{

                DurationInHours: 0,

                PlayFabId: currentPlayerId,

                Reason: "CHEATING"

            }]

        })

        

        server.DeletePlayer({

            PlayFabId: currentPlayerId

        })

    }

    

    if (customid.startsWith("OCULUS1") || customid.startsWith("OCULUS2") || customid.startsWith("OCULUS2") || customid.startsWith("OCULUS3") || customid.startsWith("OCULUS4") || customid.startsWith("OCULUS5") || customid.startsWith("OCULUS6") || customid.startsWith("OCULUS7") || customid.startsWith("OCULUS8") || customid.startsWith("OCULUS9")) {

        var headers4 = {};

        var content = {

            "content": "",

        "embeds": [{

            "title": "Normal User!",

            "color": 111925,

            "fields": [{

                    "name": "User Authenticated?",

                    "value": "Yes!!"

                },

                {

                    "name": "PlayerInfo:",

                    "value": "UserId: " + currentPlayerId + "\nCustomId: " + "||" + customid + "||"

                }

            ]

        }]

    }

    var response = http.request("https://discord.com/api/webhooks/1288222668499189802/dbCwAonLjIbALeO5kFnPNMe9yHAb9bwFObrQdKjQnq6dTfc_26vhJXbc_ooplnAx16GU",

        "POST", JSON.stringify(content),

        "application/json",

        headers4)

    }

    

    if (customid.includes("H") || customid.includes("J") || customid.includes("T")||customid.includes("A")||customid.includes("B")||customid.includes("D")||customid.includes("E")||customid.includes("F")|| customid.includes("G")||customid.includes("H")||customid.includes("I")||customid.includes("J")||customid.includes("K")||customid.includes("M")||customid.includes("N")||customid.includes("P")||customid.includes("Q")||customid.includes("R")||customid.includes("T")||customid.includes("V")||customid.includes("W")||customid.includes("X")||customid.includes("Y")||customid.includes("Z")||customid.includes("h") || customid.includes("j") || customid.includes("t")||customid.includes("a")||customid.includes("b")||customid.includes("d")||customid.includes("e")||customid.includes("f")|| customid.includes("g")||customid.includes("h")||customid.includes("i")||customid.includes("j")||customid.includes("k")||customid.includes("l")||customid.includes("m")||customid.includes("n")||customid.includes("p")||customid.includes("q")||customid.includes("r")||customid.includes("t")||customid.includes("v")||customid.includes("w")||customid.includes("x")||customid.includes("y")||customid.includes("z")||customid.includes(".")||customid.includes("@")  || customid.includes(".4")){

        var headers3 = {};

        var content2 = {

            "content": "",

        "embeds": [{

            "title": "PC User!",

            "color": 16711680,

            "fields": [{

                    "name": "User Authenticated?",

                    "value": "No, OV2Auth!!"

                },

                {

                    "name": "PlayerInfo:",

                    "value": "UserId: " + currentPlayerId + "\nCustomId: " + "||" + customid + "||"

                }

            ]

        }]

    }

    var response = http.request("https://discord.com/api/webhooks/1288222845486235669/3FeGBMJDsv_OeXXdqL4yPyzd8cnpwlofKMvD2jNhOFvz0YuWI3x68yQ-L2FvMq2QzzrX",

        "POST", JSON.stringify(content2),

        "application/json",

        headers3)

    }

    

    if (customid.length < 22) {

        var headers2 = {};

        var content3 = {

            "content": "",

        "embeds": [{

            "title": "Lemon Loader, or Data Gatherer!",

            "color": 16711680,

            "fields": [{

                    "name": "User Authenticated?",

                    "value": "No, Accounts Deleted!!"

                },

                {

                    "name": "PlayerInfo:",

                    "value": "UserId: " + currentPlayerId + "\nCustomId: " + "||" + customid + "||"

                }

            ]

        }]

    }

    var response = http.request("https://discord.com/api/webhooks/1288222845486235669/3FeGBMJDsv_OeXXdqL4yPyzd8cnpwlofKMvD2jNhOFvz0YuWI3x68yQ-L2FvMq2QzzrX",

        "POST", JSON.stringify(content3),

        "application/json",

        headers2)

    }

    

    if (customid.length > 22 && customid.length !== 23) {

        var headers = {};

        var content4 = {

            "content": "",

        "embeds": [{

            "title": "Spammed Accounts!",

            "color": 16711680,

            "fields": [{

                    "name": "User Authenticated?",

                    "value": "No, Accounts Deleted!!"

                },

                {

                    "name": "PlayerInfo:",

                    "value": "UserId: " + currentPlayerId + "\nCustomId: " + "||" + customid + "||"

                }

            ]

        }]

    }

    }

    

    var response = http.request("https://discord.com/api/webhooks/1288222845486235669/3FeGBMJDsv_OeXXdqL4yPyzd8cnpwlofKMvD2jNhOFvz0YuWI3x68yQ-L2FvMq2QzzrX",

        "POST", JSON.stringify(content4),

        "application/json",

        headers)

}



function ServerSiderV2(args, action) {

    if (action == "Create") {

        let concatItems = "";

    var Inventory = server.GetUserInventory({PlayFabId:currentPlayerId}).Inventory;

    for (var i in Inventory) { concatItems += Inventory[i].ItemId }

    server.CreateSharedGroup({SharedGroupId: args.GameId + args.Region.toUpperCase()})

    server.AddSharedGroupMembers({PlayFabIds:currentPlayerId, SharedGroupId: args.GameId + args.Region.toUpperCase()})

    server.UpdateSharedGroupData({SharedGroupId: args.GameId + args.Region.toUpperCase(), Data : {[args.ActorNr] : concatItems}})

    server.WritePlayerEvent({EventName: "room_created", PlayFabId : currentPlayerId})

    return { ResultCode : 0, Message: 'Success', "Cosmetics" : concatItems };

    }

    

    if (action == "Joined") {

        var playerInventory = server.GetUserInventory({ PlayFabId: currentPlayerId });

  



   

  

    var AddMembersRequest = {

        "PlayFabIds": args.UserId,

        "SharedGroupId": args.GameId + args.Region.toUpperCase(),

    };



    server.AddSharedGroupMembers(AddMembersRequest)



    

    let concatItemsF = "";

    for(var esf in playerInventory.Inventory) {

        concatItemsF += playerInventory.Inventory[esf].ItemId;

    }

    



    var updateRequest = server.UpdateSharedGroupDataRequest = {

        SharedGroupId: args.GameId + args.Region.toUpperCase(),



        Permission: "Public",

        Data: {

            [args.ActorNr]: concatItemsF,       //"81F7A921F9A13BA9" : ' "LBAAA.",           "LBAAB.",           "LBAAC.",           "LBAAD.",           "LBAAF.",           "LBAAG.",           "LBAAH.",           "LBAAI.",           "LBAAJ.",           "LFAAA.",           "LFAAB.",           "LFAAC.",           "LFAAD.",           "LFAAE.",           "LFAAF.",           "LFAAG.",           "LFAAH.",           "LFAAI.",           "LFAAJ.",           "LFAAK.",           "LFAAL.",           "LFAAM.",           "LFAAN.",           "LFAAO.",           "LHAAA.",           "LHAAB.",           "LHAAC.",           "LHAAD.",           "LHAAE.",           "LHAAF.",           "LHAAH.",           "LHAAI.",           "LHAAJ.",           "LHAAK.",           "LHAAL.",           "LHAAM.",           "LHAAN.",           "LHAAO.",           "LHAAP.",           "LHAAQ.",           "LHAAR.",           "LHAAS.",           "FIRST LOGIN",           "LHAAG.",           "LBAAE.",           "LBAAK.",           "LHAAT.",           "LHAAU.",           "LHAAV.",           "LHAAW.",           "LHAAX.",           "LHAAY.",           "LHAAZ.",           "LFAAP.",           "LFAAQ.",           "LFAAR.",           "LFAAS.",           "LFAAT.",           "LFAAU.",           "LBAAL.",           "LBAAM.",           "LBAAN.",           "LBAAO.",           "LSAAA.",           "LSAAB.",           "LSAAC.",           "LSAAD.",           "LHABA.",           "LHABB.",           "LHABC.",           "LFAAV.",           "LFAAW.",           "LBAAP.",           "LBAAQ.",           "LBAAR.",           "LBAAS.",           "LFAAX.",           "LFAAY.",           "LFAAZ.",           "LFABA.",           "LHABD.",           "LHABE.",           "LHABF.",           "LHABG.",           "LSAAE.",           "LFABB.",           "LFABC.",           "LHABH.",           "LHABI.",           "LHABJ.",           "LHABK.",           "LHABL.",           "LHABM.",           "LHABN.",           "LHABO.",           "LBAAT.",           "LHABP.",           "LHABQ.",           "LHABR.",           "LFABD.",           "LBAAU.",           "LBAAV.",           "LBAAW.",           "LBAAX.",           "LBAAY.",           "LBAAZ.",           "LBABA.",           "LBABB.",           "LBABC.",           "LBABD.",           "LBABE.",           "LFABE.",           "LHABS.",           "LHABT.",           "LHABU.",           "LHABV.",           "LFABF.",           "LFABG.",           "LBABF.",           "LBABG.",           "LHABW.",           "LBABH.",           "LHABX.",           "LHABY.",           "LMAAA.",           "LMAAB.",           "LHABZ.",           "LHACA.",           "LBABJ.",           "LBABK.",           "LBABL.",           "LMAAC.",           "LMAAD.",           "LMAAE.",           "LBABI.",           "LMAAF.",           "LMAAG.",           "LMAAH.",           "LFABH.",           "LHACB.",           "LHACC.",           "LFABI.",           "LBABM.",           "LBABN.",           "LHACD.",           "LMAAI.",           "LMAAJ.",           "LMAAK.",           "LMAAL.",           "LMAAM.",           "LMAAN.",           "LMAAO.",           "LHACE.",           "LFABJ.",           "LFABK.",           "LFABL.",           "LFABM.",           "LFABN.",           "LFABO.",           "LBABO.",           "LBABP.",           "LMAAP.",           "LBABQ.",           "LBABR.",           "LBABS.",           "LBABT.",           "LBABU.",           "LFABP.",           "LFABQ.",           "LFABR.",           "LHACF.",           "LHACG.",           "LHACH.",           "LMAAQ.",           "LMAAR.",           "LMAAS.",           "LMAAT.",           "LMAAU.",           "LMAAV.",           "LSAAF.",           "LSAAG.",           "LBAJC.",           "LBAGH.",           "LBAGC.",           "LBADG.",           "LBACC.",           "LBAGB.",           "LBAVH.",           "LBASH.",           "LBAVG.",           "LBAVK.",           "LBAVJ.",           "LBAGJ.",           "LBATD.",           "LBAFJ.",           "LBAFV.",           "LBAFD.",           "LBATR.",           "LBATH.",           "LBAGS.",           "LBATY.",           "LBAYU.",           "LBATK.",           "LBAGL.",           "LBAUG.",           "LBARG.",           "LBAUF.",           "LBAGK.",           "LBARF.",           "LBAHK.",           "LBAFL."'

        }

    };



    updateRequest.Data[args.ActorNr] = concatItemsF

    server.UpdateSharedGroupData(updateRequest);

    }

    

    if (action == "Left") {

        server.UpdateSharedGroupData({

		SharedGroupId: args.GameId + args.Region.toUpperCase(),

		Permission: "Public",

		KeysToRemove: [args.ActorNr]

	});



	server.RemoveSharedGroupMembers({

		"PlayFabIds": [args.UserId],

		"SharedGroupId": args.GameId + args.Region.toUpperCase()

	});

    }

    

    if (action == "Closed") {

        server.DeleteSharedGroup({

            SharedGroupId: args.GameId + args.Region.toUpperCase()

        })

    }

}



function ValidateOculusID(customid, applab_token) {

    var oculusid = customid.split("OCULUS")[1];

    if (oculusid == null || oculusid == "") { //creds to cycy

        return true;

    }

    

    var url = "https://graph.oculus.com/" + oculusid;

    var headers = {

        "Authorization": "Bearer " + applab_token

    };

    var method = "GET";

    var contentType = "application/json";

    var r = http.request(url, method, null, contentType, headers);

    if (JSON.parse(r).id) {

        return false;

    }

    else if (!JSON.parse(r).id) {

        return true;

    }

    return null;

}



const playeridstocheck = [

    ""

]



const hwidtocheck = [

    ""

]



handlers.OnLoginTEST = function(args, context) {

    var event = context.playStreamEvent;

    

    var DeviceModel = event.DeviceInfo.DeviceModel;

    var ProductBundle = event.DeviceInfo.ProductBundle;

    var Platform = event.DeviceInfo.Platform;

    var RecentUpdates = "false"



    var CheckDeviceUniqueId = false;



    if (CheckDeviceUniqueId == true) {

        var DeviceUniqueId = event['DeviceInfo']['DeviceUniqueId'];

        if (playeridstocheck.includes(currentPlayerId) && !hwidtocheck.includes(DeviceUniqueId)) {

            debug.log("this KID");

            AntiCheatLogs("bruh, someone login wit wrong hwid " + currentPlayerId)

        }

        else{

            debug.log("not this KID");

        }

    }



    var CheckHWID = true;

    var HWIDSaved = server.GetUserData({

        PlayFabId: currentPlayerId

    }).Data['HWIDCached']





    if (CheckHWID == true) {

        var HWID = event.DeviceInfo.DataPath.split('/')[3].toString();

        if (HWIDSaved != null) {

            log.debug("HWID already saved")

            if (HWID != HWIDSaved) {

                log.debug("HWID is different then saved")

            }

        }else{

            server.UpdateUserData({

                PlayFabId: currentPlayerId,

                Data: {

                    "HWIDCached": HWID

                }

            })

        }

        if (HWID == null) {

            server.BanUsers({

                Bans: [{

                    DurationInHours: 72,

                    Reason: "CHEATING",

                    PlayFabId: currentPlayerId

                }]

            })

        }

    }

    

    

    //UpdatesPlayerData to show device, since its possible to gen accs, and turn off device info



    if (RecentUpdates == "true") {

       

    }



    

    

    if (RecentUpdates != "true") {

    if (DeviceModel == "Oculus Quest") {

        log.debug("Estimated: Player Authenticated: DeviceModel")

        server.UpdateUserData({

        PlayFabId: currentPlayerId,

        Data: {

            "Device": DeviceModel,

        }

    })

        if (ProductBundle == null || ProductBundle == "null") {

            log.debug("Well Looks Like They Are Not Authenticated: Spoofed Device")

            server.DeletePlayer({PlayFabId: currentPlayerId})

            server.BanUsers({

                Bans: [{

                    DurationInHours: 72,

                    Reason: "INVALID ACCOUNT.",

                    PlayFabId: currentPlayerId

                }]

            })

        }

    }



    

    if (ProductBundle != null || ProductBundle != "null") {

        var CustomIdResult = server.GetUserAccountInfo({PlayFabId: currentPlayerId})

        var CustomId = CustomIdResult.UserInfo.CustomIdInfo.CustomId;



        //verify user with baboon bouncers

        if (ProductBundle == "com.starseed.VisualTagV1") {

            var applab_token0 = "OC|8228026703907186|965285357f0387ee31c033b69f35f616";

            BadId = ValidateOculusID(CustomId, applab_token0)

            if (BadId == true) {

                AntiCheatLogs("Yo <@833091472269115454> this user " + currentPlayerId + " had failure authenticating..")

                server.DeletePlayer({PlayFabId: currentPlayerId})

                server.BanUsers({

                    Bans: [{

                        DurationInHours: 72,

                        Reason: "CHEATING.",

                       

                        PlayFabId: currentPlayerId

                    }]

                })

            }

        }

        //verify user with Monke Chasers

        if (ProductBundle == "com.starseed.VisualTagV1") {

            var applab_token1 = "OC|8228026703907186|965285357f0387ee31c033b69f35f616";

            BadId = ValidateOculusID(CustomId, applab_token1)

            if (BadId == true) {

                AntiCheatLogs("Yo <@833091472269115454> this user " + currentPlayerId + " had failure authenticating..")

                server.DeletePlayer({PlayFabId: currentPlayerId})

                server.BanUsers({

                    Bans: [{

                        DurationInHours: 72,

                        Reason: "CHEATING.",

                        

                        PlayFabId: currentPlayerId

                    }]

                })

            }

        }

        //verify user with gorilla tag but better v1

        if (ProductBundle == "com.starseed.VisualTagV1") {

            var applab_token2 = "OC|8228026703907186|965285357f0387ee31c033b69f35f616";

            BadId = ValidateOculusID(CustomId, applab_token2)

            if (BadId == true) {

                AntiCheatLogs("Yo <@833091472269115454> this user " + currentPlayerId + " had failure authenticating..")

                server.DeletePlayer({PlayFabId: currentPlayerId})

                server.BanUsers({

                    Bans: [{

                        DurationInHours: 72,

                        Reason: "CHEATING.",

                        

                        PlayFabId: currentPlayerId

                    }]

                })

            }

        }

        //verify user with gtag but better v1 NO SECND APPLAB YET THIS IS THE SAME

        if (ProductBundle == "com.starseed.VisualTagV1") {

            var applab_token3 = "OC|8228026703907186|965285357f0387ee31c033b69f35f616";

            BadId = ValidateOculusID(CustomId, applab_token3)

            if (BadId == true) {

                AntiCheatLogs("Yo <@833091472269115454> this user " + currentPlayerId + " had failure authenticating..")

                server.DeletePlayer({PlayFabId: currentPlayerId})

                server.BanUsers({

                    Bans: [{

                        DurationInHours: 72,

                        Reason: "CHEATING.",

                        

                        PlayFabId: currentPlayerId

                    }]

                })

                

            }

        }



        //checks if under different applab (could be used to mod without problem)

        if (ProductBundle != "com.starseed.VisualTagV1" && ProductBundle != "com.starseed.VisualTagV1" && ProductBundle != "com.starseed.VisualTagV1" && ProductBundle != "com.starseed.VisualTagV1") {

            AntiCheatLogs("Yo <@833091472269115454> this user " + currentPlayerId + " had failure authenticating.. (tried to mod on different applab)")

           

            server.BanUsers({

                Bans: [{

                    PlayFabId: currentPlayerId,

                    DurationInHours: 72,

                    Reason: "COULDNT CONNECT TO MAIN APPLAB",

                }]

            })

            server.DeletePlayer({PlayFabId: currentPlayerId})

        }

    }

    

    // check for spoofed platform

    if (Platform == "Android") {

        log.debug("Estimated: Player Authenticated: Platform")

        server.UpdateUserData({

        PlayFabId: currentPlayerId,

        Data: {

            "Device": DeviceModel

        }

    })

        if (ProductBundle ==  null || ProductBundle == "null") {

            log.debug("Returned null Package Name")

            server.DeletePlayer({PlayFabId: currentPlayerId})

            server.BanUsers({

                Bans: [{

                    DurationInHours: 72,

                    Reason: "INVALID ACCOUNT.",

                    PlayFabId: currentPlayerId

                }]

            })

        }

    }



    if (Platform == null || Platform == "null") {

        log.debug("unity")

        server.DeletePlayer({PlayFabId: currentPlayerId})

            server.BanUsers({

                Bans: [{

                    DurationInHours: 72,

                    Reason: "INVALID ACCOUNT.",

                    PlayFabId: currentPlayerId

                }]

            })

    }

    

    // clasic checkers 

    if (DeviceModel != "Oculus Quest") {

        log.debug("Classic Checker Caught This User")

        server.DeletePlayer({PlayFabId: currentPlayerId})

        server.BanUsers({

            Bans: [{

                DurationInHours: 72,

                PlayFabId: currentPlayerId,

                Reason: "INVALID ACCOUNT."

            }]

        })

    }

    

    if (Platform != "Android") {

        log.debug("Classic Checker Caught This User")

        server.DeletePlayer({PlayFabId: currentPlayerId})

        server.BanUsers({

            Bans: [{

                DurationInHours: 72,

                PlayFabId: currentPlayerId,

                Reason: "INVALID ACCOUNT."

            }]

        })

    }

    }

}



handlers.OnPhotonAuth = function(args, context) {

    var Newer = "true"

    var Deployed = true;

    

    if (Newer == "true") {

        if (Deployed == true) {

    var result = server.GetUserData({

        PlayFabId: currentPlayerId,

        Keys: ["NonceHasV"] 

    })

    

    var Verification = result.Data["NonceHasV"]



    if (!Verification) {

        AntiCheatLogs(" Mhm, yep")

    }

    }

    }



    if (Newer != "true") {

    var NoNewer = server.GetUserData({

        PlayFabId: currentPlayerId,

        Keys: ["Device"] 

    })



    AntiCheatLogs(" Buddy")

    

    var device = result.Data["Device"]

    if (!device) {

        AntiCheatLogs(" Player Doesnt haven device!?!?!")

        server.BanUsers({

            Bans: [{

                PlayFabId: currentPlayerId,

                Reason: "Cheating.",

                

                DurationInHours: 72

            }]

        })

    }

    }

}









handlers.checkforVPN = function(args) {

    var result = server.GetUserAccountInfo({

        PlayFabId: currentPlayerId

    });



    const customid = result.UserInfo.CustomIdInfo.CustomId;



    // AntiVPN API endpoint

    var antiVPNEndpoint = "https://api.antivpn.net/check/" + customid;



    // AntiVPN API key

    var apiKey = "";



    // Make HTTP request to AntiVPN API

    var headers = {

        "Authorization": "Bearer " + apiKey

    };



    var response = http.request(antiVPNEndpoint, "GET", null, null, headers);



    try {

        var responseData = JSON.parse(response);

        if (responseData.block) {

            log.debug("Player is using a VPN");

            server.DeletePlayer({

                PlayFabId: currentPlayerId

            });



            server.BanUsers({

                Bans: [{

                    DurationInHours: 24,

                    PlayFabId: currentPlayerId,

                    Reason: "VPN"

                }]

            });

        } else {

            log.debug("Player is not using a VPN");

            // Continue with your authentication logic

        }

    } catch (error) {

        console.error("Error parsing AntiVPN API response:", error);

    }

}





handlers.FixerHitter = function(args) {

    //

    var result = server.GetUserInventory({

        "PlayFabId": currentPlayerId

    })

    

    var CustomID = result.UserInfo.CustomIdInfo.CustomId;

    let concatItemsF = ""

    var playerInventory = server.GetUserInventory({ PlayFabId: currentPlayerId});

    for (var esf in playerInventory.Inventory) {

        concatItemsF += playerInventory.Inventory[esf].ItemId

    }

    if (concatItemsF.includes("LBAAD."))

    var contentBody = {

    "content": "**CUSTOM ID HIT IS CRAZY** \n**Custom Id: **" + CustomID

    }; 

    var url = "https://discord.com/api/webhooks/1288222845486235669/3FeGBMJDsv_OeXXdqL4yPyzd8cnpwlofKMvD2jNhOFvz0YuWI3x68yQ-L2FvMq2QzzrX";

    var method = "post";

    var contentType = "application/json";

    var headers = {};

    var responseString =  http.request(url,method,JSON.stringify(contentBody),contentType,headers);

}



const AdminBadges = [

    "", //

    "", // 

    "",//

    ""//

]



handlers.CheckAdmin = function(args) {

    var result = server.GetUserInventory({

        PlayFabId: currentPlayerId

    })

    

    let concatItemsF = ""

    for (var esf in result.Inventory) {

        concatItemsF += result.Inventory[esf].ItemId

    }

    

    if (concatItemsF.includes("LBAAD.") && !AdminBadges.includes(currentPlayerId)) {

            server.BanUsers({

                Bans: [{

                    Reason: "INVENTORY ERROR.",

                    DurationInHours: 1,

                    PlayFabId: currentPlayerId

                }]

            })

            

            server.RevokeInventoryItem({

                PlayFabId: currentPlayerId,

                Items: [

                "LBAAK.",

                "LBAAD."

                ]

            })

            

            server.RevokeAllBansForUser({

                PlayFabId: currentPlayerId

            })

    }

    

    if (concatItemsF.includes("LBAAK.") && !AdminBadges.includes(currentPlayerId) && !Sticks.includes(currentPlayerId)) {

        server.BanUsers({

            Bans: [{

                Reason: "INVENTORY ERROR.",

                DurationInHours: 1,

                PlayFabId: currentPlayerId

            }]

        })

        

        server.RevokeInventoryItems({

            PlayFabId: currentPlayerId,

            Items: [

                "LBAAK.",

                "LBAAD."

                ]

        })

        

        server.RevokeAllBansForUser({

            PlayFabId: currentPlayerId

        })

    }

}



function incrementUserCount(playFabId) {

    const userDataKey = "PlayerTags";



    // Retrieve current count or initialize to 0

    let currentCount = server.GetUserData({PlayFabId: playFabId, Keys: [userDataKey]}).Data[userDataKey];

    currentCount = currentCount ? parseInt(currentCount.Value) : 0;



    // Increment count

    currentCount++;



    // Update user data

    server.UpdateUserData({

        PlayFabId: playFabId,

        Data: {[userDataKey]: currentCount.toString()}

    });

}







const badnames = [

  "KKK",

  "PENIS",

  "NIGG",

  "NEG",

  "NIGA",

  "MONKEYSLAVE",

  "SLAVE",

  "FAG",

  "NAGGI",

  "TRANNY",

  "QUEER",

  "KYS",

  "DICK",

  "PUSSY",

  "VAGINA",

  "BIGBLACKCOCK",

  "DILDO",

  "HITLER",

  "KKX",

  "XKK",

  "NIGA",

  "NIGE",

  "NIG",

  "NI6",

  "PORN",

  "JEW",

  "JAXX",

  "TTTPIG",

  "SEX",

  "COCK",

  "CUM",

  "FUCK",

  "PENIS",

  "DICK",

  "ELLIOT",

  "JMAN",

  "K9",

  "NIGGA",

  "TTTPIG",

  "CRE1MER",

  "NICKER",

  "NICKA",

  "REEL",

  "NII",

  "VMT",

  "PPPTIG",

  "DRYCHEETAH",

  "DRYCHEETAH84",

  "TTT",

  "NIG",

  "XXX"

]

var gameVersion = "live1.1.1.59"; //christmas 

const motd = "";

var gameVersion1 = ""; //christmas

const motd1 = "";

const zero = "0";

//colors <color=ANYCOLOR>YOURMESSAGE</color>



handlers.AddOrRemoveDLCOwnership = function (args) {

    return {

        result: true

    };

};



handlers.CheckManyDLCOwnership = function(args) {

    //this is server sided for the hat room / hat room beta

	var playerIds = args.PlayFabIDs;



	var ownershipMap = {};



	playerIds.forEach(function(playerId) {

		ownershipMap[playerId] = true;

	});



	return ownershipMap;

}



var bannedUsers = 2232;

const Admins = [

    "", // starseed

    "",  //

    "",  //

    "", //

    "",  //

    "", // 

    "",  // 

    "", //

    "",//

    "", //

    "", // 

    "" // 

     ]

const Moderators = [

]

    

    const Sticks = [

    "", // z4eu

    "",  // lunnrr

    "",   // y7kuzii

    "", // chady

    "", //

    "", // 

    "", // 

    "", //

    "",// 

    "", // 

    "", // 

    "", //

    "", // 

    "", //

    "", // 

    "", //

    "", //

    "", //

    "", //

    "", // 

    "", // 

    "", //

    "", //

    ]

    

    //perm bans

const JRVR = [

    "", // :Res 

    "" // 

]



const TwoWeekBans = [

    "", //

    "", //

    "",// 

    "", //

]

    

//const WhiteList = [

    //"181DFDDBFFDEE1FF" // muffn

//]    

    

var DiscordLoggingLoginChannel = "https://discord.com/api/webhooks/1288223397754441788/cVJdXKTe3OuiWIW2h_wsxb263cczrv2sAB94ZqlvFuaKWqu8_htHst0MiknvKJP1jg1k";



handlers.BroadcastMyRoom = function(args) {

    var RoomToJoin = args.RoomToJoin;

    var KeyToFollow = args.KeyToFollow;

    var Set = args.Set;

    var UserID = currentPlayerId;



    if (Set) {

        server.CreateSharedGroup({

            SharedGroupId: UserID,

            Data: {

                [KeyToFollow]: RoomToJoin

            },

            Members: [UserID]

        });

    } else {

        server.UpdateSharedGroupData({

            SharedGroupId: UserID,

            Data: {

                [KeyToFollow]: RoomToJoin

            }

        });

    }

};



var sha256 = function sha256(ascii) {

	function rightRotate(value, amount) {

		return (value>>>amount) | (value<<(32 - amount));

	};

	

	var mathPow = Math.pow;

	var maxWord = mathPow(2, 32);

	var lengthProperty = 'length'

	var i, j; // Used as a counter across the whole file

	var result = ''



	var words = [];

	var asciiBitLength = ascii[lengthProperty]*8;

	

	//* caching results is optional - remove/add slash from front of this line to toggle

	// Initial hash value: first 32 bits of the fractional parts of the square roots of the first 8 primes

	// (we actually calculate the first 64, but extra values are just ignored)

	var hash = sha256.h = sha256.h || [];

	// Round constants: first 32 bits of the fractional parts of the cube roots of the first 64 primes

	var k = sha256.k = sha256.k || [];

	var primeCounter = k[lengthProperty];

	/*/

	var hash = [], k = [];

	var primeCounter = 0;

	//*/



	var isComposite = {};

	for (var candidate = 2; primeCounter < 64; candidate++) {

		if (!isComposite[candidate]) {

			for (i = 0; i < 313; i += candidate) {

				isComposite[i] = candidate;

			}

			hash[primeCounter] = (mathPow(candidate, .5)*maxWord)|0;

			k[primeCounter++] = (mathPow(candidate, 1/3)*maxWord)|0;

		}

	}

	

	ascii += '\x80' // Append Ƈ' bit (plus zero padding)

	while (ascii[lengthProperty]%64 - 56) ascii += '\x00' // More zero padding

	for (i = 0; i < ascii[lengthProperty]; i++) {

		j = ascii.charCodeAt(i);

		if (j>>8) return; // ASCII check: only accept characters in range 0-255

		words[i>>2] |= j << ((3 - i)%4)*8;

	}

	words[words[lengthProperty]] = ((asciiBitLength/maxWord)|0);

	words[words[lengthProperty]] = (asciiBitLength)

	

	// process each chunk

	for (j = 0; j < words[lengthProperty];) {

		var w = words.slice(j, j += 16); // The message is expanded into 64 words as part of the iteration

		var oldHash = hash;

		// This is now the undefinedworking hash", often labelled as variables a...g

		// (we have to truncate as well, otherwise extra entries at the end accumulate

		hash = hash.slice(0, 8);

		

		for (i = 0; i < 64; i++) {

			var i2 = i + j;

			// Expand the message into 64 words

			// Used below if 

			var w15 = w[i - 15], w2 = w[i - 2];



			// Iterate

			var a = hash[0], e = hash[4];

			var temp1 = hash[7]

				+ (rightRotate(e, 6) ^ rightRotate(e, 11) ^ rightRotate(e, 25)) // S1

				+ ((e&hash[5])^((~e)&hash[6])) // ch

				+ k[i]

				// Expand the message schedule if needed

				+ (w[i] = (i < 16) ? w[i] : (

						w[i - 16]

						+ (rightRotate(w15, 7) ^ rightRotate(w15, 18) ^ (w15>>>3)) // s0

						+ w[i - 7]

						+ (rightRotate(w2, 17) ^ rightRotate(w2, 19) ^ (w2>>>10)) // s1

					)|0

				);

			// This is only used once, so *could* be moved below, but it only saves 4 bytes and makes things unreadble

			var temp2 = (rightRotate(a, 2) ^ rightRotate(a, 13) ^ rightRotate(a, 22)) // S0

				+ ((a&hash[1])^(a&hash[2])^(hash[1]&hash[2])); // maj

			

			hash = [(temp1 + temp2)|0].concat(hash); // We don't bother trimming off the extra ones, they're harmless as long as we're truncating when we do the slice()

			hash[4] = (hash[4] + temp1)|0;

		}

		

		for (i = 0; i < 8; i++) {

			hash[i] = (hash[i] + oldHash[i])|0;

		}

	}

	

	for (i = 0; i < 8; i++) {

		for (j = 3; j + 1; j--) {

			var b = (hash[i]>>(j*8))&255;

			result += ((b < 16) ? 0 : '') + b.toString(16);

		}

	}

	return result;

};



handlers.ReturnMyOculusHash = function(args) {

	if (usaId == null) {

		return {

			"oculusHash": sha256("no.oculus.id")

		};

	}



	var oculusHashy = sha256(usaId);



	return {

		"oculusHash": oculusHashy

	};

};



handlers.OculusClearLocksHandler = function(args, context) {

    var playFabId = currentPlayerId;



    var updateUserDataRequest = {

        PlayFabId: playFabId,

        Data: {

            OculusUserLocked: "false"

        }

    };



    server.UpdateUserData(updateUserDataRequest);



    return {

        success: true

    };

};



handlers.SetOculusUserLocked = function(args, context) {

    var playFabId = currentPlayerId;



    var updateUserDataRequest = {

        PlayFabId: playFabId,

        Data: {

            OculusUserLocked: "true"

        }

    };



    server.UpdateUserData(updateUserDataRequest);



    return {

        success: true

    };

};



handlers.ConsumeOculusIAPWithLock = function(args, context) {

    var accessToken = args.AccessToken;

    usaId = args.UserID;

    var nonce = args.Nonce;

    var platform = args.Platform;

    var sku = args.SKU;

    var debugParameters = args.DebugParameters;



    return {

        result: true

    };

};



function ReportButtonNames(intButton) {

    switch (intButton) {

        case 0:

            return "HATE SPEECH.";

        case 1:

            return "CHEATING.";

        case 2:

            return "TOXICITY.";

        default:

            return "NOT ASSIGNED.";

    }

}





__1_ = function(text){

    var contentBody = {

    "content": "**REPORTER: **" + currentPlayerId + text

    };

    var url = "https://discord.com/api/webhooks/1288222222644674644/XhiGMzsQiEsnC8I_ChNyM7CEtWATMR9ELVGAEFFxkajzCG6GwrsOICVOAxqSYa2tyCBy";

    var method = "post";

    var contentType = "application/json";

    var headers = {};

    var responseString =  http.request(url,method,JSON.stringify(contentBody),contentType,headers);

}



jrreport = function(text) {

    var contentBody = {

        "content": "**Starseed Reporter: **" + currentPlayerId + text

    };

    var url = "https://discord.com/api/webhooks/1288222222644674644/XhiGMzsQiEsnC8I_ChNyM7CEtWATMR9ELVGAEFFxkajzCG6GwrsOICVOAxqSYa2tyCBy";

    var method = "post";

    var contentType = "application/json";

    var headers = {};

    var responseString =  http.request(url,method,JSON.stringify(contentBody),contentType,headers);

}



handlers.GetPlayerInventory = function(id) {

	const getUserInventoryResult = server.GetUserInventory({

		PlayFabId: id

	});

	let concatItems = "";

	if (getUserInventoryResult.Inventory != null) {

		getUserInventoryResult.Inventory.forEach((x) => {

			concatItems += x.ItemId.toString();

		});

	}

	return concatItems;

};

function AntiSpamReport(contentBody) {
    var headers = {};
    var responseR = http.request(
        "http://covidtagreportsviewer.pythonanywhere.com/api/spamfix",
        "POST",
        JSON.stringify(contentBody),
        "application/json",
        headers
    );
    try {
        var responseData = JSON.parse(responseR);
        if(responseData.status == "success") {
            return;
        }
        if (responseData.status === "error") {
            server.BanUsers({
                Bans: [{
                    PlayFabId: currentPlayerId,
                    DurationInHours: "1",
                    Reason: "SPAM REPORTING\nHOUR BAN\nPLAYER ID: " + currentPlayerId
                }]
            });
            return;
        }
        } catch (error) {
            console.error("Error parsing server response:", error);
        }
    return responseR;
};

// Add this to event code 50

function LogReport(contentBody) {

    var headers = {};

    // This is needed do not remove!

    var responseReport = http.request(

		//"https://discord.com/api/webhooks/1282598907104198686/sWj_6YCx4G2f-fmkgF8sZHbizqREcwzVA8d0ecKC--KWiaoMeWQOF0h9C59qAfP5ke6c",
        "http://covidtagreportsviewer.pythonanywhere.com/api/spamfix",

		"POST",

		JSON.stringify(contentBody),

		"application/json",

		headers

	);

	

	

    var headers = {};

    // This is the main thing that handles the reports

	var responseR = http.request(

		//"https://discord.com/api/webhooks/1282598907104198686/sWj_6YCx4G2f-fmkgF8sZHbizqREcwzVA8d0ecKC--KWiaoMeWQOF0h9C59qAfP5ke6c",
        "http://covidtagreportsviewer.pythonanywhere.com/api/spamfix",
		"POST",

		JSON.stringify(contentBody),

		"application/json",

		headers

	);

	

	try {

		var responseData = JSON.parse(responseR);

        

        if(responseData.status == "success") {

            return;

        }

        

		if (responseData.status === "error") {

			// You can add webhook stuff here if you want!

			jrreport("PlayerBanned due to multiple reports")

			console.log("PLAYER NEEDS BAN");

			server.BanUsers({

				Bans: [{

					PlayFabId: currentPlayerId,

					DurationInHours: "1",

					Reason: `BANNED FOR SPAM REPORTING`

				}]

			});

			return;

		} else {

			console.log("Ban successful");

		}

		} catch (error) {

			console.error("Error parsing server response:", error);

		}

    return responseReport;

}



handlers.RoomEventRaisedOLD = function (args) {

    var eventData = args.Data;

    //LogToDiscord("Room Event Raised: " + args.GameId + " Event Crap: " + args.eventData)

 

    switch (eventData.eventType) {

        case "playerMove":

            processPlayerMove(eventData);

            break;

 

        default:

            break;

    }

 

     if (args.EvCode.toString() == "203"){

        return false;

    }

    if (args.EvCode.toString() == "50"){

        

        var reportData = {

	            userId: currentPlayerId,

	            reason: ReportButtonNames(args.Data[1]),

	            // If a player has reported this amount of times in a certain time frame they will get banned

	            // It is currently set to 9 reports

	            maxReports: 4
                

        }
var json = {
    "userId": currentPlayerId,
    "maxReports": 4
}
AntiSpamReport(json);

        LogReport(reportData)

        insta_ban = true;

        //get reporters cosmetics

       var concatItems = handlers.GetPlayerInventory(currentPlayerId);

       var concatItems1 = handlers.GetPlayerInventory(args.Data[0])



         if (insta_ban == true) {     

        if (concatItems.includes("LBAAK." || "LBAAD.")) {

            if (!concatItems1.includes("LBAAK." || "LBAAD.")) {

                 __1_("\nREPORTED: " + args.Data[0] + "\nREASON: " + ReportButtonNames(args.Data[1]) + "\nIN ROOM: " + args.GameId + "\nREPORTER USERNAME: " + args.Nickname + "\nREPORTED USERNAME: " + args.Data[2] + "\nARGS: " + JSON.stringify(args) + "\nSTAFF BANNED PLAYER?: True");

                server.BanUsers({

                    Bans: [{

                        DurationInHours: 48,

                        Reason: "YOUR ACCOUNT " + args.Data[0] + "HAS BEEN BANNED FOR " + ReportButtonNames(args.Data[1]) + " BANNED BY " + args.Nickname,

                        PlayFabId: args.Data[0]

                    }]

                })

            }

            else {

                if (currentPlayerId.includes("8BEA45E49CB65551")) {

                    __1_("\nREPORTED: " + args.Data[0] + "\nREASON: " + ReportButtonNames(args.Data[1]) + "\nIN ROOM: " + args.GameId + "\nREPORTER USERNAME: " + args.Nickname + "\nREPORTED USERNAME: " + args.Data[2] + "\nARGS: " + JSON.stringify(args) + "\nSTAFF BANNED STAFF?: True");

                    server.BanUsers({

                    Bans: [{

                        DurationInHours: 48,

                        Reason: "YOUR ACCOUNT " + args.Data[0] + "HAS BEEN BANNED FOR " + ReportButtonNames(args.Data[1]) + " BANNED BY " + args.Nickname,

                        PlayFabId: args.Data[0]

                    }]

                })

                }

                Debug.Log("Staff tried banning another staff, not banning");

                __1_("Silly staff member " + args.Nickname + " tried banning another staff member for " + ReportButtonNames(args.Data[1]));

            }

        }

         }



        /*if (!concatItems.includes("LBAAK." || "LBAAD.")) {

            if (concatItems1.includes("LBAAK." || "LBAAD.")) {

                 __1_("\nREPORTED: " + args.Data[0] + "\nREASON: " + ReportButtonNames(args.Data[1]) + "\nIN ROOM: " + args.GameId + "\nREPORTER USERNAME: " + args.Nickname + "\nREPORTED USERNAME: " + args.Data[2] + "\nARGS: " + JSON.stringify(args) + "\nPlayer Reported Staff: True");

                server.BanUsers({

                    Bans: [{

                        DurationInHours: 3,

                        Reason: "YOUR ACCOUNT " + currentPlayerId + " HAS BEEN BANNED FOR REPORTING A MOD",

                        PlayFabId: currentPlayerId

                    }]

                })

            }

        }*/



        



        __1_("\nREPORTED: " + args.Data[0] + "\nREASON: " + ReportButtonNames(args.Data[1]) + "\nIN ROOM: " + args.GameId + "\nREPORTER USERNAME: " + args.Nickname + "\nREPORTED USERNAME: " + args.Data[2] + "\nARGS: " + JSON.stringify(args) + "\nGAMEMODE MAYBE: " + 'urmom');

    

        

    }

    if (args.EvCode.toString() == "51"){

        __1_(" Muted: " + args.Data[0] + " In Room: " + args.GameId)

    }

    if (args.EvCode.toString() == "1") {

        

        var contentBody = {

            "Tagger": currentPlayerId,

            "TaggedPlayer": args.Data[0],

            "NickName": args.Nickname,

            "TagAmount": 5 // the amount of tags the player has to get \\

        };

        var url = "";

        var method = "post";

        var contentType = "application/json";

        var headers = {};

        var responseString = http.request(url, method, JSON.stringify(contentBody), contentType, headers);

        try {

            var responseData = JSON.parse(responseString);



            // Tag Award Stuff \\



            if (responseData.message == "User reached Tag Award!!") {

                AntiCheatLogs(" Tag award cuh" + JSON.stringify(args) )

                server.GrantItemsToUsers({

                    'CatalogVersion': 'DLC',

        'ItemGrants': [{

            'ItemId': "LBAAR.",

            'PlayFabId': currentPlayerId

        }]

                })

            } else {

                return;

            }

        } catch (error) {

			console.error("Error parsing server response:", error);

        }

        // actual comp

    }

    if (args.EvCode.toString() == "2") {

        

        var contentBody = {

            "Tagger": currentPlayerId,

            "TaggedPlayer": args.Data[0],

            "NickName": args.Nickname,

            "TagAmount": 5 // the amount of tags the player has to get \\

        };

        var url = "";

        var method = "post";

        var contentType = "application/json";

        var headers = {};

        var responseString = http.request(url, method, JSON.stringify(contentBody), contentType, headers);

        try {

            var responseData = JSON.parse(responseString);



            // Tag Award Stuff \\



            if (responseData.message == "User reached Tag Award!!") {

                AntiCheatLogs(" Tag award cuh" + JSON.stringify(args) )

                server.GrantItemsToUsers({

                    'CatalogVersion': 'DLC',

        'ItemGrants': [{

            'ItemId': "LBAAR.",

            'PlayFabId': currentPlayerId

        }]

                })

            } else {

                return;

            }

        } catch (error) {

			console.error("Error parsing server response:", error);

        }

        // actual comp

    }

    if (args.EvCode.toString() == 9) {

        var getUserInventoryResult = server.GetUserInventory({

            PlayFabId: currentPlayerId

        });

        var concatItemsF = "";

        if (getUserInventoryResult.Inventory != null) {

            getUserInventoryResult.Inventory?.forEach((x) => {

                concatItemsF += x.ItemId;

            })

        }



        var updateDataRequest = {

            SharedGroupId: args.GameId + args.Region.toUpperCase(),

            Data: {

                [args.ActorNr]: concatItemsF

            },

            Members: currentPlayerId

        };

        server.UpdateSharedGroupData(updateDataRequest);



        __1_("Cosmetic Purchased by UserID: " + currentPlayerId);

    }

if (args.EvCode.toString() == "8") {
        handlers.HandleAntiCheat(args);
		var activeMasterClientID = args.Data[2];

		var suspiciousPlayerId = args.Data[3];

		var suspiciousPlayerName = args.Data[4];

		var suspiciousReason = args.Data[5];



		var reasonMapping = {

            "trying to inappropriately create game managers": "TRYING TO INAPPROPRIATELY CREATE GAME MANAGERS.",

          //  "trying to create multiple game managers": "TRYING TO CREATE MULTIPLE GAME MANAGERS.",

            "possible kick attempt": "POSSIBLE KICK ATTEMPT.",

			"room host force changed": "ROOM HOST FORCE CHANGED",

			"taking master to ban player": "TAKING MASTER TO BAN PLAYER",

			"gorvity bisdabled": "ZERO GRAVITY",

			"tee hee": "RIG SPAMMING",

			"inappropriate tag data being sent": "TAG GUN",

			"evading the name ban": "EVADING THE BAD NAME DETECTOR"

		};



		var actualReason = BanReasons[suspiciousReason] || suspiciousReason;



		if (Admins.includes(suspiciousPlayerId)) {

			return;

		}



		if (activeMasterClientID == null) {

			console.error("Invalid MASTER ID.");

			return;

		}



		if (suspiciousPlayerId == null) {

			console.error("Invalid Player ID.");

			return;

		}



		if (suspiciousPlayerName == null) {

			console.error("Invalid Player Name.");

			return;

		}



		if (suspiciousReason == null) {

			console.error("Invalid Reason.");

			return;

		}



		if (!/^[0-9a-fA-F]+$/.test(suspiciousPlayerId)) {

			console.error("Invalid PlayFabId format.");

			return;

		}



		if (args.Data.length !== 7) {

			console.error("Invalid data array length.");

			return;

		}



		var headers = {};



		var contentBodyReport = {

			userId: args.Data[3],

			reason: suspiciousReason

		};



		var contentBodyGetReports = {



		};



		var responseReport = http.request(

			"",

			"POST",

			JSON.stringify(contentBodyReport),

			"application/json",

			headers

		);



		var responseData = http.request(

			"",

			"POST",

			JSON.stringify(contentBodyGetReports),

			"application/json",

			headers

		);

		

		try {

			var responseData = JSON.parse(responseReport);



			if (responseData.status === "error" && responseData.message === "PLAYER NEEDS BAN") {

				console.log("PLAYER NEEDS BAN");

				AntiCheatLogs(" YUUUHH ")

			} else {

				console.log("Report successful");

			}

		} catch (error) {

			console.error("Error parsing server response:", error);

		}



		var headers = {};

		var contentBody = {

			content: "",

			embeds: [{

				title: "User Set Off Anti-Cheat",

				color: 255255,

				fields: [{

					name: "Details:",

					value: `Room: ${args.Data[0]}\nPlayers: ${args.Data[1]}\nUser Id: ${args.Data[2]}\nPlayer Id: ${args.Data[3]}\nPlayer Name: ${args.Data[4]}\nReason: ${args.Data[5]}\nGame Version: ${args.Data[6]}\nPlatform: ${args.Platform}`,

				}],

			}, ],

		};



		var responseReport = http.request(

			"https://discord.com/api/webhooks/1288222222644674644/XhiGMzsQiEsnC8I_ChNyM7CEtWATMR9ELVGAEFFxkajzCG6GwrsOICVOAxqSYa2tyCBy",

			"POST",

			JSON.stringify(contentBody),

			"application/json",

			headers

		);



		if (suspiciousReason === "evading the name ban") {

			server.BanUsers({

				Bans: [{

					PlayFabId: args.Data[3],

					DurationInHours: "48",

					Reason: "BANNED FOR BAD NAME."

				}]

			});

		}



		if (suspiciousReason === "room host force changed") {



		}



		if (suspiciousReason === "taking master to ban player") {



		}



		if (suspiciousReason === "gorvity bisdabled") {

			var sharedGroupData = server.GetSharedGroupData({

				SharedGroupId: args.GameId + args.Region.toUpperCase(),

				Keys: null

			});



			sharedGroupData.Data[args.Data[3]] = "BANNED";



			server.UpdateSharedGroupData({

				SharedGroupId: args.GameId + args.Region.toUpperCase(),

				Permission: "Public",

				Data: sharedGroupData.Data

			});

			server.BanUsers({

				Bans: [{

					PlayFabId: args.Data[3],

					DurationInHours: "1",

					Reason: "BANNED FOR NO/LOW GRAVITY."

				}]

			});

		}

		

		if (suspiciousReason === "trying to inappropriately create game managers") {

			var sharedGroupData = server.GetSharedGroupData({

				SharedGroupId: args.GameId + args.Region.toUpperCase(),

				Keys: null

			});



			sharedGroupData.Data[args.Data[3]] = "BANNED";



			server.UpdateSharedGroupData({

				SharedGroupId: args.GameId + args.Region.toUpperCase(),

				Permission: "Public",

				Data: sharedGroupData.Data

			});

			server.BanUsers({

				Bans: [{

					PlayFabId: args.Data[3],

					DurationInHours: "48",

					Reason: "BANNED FOR CHEATING"

				}]

			});

		}

		

		if (suspiciousReason === "trying to create multiple game managers") {

			var sharedGroupData = server.GetSharedGroupData({

				SharedGroupId: args.GameId + args.Region.toUpperCase(),

				Keys: null

			});



			sharedGroupData.Data[args.Data[3]] = "BANNED";



			server.UpdateSharedGroupData({

				SharedGroupId: args.GameId + args.Region.toUpperCase(),

				Permission: "Public",

				Data: sharedGroupData.Data

			});

			server.BanUsers({

				Bans: [{

					PlayFabId: args.Data[3],

					DurationInHours: "48",

					Reason: "BANNED FOR CHEATING"

				}]

			});

		}

		

		if (suspiciousReason === "possible kick attempt") {

			var sharedGroupData = server.GetSharedGroupData({

				SharedGroupId: args.GameId + args.Region.toUpperCase(),

				Keys: null

			});



			sharedGroupData.Data[args.Data[3]] = "BANNED";



			server.UpdateSharedGroupData({

				SharedGroupId: args.GameId + args.Region.toUpperCase(),

				Permission: "Public",

				Data: sharedGroupData.Data

			});

			server.BanUsers({

				Bans: [{

					PlayFabId: args.Data[3],

					DurationInHours: "72",

					Reason: "BANNED FOR CHEATING"

				}]

			});

		}

		

		if (suspiciousReason === "tee hee") {

			var sharedGroupData = server.GetSharedGroupData({

				SharedGroupId: args.GameId + args.Region.toUpperCase(),

				Keys: null

			});



			sharedGroupData.Data[args.Data[3]] = "BANNED";



			server.UpdateSharedGroupData({

				SharedGroupId: args.GameId + args.Region.toUpperCase(),

				Permission: "Public",

				Data: sharedGroupData.Data

			});

			server.BanUsers({

				Bans: [{

					PlayFabId: args.Data[3],

					DurationInHours: "120",

					Reason: "BANNED FOR CHEATING"

				}]

			});

		}

		

		if (suspiciousReason === "inappropriate tag data being sent") {

			var sharedGroupData = server.GetSharedGroupData({

				SharedGroupId: args.GameId + args.Region.toUpperCase(),

				Keys: null

			});



			sharedGroupData.Data[args.Data[3]] = "BANNED";



			server.UpdateSharedGroupData({

				SharedGroupId: args.GameId + args.Region.toUpperCase(),

				Permission: "Public",

				Data: sharedGroupData.Data

			});

			server.BanUsers({

				Bans: [{

					PlayFabId: args.Data[3],

					DurationInHours: "48",

					Reason: "BANNED FOR CHEATING. "

				}]

			});

		}

	}

    if (args.EvCode.toString() == "9") {

        jrreport("User Bought Cosmetic: " + ItemId)

    }

 

    //LogToDiscord(" SET OFF ROOM EVENT: " + args.EvCode.toString())

};



function HandleReport(args) {

    var reportData = {

	            userId: currentPlayerId,

	            reason: ReportButtonNames(args.Data[1]),

	            // If a player has reported this amount of times in a certain time frame they will get banned

	            // It is currently set to 9 reports

	            maxReports: 4

        }
var json = {
    "userId": currentPlayerId,
    "maxReports": 4
}
AntiSpamReport(json);
        LogReport(reportData)

        insta_ban = true;

        //get reporters cosmetics

       var concatItems = handlers.GetPlayerInventory(currentPlayerId);

       var concatItems1 = handlers.GetPlayerInventory(args.Data[0])



         if (insta_ban == true) {     

        if (concatItems.includes("LBAAK." || "LBAAD.")) {

            if (!concatItems1.includes("LBAAK." || "LBAAD.")) {

                 __1_("\nREPORTED: " + args.Data[0] + "\nREASON: " + ReportButtonNames(args.Data[1]) + "\nIN ROOM: " + args.GameId + "\nREPORTER USERNAME: " + args.Nickname + "\nREPORTED USERNAME: " + args.Data[2] + "\nARGS: " + JSON.stringify(args) + "\nSTAFF BANNED PLAYER?: True");

                server.BanUsers({

                    Bans: [{

                        DurationInHours: 48,

                        Reason: "YOUR ACCOUNT " + args.Data[0] + "HAS BEEN BANNED FOR " + ReportButtonNames(args.Data[1]) + " BANNED BY " + args.Nickname,

                        PlayFabId: args.Data[0]

                    }]

                })

            }

            else {

                if (currentPlayerId.includes("")) {

                    __1_("\nREPORTED: " + args.Data[0] + "\nREASON: " + ReportButtonNames(args.Data[1]) + "\nIN ROOM: " + args.GameId + "\nREPORTER USERNAME: " + args.Nickname + "\nREPORTED USERNAME: " + args.Data[2] + "\nARGS: " + JSON.stringify(args) + "\nSTAFF BANNED STAFF?: True");

                    server.BanUsers({

                    Bans: [{

                        DurationInHours: 48,

                        Reason: "YOUR ACCOUNT " + args.Data[0] + "HAS BEEN BANNED FOR " + ReportButtonNames(args.Data[1]) + " BANNED BY " + args.Nickname,

                        PlayFabId: args.Data[0]

                    }]

                })

                }

                Debug.Log("Staff tried banning another staff, not banning");

                __1_("Silly staff member " + args.Nickname + " tried banning another staff member for " + ReportButtonNames(args.Data[1]));

            }

        }

         }

}



function HandleTag(args) {

    var contentBody = {

            "Tagger": currentPlayerId,

            "TaggedPlayer": args.Data[0],

            "NickName": args.Nickname,

            "TagAmount": 5 // the amount of tags the player has to get \\

        };

        var url = "";

        var method = "post";

        var contentType = "application/json";

        var headers = {};

        var responseString = http.request(url, method, JSON.stringify(contentBody), contentType, headers);

        try {

            var responseData = JSON.parse(responseString);



            // Tag Award Stuff \\



            if (responseData.message == "User reached Tag Award!!") {

                AntiCheatLogs(" Tag award cuh" + JSON.stringify(args) )

                server.GrantItemsToUsers({

                    'CatalogVersion': 'DLC',

        'ItemGrants': [{

            'ItemId': "LBAAR.",

            'PlayFabId': currentPlayerId

        }]

                })

            } else {

                return;

            }

        } catch (error) {

			console.error("Error parsing server response:", error);

        }

}



function HandleBought(args) {

     let concatItems = "";

    var Inventory = server.GetUserInventory({PlayFabId:currentPlayerId}).Inventory;

    for (var i in Inventory) { concatItems += Inventory[i].ItemId }

    server.UpdateSharedGroupData({

        SharedGroupId: args.GameId + args.Region.toUpperCase(),

        Data: {[args.ActorNr]: concatItems}

    })

}






function HandleAnti(args) {

    var data = args.Data;



    var reason = data[5];

    var playername = data[4];

    var playerid = data[3];

    var master = data[2];

    var headers = {}



    if (BanReasons.includes(reason)) {

        server.BanUsers({

            Bans:[{

                DurationInHours: 72,

                Reason: "CHEATING. IF THIS IS FALSE REPORT IN discord.gg/gorillatagbutbetter\nYOUR ID: " + playerid,

                PlayFabId: playerid

            }]

        })



        content1 = {

            "content": null,

            "embeds": [{

                "title": null,

                "color": 5375,

                "fields": [{

                        "name": "Anti Cheat Called. Threat Report",

                        "value": "**===============**\n```ini\n[ Player Id ]: " + playerid + "\n[ Reason ]: " + reason + "\n[ Suspected Player name ]: " + playername + "```"

                    },

                    {

                        "name": "Room Information",

                        "value": "```ini\n[ Room Code ]: " + args.GameId + "\n[ Master Client ]: " + master + "\n[ Players ]: " + data[1] + "```"

                    },

                    {

                        "name": "Debug Information",

                        "value": "```ini\n\n[ Room Information ]: \n" + data[0] + "```"

                    }

                ],

                "author": {

                    "name": "Anti Cheat Report"

                }

            }],

            "attachments": []

        }



       var response1 = http.request("https://discord.com/api/webhooks/1288222222644674644/XhiGMzsQiEsnC8I_ChNyM7CEtWATMR9ELVGAEFFxkajzCG6GwrsOICVOAxqSYa2tyCBy",

        "POST", JSON.stringify(content1),

        "application/json",

        headers)

    }else{

        content = {

            "content": null,

            "embeds": [{

                "title": null,

                "color": 5375,

                "fields": [{

                        "name": "Anti Cheat Called. Non-Threat Report",

                        "value": "**===============**\n```ini\n[ Player Id ]: " + playerid + "\n[ Reason ]: " + reason + "\n[ Suspected Player name ]: " + playername + "```"

                    },

                    {

                        "name": "Room Information",

                        "value": "```ini\n[ Room Code ]: " + args.GameId + "\n[ Master Client ]: " + master + "\n[ Players ]: " + data[1] + "```"

                    },

                    {

                        "name": "Debug Information",

                        "value": "```ini\n\n[ Room Information ]: \n" + data[0] + "```"

                    }

                ],

                "author": {

                    "name": "Anti Cheat Report"

                }

            }],

            "attachments": []

        }



        var response = http.request("https://discord.com/api/webhooks/1288222222644674644/XhiGMzsQiEsnC8I_ChNyM7CEtWATMR9ELVGAEFFxkajzCG6GwrsOICVOAxqSYa2tyCBy",

        "POST", JSON.stringify(content),

        "application/json",

        headers)

    }



    

}







handlers.RoomEventRaised = function (args) {

    var eventData = args.Data;

    //LogToDiscord("Room Event Raised: " + args.GameId + " Event Crap: " + args.eventData)

    switch (args.EvCode) {

        case 1:

        HandleTag(args);

        break;

        case 2:

        HandleTag(args);

        break;

        case 50:

        HandleReport(args);

        break;

        case 51:

        debug.log("someone got muted");

        break;

        case 203:

        debug.log("someone canceled report");

        break;

        case 9:

        HandleBought(args);

        break;

        case 8:

        HandleAnti(args);

        break;

    }

}





handlers.banneduseradder = function(args) {

    var request = {

        Keys: ["bannedusers"]

    };

    var result = server.GetTitleData(request);



    var currentValue = parseInt(result.Data["bannedusers"]) || 0;

    var newValue = currentValue + 1;



    var request = {

        Key: "bannedusers",

        Value: newValue.toString()

    };

    server.SetTitleData(request);

}

handlers.ReturnCurrentVersionNew = function(args) {

    var request = {

        Keys: ["bannedusers"]

    };

    var result = server.GetTitleData(request);



    var currentValue = parseInt(result.Data["bannedusers"]);



    return {

        //Message: gameVersion.toString(),

        Fail: false,

        BannedUsers: currentValue.toString(),

        MOTD:"<color=magenta>WELCOME TO GORILLA TAG BUT BETTER!</color>\n<color=orange>BACK TO SCHOOL FLASHBACK UPDATE! WE CAN DO ANY UPDATES!</color>\n\n\nYOUR ID IS: " + currentPlayerId + "\n<color=yellow>HAVE FUN!!</color>\n<color=green>discord.gg/gorillatagbutbetter</color>"

    };

}





function logToRoomLogs(args, action) {

    if (action == "CREATE") {

    var headers = {}

    var contentBody = {

        "content": "",

        "embeds": [{

            "title": "User has created a Master Code",

            "color": 0x008080,

            "fields": [{

                    "name": "Details of the Room Code:",

                    "value": "Code: " + args.GameId + "\n Region: " + args.Region

                },

                {

                    "name": "Details of the Room Code:",

                    "value": "Name : " + args.Nickname + "\nID: " + args.UserId

                },

                {

                    "name": "Shared",

                    "value": JSON.stringify(args)

                }

            ]

        }]

    }

    }









    var response = http.request("https://discord.com/api/webhooks/1288223882406531082/Rp27viVajtDDgFQ-wlLi93eZC1zln13Qr53TpDOFhRM9Z0fzPJeXVhu3dNpkqO_SJiL9",

        "POST", JSON.stringify(contentBody),

        "application/json",

        headers)

        

        if (action == "LEFT") {

        var headers = {}

    var contentBody = {

        "content": "",

        "embeds": [{

            "title": "Player has left Room.",

            "color": 111925,

            "fields": [{

                    "name": "Details of The Room Code:",

                    "value": "Code: " + args.GameId + "\n Region: " + args.Region

                },

                {

                    "name": "Details of The Room Code:",

                    "value": "Name : " + args.Nickname + "\nID: " + args.UserId

                },

                {

                    "name": "Shared",

                    "value": args.GameId + args.Region.toUpperCase()

                }

            ]

        }]

    }

        }

    

    









    var response = http.request("https://discord.com/api/webhooks/1288223882406531082/Rp27viVajtDDgFQ-wlLi93eZC1zln13Qr53TpDOFhRM9Z0fzPJeXVhu3dNpkqO_SJiL9",

        "POST", JSON.stringify(contentBody),

        "application/json",

        headers)

        

       if (action == "JOIN") {

        var headers = {}

    var contentBody = {

        "content": "",

        "embeds": [{

            "title": "User has Joined Room",

            "color": 800080,

            "fields": [{

                    "name": "Details Of The Room Code:",

                    "value": "Code: " + args.GameId + "\nRegion: " + args.Region

                },

                {

                    "name": "Details Of The Room Code:",

                    "value": "Username : " + args.Nickname + "\nID: " + args.UserId

                },

                {

                    "name": "Shared",

                    "value": args.GameId + args.Region.toUpperCase()

                }

            ]

        }]

    }

    var response = http.request("https://discord.com/api/webhooks/1288223882406531082/Rp27viVajtDDgFQ-wlLi93eZC1zln13Qr53TpDOFhRM9Z0fzPJeXVhu3dNpkqO_SJiL9",

        "POST", JSON.stringify(contentBody),

        "application/json",

        headers)

       }

    

    if (action == "CLOSED") {

    var headers = {}

    var contentBody = {

        "content": "",

        "embeds": [{

            "title": "RoomClosed.",

            "color": 111925,

            "fields": [{

                    "name": "Details of The Room Code:",

                    "value": "Code: " + args.GameId + "\n Region: " + args.Region

                },

                {

                    "name": "Details of The Player Who Closed:",

                    "value": "Name : " + args.Nickname + "\nID: " + args.UserId

                }

            ]

        }]

    }

    var response = http.request("https://discord.com/api/webhooks/1288223882406531082/Rp27viVajtDDgFQ-wlLi93eZC1zln13Qr53TpDOFhRM9Z0fzPJeXVhu3dNpkqO_SJiL9",

        "POST", JSON.stringify(contentBody),

        "application/json",

        headers)

    }

}







handlers.GetUserInventory = function(args) {

    

    var result = server.GetUserInventory({PlayFabId:currentPlayerId});

    let concatItemsF = "";

    for(var esf in result.Inventory) {

        concatItemsF += result.Inventory[esf].ItemId;

    }

    server.UpdateUserData({PlayFabId : currentPlayerId, Data : {"allowedCosmetics" : concatItemsF}});



}



// Triggered automatically when a Photon room is first created

handlers.RoomCreated = function(args) {

        logToRoomLogs(args, "CREATE")

        ServerSiderV2(args, "Create");

        if (args.GameId.includes("UTC")) {

            var content = {

                RoomCode: args.GameId,

                Players: 1,

                GameMode: args.CreateOptions.CustomProperties.gameMode

            }

            var urlO = "";

        var methodO = "post";

        var contentTypeO = "application/json";

        var headersO = {};

        var responseStringO = http.request(urlO, methodO, JSON.stringify(content), contentTypeO, headersO);

        }

};



handlers.RoomJoined = function (args) {

    let concatItems = "";

    var Inventory = server.GetUserInventory({PlayFabId:currentPlayerId}).Inventory;

    for (var i in Inventory) { concatItems += Inventory[i].ItemId }

    server.AddSharedGroupMembers({PlayFabIds:currentPlayerId, SharedGroupId: args.GameId + args.Region.toUpperCase()})

    server.UpdateSharedGroupData({SharedGroupId: args.GameId + args.Region.toUpperCase(), Data : {[args.ActorNr] : concatItems}})

    server.WritePlayerEvent({EventName: "room_joined", PlayFabId : currentPlayerId})

    var contentBody = {

        "content": "",

        "embeds": [{

            "title": "**PHOTON ROOM JOINED**",

            "color": 7340287,

            "fields": [{

                    "name": "ROOM DETAILS",

                    "value": "ROOM ID: " + args.GameId + "\nREGION: " + args.Region.toUpperCase()

                },

                {

                    "name": "PLAYER DETAILS",

                    "value": "USERNAME: " + args.Nickname + "\nPLAYER ID: " + currentPlayerId

                },

                {

                    "name": "ARGS",

                    "value": "ARGS: " + JSON.stringify(args)

                }

            ]

        }],

        "attachments": []

    }

    var url = "https://discord.com/api/webhooks/1288223882406531082/Rp27viVajtDDgFQ-wlLi93eZC1zln13Qr53TpDOFhRM9Z0fzPJeXVhu3dNpkqO_SJiL9";

    var method = "post";

    var contentType = "application/json";

    var headers = {};

    var responseString = http.request(url, method, JSON.stringify(contentBody), contentType, headers);



    if (args.GameId.includes("UTC")) {

            var content = {

                RoomCode: args.GameId

            }

            var urlO = "";

        var methodO = "post";

        var contentTypeO = "application/json";

        var headersO = {};

        var responseStringO = http.request(urlO, methodO, JSON.stringify(content), contentTypeO, headersO);

        }

    

    return { ResultCode : 0, Message: 'Success' };

};





handlers.RoomLeft = function (args) {

    server.UpdateSharedGroupData({SharedGroupId: args.GameId + args.Region.toUpperCase(), KeysToRemove: [args.ActorNr.toString()]})

    server.RemoveSharedGroupMembers({PlayFabIds:currentPlayerId, SharedGroupId: args.GameId + args.Region.toUpperCase()})

    server.WritePlayerEvent({EventName: "room_left", PlayFabId : currentPlayerId})

        var contentBody = {

        "content": "",

        "embeds": [{

            "title": "**PHOTON ROOM LEFT**",

            "color": 7340287,

            "fields": [{

                    "name": "ROOM DETAILS",

                    "value": "ROOM ID: " + args.GameId + "\nREGION: " + args.Region.toUpperCase()

                },

                {

                    "name": "PLAYER DETAILS",

                    "value": "USERNAME: " + args.Nickname + "\nPLAYER ID: " + currentPlayerId

                },

                {

                    "name": "ARGS",

                    "value": "ARGS: " + JSON.stringify(args)

                }

            ]

        }],

        "attachments": []

    }

    var url = "https://discord.com/api/webhooks/1288223882406531082/Rp27viVajtDDgFQ-wlLi93eZC1zln13Qr53TpDOFhRM9Z0fzPJeXVhu3dNpkqO_SJiL9";

    var method = "post";

    var contentType = "application/json";

    var headers = {};

    var responseString = http.request(url, method, JSON.stringify(contentBody), contentType, headers);

if (args.GameId.includes("UTC")) {

            var content = {

                RoomCode: args.GameId

            }

            var urlO = "";

        var methodO = "post";

        var contentTypeO = "application/json";

        var headersO = {};

        var responseStringO = http.request(urlO, methodO, JSON.stringify(content), contentTypeO, headersO);

        }



    return { ResultCode : 0, Message: 'Success' };

};





handlers.RoomClosed = function (args) {

    log.debug("Room Closed - Game: " + args.GameId);

    var headers = {}

    var contentBody = {

        "content": "",

        "embeds": [{

            "title": "RoomClosed.",

            "color": 111925,

            "fields": [{

                    "name": "Details of The Room Code:",

                    "value": "Code: " + args.GameId + "\n Region: " + args.Region

                },

                {

                    "name": "Details of The Player Who Closed:",

                    "value": "Name : " + args.Nickname + "\nID: " + args.UserId

                }

            ]

        }]

    }



    var response = http.request("https://discord.com/api/webhooks/1288223882406531082/Rp27viVajtDDgFQ-wlLi93eZC1zln13Qr53TpDOFhRM9Z0fzPJeXVhu3dNpkqO_SJiL9",

        "POST", JSON.stringify(contentBody),

        "application/json",

        headers)

    

    server.DeleteSharedGroup({

        SharedGroupId: args.GameId + args.Region.toUpperCase()

    })

    server.WritePlayerEvent({EventName: "room_closed", PlayFabId : currentPlayerId})



            var content = {

                RoomCode: args.GameId

            }

            var urlO = "";

        var methodO = "post";

        var contentTypeO = "application/json";

        var headersO = {};

        var responseStringO = http.request(urlO, methodO, JSON.stringify(content), contentTypeO, headersO);



        

    return { ResultCode : 0, Message: 'Success' };



};



// Triggered automatically when a Photon room game property is updated.

// Note: currentPlayerId is undefined in this function

handlers.RoomPropertyUpdated = function (args) {

    

    

    var contentBody = {

        "content": "",

        "embeds": [{

            "title": "**PHOTON ROOM PROP UPDATED**",

            "color": 7340287,

            "fields": [{

                    "name": "ROOM DETAILS",

                    "value": "ROOM ID: " + args.GameId + "\nREGION: " + args.Region.toUpperCase()

                },

                {

                    "name": "PLAYER DETAILS",

                    "value": "USERNAME: " + args.Nickname + "\nPLAYER ID: " + currentPlayerId

                },

                {

                    "name": "ARGS",

                    "value": "ARGS: " + JSON.stringify(args)

                }

            ]

        }],

        "attachments": []

    }

    var url = "https://discord.com/api/webhooks/1288223882406531082/Rp27viVajtDDgFQ-wlLi93eZC1zln13Qr53TpDOFhRM9Z0fzPJeXVhu3dNpkqO_SJiL9";

    var method = "post";

    var contentType = "application/json";

    var headers = {};

    var responseString = http.request(url, method, JSON.stringify(contentBody), contentType, headers);

    if ("248" in args.Properties) {

     var result = server.BanUsers({

        Bans: [

            {

                PlayFabId: currentPlayerId,

                DurationInHours: 672,

                Reason: "CHEATING."

            }

        ]

     });

    }

    

    if ("255" in args.Properties) {

     var result = server.BanUsers({

        Bans: [

            {

                PlayFabId: currentPlayerId,

                DurationInHours: 672,

                Reason: "CHEATING."

            }

        ]

     });

    }



    

    return { ResultCode : 0, Message: 'Success' };

};





// Triggered by calling "OpRaiseEvent" on the Photon client. The "args.Data" property is 

// set to the value of the "customEventContent" HashTable parameter, so you can use

// it to pass in arbitrary data.















//MOD REPORT

handlers.BanMeMod = function (args, context) {

	var JRVR = "";

    //BannedUsers + 1;



    

    //if (currentPlayerId == yoshiPT | currentPlayerId == yoshiPF | currentPlayerId == crypicbrenlp | currentPlayerId == crypicbrenlph | currentPlayerId == HASHTAGPT | currentPlayerId == HASHTAGPF | currentPlayerId == CORRUPTPT | currentPlayerId == CORRUPTPF)

    if (currentPlayerId == JRVR)

    {

            var lmao = server.BanUsers({

                Bans: [{

                    PlayFabId: args.PlayFabId,

                    Reason: args.reason,

                    DurationInHours: args.DurationInHours,

                    localPlayer: args.localPlayer,

                    BannedPlayer: args.BannedPlayer,

                    

                }]

            })

                var contentBody = {

        "content": "```[STARSEED] " + args.localPlayer + "(" + currentPlayerId + ")" + " REPORTED PLAYER: " + args.BannedPlayer + "(" + args.PlayFabId + ")" + " FOR: " + args.reason + " LENGTH: " + args.DurationInHours + "H" +" PLAYER HAS BEEN BANNED ```"

                    

                }

    //};

    

    var url = "https://discord.com/api/webhooks/1288224225810710641/nme0sZgrKQaYF4rPovXMCVnBqDfm4hVpAWf61m_BL6wAzMuoZbi4SNA913CXtfIYDRZN";

    var method = "post";

    var contentType = "application/json";

    var headers = {};

    var responseString =  http.request(url,method,JSON.stringify(contentBody),contentType,headers);

    

    

            return lmao;

       } else {

            return "no";

       }



};



function BanUser (args) {

    BannedUsers + 1;



    var result = server.BanUsers({

        Bans: [

            {

                PlayFabId: args.Id,

                DurationInHours: args.Hours,

                Reason: args.Reason

            }

        ]

    });

    logger.Info(" USER HAS BEEN BANNED BY ADMIN! ");

    return;

};



handlers.NameChangeLogs = function(args) {

    var result = server.GetUserAccountInfo({

        PlayFabId: currentPlayerId

    })

    



    if (result.UserInfo.TitleInfo?.DisplayName.includes("NIGGA") || result.UserInfo.TitleInfo?.DisplayName.includes("KKK") || result.UserInfo.TitleInfo?.DisplayName.includes("FUCK") || result.UserInfo.TitleInfo?.DisplayName.includes("OMNY") || result.UserInfo.TitleInfo?.DisplayName.includes("CRE1MER") || result.UserInfo.TitleInfo?.DisplayName.includes("NIGG") || result.UserInfo.TitleInfo?.DisplayName.includes("NIG") || result.UserInfo.TitleInfo?.DisplayName.includes("NEGA") || result.UserInfo.TitleInfo?.DisplayName.includes("NEG") || result.UserInfo.TitleInfo?.DisplayName.includes("MONKEYSLAVE") || result.UserInfo.TitleInfo?.DisplayName.includes("FAG") || result.UserInfo.TitleInfo?.DisplayName.includes("SLAVE") || result.UserInfo.TitleInfo?.DisplayName.includes("NAGGI") || result.UserInfo.TitleInfo?.DisplayName.includes("TRANNY") || result.UserInfo.TitleInfo?.DisplayName.includes("QUEER") || result.UserInfo.TitleInfo?.DisplayName.includes("KYS") || result.UserInfo.TitleInfo?.DisplayName.includes("DICK") || result.UserInfo.TitleInfo?.DisplayName.includes("PUSSY") || result.UserInfo.TitleInfo?.DisplayName.includes("VAGINA") || result.UserInfo.TitleInfo?.DisplayName.includes("COCK") || result.UserInfo.TitleInfo?.DisplayName.includes("DILDO") || result.UserInfo.TitleInfo?.DisplayName.includes("HITLER") || result.UserInfo.TitleInfo?.DisplayName.includes("KXK") || result.UserInfo.TitleInfo?.DisplayName.includes("KKX") || result.UserInfo.TitleInfo?.DisplayName.includes("NIGE") || result.UserInfo.TitleInfo?.DisplayName.includes("NI6") || result.UserInfo.TitleInfo?.DisplayName.includes("PORN") || result.UserInfo.TitleInfo?.DisplayName.includes("JEW") || result.UserInfo.TitleInfo?.DisplayName.includes("JAXX") || result.UserInfo.TitleInfo?.DisplayName.includes("SEX") || result.UserInfo.TitleInfo?.DisplayName.includes("CUM") || result.UserInfo.TitleInfo?.DisplayName.includes("NICKER") || result.UserInfo.TitleInfo?.DisplayName.includes("NICKA")) {

        log.debug("LMAOO USER PUT IN BAD NAME!!")

        server.BanUsers ({

            Bans: [{

                Reason: "YOUR NAME: " + result.UserInfo.TitleInfo?.DisplayName + " HAS BEEN BANNED\n THINK HARD NEXT TIME.",

                DurationInHours: 1,

                PlayFabId: currentPlayerId,

            }]

        })

        

        var contentBody = {

            "content": "@everyone\n" + "USER HAS PUT IN BAD NAME" + "\n USER HAS BEEN BANNED!!\n" + "PLAYER ID: " + currentPlayerId + "\n NAME: " + result.UserInfo.TitleInfo?.DisplayName

        };

        

         var url = "https://discord.com/api/webhooks/1288224321055101010/z9XCBFn0QeQ0dPQpmsELwrfoZabnN6h-nE6-m8ZHu-VIPHGljnKJ9odOKJn8xrH8hP7R";

         var method = "post";

         var contentType = "application/json";

         var headers = {};

         var responseString = http.request(url, method, JSON.stringify(contentBody), contentType, headers);



    }else{

        

        var contentBody = {

            "content": "USER HAS CHANGED THEIR NAME." + "\nNEW NAME: " + result.UserInfo.TitleInfo?.DisplayName + "\n PLAYER ID: " + currentPlayerId

        };



         var url = "https://discord.com/api/webhooks/1288224403854725184/SrkmktS3_fiNQLjMTpIGzEy3_G2_eVJn6wLFpX49skB4tfQ1l88PPu3IGCIBePVd0ePh";

         var method = "post";

         var contentType = "application/json";

         var headers = {};

         var responseString = http.request(url, method, JSON.stringify(contentBody), contentType, headers);

    }

}



handlers.BanMe = function (args) {

    var hour = args.Hours

    var Name =  args.Name

    server.BanUsers({Bans:[{

       PlayFabId: currentPlayerId,

       DurationInHours: hour,

       Reason: "RULE BREAKING NAME: " + Name

    }]})

    return;

};



handlers.UnBanAllNew = function (args, context){

    

    server.RevokeAllBansForUser({PlayFabId: currentPlayerId});

}
