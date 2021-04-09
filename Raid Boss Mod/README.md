oh boy.

is there a lot.

#

# OVERALL

AI_tree hasn't had anything worthwile yet, but it seems to dictate how they'll attack.

MainAIAction dictates how they'll act (i think)

# HERME

In file `BPCHar_VarkidLarva_Raid`, Exports `"_jwp_export_idx": 6,` seems to dictate the evolution path once a health threshold has been met, as dictated by



#

# VERME

Things to note:
File :`/proj_varkidraid_egg_verm`
`
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
`

This explains why while verme is in his pod, he can't take damage. 

problem is, we basically don't see his egg. he just kinda shows up. 
