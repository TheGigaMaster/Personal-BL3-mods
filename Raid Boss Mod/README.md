oh boy.

is there a lot.

#

# OVERALL

AI_tree hasn't had anything worthwile yet, but it seems to dictate how they'll attack.

MainAIAction dictates how they'll act (i think)

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

    "EvolvingToSpawnOptionMap": [
      {
        "_jwp_arr_idx": 0,
        "key": 240,
        "value": {
          "export": 0
        }
      }

I think this is what allows him to evolve on his map, but I'm not quite sure.

What determines what's in the pod is this:

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

## File `SpawnOptions_Varkid_RaidAddsLarva` 

This makes the varkid larva pod be in the raid. It ensures the pod will be there at a 100% chance. It uses `SpawnFactory_OakAi` to spawn him, and ` "Probability": "100.00%",` to make this chance actual.  

#

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
