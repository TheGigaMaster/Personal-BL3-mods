oh boy.

is there a lot.

#

# OVERALL

AI_tree hasn't had anything worthwile yet, but it seems to dictate how they'll attack.

MainAIAction dictates how they'll act (i think)

# HERME

In file `BPCHar_VarkidLarva_Raid`, Exports `"_jwp_export_idx": 6,` seems to dictate the evolution path once a health threshold has been met, as dictated by the following:


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
          
        ]
        
      },


This explains why while verme is in his pod, he can't take damage. 

problem is, we basically don't see his egg. he just kinda shows up. 
