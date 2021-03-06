oh boy.

is there a lot.

#

# OVERALL



The AItree for larva uses `/Game/Enemies/Varkid/_Shared/_Design/Actions` to help dictate the action it'll do, and uses `/Game/Enemies/Varkid/_Shared/_Design/Balance/Table_Varkid_Attacks` for damage. What I suspect is that it uses the base game for the normal evoultion attacks, and it's own table for raid boss attacks.

What I'm currently after is finding the health value/immunity granted when the boss enters the pod.

File :`/proj_varkidraid_egg_verm` (verme egg)
maybe herme's file's reference this... Use the obj ref to trace where the file leads. That'll give me answers.

# HERME

## File `BPCHar_VarkidLarva_Raid`

His health threshold for evolving is 10% at all stages, and is as shown by the following:

    {
    "export_type": "BPChar_VarkidLarva_Raid_C",
    "_jwp_export_idx": 3,
    "_jwp_is_asset": false,
    "_jwp_object_name": "Default__BPChar_VarkidLarva_Raid_C",
    "UberGraphFrame": {},
    "EvolveHealthPercentThreshold": {
      "ValueType": "EGbxParamValueType::Float",
      "DisabledValueModes": 64,
      "ValueFlags": 0,
      "ValueMode": "EGbxParamValueMode::Value",
      "Range": {
        "Value": 0.1,
        "Variance": 0
      },
      "AttributeInitializer": {
        "export": 0
      },
      "AttributeData": {
        "export": 0
      },
      "AttributeInitializationData": {
        "BaseValueConstant": 0,
        "DataTableValue": {
          "DataTable": {
            "export": 0
          },
          "RowName": "None",
          "ValueName": "None"
        },
        "BaseValueAttribute": {
          "export": 0
        },
        "AttributeInitializer": {
          "export": 0
        },
        "BaseValueScale": 1
      },
      "BlackboardKey": {
        "KeyName": "None",
        "bRuntimeKey": false
      },
      "Condition": {
        "export": 0
      },
      "Actor": {
        "export": 0
      }
    },

But what follows after is what caught my eye, I don't know what it does, and I'm keen to find out.

This I want to investigate further.

Both fall under `"_jwp_export_idx": 3`, which holds a TON of info, including his evolution health threshold. This is what I want to dive into.

    "EvolvingToSpawnOptionMap": [
      {
        "_jwp_arr_idx": 0,
        "key": 240,
        "value": {
          "export": 0
        }
      }
    ],
    "CustomEvolve_SpawnOption": [
      "SpawnOptions_Varkid_RaidBoss",
      "/Ixora2/Enemies/_Spawning/Varkid/_Unique/SpawnOptions_Varkid_RaidBoss"
    ],
    "VarkidPodHoldDuration": {
      "ValueMode": "EGbxParamValueMode::Value",
      "Range": {
        "Value": 0.1,
        "Variance": 0
      }
    },
    ...
    ...
    },
    "MainAIAction": [
      "AITree_VarkidLarva_Raid_C",
      "/Ixora2/Enemies/Varkid/_Unique/RaidBoss/_Design/Evolutions/AITree_VarkidLarva_Raid"
    ],
    ...
    ...
    "LandingDataTriggeredDelegate": [
      {
        "object": 3,
        "name": "OnLandingDataTriggered"
      }
    ],
    "SpawnCostSelection": {
      "Preset": "Boss",
      "SpawnCost": 80
    },

Something tells me this is the trigger for his evolution, and the line `"LandingDataTriggeredDelegate"` might lead me to what gives him his immunity

#

What determines what's in the pod when you spawn in is this:

    ],
    "CustomEvolve_SpawnOption": [
      "SpawnOptions_Varkid_RaidBoss",
      "/Ixora2/Enemies/_Spawning/Varkid/_Unique/SpawnOptions_Varkid_RaidBoss"
    ],

 Exports `"_jwp_export_idx": 6,` seems to dictate the evolution path once a health threshold has been met, as dictated by the following:


    "export_type": "StructProperty",
    "_jwp_export_idx": 6,
    "_jwp_is_asset": false,
        "_jwp_object_name": "EvolveHealthPercentThreshold"

The trigger for Herme to activate I think is `"_jwp_export_idx": 20,`, as it has 

    {
        "export_type": "ComponentDelegateBinding",
        "_jwp_export_idx": 20,
        "_jwp_is_asset": false,
        "_jwp_object_name": "ComponentDelegateBinding_1",
        "ComponentDelegateBindings": [
        {
            "_jwp_arr_idx": 0,
            "ComponentPropertyName": "OakDamageComponent",
            "DelegatePropertyName": "OnTakeAnyDamage",
            "FunctionNameToBind": "BndEvt__OakDamageComponent_K2Node_ComponentBoundEvent_1_TakeAnyPipelineDamageDelegate__DelegateSignature_BPChar_VarkidLarva_Raid"
        }
        ]
    },

#

Something really funny to note is that in `"_jwp_export_idx": 4,`, it characterizes the name based on your playthrough. as follows:

    "export_type": "AIBalanceStateComponent",
    "_jwp_export_idx": 4,
    "_jwp_is_asset": false,
    "_jwp_object_name": "AIBalanceState_GEN_VARIABLE",
    "PlayThroughs": [
      {
        "_jwp_arr_idx": 0,
        ...
      },
      {
        "_jwp_arr_idx": 1,
      },
    
I'd guess `"_jwp_arr_idx": 0,` is NVHM, and `"_jwp_arr_idx": 1,` is TVHM.

The kicker of all this is that for NVHM,

      {
        "_jwp_arr_idx": 0,
        "bOverrideUIDisplayName": true,
        "bOverrideDisplayName": true,
        "bOverrideDropOnDeathItemPools": false,
        "bOverrideEquippedItems": false,
        "bOverrideHealthInformation": false,
        "DisplayUIName": [
          "UIName_Varkid_RaidBoss",
          "/Ixora2/Enemies/Varkid/_Unique/RaidBoss/_Design/Character/UIName_Varkid_RaidBoss"
        ],
        "DisplayName": {
          "string": "Skag Adult",
          "namespace": "",
          "key": "B31CF125476239BDBBDD3C81691A8792"
        },
        

And for TVHM,

      {
        "_jwp_arr_idx": 1,
        "bOverrideUIDisplayName": true,
        "bOverrideDisplayName": false,
        "bOverrideDropOnDeathItemPools": false,
        "bOverrideEquippedItems": false,
        "bOverrideHealthInformation": false,
        "DisplayUIName": [
          "UIName_Varkid_RaidBoss",
          "/Ixora2/Enemies/Varkid/_Unique/RaidBoss/_Design/Character/UIName_Varkid_RaidBoss"
        ],
        "DisplayName": {
          "string": "",
          "namespace": "",
          "key": ""
        },

NVHM reads the display name as "Skag Adult", whereas TVHM has just "". This is odd, because NVHM uses `"bOverrideDisplayName": true,`, and TVHM has it set to false. 

The real kicker? It's this way in Verme's file too!

Don't know what this does yet, but we'll get there.

# 

## File `SpawnOptions_Varkid_RaidAddsLarva` 

This makes the varkid larva pod be in the raid. It ensures the pod will be there at a 100% chance. It uses `SpawnFactory_OakAi` to spawn him, and ` "Probability": "100.00%",` to make this chance actual.  

#

## file `Table_Varkid_Balance_Raid`

This dictates health values, experience multiplier, damage multiplier, and loot pools based on NVHM or TVHM.

# VERME

Things to note:
File :`/proj_varkidraid_egg_verm` (verme egg)


    {
    "export_type": "OakDamageComponent",
    "_jwp_export_idx": 64,
     "_jwp_is_asset": false,
    "_jwp_object_name": "OakDamage_GEN_VARIABLE",
    "bDieWhenHealthDepleted": false,
    "HealthMode": "EDamageComponentHealthMode::SimpleHealth",
    "SimpleHealthInformation": {
      "MaxHealthFormula": {
        "AttributeInitializer": [
          "Init_HealthCalc_VarkidEgg_C",
          "/Ixora2/Enemies/Varkid/_Unique/RaidBoss/_Design/Projectiles/Init_HealthCalc_VarkidEgg"
      },


This explains why while verme is in his pod, he can't take damage. 

problem is, we basically don't see his egg. he just kinda shows up. 

